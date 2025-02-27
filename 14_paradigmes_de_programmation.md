---
layout: default
title: Chapitre 14 - Paradigmes de programmation
permalink: /14-paradigmes-de-programmation/
published: true
date: 2024
---

# paradigmes de programmation

## 1) introduction

Jusqu'à présent nous avons vu un seul paradigme de programmation (manière de construire du code) : **la programmation impérative**. La programmation impérative repose sur des notions qui vous sont familières :

- la séquence d'instructions (les instructions d'un programme s'exécutent l'une après l'autre)
- l'affectation (on attribue une valeur à une variable, par exemple : a = 5)
- l'instruction conditionnelle (if / else)
- la boucle (while et for)

La programmation impérative n'est pas le seul paradigme de programmation. Nous allons étudier deux autres paradigmes : le **paradigme objet** et le **paradigme fonctionnel**.

## 2) le paradigme fonctionnel

Le paradigme fonctionnel cherche à éviter au maximum les effets de bord : on va éviter de modifier les valeurs associées à des variables. 

On va chercher au maximum à utiliser les fonctions (d'où le nom de programmation fonctionnelle), mais ces fonctions ne devront pas modifier les variables : en programmation fonctionnelle, on s’efforce de coder des fonctions qui ne modifient pas l’état courant des variables. Les fonctions utilisées en programmation fonctionnelle sont parfois appelées "fonction pure" : le résultat renvoyé par une fonction pure doit uniquement dépendre des paramètres passés à la fonction et pas des valeurs externes à la fonction :

Intéressons-nous au programme Python suivant :

```python
i = 5
def fct():
  if i > 5:
    return True
  else :
    return False
fct()
```

La fonction ci-dessus n'est pas une fonction pure, car la valeur renvoyée par la fonction fct (True ou False) dépend d'une valeur extérieure à la fonction.

Alors que dans ce cas :

```python
def fct(i):
  if i > 5:
    return True
  else :
    return False
fct(5)
```

La fonction ci-dessus est une fonction pure, car la valeur renvoyée par la fonction fct (True ou False) dépend uniquement du paramètre passé à la fonction.

Même si certains langages de programmation ont été conçus pour imposer au programmeur le paradigme fonctionnel (Lisp, Scheme, Haskell...), il est tout à fait possible d'utiliser le paradigme fonctionnel avec des langages de programmation plus généralistes (Python par exemple).

Nous allons maintenant travailler sur un exemple de programme Python utilisant le paradigme fonctionnel :

Considérons le programme suivant :

```python
l = [4,7,3]
def ajout(i):
  l.append(i)
```

Le programme ci-dessus ne respecte pas le paradigme fonctionnel, car nous avons un effet de bord (la variable l est modifiée par la fonction ajout).

Alors que dans le cas ci-dessous :

```python
def ajout(i,l):
  tab = l + [i]
  return tab
```

La fonction ajout ne modifie aucune variable, elle crée un nouveau tableau (tab) à partir du tableau l et du paramètre i (le signe + permet de fusionner 2 tableaux en un seul, ce nouveau tableau est constitué des éléments contenus dans le tableau l auxquels on ajoute la valeur i), la fonction renvoie le tableau ainsi créé.

D'une façon plus générale, la méthode append de Python ne respecte pas le paradigme fonctionnel puisque append modifie une donnée existante. Le paradigme fonctionnel va amener le programmeur non pas à modifier une valeur existante, mais plutôt à créer une nouvelle grandeur à partir de la grandeur existante : une grandeur existante n'est jamais modifiée, donc aucun risque d'effet de bord.

## 3) le paradigme objet

La programmation orientée objet repose, comme son nom l'indique, sur le concept d'objet.

Un objet dans la vie de tous les jours, vous connaissez, mais en informatique, qu'est ce que c'est ? Une variable ? Une fonction ? Ni l'un ni l'autre, c'est un nouveau concept.

Imaginez un objet très complexe, par exemple un moteur de voiture : il est évident qu'en regardant cet objet, on est frappé par sa complexité. 

Imaginez que l'on enferme cet objet dans une boîte et que l'utilisateur de l'objet n'ait pas besoin d'en connaître son principe de fonctionnement interne pour pouvoir l'utiliser. L'utilisateur a, à sa disposition, des boutons, des manettes et des écrans de contrôle pour faire fonctionner l'objet, ce qui rend son utilisation relativement simple. 

La mise au point de ce moteur par des ingénieurs a été très complexe, en revanche son utilisation est relativement simple.

Programmer de manière orientée objet, c'est un peu reprendre cette idée : utiliser des objets sans se soucier de leur complexité interne. Pour utiliser ces objets, nous n'avons pas à notre disposition des boutons, des manettes ou encore des écrans de contrôle, mais **des attributs** et **des méthodes** (nous aurons l'occasion de revenir sur ces 2 concepts). Un des nombreux avantages de la programmation orientée objet (**POO**), est qu'il existe des milliers d'objets (on parle plutôt de classes, mais là aussi nous reviendrons sur ce terme de classe est peu plus loin) prêts à être utilisés (vous en avez déjà utilisé de nombreuses fois sans le savoir). On peut réaliser des programmes extrêmement complexes uniquement en utilisant des classes préexistantes.

Le début du paradigme objet date des années 60. Mais il faudra attendre le début des années 70 et la mise au point du langage Smalltalk pour que le paradigme objet gagne en popularité chez les informaticiens. De nombreux langages permettent d'utiliser le paradigme objet : C++, Java,...

Pour nous initier à la programmation orientée objet nous allons utiliser un langage que vous connaissez bien : Python. Python permet d'utiliser le paradigme impératif (comme nous l'avons fait jusqu'à présent), mais il permet aussi d'utiliser le paradigme objet. Il est même possible, comme nous le verrons plus loin, d'utiliser les 2 paradigmes dans un même programme.

La création d'une classe en python commence toujours par le mot ```class```. Ensuite toutes les instructions de la classe seront indentées :

```python
class LeNomDeMaClasse:
  #instructions de la classe
#La définition de la classe est terminée.
```

La classe est une espèce de moule, à partir de ce moule nous allons créer des objets (plus exactement nous parlerons d'instances). Par exemple, nous pouvons créer une classe voiture, puis créer différentes instances de cette classe (Peugeot407, Renault Espace,...). Pour créer une de ces instances, la procédure est relativement simple :

```python
peugeot407 = Voiture()
```

Cette ligne veut tout simplement dire : "crée un objet (une instance) de la classe Voiture que l'on nommera peugeot407."

Ensuite, rien ne nous empêche de créer une deuxième instance de la classe Voiture :

```python
renaultEspace = Voiture()
```

Pour développer toutes ces notions, nous allons écrire un premier programme :

Nous allons commencer par écrire une classe Personnage (qui sera dans un premier temps une coquille vide) et, à partir de cette classe créer 2 instances : bilbo et gollum :

```python
class Personnage:
  pass

gollum = Personnage()
bilbo = Personnage()
```

Pour l'instant, notre classe ne sert à rien et nos instances d'objet ne peuvent rien faire. Comme il n'est pas possible de créer une classe totalement vide, nous avons utilisé l'instruction pass qui ne fait rien. Ensuite nous avons créé 2 instances de la classe Personnage : gollum et bilbo.

Comme expliqué précédemment, une instance de classe possède des attributs et des méthodes. Commençons par les attributs :

Un attribut possède une valeur (un peu comme une variable). Nous allons associer un attribut vie à notre classe Personnage (chaque instance aura un attribut vie)

Ces attributs s'utilisent comme des variables, l'attribut vie pour bilbo sera noté :

```python
bilbo.vie
```

de la même façon l'attribut vie de l'instance gollum sera noté :

```python
gollum.vie
```

Considérons maintenant le programme suivant :

```python
class Personnage:
  pass

gollum=Personnage()
gollum.vie=20
bilbo=Personnage()
bilbo.vie=20
```

Comme pour une variable nous pouvons afficher la valeur référencée par un attribut. Il suffit de faire un ```print(bilbo.vie)``` ou taper dans la console ```bilbo.vie```. 

Définir les attributs en dehors d'une classe n'est pas une bonne pratique, en effet, nous ne respectons pas un principe de base de la POO : **l'encapsulation**

Il ne faut pas oublier que notre classe doit être enfermée dans une boîte pour que l'utilisateur puisse l'utiliser facilement sans se préoccuper de ce qui se passe à l'intérieur, or, ici, ce n'est pas vraiment le cas.

En effet, les attributs (gollum.vie et bilbo.vie), font partie de la classe et devraient donc être enfermés dans la boîte.

Pour résoudre ce problème, nous allons définir les attributs dans la classe à l'aide d'une méthode (une méthode est une fonction définie dans une classe) d'initialisation des attributs.

Cette méthode est définie dans le code source par la ligne :

```python
def __init__ (self)
  ...
```

La méthode ```init``` est automatiquement exécutée au moment de la création d'une instance. **Le mot self est obligatoirement le premier argument d'une méthode**.

Nous retrouvons ce mot self lors de la définition des attributs. La définition des attributs sera de la forme :

```python
self.vie=20
```

Le mot self représente l'instance. Quand vous définissez une instance de classe (bilbo ou gollum) le nom de votre instance va remplacer le mot self.

Dans le code source, nous allons avoir :

```python
class Personnage:
  def __init__ (self):
    self.vie=20
```

Ensuite lors de la création de l'instance gollum, python va automatiquement remplacer self par gollum et ainsi créer un attribut ```gollum.vie``` qui aura pour valeur de départ la valeur donnée à self.vie dans la méthode ```init```

Il se passera exactement la même chose au moment de la création de l'instance bilbo, on aura automatiquement la création de l'attribut ```bilbo.vie```.

Si nous saisissons le programme suivant :

```python
class Personnage:
  def __init__(self):
    self.vie=20

gollum=Personnage()
bilbo=Personnage()
```

et que nous affichons ```gollum.vie```, nous obtiendrons bien ```20```.

Nous pouvons passer des arguments à la méthode ```init``` (comme pour n'importe quelle fonction).

```python
class Personnage:
  def __init__(self, nbreDeVie):
    self.vie=nbreDeVie

gollum = Personnage(20)
bilbo = Personnage(15)
```

La valeur est attribuée au premier argument de la méthode init (en dehors de self)

SYNTHESE VOCABULAIRE

- Personnage = classe
- def __init__ = méthode
- self.vie = attribut
- nbreDeVie = variable
- gollum = instance
  
Nous allons créer 2 nouvelles méthodes :

- Une méthode qui enlèvera un point de vie au personnage blessé
- Une méthode qui renverra le nombre de vies restantes

Intéressons-nous à ce programme :

```python
class Personnage:
  def __init__(self, nbreDeVie):
    self.vie=nbreDeVie
  def donneEtat (self):
    return self.vie
  def perdVie (self):
    self.vie=self.vie-1

gollum = Personnage(20)
bilbo = Personnage(15)
```

- ```gollum.donneEtat()``` affiche 20
 
- ```bilbo.donneEtat()``` affiche 15

- ```gollum.perdVie()``` enlève 1 à l'attribut ```vie``` de ```gollum```

- ```gollum.donneEtat()``` affiche maintenant 19

- ```bilbo.perdVie()``` enlève 1 à l'attribut ```vie``` de ```bilbo``

- ```bilbo.donneEtat()``` affiche 14

Vous avez sans doute remarqué que lors de l'utilisation des instances bilbo et gollum, nous avons uniquement utilisé des méthodes et nous n'avons plus directement utilisé des attributs (plus de "gollum.vie"). 

Il est important de savoir qu'en dehors de la classe l'utilisation des attributs est une mauvaise pratique en programmation orientée objet : les attributs doivent rester à l'intérieur de la classe.

L'utilisateur de la classe ne doit pas les utiliser directement. Il peut les manipuler, mais uniquement par l'intermédiaire d'une méthode (la méthode self.perdVie() permet de manipuler l'attribut self.vie)

Programme avec les méthodes :

```python
class Personnage:
  def __init__(self, nbreDeVie):
    self.vie=nbreDeVie
  def donneEtat (self):
    return self.vie
  def perdVie (self):
    self.vie=self.vie-1

bilbo = Personnage(15)
bilbo.perdVie()
point=bilbo.donneEtat()
```
Après l'exécution du programme ci-dessus, la variable ```point``` aura pour valeur 14

Selon le type d'attaque subit, le personnage peut perdre plus ou moins de points de vie. Pour tenir compte de cet élément, il est possible d'ajouter un paramètre à la méthode perdVie :

```python
class Personnage:
  def __init__(self, nbreDeVie):
    self.vie=nbreDeVie
  def donneEtat (self):
    return self.vie
  def perdVie (self,nbPoint):
    self.vie=self.vie-nbPoint

bilbo = Personnage(15)
bilbo.perdVie(2)
point=bilbo.donneEtat()
```

Après l'exécution du programme ci-dessus, la variable ```point``` aura pour valeur 13

Il est possible d'ajouter une part d'aléatoire dans la méthode perdVie :

```python
import random
class Personnage:
  def __init__(self, nbreDeVie):
    self.vie=nbreDeVie
  def donneEtat (self):
    return self.vie
  def perdVie (self):
    if random.random()>0.5:
      nbPoint = 1
    else :
      nbPoint = 2
    self.vie=self.vie-nbPoint

bilbo = Personnage(15)
bilbo.perdVie()
point=bilbo.donneEtat()
```

N.B : ```random.random()``` renvoie une valeur aléatoire comprise entre 0 et 1

Comme vous l'avez remarqué, il est possible d'utiliser une instruction conditionnelle (if / else) dans une méthode. Il est donc possible d'utiliser dans le même programme le paradigme objet et le paradigme impératif.

Il est maintenant possible d'organiser un combat virtuel entre nos 2 personnages grâce à la classe ```Personnage``` que nous venons de créer :

```python
import random

class Personnage:
  def __init__(self, nbreDeVie):
    self.vie=nbreDeVie
  def donneEtat (self):
    return self.vie
  def perdVie (self):
    if random.random()>0.5:
      nbPoint = 1
    else :
      nbPoint = 2
    self.vie=self.vie-nbPoint

def game():
  bilbo = Personnage(20)
  gollum = Personnage(20)
  while bilbo.donneEtat()>0 and gollum.donneEtat()>0 :
    bilbo.perdVie()
    gollum.perdVie()
  if bilbo.donneEtat()<=0 and gollum.donneEtat()>0:
    msg = f"Gollum est vainqueur, il lui reste encore {gollum.donneEtat()} points alors que Bilbo est mort"
  elif gollum.donneEtat()<=0 and bilbo.donneEtat()>0:
    msg = f"Bilbo est vainqueur, il lui reste encore {bilbo.donneEtat()} points alors que Gollum est mort"
  else :
    msg = "Les deux combattants sont morts en même temps"
  return msg
```
 
Nous avons encore ici la démonstration qu'il est possible d'utiliser le paradigme objet et le paradigme impératif dans un même programme.
 
## 4) conclusion

Il est important de bien comprendre qu'un programmeur doit maitriser plusieurs paradigmes de programmation (impératif, objet ou encore fonctionnelle). En effet, il sera plus facile d'utiliser le paradigme objet dans certains cas alors que dans d'autres situations, l'utilisation du paradigme fonctionnel sera préférable. 

Il est aussi important de bien comprendre que la frontière entre ces différents paradigmes est parfois floue, par exemple on utilise très souvent de l'impératif en programmation orientée objet.  

##### Exercice 1
>
>Soit la classe *Personnage* suivante :
>
>```py
>class Personnage:
>    def __init__(self, nbreDeVie):
>        self.vie=nbreDeVie
>    def donneEtat (self):
>        return self.vie
>    def perdVie (self,nbPoint):
>        self.vie=self.vie-nbPoint
>```
>Ajoutez une méthode *soigne* qui permettra d'augmenter l'attribut *vie* d'une  valeur *nbr* (*nbr* sera un paramètre de la méthode *soigne*).
>
>Testez cette méthode en saisissant dans la console Python les instructions suivantes (les unes après les autres) :
>
>- toto = Personnage(15)
>
>- toto.donneEtat()
>
>- toto.perdVie(2)
>
>- toto.soigne(3)
>
>- toto.donneEtat()

##### Exercice 2
>
>Écrivez une classe *Voiture* qui aura un attribut *vitesse* et 3 méthodes :
>
>- une méthode *accelere* qui permettra d'incrémenter l'attribut vitesse d'une unité
>- une méthode *freine* qui permettra de diminuer la vitesse
>- une méthode *getVitesse* qui renverra la valeur de la vitesse

##### Exercice 3
>
>À partir de la classe créée à l'exercice 2, écrivez un programme qui permettra d'atteindre la vitesse de 3 km/h, d'afficher cette vitesse dans la console puis de freiner jusqu'à l'arrêt complet du véhicule.
