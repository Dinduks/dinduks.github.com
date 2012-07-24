---
comments: true
date: 2011-12-16 18:31:57
layout: post
slug: symfony-2-execute-console-commands-on-a-specific-entity-manager
title: 'Symfony 2: Execute console commands on a specific entity manager'
categories:
- Development
- Pieces of code
- Symfony 2
tags:
- doctrine
- doctrine2
- php
- symfony2
---

The following isn’t an exact science, however, if you didn't `--help`, it will spare you a 10min research.
This is your lifesaver: `--em`.

### Example

In case you want to generate mapping information using the “client” entity manager:
    php app/console doctrine:mapping:convert yml /src/Acme/ClientBundle/Resources/config/doctrine/metadata/orm --from-database --force --em="client

*Translated from my french post [Symfony2: Executer les commandes console sur un Entity Manager spécifique](http://www.dinduks.com/symfony-2-executer-les-commandes-console-sur-un-entity-manager-specifique)*
