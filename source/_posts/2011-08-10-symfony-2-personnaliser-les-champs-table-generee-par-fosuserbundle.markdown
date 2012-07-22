---
comments: true
date: 2011-08-10 03:11:15
layout: post
slug: symfony-2-personnaliser-les-champs-table-generee-par-fosuserbundle
title: 'Symfony2: Personnaliser les champs de la table générée par FOSUserBundle'
wordpress_id: 1044
categories:
- Development
- Symfony 2
tags:
- fosuserbundle
- php
- symfony2
---

Bonjour, 

Mon premier _vrai_ projet sous **Symfony 2** est un site pour un serveur World Of Warcraft. 
Ce serveur, sous **MaNGOS**, utilise ses propres tables, avec leur propre structure. Je voulais donc, pour des raisons de stabilité et pour éviter les emmerdes, générer une table User avec les mêmes champs et propriétés que celles de MaNGOS. 


Pour comprendre la suite de cet article vous devez avoir une idée basique sur le fonctionnement de **FOSUserBunde**. Si ce n'est pas le cas, lisez la doc: [Getting Started With FOSUserBundle](https://github.com/FriendsOfSymfony/FOSUserBundle/blob/master/Resources/doc/index.md).

Je vous explique le topo: pour créer une table utilisateur avec **FOSUB**, il faut créer une entité (un modèle quoi) User qui "extend" la classe User du fameux bundle. Cette classe contient, entre-autres, des variables (qui se traduisent niveau base de données par des champs) nécessaires à son fonctionnement (exemple: username, canonicalusername, etc...). 
La table générée dépendra de votre User:




  * Si vous laissez votre entité User vide: Une table avec les champs par défaut de FOSUB sera générée.


  * Si vous définissez des variables dans cette classe: La table générée aura les champs par défaut + les champs portant les noms des variables définies dans la classe.


  * Si vous redéfinissez une variable de la classe User de FOSUserBundle: _ERROR!_ **Doctrine** ne supporte pas la redéfinition des variables **protected**. 



Arrivés là, vous comprenez que vous êtres dans la merde. 

Je vous le dit tout de suite: il n'y a pas de solution propre et officielle pour ce problème. [Stof](https://github.com/stof), un des principaux contributeurs à FOSUserBundle me l'a confirmé lui même. 

La solution est de hacker le code source de Doctrine, ou de FOSUserBundle. Vous avez même le choix. :) 




![Symfony 2: Personnaliser les champs de la table générée par FOSUserBundle](/wp-content/images/symfony-2-fosuserbundle.png)






### Bidouiller Doctrine


Cette solution est super simple. A mon avis, sa simplicité est proportionnelle à l'importance des dégâts qu'elle _pourrait_ infliger plutard. 

Rendez vous dans le fichier vendors/doctrine/lib/Doctrine/ORM/Mapping/ClassMetadataInfo.php, et commentez ces deux lignes: 
[php]
throw MappingException::duplicateColumnName($this->name, $mapping['columnName']);
[/php]
et
[php]
throw MappingException::duplicateFieldMapping($this->name, $mapping['fieldName']);
[/php]

Là, on annule carrément les exceptions balancées lors de la tentative de redéfinition d'une variable. 
J'espère que vous comprenez maintenant pourquoi j'ai dit que ça peut vous créer des ennuis plutard. 
Je pense que si les devs de Doctrine ont mis ces exceptions, c'est pour une raison. 

N'oubliez pas que si vous mettez Doctrine à jour, il y a de fortes chances que le fichier ClassMetadataInfo.php sera écrasé. Pensez-y.



### Plan B: bidouiller FOSUserBundle


Cette manip est moins suicidaire que la précédente, elle consiste à modifier le fichier _FOS/UserBundle/Resources/config/doctrine/User.orm.xml_.
Ce fichier gère les propriétés des champs générés par le bundle. 
Je ne vais pas vous expliquer comment, sa structure est assez évidente. 

Je vous rappelle que, comme pour le hack précédent, ce fichier peut être modifié par une màj. 



### Mon choix


Mon choix s'est porté sur la première solution parce qu'elle me permet de vraiment personnaliser mes champs: directement, elle me donne la possibilité de jouer avec mon entité User.
Indirectement elle me permet de: 




  * Donner des types non supportés ([par défaut](http://symfony2.ylly.fr/add-new-data-type-in-doctrine-2-in-symfony-2-jordscream/)) par Doctrine, tels que _tinyint_, _timestamp_ ou encore _longtext_. 
Référez vous à mon article [_Symfony 2: Utiliser des types de données non supportés par Doctrine_](http://www.dinduks.com/symfony-2-utiliser-des-types-de-donnees-non-supportes-par-doctrine) pour plus de détails.


  * Donner une valeur par défaut à un champ. Seul hic, lors de l'insertion d'un utilisateur, ces champs ne sont pas remplis automatiquement par la valeur par défaut. J'en parlerai en détails prochainement.



Pour finir, je voudrai donner mon avis à propos de FOSUserBundle: c'est un bundle utile lorsqu'on veut implémenter un gestionnaire d'utilisateurs (si on peut appeler ça comme ça) assez basique. Mais il peut vite tourner au cauchemar/mindfuck lorsqu'on veut faire un truc un peu plus poussé. 
Ce bundle est en effet assez difficile à appréhender, le style "PHP5.3 n4m3sp4c3s r so OOP LOL" et le manque de documentation n'aident pas tout. 

Bon après cet avis n'engage que moi, et est basé sur ma propre expérience. Je peux donc me tromper ou dire des bêtises. 
Veuillez me faire part de vos remarques, corrections en commentaire. 

Bonne arrachage de cheveux avec le couple FOSUserBundle/Doctrine, et à bientôt!
