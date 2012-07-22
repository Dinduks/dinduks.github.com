---
comments: true
date: 2011-10-09 20:09:41
layout: post
slug: symfony-2-creer-un-utilisateur-depuis-un-controleur-avec-fosub
title: 'Symfony2: Créer un utilisateur depuis un contrôleur avec FOSUB'
wordpress_id: 1188
categories:
- Development
- Pieces of code
- Symfony 2
tags:
- fosuserbundle
- php
- symfony
- symfony2
---

Si vous utilisez **FOSUserBundle** et que vous voulez créer un nouvel utilisateur depuis un contrôleur, sachez que vous pouvez le faire sans vous taper une série de lignes de code. Il existe en effet une classe pour cela, [UserManipulator](https://github.com/FriendsOfSymfony/FOSUserBundle/blob/master/Util/UserManipulator.php), qui fera la sale besogne à votre place, **et en une seule ligne**!

Pour l'utiliser, rien de plus simple: 
[php]
$user = $this->get('fos_user.util.user_manipulator')->create($username, $password, $email, 1, 0);
[/php]

Comme indiqué dans le fichier de la classe, le quatrième paramètre sert à définir si le compte sera activé ou pas et le cinquième à définir si ce compte est un super admin. 
Cette méthode vous renverra une instance de l'objet User qui vient d'être créé. 
