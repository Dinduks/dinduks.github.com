---
comments: true
date: 2012-04-30 16:30:49
layout: post
slug: sinatra-rspec-and-datamapper-configuring-and-using-a-database-for-tests
title: 'Sinatra, RSpec and DataMapper: Configuring and using a database for tests'
wordpress_id: 1968
categories:
- Ruby
tags:
- database
- datamapper
- rspec
- ruby
- sinatra
---


Hi there,

When testing your Sinatra application, you may need to check if some data was stored, removed, or changed in the database.

Your application would look like this:

{% gist 2559103 %}
{% gist 2559118 %}

Okay. First of all, let's tell RSpec to use a `blog_test.db` database:

{% gist 2559162 %}

**Explanations:**


* `DataMapper::setup()`: Tells DataMapper which database to use ; it will create it if it doesn't exist.
* `DataMapper.finalize`: *Finalize*  the models. More information in [DataMapper's documentation](http://datamapper.org/getting-started.html).
* `auto_migrate!` drops and recreate the tables, which is a good thing since we want to have a clean database before each test.

If it doesn't already exist, a database will be created in the application's root path the next time RSpec will be called (from the cli for example).

All what is left now is to write the test:

{% gist 2559503 %}

I hope this quick how-to was helpful.

Happy testing! :)
