
## Vérifier et configurer le fichier `sources.list`

1. **Comprendre l'importance du fichier `sources.list`** :
    - Le fichier `/etc/apt/sources.list` contient la liste des dépôts de paquets.
    - Une mauvaise configuration peut entraîner des problèmes de sécurité ou des dysfonctionnements du système.
    - **Sécurité** : Ne jamais ajouter de dépôts non officiels ou non fiables.
      
2. **Vérifier le contenu du fichier** : cat /etc/apt/sources.list
   
    Le contenu devrait ressembler à ceci :

- deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
- deb-src http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
    
- deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
- deb-src http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
    
- deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
- deb-src http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
    
