# Routage

on parle de transfert de paquets - selon les informations de la table de routage

- La table de routage contient des routes

## Classification des algorithmes de routage

Routage statique vs dynamique

### Dynamique

Automatique
Algorithme qui s'exécute et qui rempli la table de routage

- Algorithmes internes
  - IGP - Internal Gateway protocol : 1 seul organisation , décide tt ce qui se passe à l'intérieur, décide des coûts, Granularité : routeur
- Algorithmes externes
  - taille c'est l'internet , administration = cooperation d'entitées indépendantes, granularité : AS

Par rapport aux systèmes autonomes (Internet est un ensemble de système autonomes interconnectés) - ensemble de réseaux avec un seul gestionnaire

### Statique

routes statiques, les routes sont ajoutées par l'admin dans la table de routage
Pas utiliser pour lkes réseaux tres vastes

Au niveau d'un routeur : Routes à ajouter

le reseau 1 (joue le role de passerelle par défaut), le reseau d'interconnexion auquel il est connecté

#### types de routage :

routage interne RIP, OSPF
routage extern BGP-4 BGP -4 multiprotocoles (MP-BGP)

### Objectifs principaux

- supportedr des milliards d'hotes
- réduire la table de routage : meilleure aggrégation de routes dans les tables de routage
- simplifier le protocole - achemoinement des datagrammes plus rapidemment
- améliorer la sécurité

## Routage interne

trouver le meilleur chemin sur lequel les paquets sont acheminés à l'intérieur d'un système autonome

RIP et OSPF

rip est un algorithme de vecteur de distance - direction et distance (poids)

- chaque routeur maintient sa propre table de routage qui liste le cout pour cahque destination
- cout L nombre de sauts (15 sauts maximum)
- chaque routeur partage les informations qu'il détient au sujet du plus court chemin avec ces voisins
- chaque routeur transmet ces informations à des intervalles de temps fixés (ex : chaque 30s)
- rip encapsule ses messages dans un segment UDP

OSPF

- routage à état de liens
- les états des liens sont partagés entre les routeurs
- algo de djikstra
- cout : bande passante de référemce 100mbps/bande passante de l'interface
- chaque routeur transmet l'ionformation d'état de son voisinage à chaque routeur de la région(c'est de la diffusion)
- l'information d'état de lien est transmise en utilisant le processus d'inondation (à tt le monde)
- l'information n'est pas partagé périodiquement, mais quand il y a un changement
- supporté par la plupart des routeurs et implanté dans la plupart des SAs

### RIP

rip v1 et rip v2
ripv2 est classless - pas de notion de mask
ripv1 ne tient pas compte des masques, il s'effectue selon les classes (A,B,C,D,E)

Le nexthop est plus performant avec ripv2
le prochain saut est le routeur qui envoie
nexthop : quand tu veux envoyer le paquet vers un auter reseaux que le routeur partagean l'info - pour les environnements avec plusieurs algorithmes de routage

### Messages RIP

deux types de messages : requetes - reponses

requetes : envoyé aux routeurs voisins leur demande de transmettre tout le contenu ou une partie de latable de routage
reponse continne les mises à jour

#### RIPv1

- utilisa l'adrresse broadcast pour partager l'information
- protocle Classful - onne transmet pas le mask
- envoie de mise a jour RIPv1
- Reception de mises a jour RIPv1 et RIPv2
- pas de support d'authenfication

avantages :
-tres simple

- peu de ressources
- simple a metre en oeuvre et a configurer
- disponible sur une large gamme de périphériques

desavantages

- temps de stabilité long suite a un changement dans le réseau
- comptage infini - si un reseau est deconnecter, il va rester phantome et la taille du réseau serat tt le temps augmenter
- nombre de sauts limité à 15
- ne prends pas en compte d'autres types de couts

#### RIPv2

- utilise l'Adresse multicast 224.0.0.9 pour partager l'information
- protocole classless - information du subnet est transmise dans les mise a jour de routage
- supporte classful et VLSM
- envoie de mises a jour RIPv2
- reception de mise à joeurs RIPv2
- support d'authentification simples des messages de mises à jour

### Message RIPng

deux types de messages : requetes / reponses

requetes :

- envoyé aux routeurs voisins leur demandant de transmettre tout le contenu ou une partie de la table de routage
- tout le contenu d'une table est tranmis lorsqu'une seule RTE avec un préfixe de destination nul, une longueur de préfixe nulle et une métrique de 16 est recus

rponse :
Pas pris en note

### RPIv2 vs RIPng

ripv2 :

- utilise l'adresse muiilticast 224.0.0.9 pour partager l'info
- protocole Classless
- Envoie de mises a jour RIPv2
- Rececption de mises a jour Ripv2
  Support d'authentification simple des messages de mises a jour

RIPng

- utilise l'adresse multicast UPv6 pour partager l'info
- protocole classless
- suppor d'authentification des messages de mises a jour IPsec

### Paquets OSPFv2

LSA (Link stte advertisment)

- message Hello - decouvre les routeurs et maintient les relations entr eeux
- Link state update : annonces | chaque fois qu'il y a changement
- State ACK : accusées de reception
- state request packets
- databse description packets : resumer des routes partagées

OSPFv2 réseau divisé en zones

routeurs de frontières : partages des info entre les zones
a l'interne : des routeurs internes

- pour ne pas saturer les liens, tt le monde n'envoit pas a tt le monde
- tt le monde envoie a un routeur designé qui transmet l'information par après

## Routage Externe

Routage inter Ass
Protocle utilisé Border Gateway Protocl

- un noued peut établir différentes essions BGP
- un noeud est un routeur BGP
- il peut annoncer une partie ou ttes les routes disponibles qu'il désire partager avec ses voisins

### BGp

algorithme de vecteurs de distances : locale

- on voit just les AS voisins

- stratégie de routage :

  - client
  - pair
  - transit|fournisseur : AS intermédiaire pour l'acheminement de trafic

Pour le routage externe : deux manieres de trouver les meilleurs routes

- utiliser les relations entre les ASs

- BGP memorise toute sles routes vers toutes les destinations
- pas de transmission périodique des meilleurs routes

### message BGP-4

- OPEN : premier message = tcp port TCP179
- ouvre une connexion sécurisé et commence a envoyer des messages
