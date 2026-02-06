![Image chargée](https://chatgpt.com/backend-api/estuary/content?id=file_000000005af071f4bbeccc475cbc7d56&ts=491772&p=fs&cid=1&sig=4701b8dd04715ab8a5a76f26264fb7c47a3c8eef0f178f9da2f76c4ccd506ba5&v=0)

J'ai ce message d'erreur quand je veux upgrade, tu peux m'aider stp ?

Oui. D’après la capture, tu as **deux problèmes distincts** :

1. **`dpkg was interrupted`** → une installation/upgrade précédente s’est arrêtée en plein milieu, et `dpkg` doit finir sa configuration.
    
2. **`Could not open lock ... Permission denied`** → tu as lancé `apt upgrade` **sans sudo** (donc pas les droits root), d’où le lock impossible.
    

Voici la procédure propre (dans cet ordre) :

### 1) Vérifier qu’aucun autre apt/dpkg ne tourne

`ps aux | egrep 'apt|dpkg' | grep -v egrep`

Si tu vois un `apt`/`dpkg` actif (hors ta commande), attends qu’il finisse ou stoppe-le proprement.

### 2) Réparer l’état de dpkg (obligatoire)

`sudo dpkg --configure -a`

Ça va terminer la config des paquets restés “en plan”.

### 3) Corriger les dépendances cassées si besoin

`sudo apt -f install`

### 4) Relancer la mise à jour et l’upgrade (avec sudo)

`sudo apt update sudo apt full-upgrade -y`

(`full-upgrade` est souvent préférable sur Kali/rolling car il gère mieux les changements de dépendances.)

---

## Si ça bloque encore sur des locks

Si tu as un message du style “lock is held by process …”, récupère le PID indiqué et vérifie :

`ps -p <PID> -o pid,cmd`

- Si c’est un apt légitime en cours → laisse finir.
    
- Si c’est un truc planté depuis longtemps → on peut le tuer, mais fais-le seulement si tu confirmes qu’il est bloqué.
    

⚠️ **Évite** de supprimer les fichiers `lock` à la main tant que tu n’es pas sûr qu’aucun process apt/dpkg n’utilise le gestionnaire de paquets.

---

Si tu colles ici la sortie de :

`sudo dpkg --configure -a`

(et éventuellement de `sudo apt -f install` s’il y a des erreurs),  
je te dis exactement quoi faire selon le paquet qui coince.

![Image chargée](https://chatgpt.com/backend-api/estuary/content?id=file_000000002e0471f4a92ce5c8248a010b&ts=491772&p=fs&cid=1&sig=3505aaf8c42fbc2ce3c142963a740fb3d430b3513846fafeb7c1de23948b60d5&v=0)

j'ai ce message là

Le message **`fatal: not a git repository (or any of the parent directories): .git`** veut dire une chose simple : tu exécutes `git push` / `git pull` dans un dossier qui **n’est pas** un dépôt Git (il n’y a pas de dossier caché `.git`).

Selon ce que tu veux faire, voilà les cas corrects.

## Cas 1 — Tu veux récupérer le projet (tu ne l’as pas encore en local)

Tu ne fais pas `pull` sur une URL. Tu fais un **clone** :

`git clone https://github.com/kanboard/kanboard.git cd kanboard`

Ensuite seulement, tu peux faire :

`git pull`

## Cas 2 — Tu as déjà le projet, mais tu n’es pas dans le bon dossier

Va dans le dossier du projet (celui qui contient `.git`) :

`cd /chemin/vers/kanboard ls -la`

Si tu vois `.git/`, ok. Puis :

`git pull`

Astuce pour retrouver le dépôt si tu ne sais plus où il est :

`find ~ -maxdepth 4 -type d -name .git 2>/dev/null`

## Cas 3 — Tu as un dossier de code existant et tu veux le “connecter” à ce repo GitHub

Si tu as déjà des fichiers dans un dossier et tu veux en faire un dépôt :

`cd /chemin/vers/ton_dossier git init git remote add origin https://github.com/kanboard/kanboard.git git pull origin master   # ou main selon le repo`

⚠️ Mais attention : `kanboard/kanboard` est un repo public, tu ne pourras pas “push” dessus sans droits. En général tu dois **fork** puis pousser sur TON fork.

## Pourquoi ta commande `git push https://...` ne marche pas comme tu penses

`git push` / `git pull` se font depuis **un dépôt local**. L’URL, c’est normalement un _remote_ configuré (`origin`). La séquence normale est :

`git clone <url> cd <repo> git pull git push`

---

Si tu me dis juste : **tu veux télécharger Kanboard**, ou **tu veux envoyer ton code sur GitHub**, je te donne les commandes exactes (et je te dis comment gérer `main` vs `master`). En attendant, pour Kanboard, fais simplement :

`git clone https://github.com/kanboard/kanboard.git cd kanboard`

donne moi la procédure pour installer Kanboard sur Kali stp

Voici une **procédure propre et standard pour installer Kanboard sur Kali Linux** (Kali = Debian-based).  
Je te donne la méthode **Apache + PHP + SQLite** (la plus simple). MySQL est optionnel.

---

## 1️⃣ Mettre le système à jour

`sudo apt update sudo apt full-upgrade -y`

---

## 2️⃣ Installer Apache, PHP et extensions requises

Kanboard nécessite PHP ≥ 7.4 et plusieurs extensions.

`sudo apt install -y apache2 \ php php-cli php-fpm php-mbstring php-sqlite3 php-json \ php-xml php-gd php-curl php-zip php-opcache unzip git`

Vérifie PHP :

`php -v`

---

## 3️⃣ Démarrer et activer Apache

`sudo systemctl enable apache2 sudo systemctl start apache2`

Test rapide :

`curl http://localhost`

Tu dois voir la page Apache.

---

## 4️⃣ Télécharger Kanboard

On l’installe dans `/var/www/kanboard` (bonne pratique).

`cd /var/www sudo git clone https://github.com/kanboard/kanboard.git sudo chown -R www-data:www-data kanboard sudo chmod -R 755 kanboard`

---

## 5️⃣ Configuration Apache (VirtualHost)

Créer le fichier :

`sudo nano /etc/apache2/sites-available/kanboard.conf`

Contenu :

`<VirtualHost *:80>     ServerName kanboard.local     DocumentRoot /var/www/kanboard      <Directory /var/www/kanboard>         AllowOverride All         Require all granted     </Directory>      ErrorLog ${APACHE_LOG_DIR}/kanboard_error.log     CustomLog ${APACHE_LOG_DIR}/kanboard_access.log combined </VirtualHost>`

Activer le site + modules nécessaires :

`sudo a2ensite kanboard sudo a2enmod rewrite sudo systemctl reload apache2`

---

## 6️⃣ Accès à Kanboard

Ouvre ton navigateur :

`http://localhost`

ou

`http://kanboard.local`

(si tu ajoutes dans `/etc/hosts` :

`127.0.0.1 kanboard.local`

)

---

## 7️⃣ Identifiants par défaut ⚠️

Au premier accès :

- **Utilisateur** : `admin`
    
- **Mot de passe** : `admin`
    

👉 **Change le mot de passe immédiatement**

---

## 8️⃣ (Optionnel) Base MySQL/MariaDB

Si tu veux MySQL au lieu de SQLite :

`sudo apt install mariadb-server php-mysql`

Puis configurer :

`sudo nano /var/www/kanboard/config.php`

---

## 9️⃣ Vérifier les permissions (très important)

`sudo chown -R www-data:www-data /var/www/kanboard`

---

## 10️⃣ Dépannage rapide

Voir les logs si écran blanc ou erreur :

`sudo tail -f /var/log/apache2/kanboard_error.log`

---

### ✅ Résumé rapide

- Apache + PHP installés
    
- Kanboard cloné dans `/var/www/kanboard`
    
- VirtualHost configuré
    
- Accès via navigateur
    
- Login `admin / admin`
    

Si tu veux :

- installation **Docker**
    
- installation **MySQL**
    
- sécurisation (HTTPS, hardening)
    
- ou installation **en environnement pentest**
    

dis-le-moi et je t’adapte la procédure exactement à ton usage Kali.

Ouvre ton navigateur : arduino Copier le code `http://localhost` ou arduino Copier le code `http://kanboard.local` (si tu ajoutes dans `/etc/hosts` : bash Copier le code `127.0.0.1 kanboard.local` )

![Image chargée](https://chatgpt.com/backend-api/estuary/content?id=file_0000000021fc71f4a8b5b82c6ca0e36b&ts=491773&p=fs&cid=1&sig=8c635ef25b4e1844b005391577876a99f3702b563f6b55e4deb64c06060fe70d&v=0)

J'obtiens toujours que ça

C’est normal 👍  
Apache fonctionne, **mais il sert encore le site par défaut**, pas Kanboard.  
Il faut soit **désactiver le site par défaut**, soit **accéder au bon VirtualHost**.

On va régler ça proprement.

---

## 🔍 Pourquoi tu vois encore la page Debian

Quand tu vas sur :

`http://localhost`

Apache sert **`000-default.conf`**, qui pointe vers :

`/var/www/html`

Or Kanboard est dans :

`/var/www/kanboard`

Donc Apache **ne sait pas encore** que Kanboard doit répondre sur `localhost`.

---

## ✅ SOLUTION 1 (la plus simple) : accéder directement à Kanboard

Teste immédiatement dans ton navigateur :

`http://localhost/kanboard`

👉 Si Kanboard s’affiche → Apache + PHP OK, on ajustera ensuite proprement.

Si **ça marche**, dis-le moi.  
Sinon, continue avec la solution propre ci-dessous.

---

## ✅ SOLUTION 2 (recommandée) : faire de Kanboard le site principal

### 1️⃣ Désactiver le site par défaut

`sudo a2dissite 000-default.conf`

---

### 2️⃣ Vérifier que le site Kanboard est bien activé

`ls /etc/apache2/sites-enabled/`

Tu dois voir :

`kanboard.conf`

Si ce n’est pas le cas :

`sudo a2ensite kanboard.conf`

---

### 3️⃣ Vérifier le `DocumentRoot`

`sudo nano /etc/apache2/sites-available/kanboard.conf`

Il doit contenir **exactement** :

`DocumentRoot /var/www/kanboard`

---

### 4️⃣ Redémarrer Apache

`sudo systemctl restart apache2`

---

### 5️⃣ Recharger la page

Dans le navigateur :

`http://localhost`

➡️ **Kanboard doit apparaître**

---

## 🧪 Vérification PHP (important)

Si tu as une page blanche ou erreur :

`sudo tail -n 50 /var/log/apache2/error.log`

ou

`sudo tail -n 50 /var/log/apache2/kanboard_error.log`

---

## 🔐 Permissions (au cas où)

`sudo chown -R www-data:www-data /var/www/kanboard sudo chmod -R 755 /var/www/kanboard`

---

## ✅ Résumé rapide

- Apache OK ✅
    
- Tu vois la page par défaut → normal
    
- Désactiver `000-default`
    
- Activer `kanboard.conf`
    
- Redémarrer Apache
    
- Accéder à `http://localhost`
    

---

👉 **Dis-moi exactement** :

1. Est-ce que `http://localhost/kanboard` fonctionne ?
    
2. Le contenu de :
    

`ls /etc/apache2/sites-enabled/`

Avec ça, je te fais le diagnostic final en 1 message.

👉 Si Kanboard s’affiche → Apache + PHP OK, on ajustera ensuite proprement. Si **ça marche**, dis-le moi. Sinon, continue avec la solution propre ci-dessous.

![Image chargée](https://chatgpt.com/backend-api/estuary/content?id=file_000000003ab8720aaf7ff2f1f1301d45&ts=491773&p=fs&cid=1&sig=bbca2922273d4940041b9684260f7c6a5b473240ea3bc242023d6f772dfe5d22&v=0)

j'ai ça

OK — le **404 sur `/kanboard`** indique simplement que **Kanboard n’est pas installé dans `/var/www/html/kanboard`** (le DocumentRoot du site par défaut), ou que ton vhost Kanboard n’est pas actif. On va vérifier et corriger en 3 minutes.

## 1) Vérifie où est Kanboard sur le disque

Exécute :

`ls -la /var/www ls -la /var/www/kanboard`

- Si `/var/www/kanboard` **n’existe pas** ou est vide → il faut (re)cloner.
    
- Si ça existe, on configure Apache pour pointer dessus.
    

### Si le dossier n’existe pas : clone Kanboard

`cd /var/www sudo git clone https://github.com/kanboard/kanboard.git sudo chown -R www-data:www-data /var/www/kanboard`

## 2) Fais pointer Apache vers Kanboard sur `http://localhost/`

### Crée/édite le vhost Kanboard

`sudo nano /etc/apache2/sites-available/kanboard.conf`

Mets exactement :

`<VirtualHost *:80>     ServerName localhost     DocumentRoot /var/www/kanboard      <Directory /var/www/kanboard>         AllowOverride All         Require all granted     </Directory>      ErrorLog ${APACHE_LOG_DIR}/kanboard_error.log     CustomLog ${APACHE_LOG_DIR}/kanboard_access.log combined </VirtualHost>`

### Active rewrite + le site, désactive le défaut, redémarre

`sudo a2enmod rewrite sudo a2ensite kanboard.conf sudo a2dissite 000-default.conf sudo systemctl reload apache2`

## 3) Test immédiat

Va sur :

`http://localhost`

---

# Si tu veux _vraiment_ `http://localhost/kanboard` (sous-dossier)

Alors il faut un **Alias** (ou copier Kanboard dans `/var/www/html/kanboard`). Option Alias (propre) :

`sudo nano /etc/apache2/sites-available/000-default.conf`

Dans le `<VirtualHost *:80>`, ajoute :

`Alias /kanboard /var/www/kanboard <Directory /var/www/kanboard>     AllowOverride All     Require all granted </Directory>`

Puis :

`sudo a2enmod rewrite sudo systemctl reload apache2`

---

## Si après ça tu as page blanche/erreur

Regarde le log :

`sudo tail -n 80 /var/log/apache2/kanboard_error.log`

---

Fais-moi juste coller la sortie de ces 2 commandes et je te dis exactement ce qui manque :

`ls -la /var/www ls /etc/apache2/sites-enabled/`

* Si `/var/www/kanboard` **n’existe pas** ou est vide → il faut (re)cloner. * Si ça existe, on configure Apache pour pointer dessus.

![Image chargée](https://chatgpt.com/backend-api/estuary/content?id=file_000000009c7871f4a509fc401b8f37ff&ts=491773&p=fs&cid=1&sig=c2b0698705eb98d1d554f0f88684f86e90b35d20bd8f85cb38f8398567ccf131&v=0)

j'ai ça

Parfait : **Kanboard est bien présent dans `/var/www/kanboard`** (on voit `index.php`, `app/`, etc.). Donc le 404 sur `http://localhost/kanboard` vient d’Apache : **ton site par défaut pointe sur `/var/www/html`**, et il n’y a pas de sous-dossier `kanboard` dedans.

Tu as 2 options. Je te donne la plus simple (Kanboard sur `http://localhost/`) + l’option `/kanboard` si tu y tiens.

---

## Option A (recommandée) : Kanboard sur `http://localhost/`

### 1) Crée le vhost Kanboard

`sudo tee /etc/apache2/sites-available/kanboard.conf >/dev/null <<'EOF' <VirtualHost *:80>     ServerName localhost     DocumentRoot /var/www/kanboard      <Directory /var/www/kanboard>         AllowOverride All         Require all granted     </Directory>      ErrorLog ${APACHE_LOG_DIR}/kanboard_error.log     CustomLog ${APACHE_LOG_DIR}/kanboard_access.log combined </VirtualHost> EOF`

### 2) Active le site + rewrite, désactive le défaut, recharge Apache

`sudo a2enmod rewrite sudo a2ensite kanboard.conf sudo a2dissite 000-default.conf sudo systemctl reload apache2`

### 3) Va sur

**[http://localhost](http://localhost)**

---

## Option B : garder la page Apache sur `/` et accéder à Kanboard via `/kanboard`

### 1) Crée un alias Apache

`sudo tee /etc/apache2/conf-available/kanboard-alias.conf >/dev/null <<'EOF' Alias /kanboard /var/www/kanboard  <Directory /var/www/kanboard>     AllowOverride All     Require all granted </Directory> EOF`

### 2) Active rewrite + l’alias, recharge

`sudo a2enmod rewrite sudo a2enconf kanboard-alias sudo systemctl reload apache2`

### 3) Va sur

**http://localhost/kanboard**

---

## Si ça affiche encore autre chose / erreur PHP

Regarde les logs :

`sudo tail -n 100 /var/log/apache2/error.log sudo tail -n 100 /var/log/apache2/kanboard_error.log`

---

Si tu veux, dis-moi quelle option tu choisis (A ou B). Sinon, fais **Option A** (c’est le plus clean) et ouvre `http://localhost`.

Option B : garder la page Apache sur `/` et accéder à Kanboard via `/kanboard` ------------------------------------------------------------------------------ ### 1) Crée un alias Apache bash Copier le code `sudo tee /etc/apache2/conf-available/kanboard-alias.conf >/dev/null <<'EOF' Alias /kanboard /var/www/kanboard <Directory /var/www/kanboard> AllowOverride All Require all granted </Directory> EOF` ### 2) Active rewrite + l’alias, recharge bash Copier le code `sudo a2enmod rewrite sudo a2enconf kanboard-alias sudo systemctl reload apache2` ### 3) Va sur **http://localhost/kanboard**

j'ai utilisé ça et ça marche

Nickel ✅

Deux petites choses à faire maintenant pour que ce soit propre et fiable :

## 1) Sécuriser les identifiants

À la première connexion : `admin / admin` → **change le mot de passe** tout de suite (Paramètres → Utilisateur).

## 2) Activer le cron Kanboard (recommandé)

Kanboard a un “scheduler” interne pour les notifications, tâches récurrentes, etc. Ajoute une entrée cron pour `www-data` :

`sudo crontab -u www-data -e`

Ajoute :

`*/5 * * * * cd /var/www/kanboard && php cli cronjob >/dev/null 2>&1`

## 3) Vérifier que les extensions PHP clés sont bien là

Si tu vois des warnings ou des fonctions manquantes :

`php -m | egrep 'mbstring|gd|curl|json|pdo|sqlite|xml|zip'`

## 4) Logs utiles si un jour ça plante

`sudo tail -n 100 /var/log/apache2/error.log`

Si tu veux, je peux aussi te donner la config HTTPS (Let’s Encrypt en local c’est moins utile, mais en VM/serveur oui) ou la version MariaDB pour de meilleures perfs.

![Image chargée](https://chatgpt.com/backend-api/estuary/content?id=file_00000000877c71f4ba614de183297dbf&ts=491773&p=fs&cid=1&sig=2ea63131b983584b31de9af7258a2aa40625e434e503bf6642e6e72080ad6b54&v=0)

pourquoi je ne peux pas save ?

Tu ne peux pas sauvegarder **à cause d’une erreur de validation sur les dates** — elle est clairement indiquée en rouge sur la capture.

### ❌ Le problème précis

À droite, Kanboard affiche :

> **“The start date is greater than the end date”**

Tes champs sont :

- **Start Date** : `02/20/2026 00:00`
    
- **Due Date (End Date)** : `02/06/2026 00:00`
    

👉 La **date de début est après la date de fin**, ce qui est interdit logiquement.  
Kanboard bloque donc l’enregistrement (comportement normal).

---

### ✅ Comment corriger

Tu as 3 solutions possibles :

#### Option 1 — Inverser les dates

- Start Date → **02/06/2026**
    
- Due Date → **02/20/2026**
    

#### Option 2 — Supprimer la Start Date

Si tu n’as pas besoin d’une date de début :

- Vide complètement **Start Date**
    
- Garde seulement **Due Date**
    

#### Option 3 — Supprimer la Due Date

Si tu veux juste une date de début :

- Vide **Due Date**
    
- Garde **Start Date**
    

---

### ℹ️ Règle Kanboard (à retenir)

- Start Date **≤** Due Date
    
- Une seule des deux peut être définie
    
- Si les deux sont définies, l’ordre doit être cohérent
    

---

Une fois la correction faite, le bouton **Save** fonctionnera immédiatement.  
Si tu veux, je peux aussi te proposer une **structure de tâches Kanboard adaptée à un audit/pentest** (colonnes, tags, priorités).

J'ai ma VM kali qui doit faire un scan des ports de mon autre VM Métasploitable 2, déja je dois mettre une adresse ip sur ma metasploit

Oui — **absolument**, et tu es sur la bonne voie 👍  
Pour que ta **VM Kali** scanne **Metasploitable2**, **Metasploitable DOIT avoir une adresse IP accessible** sur le même réseau virtuel.

Je te donne la procédure **claire et standard**, sans ambiguïté.

---

## 1️⃣ Choisir le bon mode réseau (très important)

Sur **les deux VMs (Kali et Metasploitable2)**, mets **le même mode réseau**.

### ✅ Recommandé pour un LAB :

- **NAT Network** _(VirtualBox)_  
    ou
    
- **Host-Only Adapter**
    

👉 **Évite “NAT simple”**, sinon Kali ne verra pas Metasploitable.

### Exemple VirtualBox :

`Settings → Network → Adapter 1 ☑ Enable Network Adapter Attached to: NAT Network`

(fais pareil sur les deux VMs)

---

## 2️⃣ Donner une IP à Metasploitable2

Par défaut, Metasploitable2 **récupère une IP automatiquement (DHCP)**.

Sur Metasploitable2, connecte-toi :

- login : `msfadmin`
    
- password : `msfadmin`
    

Puis :

`ip a`

ou :

`ifconfig`

Tu dois voir une interface (`eth0`) avec une IP, par exemple :

`inet 192.168.56.101`

👉 **Cette IP est la cible de ton scan**.

---

## 3️⃣ Vérifier que Kali peut joindre Metasploitable

Sur Kali :

`ping 192.168.56.101`

Si ça répond → réseau OK.

Si ❌ :

- mauvais mode réseau
    
- VMs pas sur le même réseau
    

---

## 4️⃣ Scanner les ports depuis Kali (Nmap)

Scan simple :

`nmap 192.168.56.101`

Scan complet (recommandé en lab) :

`nmap -p- -sS -sV -O -T4 192.168.56.101`

---

## 5️⃣ (Optionnel) IP statique sur Metasploitable2

**Pas obligatoire**, mais possible si tu veux une IP fixe.

`sudo nano /etc/network/interfaces`

Exemple :

`auto eth0 iface eth0 inet static     address 192.168.56.101     netmask 255.255.255.0     gateway 192.168.56.1`

Puis :

`sudo /etc/init.d/networking restart`

---

## ✅ Résumé rapide

- Oui, Metasploitable2 doit avoir une IP
    
- Pas besoin de la définir à la main → DHCP suffit
    
- Les deux VMs doivent être **sur le même réseau**
    
- Tu scannes **l’IP de Metasploitable**, pas Kali
    

---

Si tu veux, dis-moi :

- VirtualBox ou VMware ?
    
- Mode réseau actuel (NAT / Host-only / NAT Network)
    

Je t’indique **la config exacte écran par écran** pour ton setup.

### Recommandé pour un LAB : * **NAT Network** _(VirtualBox)_ ou * **Host-Only Adapter** 👉 **Évite “NAT simple”**, sinon Kali ne verra pas Metasploitable.

J'ai modifié ça et je l'ai rallumé et j'ai eu une adresse ip

Parfait 👍  
Ça veut dire que **le réseau est maintenant correctement configuré** et que Metasploitable2 est joignable.

On enchaîne logiquement, étape par étape.

---

## 1️⃣ Confirme l’IP de Metasploitable2

Sur **Metasploitable2** :

`ip a`

ou

`ifconfig`

Note bien l’IP (exemple) :

`192.168.56.101`

---

## 2️⃣ Vérifie la connectivité depuis Kali

Sur **Kali** :

`ping 192.168.56.101`

Résultat attendu :

- réponses OK → réseau opérationnel ✅
    
- pas de réponse → problème de mode réseau (mais vu ton message, ça devrait marcher)
    

---

## 3️⃣ Premier scan Nmap (basique)

Toujours depuis **Kali** :

`nmap 192.168.56.101`

Tu devrais déjà voir plusieurs ports ouverts (Metasploitable2 est volontairement vulnérable).

---

## 4️⃣ Scan complet (recommandé en LAB)

Quand le ping fonctionne :

`sudo nmap -p- -sS -sV -O -T4 192.168.56.101`

### Ce que font les options (important à comprendre) :

- `-p-` → tous les ports (1–65535)
    
- `-sS` → SYN scan (rapide, discret)
    
- `-sV` → détection des versions
    
- `-O` → détection de l’OS
    
- `-T4` → plus rapide (OK en lab)
    

---

## 5️⃣ Sauvegarder le résultat (bonne pratique)

`sudo nmap -p- -sS -sV -O -T4 192.168.56.101 -oA metasploitable_scan`

Tu auras :

- `metasploitable_scan.nmap`
    
- `metasploitable_scan.gnmap`
    
- `metasploitable_scan.xml`
    

---

## 6️⃣ Prochaine étape logique (pentest)

Après le scan, on fait généralement :

1. Identification des services vulnérables (FTP, SMB, HTTP, MySQL…)
    
2. Enumération ciblée (ex : `smbclient`, `enum4linux`, `nikto`)
    
3. Exploitation (Metasploit)
    

---
