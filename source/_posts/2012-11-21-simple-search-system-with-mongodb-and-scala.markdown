---
layout: post
title: "Building a search system with MongoDB (and Scala)"
date: 2012-11-21 22:47
comments: true
categories:
---

If you need a search system for your web application, you can either roll your own,
or use a system that does it for you, such as *elasticsearch*.  
I've recently had to choose, and the second option was an overkill since I was looking
for something simple.

The main idea here is using an index collection, let's call it *searchresults*,
that will be updated each time the *real* entities change, thanks to hooks
implemented on the default create/update/delete tasks.  
*searchresults* will be the only collection to get queried, thus making requests
simple and search results' retrieval fast.  

### More in details

I'll use two entities in my example: `User` and `Song`.

The `SearchResult` model has 3 fields:

* `entityType`: a discriminator field that contains the indexed entity type, *user*
or *song* in this case.
* `entityId`: You think my name is Captain Obvious, don't you?
* `keywords`: An array of keywords related to that search.

That class' signature should look like this:

    case class SearchResult(
      id:         ObjectID,
      entityType: String,
      entityId:   ObjectID,
      keywords:   List[String]
    )

Paired with the class described above, a `Searchable` trait will help forcing the
implementation of some methods and properties, and more importantly be used as a
type in methods signatures.

    trait Searchable {
      def entityType:    String = this.getClass.getSimpleName,
      getSearchKeywords: List[String],
      entityId:          ObjectID
    }

Now, each of your entities class, `User` and `Song`, will implement the `Searchable`
trait, define the `entityType` property and implement the `getSearchKeywords()`
method. The `entityId` property, or some entity with the same name, should already
be implemented by your MongoDB driver.

*Example of a `getSearchKeywords()` method:*

    def getSearchKeywords: List[String] =
      List(this.username, this.firstname, this.lastname).filter(_.nonEmpty)

The next step is to implement the hooks that update the index collection each time
*users* and *songs* are updated too.

If you use *Casbah* and *Salat* for instance, the entities are created and updated when calling the
`save()` method, and deleted when `remove()` is called.  
These methods should be overriden, the hooks behaviors added to them —creating or
updating the concerned `SearchResult` entry, in case of `save()` for example—, yet
without altering their initial role.  

    override def save(user: User) {
      createSearchResult(user, SearchResult.findByEntity(user))
      super.save(user)
    }

    private def createSearchResult(user: User, searchResult: Option[SearchResult]) {
      searchResult match {
        case Some(sr) => SearchResult.save(sr.copy(keywords = user.getSearchKeywords))
        case None => SearchResult.save(SearchResult(
          entityType = user.entityType,
          entityId   = user.id,
          keywords   = user.getSearchKeywords
        ))
      }
    }

The last thing to do, is creating a MongoDB index on the keywords field of the
*searchresults* collection.  
This can be done in one single command:

    mongo myAwesomeDB --eval "db.searchresults.ensureIndex({keywords: 1});"

We're done. I guess.  

