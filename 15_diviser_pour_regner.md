---
layout: default
title: Chapitre 15 - Diviser pour régner
permalink: /15-diviser-pour-regner/
published: true
date: 2024
---

# Diviser pour régner

## 1) diviser pour régner

Le **diviser pour régner** est une **méthode algorithmique** basée sur le principe suivant :

On prend un problème (généralement complexe à résoudre), on divise ce problème en une multitude de petits problèmes, **l'idée étant que les petits problèmes seront plus simples à résoudre que le problème original**. Une fois les petits problèmes résolus, on recombine les petits problèmes résolus afin d'obtenir la solution du problème de départ.

La méthode "diviser pour régner" repose donc sur 3 étapes :

- **DIVISER** : le problème d'origine est divisé en un certain nombre de sous-problèmes

- **RÉGNER** : on résout les sous-problèmes (les sous-problèmes sont plus faciles à résoudre que le problème d'origine)

- **COMBINER** : les solutions des sous-problèmes sont combinées afin d'obtenir la solution du problème d'origine.

Les algorithmes basés sur la méthode "diviser pour régner" sont **très souvent des algorithmes récursifs**.

Nous allons maintenant étudier un de ces algorithmes basés sur le principe diviser pour régner : le tri-fusion

## 2) Tri-fusion  (merge sort en anglais)

### a) présentation

Nous avons déjà étudié en première 2 algorithmes de tri de **complexité quadratique** O(n²) : [**le tri par insertion**](https://fr.wikipedia.org/wiki/Tri_par_insertion){:target="_blank"} et [**le tri par sélection**](https://fr.wikipedia.org/wiki/Tri_par_s%C3%A9lection){:target="_blank"}. Nous allons maintenant étudier une nouvelle méthode de tri, **le tri-fusion**. Comme pour les algorithmes déjà étudiés, cet algorithme de tri fusion prend en entrée un tableau non trié et donne en sortie, le même tableau, mais trié. Cet algorithme permet de trier un tableau avec une meilleure complexité : O(nlog(n). Le principe de l’algorithme suit les phases de la méthode « diviser pour régner ».

>**Rappel :**
>
>log<sub>a</sub>(b) donne la puissance à laquelle il faudrait élever a pour obtenir b.
>
>Exemple :
>
>log<sub>2</sub>(8) = 3


#### Voici un exemple du fonctionnement du tri-fusion :

- Pour la découpe, on coupe simplement le tableau par son milieu. S’il possède n éléments, les deux sous-tableaux sont :

T1 = T[0 : n//2] et T2 = [n//2 + 1 : n].

- Les tableaux sont découpés tant qu'ils comportent plusieurs éléments. (DIVISER)

- On prépare ensuite les éléments pour la fusion. (RÉGNER)

- On tri le tableau en fusionnant les 2 sous-listes (COMBINER)

- Les éléments sont directements triés sur le tableau d'origine (grâce à la copie des valeurs)

[![image](https://github.com/user-attachments/assets/5c96d98e-a20b-4a73-8d0d-f31b45be471c)](https://github.com/user-attachments/assets/5c96d98e-a20b-4a73-8d0d-f31b45be471c){:target="_blank"}

Soit l'algorithme suivant :

```
VARIABLE
Tab : tableau d'entiers
L : tableau d'entiers (L pour left)
R : tableau d'entiers (R pour right)
p : entier (représente l'indice gauche)
q : entier (représente l'indice du milieu)
r : entier (représente l'indice à droite)
n1 : entier (nb d'élément à gauche lors de la fusion)
n2 : entier (nb d'élément à droite lors de la fusion)

DEBUT

FUSION (Tab, p, q, r):   (tableau initial, indice début, milieu, fin)
  n1 ← q - p + 1
  n2 ← r - q
  créer tableau L[1..n1] et R[1..n2]   (création de 2 tableaux vides)
  pour i ← 1 à n1:
    L[i] ← Tab[p+i-1]
  fin pour
  pour j ← 1 à n2:
    R[j] ← Tab[q+j]
  fin pour

  i ← 1
  j ← 1
  pour k ← p à r:
    si L[i] ⩽ R[j]:
      Tab[k] ← L[i]
      i ← i + 1
    sinon:
      Tab[k] ← R[j]
      j ← j + 1
    fin si
  fin pour
fin FUSION

TRI-FUSION(Tab, p, r):
  si p < r:
    q = (p + r) // 2
    TRI-FUSION(Tab, p, q)
    TRI-FUSION(Tab, q+1, r)
    FUSION(Tab, p, q, r)
  fin si
fin TRI-FUSION
FIN
```

**Pour trier un tableau Tab, on fait l'appel initial TRI-FUSION(Tab, 1, Tab.longueur)**

*Rappel : Attention, en algorithmique, les indices des tableaux commencent à 1*

Cet algorithme est composé de deux fonctions : FUSION et TRI-FUSION (fonction récursive). La fonction TRI-FUSION assure la phase "DIVISER" et la fonction FUSION assure les phases "RÉGNER" et "COMBINER".


##### Exercice 1
>
> Faire la liste, comme sur l'image plus haut, des différentes divisions et fusions qui vont avoir lieu sur le tri du tableau [23, 12, 4, 56, 35, 32, 42, 57, 3]

>**Rappel :**
>
>**Lorsqu'une fonction se termine, nous revenons à l'endroit où elle avait été précédemment appelée.**
>
>- Soit la fonction renvoie un élément et il faut le réceptionner.
>- Soit la fonction de renvoie rien et nous enchainons avec le reste du programme.

>**Une récursivité doit comporter une condition pour s'exécuter**

##### Exercice 2
>
>La fonction ```FUSION``` est appelée de nombreuses fois lors du tri du tableau de l'exercice 1.
>
> Si l'on ajoute un affichage du tableau ```Tab``` à la fin de la fonction de fusion, quel sera l'affichage successif du tableau ?
>
>```[23, 12, 4, 56, 35, 32, 42, 57, 3]```
>```[12, 23, 4, 56, 35, 32, 42, 57, 3]```
>```...```

### b) complexité

Le calcul rigoureux de la complexité de cet algorithme sort du cadre de ce cours. Mais, en remarquant que la première phase (DIVISER) consiste à couper les tableaux en deux plusieurs fois de suite, nous pouvons en déduire que la complexité tendra à être constante sur un grand nombre d'entrée (10 millions de valeur, c'est une division en plus que 5 millions). nous parlerons d'une complexité logarithmique. La deuxième phase consiste à faire des comparaisons entre les premiers éléments de chaque tableau à fusionner, on peut donc supposer que pour un tableau de n éléments, on aura n comparaisons (donc une complexité linéaire). En combinant ces 2 constations on peut donc dire que la complexité du tri-fusion est en O(nlog(n)) (la démonstration proposée ici n'a rien de rigoureux).

La comparaison des courbes de la fonction n<sup>2</sup> (en rouge) et nlog(n) (en bleu) :

![c15c_2](https://github.com/user-attachments/assets/f1f37565-6915-4861-8c80-1e28f1d5ecb0)

nous montre que l'algorithme de tri-fusion est plus efficace que l'algorithme de tri par insertion ou que l'algorithme de tri par sélection.

##### Exercice 3
>
> Proposer une implémentation de l'algorithme de tri-fusion.
>
>La création d'un tableau de n éléments peut se faire ainsi :
>
>```tab = n * [0]```
>
>Vous rencontrerez une erreur ```out of range``` dans la partie fusion, pourquoi et quelles modifications de l'algorithme pouvez-vous proposer ?

