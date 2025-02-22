---
layout: default
title: Chapitre 12 - Sécurisation des communications
permalink: /12-securisation-des-communications/
published: true
date: 2024
---

# Sécurisation des communications

## 1) notion de chiffrement

Soit 2 individus A et B qui cherchent à s'envoyer des messages par l'intermédiaire d'un réseau informatique. A et B désirent qu'une tierce personne (par exemple P) ne soit pas capable de lire les messages si par hasard ces derniers devaient être interceptés. 

Pour ce faire, A va chiffrer le message . Toute personne qui ne possédera pas le moyen de déchiffrer ce message chiffré se verra dans l'impossibilité de comprendre le contenu du message (si P intercepte le message chiffré et qu'il ne possède pas le moyen de déchiffrer ce message, l'interception aura été totalement inutile puisque P sera dans l'incapacité de comprendre le contenu du message). 

##### Activité
>Il faut savoir que l'idée de chiffrer des messages (de les rendre illisibles pour des personnes non autorisées) ne date pas du début de l'ère de l'informatique. En effet, dès l'antiquité, on cherchait déjà à sécuriser les communications en chiffrant les messages sensible.
>On trouve les origine de la cryptographie dans la Grèce antique. Faites  une  frise  chronologique  qui  reprend  les  principales  dates  de  l'histoire  de  cette  science (une dizaine de dates).
>
>Entrez un peu plus dans les détails pour les éléments suivant :
>- Code de César
>- Chiffre de Vigenère
>- Enigma

Il existe 2 grands types de chiffrement aujourd'hui en informatique : le **chiffrement symétrique** et le **chiffrement asymétrique**.

## 2) le chiffrement symétrique

Pour chiffrer un message, A va utiliser une suite de caractère que l'on appelle "**clé de chiffrement**". Dans le cas du chiffrement symétrique, cette clé de chiffrement sera aussi utilisée par B pour déchiffrer le message envoyé par A. Dans ce cas, la clé de chiffrement est identique à la clé de déchiffrement. 

Concrètement comment cela se passe-t-il ?

Comme nous avons déjà eu l'occasion de le voir en première, **toute donnée informatique peut être vue comme une suite de zéro et de un**. Nous chercherons donc à chiffrer une suite de zéro et de un.

Soit le message "Hello World!" ce qui nous donnera en binaire :

 ```
 010010000110010101101100011011000110111100100000010101110110111101110010011011000110010000100001
 ```
 
 N.B. nous avons simplement utilisé le code ASCII de chaque caractère (par exemple, on peut vérifier que le H correspond bien à l'octet 01001000).
 
Choisissons maintenant un mot (ou une phrase) qui nous servira de clé de chiffrement, prenons pour exemple le mot "toto". "toto" nous donne en binaire :

```
01110100011011110111010001101111
```

Pour chiffrer le message nous allons effectuer un **XOR** bit à bit. Pour rappel, vous trouverez la table de vérité du XOR ci-dessous :

Table de vérité "XOR" :

| E1 | E2 | S |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Comme la clé est plus courte que le message, il faut reproduire la clé vers la droite autant de fois que nécessaire (si la taille du message n'est pas un multiple de la taille de la clé, on peut reproduire seulement quelques bits de la clé pour la fin du message):

![c12c_1](https://github.com/user-attachments/assets/54251e6b-c147-49fb-b62d-9955198ad4f4)

Le signe + dans un cercle symbolise le XOR

Après ce XOR on obtient donc la suite de bits suivante :

```
001111000000101000011000000000110001101101001111001000110000000000000110000000110001000001001110
```

Soit la chaine de caractères suivante (si on cherche à afficher le message chiffré avec un éditeur de texte) : oooO#oooN

Maintenant ce message est prêt pour être envoyé à son destinataire B. Si P intercepte le message et cherche à le lire avec un éditeur de texte, il obtiendra la suite de caractère oooO#oooN

B a maintenant reçu le message chiffré, il possède la clé (toto), il va donc pouvoir déchiffrer le message en appliquant un XOR entre le message chiffré et la clé (on applique exactement la même méthode que ci-dessus).

![c12c_2](https://github.com/user-attachments/assets/a73647fd-46bf-40e2-89ee-f897f54e6112)

On trouve le code binaire suivant :

```
010010000110010101101100011011000110111100100000010101110110111101110010011011000110010000100001
```

Vous pouvez remarquer que nous avons bien retrouvé le code binaire d'origine. Si vous ne voulez pas vous embêter à vérifier bit par bit, vous pouvez utiliser ce [site](https://www.rapidtables.com/convert/number/binary-to-ascii.html) qui vous permettra de repasser du code binaire ASCII au texte.

On retrouve bien le message d'origine : Hello World!, B a pu lire le message envoyé par A alors que pour P, malgré le fait qu'il a pu intercepter le message, il n'a pas pu prendre connaissance de son contenu sans la clé.

La méthode la plus utilisée en matière de chiffrement symétrique se nomme **AES** (Advanced Encryption Standard). Cette méthode utilise une technique de chiffrement plus élaborée que ce qui a été vu ci-dessus, mais les grands principes restent identiques.

Le gros problème avec le chiffrement symétrique, c'est qu'il est nécessaire pour A et B de se mettre d'accord à l'avance sur la clé qui sera utilisée lors des échanges. Le chiffrement asymétrique permet d'éviter ce problème.

## 3) le chiffrement asymétrique

Dans le cas du chiffrement asymétrique A et B n'ont pas besoin de partager une clé secrète :

- A possède une **clé privée** que l'on notera **kprA** et une **clé publique** que l'on notera **kpuA**. En aucun cas A ne devra divulguer sa clé privée à quiconque, elle devra rester strictement secrète. En revanche sa clé publique pourra être connue de tout le monde sans aucun problème.

- B possède une clé privée que l'on notera **kprB** et une clé publique que l'on notera **kpuB**. En aucun cas B ne devra divulguer sa clé privée à quiconque, elle devra rester strictement secrète. En revanche sa clé publique pourra être connue de tout le monde sans aucun problème.

Si A désire envoyer un message "m" à B, il va utiliser la clé publique de B afin de réaliser le chiffrement (m devient chiffré en m'). Le message chiffré (m') va ensuite pouvoir transiter entre A et B. Une fois le message m' en sa possession, B va utiliser sa clé privée afin de pouvoir déchiffrer le message m' et ainsi obtenir le message m. Le processus peut être résumé par le schéma suivant :

1) kpuB(m) -> m'
2) m' transite sur le réseau de A vers B
3) kprB(m') -> m

Si P intercepte le message m', il sera incapable de déterminer m à partir de m' sans la clé privée de B.

Le chiffrement asymétrique repose sur des problèmes très difficiles à résoudre dans un sens et faciles à résoudre dans l'autre sens. 

Prenons un exemple : **l'algorithme de chiffrement asymétrique RSA** (du nom de ses 3 inventeurs : Rivest, Shamir et Adleman), est très couramment utilisé, notamment dans tout ce qui touche au commerce électronique. RSA se base sur la factorisation des très grands nombres premiers. Si vous prenez un nombre premier A (par exemple A = 16813007) et un nombre premier B (par exemple B = 258027589), il facile de déterminer C le produit de A par B (ici on a A x B = C avec C = 4338219660050123). En revanche si je vous donne C (ici 4338219660050123) il est très difficile de retrouver A et B. À ce jour, aucun algorithme n'est capable de retrouver A et B connaissant C dans un temps raisonnable. Nous avons donc bien ici un problème relativement facile dans un sens (trouver C à partir de A et B) est extrêmement difficile dans l'autre sens (trouver A et B à partir de C). Les détails du fonctionnement de RSA sont relativement complexes (mathématiquement parlant) et ne seront pas abordés ici. Vous devez juste savoir qu'il existe un lien entre une clé publique et la clé privée correspondante, mais qu'il est quasiment impossible de trouver la clé privée de quelqu'un à partir de sa clé publique.

## 4) le protocole HTTPS

Nous allons maintenant voir une utilisation concrète de ces chiffrements symétriques et asymétriques : **le protocole HTTPS**.

Avant de parler du protocole HTTPS, petit retour sur le protocole HTTP : un client effectue une requête HTTP vers un serveur, le serveur va alors répondre à cette requête (par exemple en envoyant une page HTML au client).

![c12c_5](https://github.com/user-attachments/assets/74a4461e-9a1e-43c3-896c-0c14c417cbfa)

Le protocole HTTP pose 2 problèmes en termes de sécurité informatique :

- Un individu qui intercepterait les données transitant entre le client et le serveur pourrait les lire sans aucun problème (ce qui serait problématique notamment avec un site de e-commerce au moment où le client envoie des données bancaires)

- grâce à une technique qui ne sera pas détaillée ici (le DNS spoofing), un serveur pirate peut se faire passer pour un site sur lequel vous avez l'habitude de vous rendre en toute confiance : imaginez vous voulez consulter vos comptes bancaires en ligne, vous saisissez l'adresse web de votre banque dans la barre d'adresse de votre navigateur favori, vous arrivez sur la page d'accueil d'un site en tout point identique au site de votre banque, en toute confiance, vous saisissez votre identifiant et votre mot de passe. C'est terminé, un pirate va pouvoir récupérer votre identifiant et votre mot de passe ! Pourquoi ? Vous avez saisi l'adresse web de votre banque comme d'habitude ! Oui, sauf que grâce à une attaque de type "DNS spoofing" vous avez été redirigé vers un site pirate, en tout point identique au site de votre banque. Dès vos identifiant et mot de passe saisis sur ce faux site, le pirate pourra les récupérer et se rendre avec sur le véritable site de votre banque. À noter qu'il existe d'autres techniques que le DNS spoofing qui permettent de substituer un serveur à un autre.

![c12c_6](https://github.com/user-attachments/assets/6e6dc2b2-4cb3-414a-b757-aaacdc53e1ab)

HTTPS est donc la version sécurisée de HTTP, le but de HTTPS est d'éviter les 2 problèmes évoqués ci-dessus. HTTPS s'appuie sur **le protocole TSL** (Transport Layer Security) anciennement connu sous le nom de **SSL** (Secure Sockets Layer)

### Comment chiffrer les données circulant entre le client et le serveur ?

Les communications vont être chiffrées grâce à une clé symétrique. Problème : comment échanger cette clé entre le client et le serveur ? 

Simplement en utilisant un second chiffrement, mais asymétrique.

**Voici le déroulement des opérations :**

- le client effectue une requête HTTPS vers le serveur, en retour le serveur envoie sa clé publique (KpuS) au client

- le client fabrique une clé K (qui sera utilisé pour un chiffrement symétrique dans les futurs échanges), chiffre cette clé K avec KpuS et envoie la version chiffrée de la clé K au serveur

- le serveur reçoit la version chiffrée de la clé K et la déchiffre en utilisant sa clé privée (KprS). À partir de ce moment-là, le client et le serveur sont en possession de la clé K

- le client et le serveur commencent à échanger des données en les chiffrant et en les déchiffrant à l'aide de la clé K (chiffrement symétrique).

On peut résumer ce processus avec le schéma suivant :

![c12c_7](https://github.com/user-attachments/assets/1fc8abe6-d05f-4143-8c5d-6c75a5b25486)

Ce processus se répète à chaque fois qu'un nouveau client effectue une requête HTTPS vers le serveur.

Comment éviter les conséquences fâcheuses d'une attaque de type DNS Spoofing ?

Pour éviter tout problème, il faut que le serveur puisse justifier de son identité ("voici la preuve que je suis bien le site de la banque B et pas un site pirate"). Pour ce faire, chaque site désirant proposer des transactions HTTPS doit, périodiquement, demander (acheter dans la plupart des cas) **un certificat d'authentification** (sorte de carte d'identité pour un site internet) auprès d'une autorité habilitée à fournir ce genre de certificats (chaque navigateur web possède une liste des autorités dont il accepte les certificats). 

Comme dit plus haut, ce certificat permet au site de prouver son identité auprès des clients. Nous n'allons pas entrer dans les détails du fonctionnement de ces certificats, mais vous devez juste savoir que le serveur envoie ce certificat au client en même temps que sa clé publique (étape 2 du schéma ci-dessus). En cas d'absence de certificat (ou d'envoi de certificat non conforme), le client stoppe immédiatement les échanges avec le serveur. Il peut arriver de temps en temps que le responsable d'un site oublie de renouveler son certificat à temps (dépasse la date d'expiration), dans ce cas, le navigateur web côté client affichera une page de mise en garde avec un message du style "ATTENTION le certificat d'authentification du site XXX a expiré, il serait prudent de ne pas poursuivre vos échanges avec le site XXXX".
