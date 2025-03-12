Pour prochain projet mettre proxy
proxy = entre INTERNET et notre réseaux local
on peut décider quelles sites sont ok 

## CONFIGURATION VM

Aller sur VMwaare 
prendre iso opnSense
2 coeurs
4G minimum 4096
do not use a network 
20 GB
Ajouter 2 cartes réseaux 
1 en custom Vmnet 0 NAT
2 vmnet 10 bridge NE PAS METTRE LE HOST-ONLY

Pas besoin de mettre config dans la procedure
## INSTALLATION OPNSENSE

Login : installer
password : opnsense

choisir : france accent 
choisir instalation ZFS
choisir stripe   ->  raid stripe = pas de redondance 
selectioner le disque dur
chosir yes
Exit and reboot
il faut déconnecter le CDROM (lecteur CD)

root
opnsense
option 1 : assigne interface si jamais on a pas eu d'IP
option 2 : modifier interface LAN option 1
via DHCP ->N
mettre nouvelle IP : 192.168.1.254
mettre subnet mask 24
cliquer sur entre et après N
ensuite N
ensuite entrer
DHCP - LAN -> Yes
mettre l'éttendu d'IP
changer le certificat -> N
signé certificat -> N
pas de restore d'interface web -> N

## ENSUITE UTILISER UNE VM WINDOWS 

mettre sur le même réseau que la VM OPNSENSE
démarrer VM Windows
Normallement il detecte un réseau (normallement réseau directement sur la VM)

Pare feu sert de routeur là 

tapper l'adresse IP dans un navigateur -> normallement on accède à l'inerface OPNSENSE

Username : root
Password : opnsense

Dans Wizard -> cliquer sur suivant -> langage FR -> DNS DE GOOGLE ->  Suivant -> TIMEZONE Europe/Paris -> suivant -> suivant -> laisser MDP par défaut pour le TP -> Recharger (pour appliquer les changements)

Faire la mise à jour du Pare-feu 
Onglet système -> firmware -> Mise à jour -> Status -> Verifier les mise à jour -> POP UP apparait cliquer sur fermer -> en bas de mise à jour cliquer sur Mise à jour 

Se reconnecter après que la mise à jour est terminé

## Configuration proxy fonctionnel

Création certificat SSL

Système -> gestion des certificats -> autorité
Cliquer sur + -> laisser créer une autorité de certification interne -> donner description (certificat SSL) -> pays : France -> Provinses Grand EST -> Lieux : Metz -> Organisation : MNS

C'est - a - dire c'est un certificat de confiance
Télécharger le certificat comme un certificat 
Dans le dossier téléchargement il faut renommer l'extension par .crt
Double cliquer sur le certificat -> l'ouvrir -> l'installer sur l'ordinateur local -> placer certificat dans un magasin -> Autorité de certifications de confiances -> cliquer sur OK

Ensuite installation proxy

Système -> firmware -> greffons (pluggin) -> chercher le proxy squid -> cliquer + pour l'installer   -> cliquer sur Alimentation et redémarrer une fois qu'il est installer 

Services -> Squid Web proxy -> Forward proxy -> interface LAN -> Certificat à utiliser c'est celui qu'on a créer avant 
Dans paramètres généraux -> activer le proxy -> cliquer sur petite flèche pour paramètre cache locale -> Activer le cache local -> Appliquer

## CREATION DE REGLES PARE - FEU : 

Pare - feu -> règles -> LAN -> cliquer sur + -> Action : bloquer -> protocole : TCP -> Source : LAN net -> plage de port : HTTP -> description: Bloquage HTTP pour forcer le proxy -> sauvegarder -> Duppliquer -> changer en HTTPS -> appliquer
Les règles les plus hautes sont les prioritaires 
cocher les règles crée puis cliquer sur la première flèche pour les mettre en premier -> Appliquer les changements 

Normalement plus accès à INTERNET 

activier proxy windows -> cliquer modifier paramètres de proxy -> Activé configuration manuelle du proxy mettre l'adresse IP et port 3128 -> enregister 

Vérifier Forward Proxy si les changements sont appliquer

PROXY transparant pour profiter du proxy sans le renseigner (desactiver proxy manuel): 

dans Forward Proxy -> Activer le proxy transparant + Activer l'inspection SSL -> Appliquer les configs

Dans l'inspection SSL -> cliquer sur "Add a new firewall rule" -> tout est préremplis -> cliquer sur sauvegarder

Faire pareil sur proxy HTTP transparent -> cliquer sur le lien orange et appliquer les changements

Normalement on retrouve une connection internet sans avoir besoin de renseigner le proxy manuel 

dans proxy -> Administration -> Listes de contrôle -> Ajouter Blacklist -> mettre URL -> catégories rien de selectioné -> description blacklist -> Appliquer -> télécharger les ACLs


Editer -> effacer tout mettre social_network -> appliquer -> cliquer télécharger les ACLs & les Appliquer

vérifier si ça marche
