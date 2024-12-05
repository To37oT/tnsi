---
layout: default
title: Chapitre 8 - Algorithmes sur les arbres binaires
permalink: /08-algo-arbres/
published: true
date: 2024
---

# Algorithmes sur les arbres binaires

## 1) notations utilisées

Dans ce chapitre nous allons utiliser les notations suivantes :

Soit un arbre T : ```T.racine``` correspond au noeud racine de l'arbre T

Soit un noeud x :

- ```x.gauche``` correspond au sous-arbre gauche du noeud x
- ```x.droit``` correspond au sous-arbre droit du noeud x
- ```x.clé``` correspond à la clé du noeud x

Il faut noter que si le noeud x est une feuille, ```x.gauche``` et ```x.droite``` sont des arbres vides (NIL)

## 2) calculer la hauteur d'un arbre

Voici l'algorithme qui permet de calculer la hauteur d'un arbre :

```
VARIABLE
T : arbre
x : noeud

DEBUT
HAUTEUR(T) :
  si T ≠ NIL :
    x ← T.racine
    renvoyer 1 + max(HAUTEUR(x.gauche), HAUTEUR(x.droit))
  sinon :
    renvoyer 0
  fin si
FIN
```

N.B. la fonction max renvoie la plus grande valeur des 2 valeurs passées en paramètre (exemple : max(5,6) renvoie 6)

Nous avons ici un algorithme récursif. Vous aurez l'occasion de constater que c'est souvent le cas dans les algorithmes qui travaillent sur des structures de données telles que les arbres.

##### Exercice 1
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/d26d82e6-ec84-414d-9e47-7b7a4fd473a0)
>
>Appliquez l'algorithme qui permet de calculer le hauteur d'un arbre binaire à l'arbre ci-dessus. Quel résultat obtenez-vous ?

## 3) calculer la taille d'un arbre

Nous allons maintenant étudier un algorithme qui permet de calculer le nombre de noeuds présents dans un arbre.

```
VARIABLE
T : arbre
x : noeud

DEBUT
TAILLE(T) :
  si T ≠ NIL :
    x ← T.racine
    renvoyer 1 + TAILLE(x.gauche) + TAILLE(x.droit)
  sinon :
    renvoyer 0
  fin si
FIN
```

##### Exercice 2
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/d26d82e6-ec84-414d-9e47-7b7a4fd473a0)
>
>Appliquez l'algorithme qui permet de calculer la taille d'un arbre binaire à l'arbre ci-dessus. Quel résultat obtenez-vous ?

## 4) parcours d'un arbre

Il existe plusieurs façons de **parcourir un arbre** (parcourir un arbre = passer par tous les noeuds). Le choix du parcours dépend du problème à traiter

### a) parcourir un arbre dans l'ordre préfixe

Voici l'algorithme qui va permettre de parcourir un arbre dans l'ordre préfixe :

```
VARIABLE
T : arbre
x : noeud

DEBUT
PARCOURS-PREFIXE(T) :
  si T ≠ NIL :
    x ← T.racine
    affiche x.clé
    PARCOURS-PREFIXE(x.gauche)
    PARCOURS-PREFIXE(x.droit)
  fin si
FIN
```

**Dans le cas du parcours préfixe, on affiche chaque noeud avant de parcourir son sous-arbre gauche et son sous-arbre droit.**

##### Exercice 3
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/d26d82e6-ec84-414d-9e47-7b7a4fd473a0)
>
>Appliquez l'algorithme qui permet de trouver un parcours dans l'ordre préfixe à l'arbre ci-dessus. Quel résultat obtenez-vous ?


### b) parcourir un arbre dans l'ordre suffixe

Voici l'algorithme qui va permettre de parcourir un arbre dans l'ordre suffixe :

```
VARIABLE
T : arbre
x : noeud

DEBUT
PARCOURS-SUFFIXE(T) :
  si T ≠ NIL :
    x ← T.racine
    PARCOURS-SUFFIXE(x.gauche)
    PARCOURS-SUFFIXE(x.droit)
    affiche x.clé
  fin si
FIN
```

**Dans le cas du parcours suffixe, on affiche chaque noeud après avoir parcouru son sous-arbre gauche et son sous-arbre droit.**

##### Exercice 4
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/d26d82e6-ec84-414d-9e47-7b7a4fd473a0)
>
>Appliquez l'algorithme qui permet de trouver un parcours dans l'ordre suffixe à l'arbre ci-dessus. Quel résultat obtenez-vous ?

### c) parcourir un arbre dans l'ordre infixe

Voici l'algorithme qui va permettre de parcourir un arbre dans l'ordre infixe :

```
VARIABLE
T : arbre
x : noeud

DEBUT
PARCOURS-INFIXE(T) :
  si T ≠ NIL :
    x ← T.racine
    PARCOURS-INFIXE(x.gauche)
    affiche x.clé
    PARCOURS-INFIXE(x.droit)
  fin si
FIN
```

**Dans le cas du parcours infixe, pour un noeud A donné, on parcourra le sous-arbre gauche de A, puis on affichera la clé de A puis enfin, on parcourra le sous-arbre droite de A.**

##### Exercice 5
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/d26d82e6-ec84-414d-9e47-7b7a4fd473a0)
>
>Appliquez l'algorithme qui permet de trouver un parcours dans l'ordre infixe à l'arbre ci-dessus. Quel résultat obtenez-vous ?

### d) parcourir un arbre en largeur d'abord

Voici l'algorithme qui va permettre de parcourir un arbre en largeur d'abord :

```
T : arbre
Tg : arbre
Td : arbre
x : noeud
f : file (initialement vide)

DEBUT
PARCOURS-LARGEUR(T) :
  enfiler(T.racine, f) //on place la racine dans la file
  tant que f non vide :
    x ← defiler(f)
    affiche x.clé
    si x.gauche ≠ NIL :
      Tg ← x.gauche
      enfiler(Tg.racine, f)
    fin si
    si x.droit ≠ NIL :
      Td ← x.droite
      enfiler(Td.racine, f)
    fin si
  fin tant que
FIN
```

Vous noterez aussi que cet algorithme n'utilise pas de fonction récursive. Il est aussi important de bien noter l'utilisation d'une file (FIFO) pour cet algorithme de parcours en largeur.

**Dans le cas d'un parcours en largeur d'abord on affiche tous les noeuds situés à une profondeur n avant de commencer à afficher les noeuds situés à une profondeur n+1.**

##### Exercice 6
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/d26d82e6-ec84-414d-9e47-7b7a4fd473a0)
>
>Appliquez l'algorithme qui permet de trouver un parcours en largeur d'abord à l'arbre ci-dessus. Quel résultat obtenez-vous ?

## 5) algorithmes pour les arbres binaires de recherche

### a) Recherche d'une clé dans un arbre binaire de recherche

Nous allons maintenant étudier un algorithme permettant de rechercher une clé de valeur ```k``` dans un arbre binaire de recherche. Si ```k``` est bien présent dans l'arbre binaire de recherche, l'algorithme renvoie vrai, dans le cas contraire, il renvoie faux.

```
VARIABLE
T : arbre
x : noeud
k : entier
DEBUT
ARBRE-RECHERCHE(T,k) :
  si T == NIL :
    renvoyer faux
  fin si
  x ← T.racine
  si k == x.clé :
    renvoyer vrai
  fin si
  si k < x.clé :
    renvoyer ARBRE-RECHERCHE(x.gauche,k)
  sinon :
    renvoyer ARBRE-RECHERCHE(x.droit,k)
  fin si
FIN
```

Cet algorithme de recherche d'une clé dans un arbre binaire de recherche ressemble beaucoup à la recherche dichotomique vue en première dans le cas où l'arbre binaire de recherche traité est équilibré. 

La complexité en temps dans le pire des cas de l'algorithme de recherche d'une clé dans un arbre binaire de recherche équilibré est donc O(log<sub>2</sub>(n)). Dans le cas où l'arbre est filiforme, la complexité est O(n). Rappelons qu'un algorithme en O(log<sub>2</sub>(n)) est plus efficace qu'un algorithme en O(n).

À noter qu'il existe une version **itérative** (qui n'est pas récursive) de cet algorithme de recherche :

```
VARIABLE
T : arbre
x : noeud
k : entier
DEBUT
ARBRE-RECHERCHE_ITE(T,k) :
  x ← T.racine
  tant que T ≠ NIL et k ≠ x.clé :
    x ← T.racine
    si k < x.clé :
      T ← x.gauche
    sinon :
      T ← x.droit
    fin si
  fin tant que
  si k == x.clé :
    renvoyer vrai
  sinon :
    renvoyer faux
  fin si
FIN
```

##### Exercice 7
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/15cac7ae-95fe-4f74-843a-5310ad1c373e)
>
>Appliquez l'algorithme de recherche d'une clé dans un arbre binaire de recherche sur l'arbre ci-dessous. On prendra k = 13. Quel résultat obtenez-vous ?

##### Exercice 8
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/15cac7ae-95fe-4f74-843a-5310ad1c373e)
>
>Appliquez l'algorithme de recherche d'une clé dans un arbre binaire de recherche sur l'arbre ci-dessous. On prendra k = 16. Quel résultat obtenez-vous ?


### b) Insertion d'une clé dans un arbre binaire de recherche

Il est tout à fait possible d'insérer un noeud y dans un arbre binaire de recherche (non vide) :

```
VARIABLE
T : arbre
x : noeud
y : noeud
DEBUT
ARBRE-INSERTION(T,y) :
  x ← T.racine
  tant que T ≠ NIL :
    x ← T.racine
    si y.clé < x.clé :
      T ← x.gauche
    sinon :
      T ← x.droit
    fin si
  fin tant que
  si y.clé < x.clé :
    insérer y à gauche de x
  sinon :
    insérer y à droite de x
  fin si
FIN
```

### c) arbre binaire de recherche et parcours infixe

Il est important de noter qu'un parcours infixe d'un arbre binaire de recherche permet d'obtenir les valeurs des noeuds de l'arbre binaire de recherche dans l'ordre croissant.

##### Exercice 9
>Soit l'arbre suivant :
>
>![image](https://github.com/user-attachments/assets/15cac7ae-95fe-4f74-843a-5310ad1c373e)
>
>Appliquez l'algorithme qui permet de trouver un parcours dans l'ordre infixe à l'arbre ci-dessus. Quel résultat obtenez-vous ?

## 6) Implémentation des algorithmes pour les arbres binaires de recherche


##### Exercice 10
>Dans cette activité, nous allons implémenter des arbres binaires en Python en utilisant des dictionnaires (nous verrons un peu plus tard dans l'année une autre façon de procéder). L'idée est relativement simple : chaque noeud est modélisé à l'aide d'un dictionnaire, ces dictionnaires seront composés de 3 clés (et donc 3 valeurs) : une clé "valeur", une clé "arbre_gauche" et une clé "arbre_droit". La valeur associée à la clé "valeur" sera tout simplement la valeur du noeud. La valeur associé à la clé "arbre_gauche" sera un noeud (donc un autre dictionnaire) si l'arbre gauche existe et None dans le cas contraire. La valeur associée à la clé "arbre_droit" sera un noeud (donc un autre dictionnaire) si l'arbre droit existe et None dans le cas contraire.
>
>L'arbre binaire suivant :
>
>![image](https://github.com/user-attachments/assets/ade5d990-0712-4f25-b58a-ed65297af637)
>
>sera implémenté en Python avec le dictionnaire suivant :
>
>```
>arbre_1 = {"valeur" : "A", "arbre_gauche" : {"valeur" : "B", "arbre_gauche": {"valeur" : "D", "arbre_gauche": None, "arbre_droit": None}, "arbre_droit": {"valeur" : "E", "arbre_gauche": None, "arbre_droit": None}}, "arbre_droit" : {"valeur" : "C", "arbre_gauche": None, "arbre_droit": None}}
>```
>
>que l'on peut aussi représenter comme ceci afin d'améliorer la visibilité : 
>
>```
>arbre_1 = {"valeur":"A",
>            "arbre_gauche":
>                            {"valeur" : "B",
>                            "arbre_gauche": 
>                                            {"valeur" : "D", 
>                                            "arbre_gauche": None, 
>                                            "arbre_droit": None}, 
>                            "arbre_droit": {"valeur" : "E",
>                                            "arbre_gauche": None, 
>                                            "arbre_droit": None}}, 
>            "arbre_droit" : {"valeur" : "C", 
>                            "arbre_gauche": None, 
>                            "arbre_droit": None}}
>```
>
>1. Écrire en Python une fonction `taille` qui prend en paramètre un arbre `arb`(arbre implémenté sous forme de dictionnaire) et qui renvoie la taille de l'arbre `arb`.
>2. Écrire en Python une fonction `hauteur` qui prend en paramètre un arbre `arb`(arbre implémenté sous forme de dictionnaire) et qui renvoie la hauteur de l'arbre `arb`.
>3. Écrire en Python une fonction `parcours_prefixe` qui prend en paramètre un arbre `arb`(arbre implémenté sous forme de dictionnaire) et qui affiche les noeuds de l'arbre `arb` dans l'ordre préfixe.
>4. Écrire en Python une fonction `parcours_infixe` qui prend en paramètre un arbre `arb`(arbre implémenté sous forme de dictionnaire) et qui affiche les noeuds de l'arbre `arb` dans l'ordre infixe.
>5. Écrire en Python une fonction `parcours_suffixe` qui prend en paramètre un arbre `arb`(arbre implémenté sous forme de dictionnaire) et qui affiche les noeuds de l'arbre `arb` dans l'ordre suffixe.
>6. Écrire en Python une fonction `parcours_largeur` qui prend en paramètre un arbre `arb`(arbre implémenté sous forme de dictionnaire) et qui affiche les noeuds de l'arbre `arb` en respectant le parcours en largeur.
>7. Implémenter en Python un arbre binaire de recherche 'arbre_2' constitué des nombres suivants : 30, 0, 10, 40 et 20
>8. Écrire en Python une fonction récursive `arbre_recherche_rec` qui prend en paramètre un arbre binaire de recherche `arb`(arbre implémenté sous forme de dictionnaire) et un entier `k` et qui renvoie `True`si k est bien présent dans l'arbre et False dans le cas contraire.
>9. Écrire en Python une fonction non récursive `arbre_recherche_it` qui prend en paramètre un arbre binaire de recherche `arb`(arbre implémenté sous forme de dictionnaire) et un entier `k` et qui renvoie `True`si k est bien présent dans l'arbre et False dans le cas contraire.
>10. Écrire en Python une fonction non récursive `insertion` qui prend en paramètre un arbre binaire de recherche `arb`(arbre implémenté sous forme de dictionnaire) et un entier `k`et qui place l'entier `k`dans l'arbre binaire de recherche `arb`.
