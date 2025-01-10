---
layout: default
title: Chapitre 9 - Les graphes
permalink: /09-graphes/
published: true
date: 2024
---

# Les graphes

## 1) introduction

Imaginez un réseau social ayant 6 abonnés (A, B, C, D, E et F) où :

- A est ami avec B, C et D
- B est ami avec A et D
- C est ami avec A, E et D
- D est ami avec tous les autres abonnés
- E est ami avec C, D et F
- F est ami avec E et D

La description de ce réseau social, malgré son faible nombre d'abonnés, est déjà quelque peu rébarbative, alors imaginez cette même description avec un réseau social comportant des millions d'abonnés !

Il existe un moyen plus "visuel" pour représenter ce réseau social : on peut représenter chaque abonné par un cercle (avec le nom de l'abonné situé dans le cercle) et chaque relation "X est ami avec Y" par un segment de droite reliant X et Y ("X est ami avec Y" et "Y est ami avec X" étant représenté par le même segment de droite).

Voici ce que cela donne avec le réseau social décrit ci-dessus :

![c9c_1](https://github.com/user-attachments/assets/008be603-bfbf-4216-aa13-0a8553c362d6)

##### Exercice 1
>
>Construisez un graphe de réseau social à partir des informations suivantes :
>
>- A est ami avec B et E
>- B est ami avec A et C
>- C est ami avec B,F et D
>- D est ami avec C,F et E
>- E est ami avec A,D et F
>- F est ami avec C, D et E

## 2) notion de graphes

Ce genre de figure s'appelle **un graphe**. Les graphes sont des objets mathématiques très utilisés, notamment en informatique. Les cercles sont appelés **des sommets** et les segments de droites qui relient 2 sommets **des arêtes**.

Plus formellement on dira qu'un graphe G est un couple G = (V,E) avec V un ensemble de sommets et E un ensemble d'arêtes.

Autre utilisation possible des graphes : les logiciels de cartographie (ces logiciels sont souvent utilisés couplés à des récepteurs GPS). Ces logiciels de cartographie permettent, connaissant votre position grâce à un récepteur GPS, d'indiquer la route à suivre pour se rendre à un endroit B. Comment modéliser l'ensemble des lieux et des routes ? Simplement à l'aide d'un graphe ! Chaque lieu est un sommet et les routes qui relient les lieux entre eux sont des arêtes.

Soit les lieux suivants : A, B, C, D, E, F et G.

Les différents lieux sont reliés par les routes suivantes :

- il existe une route entre A et C
- il existe une route entre A et B
- il existe une route entre A et D
- il existe une route entre B et F
- il existe une route entre B et E
- il existe une route entre B et G
- il existe une route entre D et G
- il existe une route entre E et F

Ici aussi, la représentation sous forme de graphe s'impose :

![c9c_2](https://github.com/user-attachments/assets/94ac4f2a-d0b3-4004-bd60-6ac12a8a7115)

Problème : avec cette représentation du réseau routier sous forme de graphe, il est impossible de tenir compte des routes en sens unique (par exemple il est possible d'aller de A vers D mais pas de D vers A)

Voici de nouvelles contraintes :

- il existe une route entre A et C (double sens)
- il existe une route entre A et B (sens unique B->A)
- il existe une route entre A et D (sens unique A->D)
- il existe une route entre B et F (sens unique B->F)
- il existe une route entre B et E (sens unique E->B)
- il existe une route entre B et G (double sens)
- il existe une route entre D et G (double sens)
- il existe une route entre E et F (double)

Pour tenir compte de ces nouvelles contraintes, on utilisera **un graphe orienté** :

![c9c_3](https://github.com/user-attachments/assets/f9a5da7d-72dc-4005-a469-d43e541cdd13)

Dans un graphe orienté, les arêtes possèdent une orientation. Ces "arêtes orientées" sont souvent appelées "**arcs**". On dira qu'un graphe orienté G est un couple G = (V,A) avec V un ensemble de sommets et A un ensemble d'arcs.

Parfois il est intéressant d'associer aux arrêtes ou aux arcs des valeurs, on parle alors de **graphes pondérés**. Si nous revenons à notre "graphe cartographie", il est possible d'associer à chaque arête la distance en Km entre les 2 lieux :

![c9c_4](https://github.com/user-attachments/assets/2652b973-1c46-4e08-ba6f-9d1875bf8442)

Il est aussi possible d'associer à chaque arête la durée du trajet entre 2 points :

![c9c_5](https://github.com/user-attachments/assets/765b83b5-9902-4303-9634-0700e9e31fbd)

En fonction du choix fait par le conducteur (trajet le plus court en distance ou trajet le plus court en temps), l'algorithme permettant de déterminer le chemin le plus court entre 2 points travaillera sur le graphe correspondant. À noter que le graphe pondéré en minutes peut évoluer au cours du temps en fonction du trafic routier : une application comme Waze utilise les données en provenance des utilisateurs de l'application afin de mettre à jour en temps réel le graphe.

Pour terminer avec ces généralités sur les graphes, voici 2 définitions qui nous seront utiles par la suite :

- **Une chaine** est une suite d'arêtes consécutives dans un graphe, un peu comme si on se promenait sur le graphe. On la désigne par les lettres des sommets qu'elle comporte.
- **Un cycle** est une chaine qui commence et se termine au même sommet.

## 3) implémentation des graphes

Il existe deux méthodes permettant d'implémenter un graphe : **les matrices d'adjacences** et **les listes d'adjacences**.

### a) implémentation d'un graphe à l'aide d'une matrice d'adjacence

Une matrice est un tableau à double entrée :

![c9c_6](https://github.com/user-attachments/assets/b56f4286-1e8a-4af0-8f1b-205297fda81d)

La matrice A ci-dessus est constitué de 5 lignes et 4 colonnes. On appelle matrice carrée une matrice qui comporte le même nombre de lignes et de colonnes. Les matrices d'adjacences sont des matrices carrées.

Reprenons l'exemple du "graphe cartographie" :

![c9c_2](https://github.com/user-attachments/assets/85dd5e61-7469-4526-b935-957fb3399ecb)

Voici la matrice d'adjacence de ce graphe :

![c9c_7](https://github.com/user-attachments/assets/369c4f13-0571-4621-bd3e-ebe7ae38ab04)

Comment construire une matrice d'adjacence ?

Il faut savoir qu'à chaque ligne correspond un sommet du graphe et qu'à chaque colonne correspond aussi un sommet du graphe. À chaque intersection ligne i - colonne j (ligne i correspond au sommet i et colonne j correspond au sommet j), on place un 1 s'il existe une arête entre le sommet i et le sommet j, et un zéro s'il n'existe pas d'arête entre le sommet i et le sommet j.

![c9c_8](https://github.com/user-attachments/assets/053df0cd-587d-4c13-8bd7-b4fae6dada4c)

- Il existe une arête entre le sommet E et le sommet F, nous avons donc placé un 1 à l'intersection de la ligne E et de la colonne F (il en est de même à l'intersection de la ligne F et de la colonne E)
- Il n'existe pas d'arête entre le sommet D et le sommet C, nous avons donc placé un 0 à l'intersection de la ligne D et de la colonne C (il en est de même à l'intersection de la ligne C et de la colonne D)

##### Exercice 2
>
>Soit le graphe suivant :
>![c9a_1](https://github.com/user-attachments/assets/98925320-7a92-4198-b776-22621ad8719c)
>Déterminez sa matrice d'adjacence.

Il est aussi possible d'établir une matrice d'adjacence pour un graphe orienté. Le principe reste le même : si le sommet i (ligne) est lié au sommet j (colonne), nous avons un 1 à l'intersection (0 dans le cas contraire).

![c9c_3](https://github.com/user-attachments/assets/b6b785a7-d08c-41da-aa16-9060d1d3c016)

![c9c_9](https://github.com/user-attachments/assets/1787205b-395d-4a5c-a781-f18ba07f19c7)

Il est aussi possible d'utiliser une matrice d'adjacence pour implémenter un graphe pondéré : on remplace les 1 par les valeurs liées à chaque arc.

![c9c_5](https://github.com/user-attachments/assets/b760ea19-6ae6-4a07-bc0f-8ab7db701434)

![c9c_10](https://github.com/user-attachments/assets/61fe2d29-ecd8-4c85-9fb5-5a83f134ee3f)

Il est assez simple d'utiliser les matrices d'adjacence en Python grâce aux tableaux de tableaux vus l'année dernière :

```python
#matrice d'ajacence
m = [[0, 1, 1, 1, 0, 0, 0],
     [1, 0, 0, 0, 1, 1, 1],
     [1, 0, 0, 0, 0, 0, 0],
     [1, 0, 0, 0, 0, 0, 1],
     [0, 1, 0, 0, 0, 1, 0],
     [0, 1, 0, 0, 1, 0, 0],
     [0, 1, 0, 1, 0, 0, 0]]

```
### b) implémentation d'un graphe à l'aide de listes d'adjacence

Pour commencer, on définit une liste des sommets du graphe. À chaque élément de cette liste, on associe une autre liste qui contient les sommets lié à cet élément :

Reprenons l'exemple du "graphe cartographie" :

![c9c_2](https://github.com/user-attachments/assets/69b249e6-1ec8-4951-9a26-73ff09b33c84)

Voici la liste d'adjacence de ce graphe :

![c9c_11](https://github.com/user-attachments/assets/20f34a9c-c5af-41db-bf75-f73ec1c9ee51)

##### Exercice 3
>
>Établissez la liste d'adjacence du graphe ci-dessous.
>![c9a_1](https://github.com/user-attachments/assets/98925320-7a92-4198-b776-22621ad8719c)

Pour les graphes orientés, il est nécessaire de définir 2 listes : la liste des **successeurs** et la liste des **prédécesseurs**. Soit un arc allant d'un sommet A vers un sommet B (flèche de A vers B). On dira que B est un successeur de A et que A est un prédécesseur de B.

![c9c_3](https://github.com/user-attachments/assets/09f41337-6728-4617-be4e-b419500a05de)

liste d'adjacence successeurs du graphe orienté cartographie :

![c9c_13](https://github.com/user-attachments/assets/7a3a4256-83c8-4935-9584-2e3ce1d6e6ab)

liste d'adjacence prédécesseurs du graphe orienté cartographie :

![c9c_12](https://github.com/user-attachments/assets/a8994043-de4c-486a-980e-8010c53359b4)

Il est possible de travailler avec des listes d'adjacences en Python en utilisant les dictionnaires :

```python
#liste d'ajacence
l = {'A':('B','C','D'), 'B':('A', 'E', 'F', 'G'), 'C':('A'), 'D':('A', 'G'), 'E':('B', 'F'), 'F':('B', 'E'), 'G':('B', 'D')}
```

##### Exercice 4
>
>Soit la matrice d'adjacence d'un graphe G composé des sommets A, B, C, D  :
>
>![c9a_2](https://github.com/user-attachments/assets/1749d035-a335-4bd1-aa45-a0ee67161ade)
>
>- le graphe G est-il orienté ou non-orienté ? Justifiez votre réponse.
>
>- représentez ce graphe G

##### Exercice 4
>
>Soit G un graphe non-orienté implémenté en Python comme suit :
>
>```python
>G = {'A':['B', 'C', 'E'], 'B':['A', 'E'], 'C':['A','D'], 'D':['C'], 'E':['A','B']}
>```
>Représentez le graphe G.

### c) matrice d'adjacence ou liste d'adjacence ?

Comment choisir l'implémentation à utiliser (matrice d'adjacence ou liste d'adjacence) ?

- le choix se fait en fonction de la densité du graphe, c'est-à-dire du rapport entre le nombre d'arêtes et le nombre de sommets. Pour un graphe dense on utilisera plutôt une matrice d'adjacence.
- certains algorithmes travaillent plutôt avec les listes d'adjacences alors que d'autres travaillent plutôt avec les matrices d'adjacences. Le choix doit donc aussi dépendre des algorithmes utilisés (nous aurons très prochainement l'occasion d'étudier plusieurs de ces algorithmes).
  
