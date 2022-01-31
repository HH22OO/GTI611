# Cours 1

système de communication IP : qui communique à travers internet.
Implique des composantes du réseaux dispersés au travers de l'internet.
Communication par internet

Les réseaux sont des services à l'utilisateur : présent en tt le temps (minimiser le temps d'interruption du service)

Réseaux de capteurs : dispositif petit

### Rappel : pile des protocoles

**Application transport réseaux et liaison**

La pile de protocole prends un message et le transfert jusqu'à la destination

Couche physique apres la couche liaison.

Couche application : couche la plus proche de l'utiliseur, lieu d'exécution des applications qui génère des messages. Communication par message.

Couche transport : TCP / UDP. Elle réalise la communication de bout en bout entre processus. Elle s'assure de la destination.. connais le numéro de port d'arrivé et le processus d'arrivé.

_processus est identifié par un numéro de port_

On ajoute l'entete de transport qui contient les numéros de port source et de destination.

Couche réseau : Elle fait le routage dans le sous-réseau. Elle s'occupe de l'adressage IP.. Elle réalise la communication de bout en bout entre les hotes. On identifi les hotes par des adresses IP.

Couche liaison : communication entre les lieux adjacents.. Communication locale, à travers du réseau. Wifi, ethernet... Utilise les adresses physiques (mac)

différence entre routage interne et externe

Internet : FAI connecte entre eux

## Système multimédias

avant le début de la communication, il y a établissement de la connexion

session multimédia : ouverture de la session entre 2 entités, c'est un échange entre deux éléments

#### Étapes avant l'échange de données entre deux hotes

1. localiser la personne (IP?)
1. envoyer demande d'appel
1. négociations

entre ces points la, il y a dautres étapes

### Session multi-participants et mulimédia

- trois composantes principales :
  - signalisation
    - établir la session
    - modifier la session
    - terminer la session
    - négocier le média que chaque participant peut traiter
- Traitement de média
  - Transmission
  - mixage
  - transcodage
- controle
  - admission
  - controle d'Acces aux ressources partages

#### Protocoles

- signalisation
  - H.323
  - sip
- Traitement de médai
  - transport
    - RTP (real time protocol)
    - RTCP (Real time control protocol)
  - control de media
    - megaco (media gateway control protocol) :H.248
    - SIP MSCML (Media server control markup language)
- Controle
  - controle de politiques : CPCP (conference policy control protocol) XCAP
  - controle d'Accès aux ressources partagées : BFCP (Binary floor control protocol)

##### Protocoles propriétaires :

requiert une force de persuasion auprès du consommateur - faire accepter au consommateur de télécharger une application propriétaire

##### Protocoles normalisé

permet à qui offre le service d'ouvrir une compétition entreles manufacturiers
Approches :

- téléphonie traditionnelles
- internet

#### Protocoles et signalisation

h.323 : Intelligence au niveau des éléments du réseau
sip : intelligence au niveau des points extrémités, mais pas au niveau du réseau

rappel : datagramme, les paquets emprunte le chemin le plus facile, pas tt le temps le meme
circuit : on garde le chemin pour tt le transfert. les canaux restes ouverts

H.323 est de type circuit

### H.323

- systèmes et équipements téléphinques visuels pour les réseaux locaux offrant une qualité de service non garantie
- norme UIT pour la transmission en temps réel de l'audio , de la vidéo et des données dans des réseaux a commutation de paquets
- réfère à des protocoles préexistants, et définit les entités foncitonnelles, les protocoles et le sprocédures marquantes
- utilisable pour les sessions multimédias multi-participants

**Dans un réseau h.323 - les entitée:**

1. terminal
   - poste de travail ou portable de l'utilisateur
   - pile de protocoles h.323 - partie client de l'application multimédia
1. Gatekeeper
   - adressage (correspondance entre un alias d'un utilisateur et son adresse IP) enregistrement
   - autorisation et authentification
   - gestion de la bande passante (pas le seul régulateur de la bande passante)
   - facturation
   - routage d'appel
1. MCU - multipoint control units
   - gestionnaire de conférences centralisées
     - permet de gerer les conférences entre des points extrémités . gère la signalisation et les fonctions de controle pour supporter les services de conférence
     - recoit les flux des points extrémités, les traite et les retourne aux points extrémités impliqués dans la conférence
     - peut etre autonome ou integre dans un gateway ou un terminal
1. Gateway
   - passerelles entre systèmes h.323 et autre systèmes, incluant les systèmes de téléphonie
1. Zone h.323

   - minimum qu'on peut avoir : terminaux et gatekeeper,
   - 1 gatekeeper par zone
   - Un ensemble de Terminaux, gateways et MCUs controlées par **un seul gatekeeper**

   quelques procotoles dans la pile h.323 :
   signalisation : Q931, h.245, h.224
   pour les médias : RTP/ RTCP
   G711 : obligatoire pour tous les équipements h.323

#### Les protocoles:

**H.323 est un spécification parapluie de plusieurs protocoles**
H.225 : communication entre terminaux et controleur d'accès
q.931 : signalisation de session - établissement et libération des connexions - tonalités, numérotation sonneries
RAS (registration admission status) : canal (du pc vers le controleur / vers le mcu), joindre et/ou quitter une zone, demander-rendre bande passante

h.245 : négociation de média (de codage)
négociation de l'algorithme de compression des données à utiliser , négocie débit binaire

G.711 : codate et décodage audio
normes téléphoniques : débit d'un canal vocal numérique : 64kbits
Transmission de données  
 rtp sur udp (géré par RTCP)

#### établissement d'un appel h.323 : enregistrement avec un gatekeeper

client transmet un paquet requete multicast au gatekeeper
gk repôn en transmettant un paquet de confirmation ou de refus
enregistrement avec un gatekeeper
le client transmet une requete d'enregistrement au gatekeep qui inclu son adresse
le gatekeep repond avec une confirmation d'enregistrement ou un refus
les deux clients a et b s'enregistrent avec le gatekeeper

## SIP

protocol de signalisation pour :

- l'établissement de la session,
- la modification des participants
- terminaisaon de la session
- echange des parametre de la session
- d'auters protocoles s'occupent du transport de données
- transport : UDP TCP
- OSI couche applicative

Standard developpé par l'IETF - RFC3261

#### Les requetes SIP

- protocole basé sur le modele client serveur
  - protocole requete réponse

#### Session :

- 2 interlocuteurs, ou plus
- multicast
- contenu: audio video données

#### numéros de téléphone sous forme d'url

### les entités fonctionnelles

- du coté client :
  agent usager client

  - entité logique qui envoire des requetes
    agent usager serveur
  - entité logiquie qui traite les requetes et envoie les réponses
    il est possible d'accepter, de rejeter ou de rediriger une requete

- du cote serveur
  regristrar (serveur d'enregistrement)
  - enregistre les contacts des clients
    proxy
  - recoit traite et au besoin réachemine les messages de signalisation
  - fait le routage au niveau application
    redirect (serveur de redirection)
  - aide à localiser les terminaux en fournissant une adresse alternative à laquelle le terminale demandé peut etre joinr
  - redirige le client vers le prochain serveur sur le chemin

### Les messages SIP

- register : enregistre des informations de contact
- options : demandes d'information sur les options supportées par un serveur / utilisé typiquement avant le invite, pour vérifier si une session est viable
- invite : message de requete qui invite l'usager à une session / specifie des informations sur la session / négociation en 3 temps : Invite, 200 ok, ACK
  invite et 200 ok contiennent la négociation des médias
- ACK : confirme que le client a recu une réponse à une requete d'invitation
- Bye : demande de fin de session / en 2 temps bye, 200ok
- Cancel : annulation de session

### les reponses ;

1xx : indique progression d'un appel
2xx : indique reception ou execution d'une requete réussie
3xx : le serveur RS (redirect server) a retourné des localisations possibles
4xx : indique qu'une requete ne peut etre executée telle qu'elle a été envoyé
5xx : indique qu'une requete a échoué à cause d'une erreur au niveau serveur
6xx : indique qu'une requete a echoué et ne devrait pas etre retransmise vers un autre serveur

2 types de reponses : provisoires (181 : finales (404)

### Corps des messages SIP

- SDP : utiliser pour la négociation de média | une offre suivie d'une réponses (pas de contre offre)
- SDP transmet l'information nécessaire pour permettre à une entité de joinrdre une session
