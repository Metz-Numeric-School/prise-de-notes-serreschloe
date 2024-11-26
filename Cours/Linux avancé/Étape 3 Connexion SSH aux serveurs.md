## Installer le serveur SSH sur server1 et server2

1. **Vérifier si openSSH est installé** :  sudo apt install openssh-server

	Si le serveur SSH est déjà installé, le système vous le signalera.
    
2. **Vérifier le statut du service SSH** : sudo systemctl status ssh
  
    Le service doit être actif et en cours d'exécution.

##  Générer une paire de clés SSH sur le client Windows

1. **Ouvrir powerShell** :
    - Appuyez sur **Windows + X** et sélectionnez **Windows PowerShell**.
      
2. **Générer la paire de clés** : ssh-keygen -t rsa -b 2048
    - Acceptez l'emplacement par défaut (`C:\Users\VotreNom\.ssh\id_rsa`).
    - Choisissez une passphrase ou appuyez sur **Entrée** pour ne pas en mettre.

##  Configurer l'authentification par clé SSH sur les serveurs

1. **Copier la clé publique sur Server1** :
    
    - Si `ssh-copy-id` n'est pas disponible sur Windows, vous pouvez copier manuellement la clé publique.
        
    - Affichez le contenu de la clé publique : type $env:USERPROFILE\.ssh\id_rsa.pub
    - Connectez-vous au serveur : ssh user@192.168.200.254
    - Sur le serveur, créez le dossier `.ssh` et le fichier `authorized_keys` : mkdir -p ~/.ssh
												       nano ~/.ssh/authorized_keys

    - Collez le contenu de votre clé publique dans ce fichier, enregistrez et quittez.


## Se connecter en SSH depuis le client Windows

- Vous pouvez maintenant vous connecter sans mot de passe :  ssh user@192.168.200.254
												    ssh user@192.168.200.2

