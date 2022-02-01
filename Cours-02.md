# Cours 2

## IMS (IP Multimedia Subsystem)

fournis plusieurs services
1 points de services pour une multitudes de requetes

- Plateforme commune à tout service sur IP
- facilite l'accès aux serveurs d'applications
- il ne repond pas à la requete, il aiguille
- 3G
- utilise SIP / SDP / RTP

**Contexte de convergence**

- télécoms / informatique
- hétérogénéité des réseaux d'accès
- tout s'oriente vers le monde IP

IMS c'est quoi : c'est un réseau de recouvrement - un ensemble de serveurs interconnectés entre eux
couche de connectivité c'est internet (Couche IP)
connexion à partir de n'importe quel type de réseau

### Architecture

- L'architecture IMS est organisée en deux couches
  - la couche de services et applications
    - inclut et exévute un ensemble de services
  - la couche de controle
    - inclut les noeuds responsables de la gestion d'appel
- Les deux couches se situent au-dessus de la couche de connectivité IP

**IMS s'occupe de la signalisation**

### Architecture

reseau ims contient un ensemble de serveurs

HSS = base de données des clients
MRF = si on a besoin de conférence (repartie en controlleurs et processeurs)
MGCF = media gateway, passer vers un autre type de réseau / controle / médai gateway

### Pile de protocoles IMS

similarité pour Transport, network, datalink, physical
Application varie selon l'application|réseau
IMS utilise SIP,

SDP utiliser pour decrire la session | parametre des codegs
SIP messages de requetes et de réponses|lignes d'entetes| contenu
RTP Échange des données
RTCP messages de controles

### Protocoles

SIP est le principal dans IMS
utilisé par tous les équipements
session = connexion entre des services

protocoles utilisé :
Megacp/h-248 s'occupe de la passerelle média
Diameter - sécurisation | authentification

SIP : ouvertur d'une session, définition de la session, établir connexion et définir paramètres

### Entités foncitonnelles

composantes de controle est un ensemble de serveurs

premier c'Est le proxy

#### Proxy

-premier point de contact entre un terminal IMS et le réseau IMS

- authentifie l'utilisateur, effectue un controle d'accès
- agit comme intermédiaire
- génère l'information de facturation
- n'offre pas le service
- transmet la requete vers un autre serveur
  -> service = trouver le serveur d'application qui va repondre au client et transferer la requete vers ce serveur la

#### l'interrogation CSCF

proxy qui donne l'accès au domaine

- est un SIP proxy situé à la lim ite d'un domaine administratif
- route les requetes SIP ver sla destination appropriés (serveurs de services)
- généralement, situé dans un réseau domiciliaire
- dernier noeud parmi les serveurs de controles

#### Le serving CSCF (S-CSCF)

- noeud central sur le plan de signalisation
- se charge du controle de session
  - maintient l'état de la session, interroge le HSS pour vérifier les droits d'un utilisateur et les services auquels il est abonnés
- toujours situé dans le réseau domicilaire

#### Le Home subscriber Server (HSS)

base de donnée accèder soit par I-CSCF
HSS = base de donnée
contient toutes les info sur l'utilisateur - compte utilisateur - localisation - droits d'accès - profil de l'usager - s-cscf alloué à l'usager

### HSS

dans un réseau plus grand == plusieurs HSS nécessite un SLF

- SLF est la lorsque plusieurs HSS dans le réseau
- indique ou se trouve l'information d'un client
- les deux utilisent le diameter protocol
  - communiquent ensemble

Le I-CSCF communique avec le HSS pour avoir des informations sur le client, informations de localisation, route les requetes SIP vers la destination appropriés
Le S-CSCF est le dernier dans la chaine, il se charge d'aller trouver le serveur d'application repondant, transmet la requete vers ce serveur

### Serveurs d'applications

repondent aux requetes des utilisateurs

- offrent les applicaitons services IMS
  le serveur d'application peut etre dans le réseau IMS ou dans un réseau tierce

### entitées foncitonnelles MGCF

media gateway control funciton

- conversion de protocole de controle d'appels entre PSTN/2g et IMS
- identification de l'I-CSCF pour un appel entrant du PSTN
- controle de la MGW

### La MGW media gateway

- Responsable de la conversion de média (sour le controle de la MGCF) entre 2G et IMS
  - codec, annulation d'écho, conférences

### Entités de controles - sessions multi participants multimédias MRF

- MRFC (MRF controller)
- MRFP (MRF processor)

## Réseau CDN Content Delivery Network

- diffusion de contenu

réseau ip, de recouvrement

#### Contexte :

- ameliorer l'expérience utilisateur en offrant un téléchargement de contenu efficace et rapide
- offrir du contenu avec la même qualité pour tous les consommateurs indépendamment de leur localisation géo

#### Stratégie d'amélioration

- architecture distributé de diffusion de contenu ou les serveurs de contenu sont placés **Proche** du consommateur
- serveurs d'origine : introduction du contenu dans le réseau
- serveurs périphériques : réplication du contenu des serveurs d'origines

#### CDN

- plateforme de **diffusion de contenu** à travers l'Internet qui permet :
  - repliquer le contenu dans des serveurs antémémoires (caching serveur)
  - identifier le serveur le plus prpoche du consommateur pour assurer une livraison rapide du contenu
- standards ETSI, IETF
- Utilise HTTP, RTP

### Historique

trois génération, on veut la plus rapide, on veut un réseau intelligent

1ere developpement des serveurs périphériques : plusieurs centre de données | developpement des méthodes de routage et de calcul périphérique | contenu statique et dynamique (dynamique change d'un client à un autre)
2e apparition de la vidéo sur demande, audio, vidéo streaming | utilisation pair-a-pair pour le partage de fichier (maintenir la connexion pour des fichiers populaires pour accelerer le prochain transfert) | apparition du cloud
3e CDN comme on les voit auj | auto config | auto adaptable

### Principes généraux

#### Contenu

informations que je recherches : multimédias codés (données multimédias statiques, dynamiques, et en continu) | métadonnées (represente description du contenu - pour l'identification, la découverte et la gestion des données multimédias)

#### Entités de l'architecture

- Fournisseur de contenus (fournit le contenu à diffuser)
- Fournisseur CDN (fournit les installations de l'infrastructure pour les fournisseurs de contenus)
- Consommateurs (utilisateurs) : accède au contenu à partir du site web du fournisseur de contenu

### Infrastructure CDN

**infrastructure de diffusion de contenu :** livre les contenus aux utilisateurs

- serveur d'origine (SO): source de diffusion
- serveur de stockage (SS): joue le role d'un tiers serveur antémémoire situé entre le SO et le SA | fournit le contenu au SA |utilisé pour la prépublication de contenu
- serveurs d'antémémoire (SA) : replication de contenu | placés à différentes localisations géo | offrent des applications de diffusion de contenu

**infrastructure de controle:** gère achemine surveille le contenu | surveille les performances de la dfiffusion | controle les états du système et de la diffusion | gère stockage

- systeème d'Acheminement de requetes : dirige la requete de l'utilisateur vers le SA approprié
- système de distribution : livre le contenu de l'origine vers le système cache | assure consistance du contenu
- système de comptabilité : collecte les infroamtions | logs reliés aux accès des utilisateurs

### Déploiement du CDN ( niveau transport)

les serveurs CDN gèrent la diffusion du contenu à travers un réseau de transport

- Stratégie de recouvrement : itnernet utilisé | routeurs utilisé de la manière classique (recoit et transfert sans intervenir) | CDN ne gère pas les équipements de l'infrastructure réseau de transport
- Stratégie réseau : équipement réseau peut jouer le role de front end pour une ferme de serveurs CDN - redirige les requetes de contenu vers le serveur antémémoire le plus proche

### Distribution du contenu dans CDN

**Nombre de serveurs périphériques:** Consiste à identifier le nombre de serveurs requis selon une approche à multi-ISP ou à ISP (Internet Service Provider)

- Multi-ISP (Enter deep): consiste à déployers des SA dans des ISP d'Accès, donc proche des utilisateurs | assure fiabilité et rapidité de diffusion de contenu
- ISP unique (bring home): grands clusters de sserveurs antémémoire en un nombre de petit localisations, typiquement des IXP.

Multi ISp : plus proche des utilisateurs | reponses plus rapide | pour le fournisseur CDN, maintenance plus compliqué

#### Sélection et livraision du contenu

stratégie de sélection (du contenu à repliquer) et de livraison de contenu permet de réduire le temps de téléchargement du contenu et la charge de travail sur les serveurs

**plusieurs approches**

- sélection empirique : admin du site de contenu sélectionne ce qui doit être repliquer dans les SA selon une heuristique | necessite un bon heuristique
- sélection basée sur la popularité d'un objet : contenu populaire sont replique dans les SA | fiabilité pas garantie
- sélection basée sur les grappes : groupés selon leur corrélation leur fréquence d'accès
  - sélection basée sur les sessions : grouper les sessiosn de navigation des utilisateurs avec des caractéristiques similaires comme des modeles de navigation similaire et des pages ayant des contenus associés
  - sélection basée sur l'URL : les objets les plus populaires sont identifiés à partir du site web et sont répliqués sous forme de grappes | corrélation entre les paires d'URLS basé sur une métrique

#### stratégie de livraison

- livraison de contenu de dimensions ordinaires : tous le contenu en une seule fois
  - SA replique la totalité du contenu et livre la totalité du contenu à l'utilasteur
  - simple mais couteuse en capacité
- livraison de contenu de dimensions partielles :
  - SA réplique partiellement le contenu pour ne livrer que les objets intégrés dans un contenu tels que les images d'une page web
  - lorsque le contenu integre ne change pas fréquemment, cette appropche offre de meilleurs performances

### Acheminement des requets dans CDN

système d'acheminement utilise un ensemble de métriques pour acheminer les requetes de l'utilisateur au SA le plus proche.

- Métriques : proximité du réseau périphérique | latence percue par l'utilisateur | distance entre l'utilisateur et le SA | charge de travail du SA
- Stratégie d'acheminement :
  - dimensions ordianires : système dirige la requete de l'utilisateur vers le SA
  - dimensions partielles : SO livre le contenu de base | SA livrent les objets intégrés

## IPv4

Taille des adresses limitée à 32 bits

- épuisement des adresses
  Limitation au niveau : sécutirét , QoS, mobilité

Espace d'adressage divisé en 5 calsses

- Classe A : 1er octet = 0 a 127 (unicast)
- Classe B : 1er octet = 128 a 191 (unicast)
- Classe C : 1er octet = 192 a 223 (unicast)
- Classe D : 1er octet = 224 a 239 (multicast)
- Classe E : 1er octet = 240 a 255 (réservés)

### Protocoles d'adressage

clases d'adresses non flexibles par rapport à la taille de la plupart des organisations

manques d'adresses

solutions à court terme :

- allocation flexible des adresses CIDR (Classless interdomain routing)
- Adressage privé et translation NAT (Network address translation)
- Partage dans le temps DHCP (Dynamic host configuration protocole)

#### CIDR (allocation flexible) - masque à longueur variable

classless interdomain routing: allocation flexible des adresses

on n'a pas de classes (A,B,C,D,E)

NetId peut etre de m'importe quelle taille

Si on a besoin de 2000 ordinateurs, il faut 2003 -- adresse réseau, adresse de diffusion, passerelle par défaut
demande 2^11 bits (2048)

routage complexe - on subdivise la table d'adresse d'adresse

#### NAT adressage

adressage privé et translation

permet de créer plusieurs adresses a l'intérieur d'un réseau et auxquelles correspondent une ou plusieurs adresses à l'extérieur de ce même réseau
Ces adresses ne sont pas routables

trois sortes d'adresses peuvent être utilisées pour des réseaux privés
10.0.0.0 a 10.255.255.255
172.13.0.0 a 172.31.255.255.255
192.168.0.0 a 192.168.255.255

#### DHCP

pool d'adresse qu'on utilise
partage d'adresse dans le temps
permet à un équipement terminal d'obtenir une adress IP de manière automatique ainsi que différentes i nformations utilses telles que l'adresse du routeur de premier bond et de celle de son s erveur DNS

qualifié de protocole plug and play permettant a un équipement terminal d'obtenir une adresse permanente ou temporaire

## IPv6

concu pour remplacer IPv4 en supprmiant certains des problèmes de la version 4

IPv6 doit permettre une transition facile

#### Objectifs

supporter plus d'adresses
simplifier l'en-tete pour faciliter l'acheminement de paquets

- des champs IPv4 on été supprimés ou sont optionnels
- malgré une taille des adresses de 16 octets, l'entete ne dépasse pas les 4- octets

Fournir plus d'options pour plus de flexibilité

- QoS
- Sécurité
- Mobilité

### Entête IPv6

- version (4 bits)
- traffic class (classe de trafic 8 bits) : identifie différentes classes ou priorités pour la QoS (DiffServ) Équivalent de ToS dans IPv4
- flow label (étiquette de flux 20 bits) : source peut utiliser ce champ pour marquer un ensemble de paquets appartenant au même flot. utilisé pour établir une correspondance avec les réseaux niveaux 2 pour classer et donner des priorités aux paquets IP
- payload length : longueur de charge utile uniquement (dans IPv4 header + payload, les options sont considérées co mme faisant partie de la charge utile)
- next header (en-tete suivant : 8bits): équivalent du champ protocle dans IPv4. Utilisé pôur identifier le protocole contenu dans le cha mp de données (TCP/UDP, ICMP, extension d'en-tete)
- Nombre de saut limite : Équivalent au TTl dans IPv4
- Fragmentation : avec IPv6, le path MTU est découvert au préalable. La source est le seul noeud pouvant fragmenter un paquet. Chaque noeud doit ajuster ses paquets enfonction du plus petit MTU sur le chemin. Si la découverte du Path MTU n'est pas activé dans un résean IPv6. Le RFC 2460 recommande de se limiter à un path MTU minim al qui est de 1280 octets
