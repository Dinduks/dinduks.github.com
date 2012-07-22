---
comments: true
date: 2011-05-29 21:54:51
layout: post
slug: jquery-faire-reapparaitre-un-element-avec-un-nouveau-contenu
title: 'jQuery: Faire réapparaître un élément avec un nouveau contenu'
wordpress_id: 835
categories:
- Development
- Pieces of code
tags:
- ajax
- javascript
- jquery
---

Salut,

Je vais partager un bout de code pour cacher un texte ou un bloc, le mettre à jour, et le ré-afficher avec un nouveau contenu, avec **jQuery**. 

Cette technique est intéressante lorsqu'on veut mettre à jour un élément avec un contenu **AJAX**. 
Il faut noter que dans le cas d'une utilisation avec ce dernier, il faut mettre une de ces fonctions dans le success. 




![jQuery: Faire réapparaître un élément avec un nouveau contenu](/wp-content/images/jquery-reapparaitre-element-nouveau-contenu.png)





Vous vous demandez peut-être quel est l'intérêt d'un tel code, un fadeOut() suivi d'un html() puis d'un fadeIn() feront l'affaire. 
Mais en pratique ce n'est pas aussi simple que ça, car il faut faire une pause entre le fadeOut() et le html() ; on se retrouve du coup avec un setTimeout() dans le meilleur des cas, ou dans le pire, un long code bordélique. 



  * Sans plus attendre, voici la fonction que j'utilise pour le texte: 

[js]
function refreshText(elemId, content, delay, fadeInDuration){
  $('#' + elemId)
    .fadeOut()
    .delay(delay)
    .queue(function(n){
      $('#' + elemId).html(content);
      n();
    })
    .fadeIn(fadeInDuration);
}
[/js]


  * Et celle pour les blocs, la même que la première mais avec des slides: 

[js]
function refreshBlock(elemId, content, delay, slideDownDuration){
  $('#' + elemId)
    .slideUp()
    .delay(delay)
    .queue(function(n){
      $('#' + elemId).html(content);
      n();
    })
    .slideDown(slideDownDuration);
}
[/js]

Enjoy! 
