---
comments: true
date: 2010-11-18 17:56:51
layout: post
slug: lire-et-ecrire-des-fichiers-avec-java
title: 'Java: Lire et écrire des fichiers'
wordpress_id: 260
categories:
- Development
- Pieces of code
tags:
- java
---

![Lire et écrire des fichiers avec Java](/wp-content/images/lire-ecrire-fichiers-java.png)





Bonjour,

Lors de la résolution d'un problème en **Java**, j'ai du récupérer une **chaîne de caractères** à partir d'un fichier, et la parser dans un autre après l'avoir modifié.

Il y a plusieurs techniques pour le faire, je vais vous présenter la mienne que j'ai assimilé après avoir lu pas mal de forums et de documentations.




**Lecture:**

    
    try {
    File fileIn = new File("file.in"); //ouverture du fichier
    FileInputStream fis = new FileInputStream(fileIn);
    byte[] buffer = new byte[fis.available()]; //Récupération du contenu du fichier dans une variable de type byte
    fis.read(buffer); //Lecture du contenu de la variable buffer
    stringIn = new String(buffer); //On parse le contenu de buffer dans notre chaîne
    fis.close(); //Fermeture du fichier
    } catch(Exception e) {
    e.printStackTrace();
    }
    


**Écriture:**

    
    try {
    File fileOut= new File("file.out"); //Overture du fichier
    FileOutputStream fos = new FileOutputStream(fileOut);
    fos.write( stringOut.getBytes() ); //On parse le contenu de la chaîne qu'on converti d'abord en variable de type byte
    fos.close(); //Fermeture du fichier
    } catch(Exception e) {
    e.printStackTrace();
    }
    
