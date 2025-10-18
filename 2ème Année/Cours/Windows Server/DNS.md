#windows-server

# Domain Name System (DNS)

L'ICANN est un organisme qui gère la liste des Top Level Domain (TLD)

Il existe une TLD par pays (.fr -> france, .lu -> luxembourg, .uk -> Angleterre) et quelques TLD générales (.com, .net, .org, ...)

L'ICANN délègue la gestion de chaque TLD à un organisme (**registry**)

Les registry doivent tenir à jour la liste des domaines définis sur sa ou ses TLD

**AFNIC** -> registry .fr
**VeriSign** -> .com, .net, ...

Chaque registry peut gérer comme bon lui semble l'attribution des noms de domaine sur sa TLD

Les registry ont un **rôle technique**


Chaque **registry** autorise des **registrars** à vendre des noms de domaine. Les **registrars** ont un **rôle commercial**

Chaque pays possède un TLD qui correspond à son code pays ISO, on les appelle ccTLD (Country-code TLD).

La gestion de ces TLD repose sur des serveurs racines (appelé DNS root server)

**DNS = service TCP/IP**

Permet la correspondance entre un nom de domaine qualifié FQDN (Fully Qualified Domain Name) et une adresse IP (ex: www.google.fr = 74.125.230.82)
FQDN se termine toujours par un point
### Domaine inversé 

Résolution d'une adresse IP en nom de domaine avec l'ajout d'un domaine spécial i**n-addr.arpa** à la fin.

Ex : réseau 10.1.0.0. Adresse inversé : 1.10.in-addr.arpa

## Zone primaire et zone secondaire

Transfert de zones entre serveur maître (primaire) et un autre serveur (secondaire) chacun ayant autorité sur la zone. Vis-à-vis d'un client, l'un ou l'autre répond en fonction de la vitesse du réseau.

### Sénarios possible

- Serveur cache (DNS)
- Serveur Primaire (zone primaire)
- Serveur Secondaire (secondaire)
- Serveur stub

## Serveur cache

But: Effectuer des requêtes DNS pour se rappeler de la réponse pour la prochaine requête

Avantages : 
- Réduction de la bande passante
- Réduction du temps de latence

## Serveur primaire (maître)

But: Contenir des enregistrements DNS d'un nom de domaine enregistré

Un ensemble d'enregistrement DNS pour un nom de domaine est appelé une "zone"

Le nom de domaine peut être imaginaire, mais seulement sur un réseau local fermé, non connecté à Internet

## Serveur secondaire (esclave)

But: Contenir une copie des zones configurées sur le serveur maître

Avantages : 
- Recommandé sur les réseaux importants
- Assure la disponibilité de la zone DNS si le serveur maître n'est pas disponible 

## Serveur stub

But: Idem que le serveur esclave, mais copie uniquement les données du serveur et pas les données de l'hôte 

## Enregistrements DNS

But: mapper nom d'hôte / adresse IP et adresse IP / nom d'hôte

| Enregistrements         | Mappages                                     |
| ----------------------- | -------------------------------------------- |
| SOA (Start of Autority) | Serveur DNS de la zone primaire / Adresse IP |
| NS (Name Server)        | Serveur DNS / Adresses IP                    |
| A                       | Hôte / Adresse IPv4                          |
| AAAA                    | Hôte / Adresse IPv6                          |
| PTR (PoinTeR)           | Adresse IP / Hôte (recherche inversé)        |
| CNAME (Canonical Name)  | Hôte / Hôte Alias                            |
| MX (Mail eXchanger)     | Serveur de messagerie / Adresse IP           |


Expérience de bureau -> windows server