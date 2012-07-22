---
comments: true
date: 2010-12-01 14:20:09
layout: post
slug: rust-le-langage-de-programmation-de-mozilla
title: 'Rust: Le langage de programmation de Mozilla'
wordpress_id: 327
categories:
- Development
tags:
- mozilla
- rust
---

![Rust: Le langage de programmation de Mozilla](/wp-content/images/rust-langage-mozilla.png)





#### Bref résumé





La fondation de Mountain View travaille en temps partiel depuis 2006 sur un langage de programmation appellé **Rust**, dans le but de palier les insuffisances des autres langages et d'élaborer un langage statique efficace, concurrentiel et sûr.

Malgré sa jeunesse, celui-ci est assez mature, stable et complet pour effectuer des taches basiques.
**Rust** est disponible au public et un compilateur (en **Ocaml**) est disponible, ainsi qu'une bibliothèque standard fonctionnelle.







#### A quoi ça ressemble?




    
    iter pairs() -> tup(int,int) {
      let int i = 0;
      let int j = 0;
      while (i < 10) {
        put tup(i, j);
        i += 1;
        j += i;
      }
    }
    fn main() {
      let int i = 10;
      let int j = 0;
      for each (tup(int,int) p in pairs()) {
          log p._0;
          log p._1;
          check (p._0 + 10 == i);
          i += 1;
          j = p._1;
        }
      check(j == 45);
    }
    





#### Et techniquement?





	
  * Mémoire saine: pas de pointeurs NULL, pointeurs sauvages, etc.

	
  * Contrôle de la mutabilité. Tout est immutable par défaut.

	
  * Contrôle de la mémoire explicite.

	
  * Tâches très légères (coroutines).

	
  * Possibilité d'accumuler des itérateurs.

	
  * Compilation native et statique.

	
  * **Rust** est multi-paradigme, pouvant être codé selon plusieurs styles: procédural, fonctionnel, ou orienté objet.

	
  * Multi-platformes: développé pour **Windows**, **Linux** et OSX.

	
  * Chaînes en UTF8 par défaut.





Rendez-vous sur [le portail **GitHub** du projet](https://github.com/graydon/rust/) pour plus d'informations.
