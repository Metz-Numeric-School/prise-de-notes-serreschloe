#  Service WDS

Le rôle WDS (Windows Deployment Services) apparu avec Windows Server 2003 SP2 est le successeur du serveur RIS (Remote Installation Service).

Il ne peut avoir que des clients Windows Server 2008 à 2022 et Windows 7, 8, 10 et 11 car il travaille sur le même modèle d’installation que le DVD.

Néanmoins, il supporte également le déploiement de Windows XP et Windows Server 2003 via le format WIM (Windows Imaging).

WDS assure 2 fonctions majeures :
- Le déploiement des images WIM pour les systèmes d’exploitation Windows
- La fourniture d’images de démarrage via PXE (Preboot exécution Environnment) pour l’initialisation des processus d’installation (ou de réparation) qui se base sur les protocoles DHCP (Dynamic Host Configuration Protocol) et TFTP (Trival File Transfer Protocol).

# Avantages d'utiliser WDS :

- Offrir une dématérialisation des DVD de distribution afin de les centraliser sur un serveur et fournir par la même occasion un système d’amorçage via le réseau PXE.
- Offrir une capacité de flux multiples dits multicast. Le déploiement d’images identiques est alors réduit de façon significative dès lors que le nombre d’ordinateurs ciblés est important. (>5)
- Contrairement aux versions antérieures à Windows Server 2012R2, le serveur WDS n’a plus besoin d’appartenir impérativement à un domaine Active Directory. Autrement dit, dorénavant, vous pouvez installer un serveur WDS en mode « autonome », ce qui me semble un choix parfaitement adapté à des déploiements en mode atelier.
- L’installation automatisée requiert un fichier de réponse unattend.xml présent sur un support amovible.