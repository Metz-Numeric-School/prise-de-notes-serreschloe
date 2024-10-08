## Catégorisation des services de calcul

| Services                                              | Concepts clés                                                                                   | Caractéristiques                                                                                                                                                                             | Simplicité                                                                                                                                             |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Amazon EC2                                            | - Infrastructure en tant que service "IaaS"<br>- Basé sur une instance<br>- Machines virtuelles | - Mettez en service des machines virtuelles que vous pouvez gérer à votre guise                                                                                                              | Concept que de nombreux profesionnels de l'informatique connaisse                                                                                      |
| AWS Lambda                                            | - Calcul sans serveur<br>- Basé sur une fonction<br>- Faible coût                               | - Ecrivez et déployez du code qui s'execute selon un calendrier spécifique ou qui peut être déclencher par des évènements<br>- A utiliser quand cela est possible (architecte pour le cloud Concept relativement récent pour de nombreux profesionnels de l'informatique mais facile à utiliser une fois que vous avez les connaissances requises es  |
| Amazon ECS<br>Amazon EKS<br>AWS Fargate<br>Amazon ECR | - Calcul basé sur des conteneurs <br>- Basé sur une instance                                    | - Lancez et éxecutez les taches plus rapidemment                                                                                                                                             | AWS Fargate réduit la charge administrative mais des options sont à votre disposition pour avoir plus de cont                                          |
| AWS Elastic Beanstalk                                 | - Plateforme en tant que service (PaaS)<br>- Pour les applications web                          | - Concentrez-vous sur votre code (création de votre application)<br>- Peut facilement se connecter à d'autres services (base de données, système de nom de domaine (DNS) etc)                | Démarrage rapide et f                                                                                                                                  |

## Choisir le service de calcul optimal

- Les services de calcul optimaux que vous utiliserez dépendent de votre cas d'uitilisation
- Aspects à prendre en considération : 
	- Quelle est la conception de votre application ?
	- Quelles sont vos modèles d'utilisation ?
	- Quels sont les paramètres de configuration que vous souhaitez gérer ?
- La sélection d'une solution de calcul inadéquate pour une architecture peut nuire à l'éfficacité des performances
	- Un bon point de départ consiste à connaître les options de calcul disponibles 

## Présentation d'Amazon EC2

#### Amazon Elastic Compute Cloud (Amazon EC2)  
• Fournit des machines virtuelles (appelées instances EC2) dans le cloud.  
• Permet un contrôle total du système d'exploitation invité (Windows ou Linux) sur chaque instance.  
• Vous pouvez lancer des instances, quelle que soit leur taille, dans une zone de disponibilité n'importe où dans le monde.  
• Lancez des instances à partir d'Amazon Machine Images (AMI).  
• Lancez en quelques clics ou à partir d'une ligne de code des instances qui seront prêtes en quelques minutes.  
• Vous pouvez contrôler le trafic entrant et sortant des instances.

## Types d'instances : fonctions de mise en réseau 

- La bande passante réseau (Gbit/s) varie selon le type d'instance 
	- Consultez le tableau de comparaison types d'instances Amazon EC2
- Pour optimiser les performances de mise en réseau et de bande passante de votre type d'instances :
	- Si vous avez des instances indépendantes, lancez-les dans un groupe de placement du cluster 
	- Activez la mise en réseau améliorée
- La mise en réseau améliorée est prise en charge pour la plupart des types d'instances
	- Consultez la documentation fonctions de mise en réseau et de stockage pour en savoir plus
- Types de réseaux améliorés :
	- ENA (Elastic Network Adapter) : prend en charge des vitesses réseau allant jusqu'à 100 Gbit/s
	- Interface VF (Virtual Function) Intel 82599 : prend en charge des vitesses réseau allant jusqu'à 10 Gbit/s


#### Options de stockage Amazon EC2 AWS 
- Amazon Elastic Block Store (Amazon EBS)  
- Volumes de stockage durables de type bloc  
- Si vous arrêtez l'instance et que vous la redémarrez, les données seront toujours présentes  
#### Stockage d'instances Amazon EC2  
- Le stockage éphémère concerne les disques attachés à l'ordinateur hôte sur lequel l'instance EC2 est exécutée  
- Si l'instance s'arrête, les données stockées sont supprimées.  
#### Autres options de stockage (ne concerne pas le volume racine) :  
- Montez un système de fichiers Amazon Elastic File System (Amazon EFS)  
- Connectez-vous à Amazon Simple Storage Service (Amazon S3)


![[Pasted image 20241008094238.png]]


## Paramètres des groupes de sécurité

- Un groupe de sécurité est un ensemble de règles de par-feu qui contrôlent le trafic entrant de l'instance 
	- Il existe en dehors du systeme d'exploitation invité de l'instance
- Créer des règles qui indiquent la source et les ports que les communication réseau peuvent utiliser
	- Indiquer le numéro de port et le protocole par exemple TCP, UDP ou ICMP
	- Indiquez la source autorisée à utiliser la règle

## Quand utiliser une adresse IP Elastic

- Le redémarrage d'une instance ne modifie aucune adresse IP ni aucun nom d'hôte DNS.  
- Lorsqu'une instance est arrêtée puis redémarrée:  
	- L'adresse IPv4 publique et le nom d'hôte DNS externe changent.  
	- L'adresse IPv4 privée et le nom d'hôte DNS interne ne changent pas.  
- Si vous avez besoin d'une adresse IP publique persistante  
	- Associez une adresse IP Elastic à l'instance  
- Caractéristiques des adresses IP Elastic:  
	- Peuvent être associées aux instances de la région selon les besoins.  
	- Restent allouées à votre compte jusqu'à ce que vous choisissiez de les libérer

## Métadonnées d'instance EC2

- Les métadonnées d'instance sont des données relatives à votre instance.  
- Vous pouvez les visualiser lorsque vous êtes connecté à l'instance:  
	- Dans un navigateur: http://169.254.169.254/latest/meta-data/  
	- Dans une fenêtre de terminal: curl http: //169.254.169.254/1atest/meta-data/  
• Exemple de valeurs récupérables :  
	- Adresse IP publique, adresse IP privée, nom d'hôte public, ID d'instance, groupes de sécurité, région, zone de disponibilité.  
	- Toutes les données utilisateur spécifiées au lancement de l'instance sont également accessibles à l'adresse: http://169.254.169.254/latest/user-data/  
- Elles peuvent être utilisées pour configurer ou gérer une instance en cours d'exécution.  
	- Par exemple, vous pouvez créer un script de configuration qui lit les métadonnées et les utilse pour configurer les applications ou les paramètres du système d'exploitation

## Amazon CloudWatch pour la surveillance

#### Utilisez Amazon CloudWatch pour surveiller les instances EC2:  
• Fournit des métriques en temps quasi réel.  
• Vous donne acces à des graphiques dans l'onglet  
Monitoring (Surveillance) de la console Amazon EC2  
• Conserve 15 mois de données historiques  
#### Surveillance basique  
• Activée par défaut, n'entraine aucun coût supplémentaire  
• Données de métriques envoyées à CloudWatch toutes les 5 minutes  
#### Surveillance détaillée  
• Tarif mensuel fice pour sept métriques présélectionnées  
• Données de métriques fournies toutes les minutes

## Déploiements AWS Elastic Beanstalk

- Prend en charge les applications web écrites pour les plateformes courantes
	- Java, PHP, Python, Node.Js, Ruby, Go et Docker
- Vous chargez votre code 
	- Elastic Beanstalk gère automatiquement le déploiement
	- Effectue les déploiements sur des serveurs tel que Apache, NGNIX, Passenger, Puma, Microsoft Internet Information Services (IIS)

### Avantages AWS Elastic Beanstalk

- Prise en main facile et rapide
- Productivité des devs
- Grande évolutivité 
- Contrôle total des ressources 