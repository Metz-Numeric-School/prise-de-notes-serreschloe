
35 pages -> hors annexes = PDF + 2 versions papier
Classroom -> 20/09/26
une partie en anglais
Soutenance : 31/09 - 01/10 - 02/10

SUjet cyber :

Prendre des notes :
COntexte
Contreintes
Enjeux -> Business, techniques, sécurité 
Problème à résoudre ? 


## Contexte : 

### Metz Cyber Academy (MCA) : 
- Établissement d’enseignement supérieur privé français
- Spécialisé en cybersécurité et protection des systèmes d’information
- Créé il y a plus de 9 ans

### Activité et effectifs : 
- Environ 500 apprenants par an
- 25 collaborateurs permanents
- Formations du Bac +2 au Bac +5

### Organisation géographique (2 sites à Metz) :
- Technopôle (site principal)
- Centre gare (nouveau site)

### Évolution stratégique, ouverture d’un nouveau programme :
- « Spécialiste Cyberdéfense »
- 6ᵉ année post-master
- Accueil de 20 apprenants supplémentaires
- Besoins techniques spécifiques et avancés

### État du système d’information :
- SI déployé progressivement depuis la création
- Architecture non adaptée à la croissance
- Technologies vieillissantes et en partie hors support
  
### Incident majeur : 
- Indisponibilité totale de l’accès Internet pendant 5 jours
- Impact sur :
	- Accès aux outils pédagogiques
    - Messagerie des équipes administratives

### Constat de la direction : 
- SI ne répond plus aux exigences actuelles
- Besoin urgent de :
	- Modernisation
    - Sécurisation
    - Amélioration de la disponibilité
    - Mise en conformité

## Contraintes : 

### Contraintes organisationnelles :
- Équipe IT réduite (2 techniciens dédiés à l’infrastructure).
- Fonctionnement actuel essentiellement **réactif**, peu de temps pour l’anticipation.
- Continuité de service indispensable pour les apprenants et l’administration.

### Contraintes techniques  : 
- Infrastructures **vieillissantes** (ESXi 5.5, Windows Server 2012 R2, Exchange 2016).
- Absence de redondance (Internet, hyperviseur, pare-feu).
- Segmentation réseau très basique (2 VLAN).
- Aucun lien inter-site.
- Pas d’infrastructure pédagogique dédiée pour le cursus Cyberdéfense.
- Sauvegardes non conformes aux standards actuels (pas de tests, pas de 3-2-1-1-0).

### Contraintes budgétaires  : 

- **CAPEX** :
    - 100 000 € HT pour la modernisation globale
    - - 50 000 € HT dédiés au projet « Spécialiste Cyberdéfense »

- **OPEX** :
	- 30 000 € HT par an sur 5 ans (cloud, cybersécurité, support)
	- Tolérance de dépassement possible de ±20 % si justifiée.
	- Éligibilité aux **licences Éducation** des éditeurs
 
### Contraintes réglementaires et normatives  : 
- Conformité **RGPD**.
- Respect des **recommandations ANSSI**.
- Exigences strictes liées à une **assurance cyber** (MFA, SIEM, EDR, Zero Trust, PRA/PCA).

## Enjeux :

### Enjeux business  : 
- Éviter les pertes financières liées aux interruptions (≈ **20 000 € HT / jour** d’arrêt).
- Préserver l’image et la crédibilité d’une école spécialisée en cybersécurité.
- Garantir la continuité pédagogique et administrative.
- Accompagner la croissance (+20 % d’apprenants estimée sur 5 ans).
- Offrir des services numériques fiables et modernes aux apprenants.

### Enjeux techniques : 
- Moderniser l’infrastructure (virtualisation, réseau, sauvegarde).
- Mettre en place une **haute disponibilité** et de la **redondance**.
- Intégrer une infrastructure dédiée et isolée pour le cursus Cyberdéfense.
- Automatiser les déploiements et la gestion des utilisateurs.
- Mettre en place une supervision centralisée et proactive.
- Atteindre les objectifs **RTO/RPO** définis :
    - RTO SI interne : 8 h
    - RTO Internet : 1 h
    - RPO : 8 h

### Enjeux de sécurité : 
- Élever drastiquement le niveau de cybersécurité (actuellement très faible).
- Protéger les données administratives et pédagogiques.
- Sécuriser les accès (MFA, authentification forte, Zero Trust).
- Mettre en place EDR, SIEM, journalisation centralisée.
- Chiffrement des flux et des données.
- Sécurisation du réseau pédagogique (BYOD).
- Mise en conformité pour l’assurance cyber.

### PLAN :

