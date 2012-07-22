---
comments: true
date: 2011-08-13 22:19:19
layout: post
slug: symfony-2-executer-les-commandes-console-sur-un-entity-manager-specifique
title: 'Symfony2: Executer les commandes console sur un Entity Manager spécifique'
wordpress_id: 1086
categories:
- Development
- Pieces of code
- Symfony 2
tags:
- doctrine
- doctrine2
- php
- symfony
- symfony2
---

Ce qui suit n'est pas une science exacte mais ça peut vous éviter 10 minutes de recherche. 

C'est cet argument qui vous sauvera la vie: _--em_



#### Exemple:


Dans le cas où vous voudrez générer les informations sur le mapping à partir de l'Entity Manager "client":
[bash]
php app/console doctrine:mapping:convert yml /src/Acme/ClientBundle/Resources/config/doctrine/metadata/orm --from-database --force --em="client
[/bash] 
