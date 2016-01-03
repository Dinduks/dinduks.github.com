---
comments: true
date: 2008-06-16 01:35:00
layout: post
slug: j-apprends-le-c
title: J'apprends le C ! :p
categories:
- Development
---

Salut !

Bah l'été commence, et j'ai eu l'idée de reprendre le C.  
Je viens de commencer la révision de la partie console du SdZ (le lien à droite).

Quand j'avais fini tout le cours, j'avais codé une calculette, en me basant sur tout ce que j'avais appris. :)

Voici son code source :

    #include <stdlib.h>
    #include <math.h>

    int main(int argc, char *argv[])
    {
      long oper;
      float n1, n2, resul, df;


      while(1)
      {

      printf("  ==== Calculette ====\n\n");
      printf(" Choisissez le type d'operation a executer:\n");
      printf("  1. Addition\n");
      printf("  2. Soustraction\n");
      printf("  3. Multiplication\n");
      printf("  4. Division\n");
      printf("  5. Puissance\n");
      printf("  6. Carre\n");
      printf("  7. Racine carree\n");
      printf("  8. Sinus\n");
      printf("  9. Cosinus\n");
      printf(" 10. Tangente\n");
      printf(" 11. Quitter\n\n");
      printf(" Que voulez vous faire?  ");
      scanf("%ld", &oper;);
      printf("\n\n");


      switch(oper)
      {
      case 1:
          printf(" Veuillez rentrer le premier nombre:  ");
          scanf("%f", &n1;);
          printf(" Veuillez rentrer le deuxieme nombre:  ");
          scanf("%f", &n2;);
          resul = n1 + n2;
          printf(" \nResultat:  %f + %f = %f\n\n\n\n\n\n", n1, n2, resul);
          break;
        case 2:
          printf(" Veuillez rentrer le premier nombre:  ");
          scanf("%f", &n1;);
          printf(" Veuillez rentrer le deuxieme nombre:  ");
          scanf("%f", &n2;);
          resul = n1 - n2;
          printf(" \nResultat:  %f - %f = %f\n\n\n\n\n\n", n1, n2, resul);
          break;
        case 3:
          printf(" Veuillez rentrer le premier nombre:  ");
          scanf("%f", &n1;);
          printf(" Veuillez rentrer le deuxieme nombre:  ");
          scanf("%f", &n2;);
          resul = n1 * n2;
          printf(" \nResultat:  %f x %f = %f\n\n\n\n\n\n", n1, n2, resul);
          break;
      case 4:
            printf(" Veuillez rentrer le nombre a diviser:  ");
            scanf("%f", &n1;);
                  do
                  {
                        printf(" Veuillez rentrer le nombre diviseur:   ");
                        scanf("%f", &n2;);
                        if(n2 == 0)
                        {
                        printf(" Erreur! division par 0 impossible!\n\n");
                        }
                  }while(n2 == 0);
            resul = n1 / n2;
            printf(" Resultat: %f : %f = %f\n\n\n\n\n\n", n1, n2, resul);
            break;
      case 5:
            printf(" Veuillez rentrer le nombre dont vous voulez calculer la puissance:   ");
            scanf("%f", &n1;);
            printf(" Veuillez rentre la puissance:   ");
            scanf("%f", &n2;);
            resul = pow(n1, n2);
            printf(" La puissance de %f est %f\n\n\n\n\n\n", n1, resul);
      case 6:
            printf(" Veuillez rentrer le nombre dont on va calculer le carre:   ");
            scanf("%f", &n1;);
            resul = pow(n1, 2);
            printf(" Le carre de %f est %f\n\n\n\n\n\n", n1, resul);
            break;
      case 7:
            printf(" Veuillez le nombre dont vous voulez calculer la racine carree:   ");
            scanf("%f", &n1;);
            resul = sqrt(n1);
            printf(" La racine carree de %f est %f\n\n\n\n\n\n", n1, resul);
            break;
      case 8:
            printf(" Veuillez rentrer le degre dont vous voulez calculer le sinus:   ");
            scanf("%f", &n1;);
            resul = sin(n1);
            printf(" Le sinus de %f est %f\n\n\n\n\n\n", n1, resul);
            break;
      case 9:
            printf(" Veuillez rentrer le nombre dont vous voulez calculer le cosinus:   ");
            scanf("%f", &n1;);
            resul = cos(n1);
            printf(" Le cosinus de %f est %f\n\n\n\n\n\n", n1, resul);
            break;
      case 10:
            printf(" Veuillez rentrer le nombre dont vous voulez calculer la tangente:   ");
            scanf("%f", &n1;);
            resul = tan(n1);
            printf(" La tangent de %f est %f\n\n\n\n\n\n", n1, resul);
            break;
      case 11:
            printf(" Au revoir! :)\n\n\n\n\n\n");
            system("PAUSE");
            return 0;
            break;


      }



      }
      system("PAUSE");
      return 0;
    }

Gz Dinduks.
