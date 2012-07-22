---
comments: true
date: 2011-07-25 12:22:55
layout: post
slug: cpp-retourner-un-tableau-dans-une-fonction-ou-methode
title: 'C++: Retourner un tableau (dans une fonction ou méthode)'
wordpress_id: 944
categories:
- Development
- Pieces of code
tags:
- c++
- cpp
---

Il faudra retourner un pointeur qui pointe sur ce tableau, et ensuite récupérer le tableau (ailleurs) grâce au pointeur: 



### La fonction en question


[cpp]
int *multiplierParDeux(int a, int b){
    int *array= new int[2];
    array[0] = a*2;
    array[1] = b*2;
    return array;
}
[/cpp]



### Récupérer ce tableau


[cpp]
int *array = multiplierParDeux(2, 4);
cout << array[1]; // retournera 8
[/cpp] 
