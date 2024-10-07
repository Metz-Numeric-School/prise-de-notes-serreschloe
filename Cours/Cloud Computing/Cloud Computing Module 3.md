# Infrastructure mondiale AWS

### Region AWS  
  
- Une région AWS est une zone géographique.  
- Vous contrôlez la réplication des données entre les régions.  
- La communication entre les régions s'effectue par le biais de l'infrastructure de réseau de base AWS  
- Chaque région AWS assure une redondance et une connectivité au réseau complètes.  
- Une region se compose de deux zones de disponibilite ou plus

### Zones de disponibilité  
  
- Chaque région compte plusieurs zones de disponibilité.  
-  Chaque zone de disponibilité est une partition entièrement isolée de l'infrastructure mondiale AWS.  
- Les zones de disponibilité consistent en un ou plusieurs centres de données  
- Elles sont conçues pour l'isolation des défaillances.  
- Elles sont interconnectees avec d'autres zones de disponibilité via des réseaux privés à haut débit 
- Vous choisissez vos zones de disponibilite  
- AWS recommande de répliquer les données et les ressources dans les zones de disponibilité pour la résilience  

### Centres de données AWS  

- Les centres de données AWS sont conçus pour la sécurité.  
- Les centres de données sont l'emplacement où les données sont hébergées et où le traitement des données a lieu.  
- Chaque centre de données dispose d'une alimentation, d'un réseau et d'une connectivité redondants et est hébergé dans une installation distincte.  
- Un centre de données compte généralement entre 50 000 et 80 000 serveurs physiques.

## Points de présence 

- AWS fournit un réseau mondial de points de présence
- Il se compose d'emplacements périphériques et d'un nombre beaucoup plus faible de caces périphériques régionaux
- Il est utilisé avec Amazon CloudFront (réseau mondial de diffusion de contenu CDN, qui fournit du contenus aux utilisateurs finaux avec une latence réduite)
- Caches périphériques régionaux pour le contenu avec accès peu fréquent 

## Caractéristiques de l'infrastructure AWS

- Élasticité et scalabilité  
- Infrastructure élastique, adaptation dynamique de la capacité  
- Infrastructure évolutive, adaptation a la croissance  
- Tolérance aux pannes  
- Fonctionnement continu en cas de panne  
- Redondance intégrée des composants  
- Haute disponibilité  
- Haut niveau de performances opérationnelles  
- Temps d'arrêt réduit  
- Aucune intervention humaine

### Catégorie de service Stockage 

Amazon Simple Storage Service (Amazon S3)  
Amazon Elastic Block Store (Amazon EBS)  
Amazon Bastic File System (Amazon EFS)  
Amazon Simple Storage Service Glader

### Catégorie de service de calcul

Amazon EC2  
Amazon EC2 Auto Scaling  
Amazon Elastic Container Service  (Amazon ECS)  
Amazon EC2  Container Registry  
AWS Elastic Beanstalk  
AWS Lambda  
Amazon Elastic Kubernetes Service (Amazon EKS)  
AWS Fargate

### Catégorie de service de Base de données

Amazon Relational Database Service
Amazon Aurora
Amazon Redshift
Amazon DynamoDB

### Catégorie de services Sécurité, identité et de conformité 

AWS Identity and Access Management (LAM)  
AWS Organizations  
Amazon Cognito  
AWS Artifact  
AWS Key Management Service  
AWS Shield  
  
### Catégorie de service Mise en réseau et diffusion de contenu  
  
Amazon VPC  
Elastic Load Balancing  
Amazon CloudFront  
AWS Transit Gateway  
Amazon Route 53  
AWS Direct Connect  
AWS VPN  
  
### Catégorie de service Gestion des coûts  
  
AWS Cost and Usage Report  
AWS Budgets  
AWS Cost Explorer  
  
### Catégorie de services Gestion et gouvernance  
  
AWS Management Console  
AWS Config  
Amazon CloudWatch  
AWS Auto Scaling  
Interface de ligne de commande AWS  
AWS Trusted Advisor  
AWS Wel-Architected Toal  
AWS CoudTail


### Modèle de responsabilité partagée AWS 

![[Pasted image 20241007153408.png]]

### Caractéristique de service et résponsabilité en matière de sécurité 

#### Infrastructure en tant que service (laas)  
- Le client dispose d'une plus grande souplesse pour  
conigurer les parametres de reseau et de stockage  
- Le client est responsable de la gestion des autres aspects de la sécurité  
- Le client configure les contrôles d'accès  
  
#### Plateforme en tant que service (PaaS)  
- Le client n'a pas besoin de gérer l'infrastructure sous-jacente  
- AWS gère le systeme d'exploitation, l'application des correctifs a la base de données, la configuration des pare-feu et la reprise après sinistre (RS)  
- Le client peut se concentrer sur la gestion du code ou les données

Logiciel en tant service (SaaS)  
- Le logiciel est heberge de maniere centraisee.  
- Licence sur un modèle d'abonnement ou sur une base de paiement a lutlisation.  
- Les services sont généralement accessibles via un navigateur web, une application mobile ou une interface de programmation d'application (AP).  
- Les clients ne gérent pas l'infrastructure qui prend en charge le service