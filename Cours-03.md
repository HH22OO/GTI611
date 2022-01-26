# Cours 3

## IPv6

pourquoi : repondre au manque d'addresse et contrer les limitations de IPv4
Limitations par rapport à la mobilité, la qualité de service.

On sait que IPv4 ne le supporte pas en regardant l'entete. Il n'y aura pas de champ parlant de la mobilité, de sécurité. Pour la qualité de service, pas assez de bits sont attribués

On veut que IPv6 passe plus rapidement :
Raison : - Pas de vérification, checksum, (IPv4 a un checksum sur l'entete. Chaque changement de l'entete entraine un recalcul de checksum) - Pas d'options. IPv4 a un champ d'options, mais on rajoute au routeur du contenu a relire (options). Le routeur n'a pas a lire des informations qui ne lui sont pas destinées. - Fragmentation n'existe pas. Avant l'envoie, la source va faire la découverte du MTU. si il y a lieu, c'est elle qui va faire la fragmentation du paquet

### Schéma d'adressage

trois types d'Adresses :
unicast : une seule interface qui a cette adresse la. Un paquet vers une interface unique, une seule interface recoit le paquet
multicast : tt le monde recoit le paquet. Toutes les interfaces appartenant au groupe recoit le paquet. IPv6 est plus riche que IPv4
on parle de porté, juste le site, ou global.
anycast: une adresse quon peut donner a plusieurs interfaces. Quand on envoie un paquet vers une interface anycast, une seule interface recoit le paquet. Celle qui est plus proche.
semblable au serveur cdn

l'adresse est assignée à une interface, pas à un noued. Une adresse unicast d'une interface peut etre utilisée pour identifier le noeud.
Une interface doit avoir au moins une adresse unicast. elle peut également avoir plusieurs adresses de chaque type.
Les adresses IPv6 sont assignées d'une manière hiérarchique - un usager obtient une adresse IPv6 de son Fournisseur d'accès Inteernt (FAI) - un FAI obtient un espace d'Adressage du registre internat local (RIL) du registre Internet National ou du registre internet regional - l'organisation IANA alloue un espace adressage aux différents registres RIR

    IPv4  32 bits 32 bits decimal
    IPv6 128btis hexa

#### Representation des adresses

trois formes conventionnelles pour la représentaiton des adresse IPv6
forme x:x:x:x:x:x:x:x ou x est la valeur hexadécimale de 16bits
on peut supprimer les zéros obsolètes (à gauche)
3001:0:0:a:0:0:15:80 = 3001:0000:0000:000a:0000:0000:0015:0080

forme de séros compressés : il sera commun de retrouver une longue chaines de 0 :: indique un ou plusieurs groupes de 16 bits de 0. "::" peut apparaitre seulement une fois dans une adresse
3001:0:0:a::15:80 = 3001:0000:0000:000a:0000:0000:0015:0080

formes combin. : pour les environnements mixte IPv4 et IPv6. les 4 derniers octets sont des valeurs décimales
ce n'es tpas une adresse roubable (on ne peut pas acceder a internet avec une adresse combinée)
6 zeros suivi de l'adresse IPv4
0:0:0:0:0:0:192.168.10.5 obsolète
0:0:0:0:0:FFFF:129:144:52:38 IPv4 mappé en IPv6

### Forme générale d'une adresse IPv6

128 bit, 32 octets
type d'adresse | adressage dans le domaine public | adressage dans le domaine privé | identification de l'interface
identification de l'interface est tout le temps 64 bits,

le type d'Adresse est identifier par des bits de haut niveau ou les bits les plus a gauche

0:0:0:0:0:0:0:0/128 adresse non spécifié
0:0:0:0:0:0:0:1/128 adresse de bouclage
FE80::/10 adresse unicast locale à un lien
FC00::/7 adresse unicast locale unique (VPN) peut etre FD aussi
FF00::/8 adresse multicast
Autre adresse unicast globale

- les adresse anycast sont prises dans l'espace unicast
- RFC 6164 recommande d'utiliser un préfixe de longueur /127 pour liaisons point a point
  - raison : limiter les attaques issues par NDP (Neighbor Discovery Protocol)
  - 127 bits figés et 2 bits reserver pour les deux instances communicant
- Les adresses ont une signification :
  - Globale pour aller sur internet
  - Locale unique (Locale à un site) local et prive
  - Locale à un lien -- juste une interface qui peut me voir

IPv6 na pas de reservation d'adresse pour le réseau et pour la diffusion

Une partie de l'entete est donne par IANA, l'autre par RIR, la derniere RIR ou FIA, ensuite ID du sous-groupe et fnl ID de l'interface

### Adresse unicast globale

Configuration d'une adresse d'une interface

Configuration peut etre faites selon DHCPv6, De manière statique, ou par autoconfiguration sans état SLAAC (stateless Address Autoconfiguration)

SLAAC est calculé en utilisant l'adresse mac de l'interface
on modifie le 7 bits des 24 premiers bits (pour l'identificateur du constructeur)

    separe l'adresse mac en 2, colle la partie de droite ensemble, ajoute a gauche  FF:FE
    prends la partie de gauche, inverse le 7e bit, ajoute la nouvelle partie a gauche de l'adresse

### adresse anycast

comment faire pour distinguer ces adresses : la partie identificateur d'interface est des zéros

### adresse multicast

FF00/8 fixés
pour les autres bits,
les quatre premiere (flags)
si les trois premier sont a 0 et 4 = 1, adresse temporaire, si 4e = 0, adresse permanente
