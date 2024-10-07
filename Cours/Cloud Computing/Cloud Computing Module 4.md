
## Adresses IP

Adresse IPv4 -> 192.0.2.0
Adresse IPv6 -> 2600:1f18:22ba:8c00:ba86:a05e.a5ba.00FF

## Amazon VPC

Permet de mettre en service une section logiquement isolée d'AWS Cloud où vous pouvez lancer des ressources  
AWS dans un réseau virtuel que vous définissez.  
• Vous permet de contrôler vos ressources de réseau virtuel, notamment  
• La sélection d'une plage d'adresses IP  
• La création de sous-réseaux  
• La configuration de tables de routage et de passerelles réseau  
• Vous permet de personnaliser la configuration réseau de votre VPC  
• Vous permet d'utiliser plusieurs couches de sécurité.  
  
### VPC et sous-réseaux  

#### VPC:  
• Logiquement isolés des autres VPC  
• Dédiésà votre compte AWS  
• Appartiennent à une seule region AWS et peuvent s'étendre sur plusieurs zones de disponibilité  
#### Sous-réseaux:  
• Plage d'adresses IP qui divisent un VPC  
• Appartiennent à une seule zone de disponibilité  
• Classés comme publics ou privés

### Adressage IP

• Lorsque vous créez un VPC, vous l'affectezà un bloc d'adresse CIDRIPV4 (plage d'adresses (Pv4 privées).  
• Une fois que vous avez créé le VPC, vous ne pouvez plus modifier la plage d'adresses.  
• La plus grande taille de bloc d'adresse CIDR IPv4 est /16.  
• La plus petitetaille de bloc d'adresse CIDR IPv4 est / 28.  
• IPv6 est également pris en charge (avec une limite de taille de bloc différente).  
• Les blocs d'adresse CIDR de sous-réseau ne peuvent pas se chevaucher.  
  
### Types d'adresses IP publiques  
  
**Adresse IPv4 publique**  
• Attribuée manuellement via une adresse IP Elastic  
• Attribuée automatiquement via les paramètres d'attribution automatique d'adresse IP publique au niveau du sous-réseau  
  
**Adresse IP Elastic**  
• Associée à un compte AWS  
• Peut être allouée et remappée à tout moment  
• Des frais supplémentaires  
peuvent s'appliquer  

### Interface réseau Elastic  
  
• Une interface réseau Elastic est une interface réseau virtuelle que vous pouvez:  
• Attacher à une instance  
• Détacher de l'instance et attacher à une autre instance pour rediriger le trafic réseau  
• Ses attributs sont conservés lorsqu'elle est rattachée à une nouvelle instance.  
• Chaque instance de votre VPC possède une interface réseau par défaut à laquelle est attribuée une adresse IPv4 privée à partir de la plage d'adresses IPv4 de votre VPC.

### Tables de routage et routes  

• Une table de routage contient un ensemble de règles (ou routes) que vous pouvez configurer pour diriger le trafic réseau depuis votre sous-reseau.  
• Chaque route spécifie une destination et une cible  
• Par défaut, chaque table de routage contient une route locale pour la  
communication au sein du VPC  
• Chaque sous-réseau doit être associé à une table de routage (au plus une).

