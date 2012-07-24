---
comments: true
date: 2011-08-18 15:03:43
layout: post
slug: symfony-2-utiliser-des-types-de-donnees-non-supportes-par-doctrine
title: 'Symfony2: Utiliser des types de données non supportés par Doctrine'
categories:
- Development
- Symfony 2
tags:
- doctrine
- doctrine2
- php
- symfony
- symfony2
---

*Doctrine2*, en tant qu'ORM, doit assurer la compatibilité des types de données (_varchar_, _integer_, _datetime_, etc...) entre différents SGBD, et ne supporte donc pas certains types propres à *MySQL* (dans mon cas).  
Il est cependant possible de lui ajouter des types manuellement, mais la procédure est assez longue et n'en vaut pas la peine à mon avis.

Si vous êtes sûr que votre site n'utilisera qu'un seul SGBD et que ça ne va pas changer plutard, vous pouvez spécifier, dans vos *annotations*, *une partie* du code *SQL* qui servira à générer le champ.

### Exemple

Pour générer un champ _tinyint_ qui est _NOT NULL_ et qui a une valeur par défaut de 10, voici le code nécessaire:

    /**
    * @ORM\Column(columnDefinition="tinyint(4) NOT NULL DEFAULT '10'", name="foo")
    */
    protected $foo;

A vous d'adapter ce code pour votre cas. ;)
