# Cours 4

## Protocol NDP

### Entetes d'extension

remplace la partie option présente dans l'adresse IPv4

Les informations optionnelles sont encodée dans des en-tetes séparés, enchaines entre l'en t^te de la base de IPv6 et l'en-tête de transport

Data gramme IP = Entête IP et la charge utile - Charge utile est un segment TCP ou UDP

ICMP peut etre encodés dans un datagramme TCP/UDP

extensions entetes passe rapidemnt car il n'y a pas de champ d'option, lecture plus rapide.
1 seule extension d'entête peut etre traiter par le retour

ESP = entetes d'encryptage
