---
comments: true
date: 2011-06-15 16:27:37
layout: post
slug: php-addition-soustraction-des-dates-heures
title: 'PHP: Addition/Soustraction des dates/heures'
categories:
- Development
- Pieces of code
tags:
- php
---

Je partage ces deux [bouts de code](http://www.dinduks.com/category/bouts-de-code) tellement banals, mais que j'oublie toujours.  
(et je m'évite cette [punition](https://twitter.com/#!/Dinduks/status/80677872561422336) en même temps)

### Dates:

    $aujourdhui = "2011-06-15";
    $demain = date("Y-m-d", strtotime("+1 day", strtotime($aujourdhui)));
    $ilYADeuxMois = date("Y-m-d", strtotime("-2 month", strtotime($aujourdhui)));

### Heures:

    $maintenant = "15:00:00";
    $dansUneHeure = date("H:i:s", strtotime("+1 hour", strtotime($maintenant)));
    $ilYAUnQuartDHeure = date("H:i:s", strtotime("-15 minute", strtotime($maintenant)));

#### Liste de mots-clé utiles:
  * day
  * week
  * month
  * year
  * hour
  * minute
  * second
