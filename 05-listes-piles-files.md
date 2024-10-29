---
layout: default
title: Chapitre 5 - Listes Piles Files
permalink: /05-listes-piles-files/
published: true
date: 2024
---

# Listes Piles Files

## 1) introduction
De nombreux algorithmes manipulent des structures de données plus complexes que des simples nombres. Nous allons ici voir quelques-unes de ces structures de données : les listes, les piles et les files. Ces trois types de structures sont qualifiés de linéaires.

## 2) les listes
Une liste est une structure de données permettant de regrouper des données. Une liste **L** est composée de 2 parties : **sa tête** (souvent noté **car**), qui correspond au dernier élément ajouté à la liste, et sa **queue** (souvent noté **cdr**) qui correspond au reste de la liste. Le langage de programmation Lisp (inventé par John McCarthy en 1958) a été un des premiers langages de programmation à introduire cette notion de liste (Lisp signifie "list processing"). Voici **les seules opérations** qui peuvent être effectuées sur une liste :

- obtenir une liste vide (vide)
- tester si une liste est vide (estVide)
- obtenir le dernier élément ajouté à la liste (car)
- obtenir une liste contenant tous les éléments d'une liste à l'exception du dernier élément ajouté (cdr)
- construire une liste à partir d'un élément et d'un autre liste (cons)

Une liste vide est très souvent représentée par **nil**.

**Exemples :**

```python
L = vide()
```
permet d'obtenir une liste vide notée L

---

```python
estVide(L)
```
renvoie True

---

```python
L1 = cons(12, L)
```
permet d'obtenir une liste L1 qui contient le nombre 12

---

```python
estVide(L1)
```
renvoie False

---

```python
L1 = cons(15, L1)
```
désormais la liste L1 contient les nombres 15 et 12

---

```python
L1 = cons(1, cons(11, L1))
```
permet d'obtenir un liste L1 qui contient désormais les nombres 1, 11, 15 et 12

---

```python
car(L1)
```
renvoie 1, la liste L1 reste inchangée

---

```python
L2 = cdr(L1)
```
la liste L2 contient 11,15 et 12 (la liste L1 reste inchangée)

##### exercice 1
>
>Soit la suite d'instructions suivantes :
>
>```python
>L = vide()
>L = cons(2, cons(15, cons (23, L)))
>L1 = cdr(L)
>res = car(L1)
>L1 = cons(4, cons(3, L1))
>```
>Donnez le contenu des listes **L** et **L1** et la valeur de **res** à la fin du programme.

## 3) les  piles

On retrouve dans les piles une partie des propriétés vues sur les listes. Dans les piles, il est uniquement possible de manipuler le dernier élément introduit dans la pile. On prend souvent l'analogie avec une pile d'assiettes : dans une pile d'assiettes la seule assiette directement accessible est la dernière assiette qui a été déposée sur la pile.

![image](https://github.com/user-attachments/assets/f3614086-9f6c-4b33-ac6d-fe5707e52610)

Les piles sont basées sur le principe **LIFO** (Last In First Out : le dernier rentré sera le premier à sortir). On retrouve souvent ce principe LIFO en informatique.

Voici les opérations que l'on peut réaliser sur une pile :

- on peut savoir si une pile est vide (estVide)
- on peut empiler un nouvel élément sur la pile (empiler en français, push en anglais)
- on peut récupérer l'élément au sommet de la pile tout en le supprimant. On dit que l'on dépile (dépiler en français, pop en anglais)
- on peut connaitre le nombre d'éléments présents dans la pile (taille)

**Exemples :**

Soit une pile P composée des éléments suivants : 12, 14, 8, 7, 19 et 22 (le sommet de la pile est 22) **Pour chaque exemple ci-dessous on repart de la pile d'origine** :

```python
dépile(P)
```
renvoie 22 et la pile P est maintenant composée des éléments suivants : 12, 14, 8, 7 et 19 (le sommet de la pile est 19)

---

```python
empile(P,42)
```
la pile P est maintenant composée des éléments suivants : 12, 14, 8, 7, 19, 22 et 42  (le sommet de la pile est 42)

---

Si on applique dépile(P) 6 fois de suite, estVide(P) renvoie vrai

---

Après avoir appliqué dépile(P) une fois, taille(P) renvoie 5

---

##### exercice 2
>
>Soit une pile P initialement vide. Soit les instructions suivantes :
>
>```python
>empile(P,4)
>empile(P,7)
>var1 = dépile(P)
>var2 = taille(P)
>var3 = dépile(P)
>empile(P,3)
>empile(P,2)
>var4 = taille(P)
>```
>
>Donnez le contenu de la pile **P**, la valeur de **var1**, la valeur de **var2**, la valeur de **var3** et la valeur de **var4**.

## 4)  les  files
Comme les piles, les files ont des points communs avec les listes. Différences majeures : dans une file on ajoute des éléments à une extrémité de la file et on supprime des éléments à l'autre extrémité. On prend souvent l'analogie de la file d'attente devant un magasin pour décrire une file de données.

![image](https://github.com/user-attachments/assets/7bc91180-31d0-45ce-b4c6-c1aa2f719ef1)

Les files sont basées sur le principe **FIFO** (First In First Out : le premier qui est rentré sera le premier à sortir). Ici aussi, on retrouve souvent ce principe FIFO en informatique.

Voici les opérations que l'on peut réaliser sur une file :

- on peut savoir si une file est vide (estVide)
- on peut ajouter un nouvel élément à la file (enfiler en français, enqueue en anglais)
- on peut récupérer l'élément situé en bout de file tout en le supprimant (défiler en français, dequeue en anglais)
- on peut connaitre le nombre d'éléments présents dans la file (taille)

**Exemples :**

Soit une file F composée des éléments suivants : 12, 14, 8, 7, 19 et 22 (le premier élément rentré dans la file est 22 ; le dernier élément rentré dans la file est 12). **Pour chaque exemple ci-dessous on repart de la file d'origine** :

```python
enfile(F,42)
```
la file F est maintenant composée des éléments suivants : 42, 12, 14, 8, 7, 19 et 22 (le premier élément rentré dans la file est 22 ; le dernier élément rentré dans la file est 42)

---

```python
défile(F)
```
la file F est maintenant composée des éléments suivants : 12, 14, 8, 7, et 19 (le premier élément rentré dans la file est 19 ; le dernier élément rentré dans la file est 12)

---

Autre variante :

```python
var = défile(F)
```
la file F est maintenant composée des éléments suivants : 12, 14, 8, 7, et 19 (comme précédemment)

**var** contient la valeur 22

---

si on applique défile(F) 6 fois de suite, estVide(F) renvoie vrai

---

après avoir appliqué défile(F) une fois, taille(F) renvoie 5.

---

##### exercice 3
>
>Soit une file F initialement vide. Soit les instructions suivantes :
>
>```python
>enfile(F,6)
>enfile(F,3)
>var1 = défile(F)
>enfile(F,9)
>var2 = taille(F)
>enfile(F,17)
>var3 = défile(F)
>enfile(F,2)
>var4 = taille(F)
>```
>
>Donnez le contenu de la file F, la valeur de var1, la valeur de var2, la valeur de var3 et la valeur de var4.

## 5) Types abstraits et représentation concrète des données

Nous avons évoqué ci-dessus la manipulation des types de données (liste, pile et file) par des algorithmes, mais le but de l'opération est souvent de traduire ces algorithmes dans un langage compréhensible pour un ordinateur (Python, Java, C,...). On dit alors que l'on **implémente un algorithme**. Il est donc aussi nécessaire d'implémenter les types de données comme les listes, les piles ou les files afin qu'ils soient utilisables par les ordinateurs. 

Les listes, les piles ou les files sont des types présents uniquement dans la tête des informaticiens, on dit que ce sont des **types abstraits**. 

Pour implémenter les listes (ou les piles et les files), beaucoup de langages de programmation utilisent 2 structures : **les tableaux** et **les listes chaînées**.

Un tableau est une suite contiguë de cases mémoires (les adresses des cases mémoire se suivent) :

![image](https://github.com/user-attachments/assets/54858c43-c4f8-490a-ace1-2a129e6d10f7)

Le système réserve une plage d'adresse mémoire afin de stocker des éléments.

![image](https://github.com/user-attachments/assets/e3774035-1ffc-44fb-b451-284365b7d6ae)

La taille d'un tableau est fixe : une fois que l'on a défini le nombre d'éléments que le tableau peut accueillir, il n'est pas possible modifier sa taille. Si l'on veut insérer une donnée, on doit créer un nouveau tableau plus grand et déplacer les éléments du premier tableau vers le second tout en ajoutant la donnée au bon endroit !

Dans certains langages de programmation, on trouve une version "évoluée" des tableaux : **les tableaux dynamiques**. Les tableaux dynamiques ont une taille qui peut varier. Il est donc relativement simple d'insérer des éléments dans le tableau. Ce type de tableaux permet d'implémenter facilement le type abstrait liste (de même pour les piles et les files).

À noter que les tableaux Python (type list) sont des tableaux dynamiques. **Attention de ne pas confondre avec le type abstrait liste défini ci-dessus avec le type list de python**.

Autre type de structure que l'on rencontre souvent et qui permet d'implémenter les listes, les piles et les files : les listes chaînées.

Dans une liste chaînée, à chaque élément de la liste on associe 2 cases mémoire : la première case contient l'élément et la deuxième contient l'adresse mémoire de l'élément suivant.

![image](https://github.com/user-attachments/assets/f2cf0e10-4aac-4acd-ab3d-fd088843a0f1)

Il est relativement facile d'insérer un élément dans une liste chaînée :

![image](https://github.com/user-attachments/assets/c7c33331-2938-4cf0-8b76-27c0118973ee)

## 6) Liste, pile, file avec Python

Soit le programme Python suivant :

```python
def vide():
    return None
def estVide(L):
    return L is None
def cons(x,L):
    return (x,L)
def car(L):
    return(L[0])
def cdr(L):
    return(L[1])
```

Prendre le temps d'analyser le programme.

Nous avons ici des fonctions permettant de simuler une liste.

##### Exercice 4
>
> Soit le prgramme suivant :
>
>```python
>L = vide()
>L = cons(12, cons(5, cons (32, L)))
>a = car(L)
>L1 = cdr(L)
>L1 = cons(42, cons(23, L1))
>```
>
>Quel résultat obtenez-vous ?

##### Exercice 5
>
>Soit le programme Python suivant :
>
>```python	
>pile = []
>tab = [5,8,6,1,3,7]
>pile.append(5)
>pile.append(10)
>pile.append(8)
>pile.append(15)
>for i in tab:
>    if i > 5:
>        pile.pop()
>```
>Donnez l’état de la pile après l’exécution de ce programme.

##### Exercice 6 
>
>Soit le programme Python suivant :
>
>```python
>from collections import deque
>file = deque([])
>tab = [2,78,6,89,3,17]
>file.append(5)
>file.append(10)
>file.append(8)
>file.append(15)
>for i in tab:
>    if i > 50:
>        file.popleft()
>```
>
>Donnez l’état de la file après l’exécution de ce programme

##### Exercice 7
>
>Python propose une implémentation des piles.
>
>Après avoir étudié la documentation consacrée à l'implémentation des piles en Python (voir [https://docs.python.org/fr/3/tutorial/datastructures.html](https://docs.python.org/fr/3/tutorial/datastructures.html#using-lists-as-stacks){:target="_blank"} partie 5.1.1), vous écrirez un programme permettant de vérifier que les réponses que vous avez apportées à l'activité 5.3 étaient correctes.

##### Exercice 8
>
>Python propose une implémentation des files.
>
>Après avoir étudié la documentation consacrée à l'implémentation des files en Python (voir [https://docs.python.org/fr/3/tutorial/datastructures.html](https://docs.python.org/fr/3/tutorial/datastructures.html#using-lists-as-queues){:target="_blank"} partie 5.1.2), vous écrirez un programme permettant de vérifier que les réponses que vous avez apportées à l'activité 5.5 étaient correctes.

##### Exercice 9
>
>Écrivez une fonction Python permettant de déterminer le nombre d'éléments présents dans une liste.

### exercices du bac

- [Sujet 1 2021 Exercice 1](https://pixees.fr/informatiquelycee/term/suj_bac/2021/sujet_01.pdf){:target="_blank"}
- [Sujet 3 2021 Exercice 5](https://pixees.fr/informatiquelycee/term/suj_bac/2021/sujet_03.pdf){:target="_blank"}
- [Sujet 6 2021 Exercice 5](https://pixees.fr/informatiquelycee/term/suj_bac/2021/sujet_06.pdf){:target="_blank"}
- [Sujet 7 2021 Exercice 1](https://pixees.fr/informatiquelycee/term/suj_bac/2021/sujet_07.pdf){:target="_blank"}
- [Sujet 8 2021 Exercice 5](https://pixees.fr/informatiquelycee/term/suj_bac/2021/sujet_08.pdf){:target="_blank"}
- [Sujet 1 2022 Exercice 4](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_01.pdf){:target="_blank"}
- [Sujet 2 2022 Exercice 1](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_02.pdf){:target="_blank"}
- [Sujet 3 2022 Exercice 2](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_03.pdf){:target="_blank"}
- [Sujet 4 2022 Exercice 5](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_04.pdf){:target="_blank"}
- [Sujet 10 2022 Exercice 1](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_10.pdf){:target="_blank"}
- [Sujet 11 2022 Exercice 1](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_11.pdf){:target="_blank"}
- [Sujet 14 2022 Exercice 5](https://pixees.fr/informatiquelycee/term/suj_bac/2022/sujet_14.pdf){:target="_blank"}
