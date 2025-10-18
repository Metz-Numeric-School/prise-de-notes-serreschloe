## Introduction à `sudo`

**Qu'est-ce que `sudo` ?**
- `sudo` (Super User DO) est un programme qui permet à un utilisateur d'exécuter des commandes avec les privilèges d'un autre utilisateur, par défaut l'utilisateur `root`.
- Il est essentiel pour effectuer des tâches administratives sans avoir à se connecter directement en tant que `root`, améliorant ainsi la sécurité du système.
      
Pourquoi utiliser `sudo` ?
- Limite les risques associés à l'utilisation du compte `root`.
- Permet de tracer les actions des utilisateurs.
- Offre un contrôle granulaire sur les permissions.

## Installation de `sudo` sur Debian 12

Par défaut, Debian 12 n'installe pas le paquet `sudo` lors de l'installation minimale. Vous devez donc l'installer manuellement.

1. **Se connecter en tant que `root`**
    - Si vous êtes connecté en tant qu'utilisateur normal (par exemple, `user`), vous devez d'abord passer à l'utilisateur `root` : "su-"        ```
        
1. **Installer le paquet `sudo`**
    - Mettez à jour la liste des paquets : apt update
    - Installez `sudo` :  apt install sudo

## Ajouter un utilisateur au groupe `sudo`

Pour permettre à un utilisateur d'exécuter des commandes avec `sudo`, vous devez l'ajouter au groupe `sudo`.

1. **Ajouter l'utilisateur `user` au groupe `sudo`** : usermod -aG sudo user

    - **Explication** :
		- `usermod` : Commande pour modifier les informations d'un utilisateur.
        - `-aG sudo` : Ajoute (`a`) l'utilisateur aux groupes (`G`), ici le groupe `sudo`.
        - `user` : Nom de l'utilisateur à modifier.
    
2. **Vérifier que l'utilisateur a été ajouté au groupe `sudo`**
	- Affichez les groupes de l'utilisateur : groups user     
	 - La sortie devrait inclure `sudo` : user : user sudo

## Conseils de sécurité pour l'utilisation de `sudo`

- **Utiliser `sudo` avec Précaution**
    - N'utilisez `sudo` que lorsque c'est nécessaire.
    - Évitez d'exécuter des commandes potentiellement dangereuses.
      
- **Auditer les Actions**
    - Les commandes exécutées avec `sudo` sont généralement enregistrées dans les logs système, ce qui permet de tracer les actions en cas de besoin.
	-  **Ne Pas Utiliser `sudo` pour Ouvrir une Session Permanente**
	  
- **Ne Pas Utiliser `sudo` pour Ouvrir une Session Permanente**
    - Évitez d'utiliser `sudo su` ou `sudo -i` pour ouvrir une session `root`.
    - Préférez exécuter des commandes individuelles avec `sudo` pour limiter les risques.

