---
layout: default
title: Chapitre 7 - Les arbres
permalink: /07-arbres/
published: true
date: 2024
---

# Les arbres

## 1) La notion d'arbre 

Un organisateur de tournoi de rugby recherche la meilleure solution pour afficher les potentiels quarts de final, demi-finales et finale :

Au départ nous avons 4 poules de 4 équipes. Les 4 équipes d'une poule s'affrontent dans un mini championnat (3 matchs par équipe). À l'issue de cette phase de poule, les 2 premières équipes de chaque poule sont qualifiées pour les quarts de finale.

Dans ce qui suit, on désigne les 2 qualifiés par poule par :

- Poule 1 => 1er = Eq1 ; 2e = Eq8
- Poule 2 => 1er = Eq2 ; 2e = Eq7
- Poule 3 => 1er = Eq3 ; 2e = Eq6
- Poule 4 => 1er = Eq4 ; 2e = Eq5

En quart de final, on va avoir :

- quart de finale 1 => Eq1 contre Eq5
- quart de finale 2 => Eq2 contre Eq6
- quart de finale 3 => Eq3 contre Eq7
- quart de finale 4 => Eq4 contre Eq8

Pour les demi-finales on aura :

- demi-finale 1 => vainqueur quart de finale 1 contre vainqueur quart de finale 3
- demi-finale 2 => vainqueur quart de finale 2 contre vainqueur quart de finale 4

L'organisateur du tournoi affiche les informations ci-dessus le jour du tournoi. Malheureusement, la plupart des spectateurs se perdent quand ils cherchent à déterminer les potentielles demi-finales.

Pourtant, un simple graphique aurait grandement simplifié les choses :

![nsi_term_structDo_arbre_1](https://github.com/user-attachments/assets/4c8ff017-92da-4835-9d0f-e0806fcf1da8)

Nous avons ci-dessous ce que l'on appelle **une structure en arbre**. On peut aussi retrouver cette même structure dans un arbre généalogique :

![nsi_term_structDo_arbre_2](https://github.com/user-attachments/assets/1ad01db8-2ca3-48d3-9a25-851f7d631160)

Dernier exemple, les systèmes de fichiers dans les systèmes de type UNIX ont aussi une structure en arbre (notion vue l'année dernière)

![nsi_prem_base_linux_2](https://github.com/user-attachments/assets/bc0332fe-0c99-4461-93ab-b9d7d10cc92e)

Les arbres sont des **types abstraits** très utilisés en informatique. On les utilise notamment quand on a besoin d'une structure hiérarchique des données : dans l'exemple ci-dessous le fichier grub.cfg ne se trouve pas au même niveau que le fichier rapport.odt (le fichier grub.cfg se trouve "plus proche" de la racine / que le fichier rapport.odt). 

On ne pourrait pas avec une simple liste qui contiendrait les noms des fichiers et des répertoires, rendre compte de cette hiérarchie (plus ou moins "proche" de la racine). 

On trouve souvent dans cette hiérarchie une notion de temps (les quarts de finale sont avant les demi-finales ou encore votre grand-mère paternelle est née avant votre père), mais ce n'est pas une obligation (voir l'arborescence du système de fichiers).

## 2) Les arbres binaires

### a) Introduction

Les arbres binaires sont des cas particuliers d'arbres : l'arbre du tournoi de rugby et l'arbre "père, mère..." sont des arbres binaires, en revanche, l'arbre représentant la structure du système de fichier n'est pas un arbre binaire. **Dans un arbre binaire, on a au maximum 2 branches qui partent d'un élément.**

Dans la suite nous allons uniquement travailler sur les arbres binaires.

Soit l'arbre binaire suivant :

![nsi_term_structDo_arbre_3](https://github.com/user-attachments/assets/f0d586dc-3f7c-4eb6-8e99-0ddbdf304480)

### b) Un peu de vocabulaire

- chaque élément de l'arbre est appelé **noeud** (par exemple : A, B, C, D,...,P et Q sont des noeuds)
- le noeud initial (ici A) est appelé **racine**
- On dira que le noeud E et le noeud D sont **les fils** du noeud B. On dira que le noeud B est **le père** des noeuds E et D
- Dans un arbre binaire, un noeud possède **au plus 2 fils**
- Un noeud n'ayant aucun fils est appelé **feuille** (exemples : D, H, N, O, J, K, L, P et Q sont des feuilles)
- À chaque noeud d'un arbre binaire, on associe **une clé** (on peut aussi utiliser le terme "valeur" à la place de clé), un **sous-arbre gauche** et un **sous-arbre droit** (exemple : à partir du noeud ayant pour clé C on va trouver un sous-arbre gauche composé des noeuds F, J et K et un sous-arbre droit composé des noeuds G, L, M, P et Q)
- Un arbre (ou un sous-arbre) vide est noté **NIL** (NIL est une abréviation du latin nihil qui veut dire "rien"). Par exemple, le sous-arbre gauche du noeud D est NIL (même chose pour son sous-arbre droit d'ailleurs puisque D est une feuille).
- On appelle **arête** le segment qui relie 2 noeuds.
- On appelle **taille** d'un arbre le nombre de noeuds présents dans cet arbre
- On appelle **profondeur** d'un noeud ou d'une feuille dans un arbre binaire le nombre de noeud du chemin qui va de la racine à ce noeud. 
_ATTENTION : la racine peut être initialisé à une profondeur de 0 ou 1, cela vous sera toujours précisé. Par exemple, la profondeur de B est 1 si la racine est à 0, la profondeur de B est 2 si la racine est à une profondeur de 1._
- On appelle **hauteur** d'un arbre la profondeur maximale des noeud de l'arbre. Exemple : la profondeur de P = 5, c'est un des noeuds les plus profond, donc la hauteur de l'arbre est de 5.
_ATTENTION : comme pour la profondeur, on trouvera 2 approches différentes pour le calcul de la hauteur. Ici la hauteur de l'arbre est 5 si la racine est à 1, 4 si la racine est à 0._

### c) Structure récursive

Il est important de bien noter que l'on peut aussi voir les arbres comme des structures récursives : les fils d'un noeud sont des arbres (sous-arbre gauche et un sous-arbre droite dans le cas d'un arbre binaire), ces arbres sont eux-mêmes constitués d'arbres...

### d) Encadrement de la hauteur d'un arbre

Il est possible d'avoir des arbres binaires de même taille, mais de "forme" très différente :

![nsi_term_structDo_arbre_4](https://github.com/user-attachments/assets/870c0964-1700-4979-80ce-4cbc5b53919a)

Sur le schéma ci-dessus l'arbre 1 est dit **filiforme** alors que l'arbre 2 est dit **complet** (on dira qu'un arbre binaire est complet si tous les noeuds possèdent 2 fils et que toutes les feuilles se situent à la même profondeur).

Si on prend un arbre filiforme de taille $n$, on peut dire que la hauteur de cet arbre est égale à $n$ (si on prend la définition de la hauteur d'un arbre où la racine a une profondeur 1)

Si on prend un arbre complet de taille $n$, on peut démontrer que la hauteur de cet arbre est égale à $log_2(n+1)$. Dans le cas de l'arbre 2, nous avons $log_2(8)=3$ nous avons bien la hauteur de l'arbre 2 égale à 3 (si on prend la définition de la taille d'un arbre où la racine a une profondeur 1).

Un arbre filiforme et un arbre complet étant deux cas extrêmes, on peut affirmer que pour un arbre binaire quelconque :

$\lfloor log_2(n) \rfloor  \leq h \leq n-1$
				
avec n la taille de l'arbre et h la hauteur de l'arbre ($\lfloor log_2(n) \rfloor$ permet de prendre la partie entière du logarithme base 2 de n)

### e) les arbres binaires en Python

Python ne propose pas de façon native l'implémentation des arbres binaires. Mais nous aurons, plus tard dans l'année, l'occasion d'implémenter des arbres binaires en Python en utilisant la programmation orientée objet.

## 3) les arbres binaires de recherche 

Un arbre binaire de recherche est un cas particulier d'arbre binaire. Pour avoir un arbre binaire de recherche :

- il faut avoir un arbre binaire
- il faut que les clés de noeuds composant l'arbre soient ordonnables (on doit pouvoir classer les noeuds, par exemple, de la plus petite clé à la plus grande)
- soit x un noeud d'un arbre binaire de recherche. Si y est un noeud du sous-arbre gauche de x, alors il faut que y.clé ⩽ x.clé. Si y est un noeud du sous-arbre droit de x, il faut alors que x.clé ⩽ y.clé

exemple d'arbre binaire de recherche :

![](img/nsi_term_arbre_5.jpg)

Vous pouvez vérifier que le fils gauche d'un noeud a une valeur plus petite que son père (par exemple 3 < 6) et que le fils droit d'un noeud a une valeur plus grande que son père (par exemple 7 > 6)

Attention : pour un noeud donné A, tous les noeuds de l'arbre gauche de A auront des valeurs plus petites que la valeur du noeud A et tous les noeuds de l'arbre droit de A auront des valeurs plus grandes que la valeur du noeud A. 
