# Installer un VPS

[← Retour à l'accueil](/README.md)

## Configuration

Hébergement chez Hostinger, système Debian sans UI surcouche UI en backoffice.

## Debian

* [cheatsheet linux](https://linuxconfig.org/linux-commands-cheat-sheet)systemctl status docker
* [cheatsheet VIM](https://vim.rtorr.com)

Se connecter au serveur via SSH via la commande : `ssh NOMUSER@HOST`. Demandera le mot de passe si pas de clé ssh enregistrée. De base, on pop dans son dossier user si on en a un et pas root.

### Créer un nouvel utilisateur

* `useradd -m -s /bin/bash NOMUSER` : Ajout un utilisateur `NOMUSER`
  * `-m` : Crée le répertoire de l’utilisateur (home) – par défaut `/home/utilisateur`
  * `-s` : Indique le shell de connexion (/bin/bash, /bin/false, …)
* `userdel NOMUSER`
* `userpasswd NOMUSER`
* `usermod -aG sudo NOMUSER` : Ajouter l'utilisateur (addgroup) au groupe SUDO (pas aussi fort de root nonobstant)

> Penser à créer utilisateur avec bash et pas sh. Sinon [tuto ici](https://askubuntu.com/questions/325807/arrow-keys-home-end-tab-complete-keys-not-working-in-shell) pour changer.

### Ne pas demander le mdp à chaque sudo

* `cd /etc/sudoers.d`: bouger dans le repertoire des permissions sudo (sudoers)
* `sudo touch 90-olivier`: créer un fichier pour donner les instructions sudo
* `sudo vim 90-olivier`: édition du fichier avec VIM (`i`: insert pour écrire)
* Ajouter la ligne `NOMUSER ALL=(ALL) NOPASSWD:ALL`
* Quitter et save VIM (`esc`, `:wq`, enter)

### Ajouter une clé SSH

La démarche suivante part du principe qu'on a déjà ajouté notre clé SSH à root.

* Ajouter une clé SSH pour un utilisateur en copiant root
* Depuis le dossier `NOMUSER`: `mkdir .ssh`
* `sudo cp /root/.ssh/authorized_keys .ssh/authorized_keys`: copier le fichier chez nous
* `sudo chown olivier:olivier authorized_keys`: change propriétaire du fichier

### Editer le fichiers hosts windows pour avoir un raccourci de connexion console

Ajouter un fichier `config` dans le dossier `users/$USER/.ssh` :

```config
Host NOMALIAS
  HostName HOSTIP
  User NOMUSER
```

Permet en console de faire la commande `ssh NOMALIAS` qui sera un alias pour `ssh User@HostName`

### Installer docker

* RTFM [Installer docker sur debian](https://docs.docker.com/engine/install/debian/)
* [Ajouter les permissions à la commande](https://docs.docker.com/engine/install/linux-postinstall/) `docker`

### Nginx Proxy manager

* [Doc d'install de nginx proxy manager](https://nginxproxymanager.com/guide/#hosting-your-home-network)
* Créer un répertoire pour le docker-compose `var/www/nginx-proxy-manager`
* Dedans, créer le fichier docker-compose : `touch docker-compose.yml`
* Vérifier que le service docker tourne sur le vps `systemctl status docker.service`
  * Si non, le (re)lancer : `sudo service docker restart`
* Lister les services: `systemctl --type=service`
* Apache empêche nginx d'écouter le port, tuer apache avec `sudo service apache2 stop`

### Cloner un repo

* Gérer la config ssh : [documentation git](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
* Pas possible de cloner directement dans `/var/www/` pour cause de permissions
* Créer le dossier pour accueillir le repo à la main `sudo mkdir NOMDUDOSSIER`
* Se déplacer dans le dossier `cd NOMDUDOSSIER/`
* Changer les droits du dossier `sudo chown olivier:olivier .`
* `git clone` le repo
