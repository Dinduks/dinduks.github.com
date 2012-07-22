---
comments: true
date: 2011-12-03 18:51:07
layout: post
slug: symfony2-using-multiple-databases
title: 'Symfony2: Using multiple databases'
wordpress_id: 1514
categories:
- Development
- Symfony 2
- Tutorials
tags:
- doctrine
- doctrine2
- php
- symfony
- symfony2
---

In case your website, built with **Symfony2**, is using multiple databases, you must setup as much connections and _**Entity Managers**_ as databases.

_An **Entity Manager** is simply a service that persists and fetches data in and from a **database**._


In order to illustrate my example, I will be using two databases: _site_ and _forum_.



#### Set up the connections in _**config.yml**_


[yaml]
doctrine:
  dbal:
    default_connection: site # specify the connexion used by default
    connections:
      site:
        driver:   %database_driver%
        host:     %database_host%
        port:     %database_port%
        dbname:   site
        user:     site_usr
        password: site_pwd
        charset:  UTF8
      forum:
        driver:   %database_driver%
        host:     %database_host%
        port:     %database_port%
        dbname:   forum
        user:     forum_usr
        password: forum_pwd
        charset:  UTF8
[/yaml]



#### Set up EM, in the same file


To begin with, disable _auto-mapping_, so you will be able to choose which EM is going to manage which **bundle**’s entities.
[yaml]
doctrine:
  orm:
    auto_mapping: false
[/yaml]

_Note: If there’s an error bounded with this line, just delete it._

Then, right below, set up EM while specifying **mappings** to each bundle.
[yaml]
doctrine:
  orm:
    auto_mapping: false
    default_entity_manager: web # specify the EM used by default (when using console commands f.e)

    entity_managers:
      web:
        connection: web
        mappings: 
          DinduksFooBundle : ~
          DinduksBarBundle : ~
          FOSUserBundle: ~
      forum:
        connection: forum
        mappings:
          DinduksForumBundle : ~
[/yaml]

Simply put, mappings connect and constitute the bridge between an EM and the entities of a specific bundle.
In other terms, mappings call up an EM X when wanting to manipulate an entity Y.

Warning: Always make sure you map your fresh-created bundles to an EM, otherwise a "non-existent bundle" error will occur when using the _doctrine:generate:entities_ command.



#### Utilization


In the same way you call your default EM, call the EM you need by passing its name to the _**getEntityManager()**_ function.

[php]
$forumEm = $this->get('doctrine')->getEntityManager('forum');
[/php]



I hope you’ll find this tutorial useful. :)





Translated from my french post [Symfony2: Utiliser plusieurs bases de données](http://www.dinduks.com/symfony-2-utiliser-plusieurs-bases-de-donnees)
