---
comments: true
date: 2011-10-23 11:18:32
layout: post
slug: twig-traduction-dans-du-javascript
title: 'Twig: Traduction dans du JavaScript'
wordpress_id: 1264
categories:
- Development
- Symfony 2
- Tutorials
tags:
- javascript
- js
- php
- silex
- twig
---

Hello, 

Lors du développement d'une application **Silex**, je devais générer du code à la volée à l'aide de **JavaScript**. 
Le code généré ne pouvait évidemment pas être traduit. Pour palier à cela, le principe est de mettre les traductions dans un objet javascript, et de l'utiliser dans votre code **JS**. 

Ce qui suit est une manière de procéder.

Je pars du principe que votre traduction est déjà mise en place et qu'elle marche correctement dans vos templates **Twig**.



  * Créer un fichier translations.html.twig

Je l'ai personnellement mis avec les autres vues. 
Mettez y un script JS avec les expressions que vous voulez traduire. 
[html]
<script type="text/javascript">
    var translations = {
        'hello_world': '{% trans %}hello_world{% endtrans}',
        'foobar': '{% trans %}foobar{% endtrans}'
    }
</script>
[/html]


  * Ensuite, incluez ce template dans votre layout:

Avant la déclaration des autre scripts bien sûr.
[html]
{% include './translations.html.twig' %}
[/html]

Et voilà, vous pouvez maintenant accéder à l'objet _translations_ depuis vos scripts JS.



  * Exemple:

[js]
console.log(translations.hello_world);
[/js] 
