# Installer Ubuntu

[← Retour à l'accueil](/README.md)

## Paramétrage linux

* `sudo apt update && sudo apt upgrade`: Mettre à jour linux.
* `sudo dpkg-reconfigure --priority=low unattended-upgrades`: Mettre à jours les paquets automatiquement.
* `chsh -s /bin/bash`: change de shell pour l'utilisateur courant (bash dans ce cas).

## Pare-feu

`ufw` (**uncomplicated firewall**): Pare-feu linux. [Documentation](https://doc.ubuntu-fr.org/ufw).

* `sudo ufw status`: état courant du pare-feu. Devrait être inactif par défaut.
* `sudo ufw enable`: active le pare-feu.
* `sudo systemctl status ssh`: status de la commande ssh.
* `sudo ufw allow ssh`: autoriser les connexion ssh.

## Utilitaires système

Neofetch permet d'afficher les informations du système dans un terminal. [Neofetch github](https://github.com/dylanaraps/neofetch?tab=readme-ov-file).

* `sudo apt install neofetch`.
* `neofetch`

Htop permet de voir les processus en cours dans un terminal. [Htop github](https://github.com/htop-dev/htop).

* `sudo apt install htop`.

## Codex et Gui (facultatif)

`sudo apt install ubuntu-restricted-extras`

Ubuntu Restricted Extras améliore l'expérience de l'utilisateur sur Ubuntu en fournissant un ensemble d'utilitaires et de codecs importants qui ne sont généralement pas inclus dans l'installation standard ([Source](https://linuxconfig.org/ubuntu-restricted-extras-what-they-are-and-how-to-install-them)).

`sudo apt install vlc`

Intallation de vlc si besoin.

`sudo apt-get install tasksel`

Installer un GUI (graphic user interface) Tasksel. Tasksel est une application d'installation de logiciels faisant partie intégrante de l'installeur Debian. Tasksel regroupe les paquets à installer par tâches (ex. serveur LAMP, création audio, etc.), permettant ainsi à l'utilisateur d'installer très facilement l'ensemble des paquets nécessaires à une tâche particulière ([Source](https://doc.ubuntu-fr.org/tasksel)).

## Partage de fichiers

* `sudo apt install samba`
* Tester samba `samba --version` `whereis samba`.
* Créer un dossier de partage `mkdir /home/<username>/<foldername>/`.
* Editer les paramètres samba pour ajouter le répertoire `sudo nano /etc/samba/smb.conf`.
* Ajouter les lignes suivantes à la fin du fichier:

``````shell
[sambashare]
    comment = Samba on Ubuntu
    path = /home/<username>/<foldername>
    read only = no
    browsable = yes
``````

* Redémarrer le service pour mettre à jour les paramètres `sudo service smbd restart`.
* Ajouter une permission pour samba au pare-feu `sudo ufw allow samba`.
* Créer un mot de passe pour le partage de fichiers `sudo smbpasswd -a <username>`. Ce mot de passe permettra d'ajouter le lecteur réseau depuis windows par exemple.

### Ajouter le lecteur depuis windows

* Ouvrir l'explorateur de fichiers.
* Dans le volet de gauche, sélectionner "Ce PC". Dans la barre d'actions, déployer le menu "..." > Mapper le lecteur réseau.
* Ajouter le lecteur : `\\<serverip>\<sambashare>`.
* Valider et compléter les champs "username" et "password" (mot de passe samba).

* [Install and configure samba](https://ubuntu.com/tutorials/install-and-configure-samba#1-overview).
* [Mapper un lecteur réseau dans Windows](https://support.microsoft.com/fr-fr/windows/mapper-un-lecteur-r%C3%A9seau-dans-windows-29ce55d1-34e3-a7e2-4801-131475f9557d#ID0EBD=Windows_11)

## Git

* `sudo apt-get install git` puis `git --version`.
* `git config --list (--show-origin)`.
* Générer une clé ssh : [doc github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux).
* [Ajouter une nouvelle clé ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) à son compte github.

## Docker

1. Installer docker ([documentation officielle](https://docs.docker.com/engine/install/ubuntu/)).
2. Post-install: ajouter les droits à un utilisateur ([documentation officielle](https://docs.docker.com/engine/install/linux-postinstall/))

### Portainer

* Installer portainer CE edition ([documentation officielle](https://docs.portainer.io/start/install-ce/server/docker/linux)).
* Mettre à jour portainer ([documentation officielle](https://docs.portainer.io/start/upgrade)).
* Portainer 101 ([Playlist YT](https://www.youtube.com/watch?v=n5ctCWPoCCI&list=PLhawEudhdubTUe0ip9j12ceeN0foAJQgu)).

## Installer nvm, node.js et npm

### NVM

1. Installer cURL (outil utilisé pour télécharger du contenu à partir d’Internet dans la ligne de commande) : `sudo apt-get install curl`.
2. Installer nvm : `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash`.
3. Tester l'installation : `command -v nvm`. Doit retourner "nvm".
4. Installer la version LTS stable actuelle de Node.js : `nvm install --lts`.
5. Vérifier les installations de node et npm avec `node --version` et `npm --version`.

[Supprimer NVM](https://github.com/nvm-sh/nvm?tab=readme-ov-file#uninstalling--removal)

*Source: [Installer nvm, node.js et npm](https://learn.microsoft.com/fr-fr/windows/dev-environment/javascript/nodejs-on-wsl#install-nvm-nodejs-and-npm).

## Ressources

* [Install and configure ubuntu server - full setup guide (YT)](https://www.youtube.com/watch?v=nUOmuN-7-d4)
* [Incredible Budget Home Server! (Minecraft, Plex, Home Assistant, NAS) (YT)](https://www.youtube.com/watch?v=72D3MvPk3Xs)
* [Ubuntu tutorials](https://ubuntu.com/tutorials)
* [Installer Plex sur Docker](https://technologie-geek.fr/comment-installer-plex-sur-docker/)
* [Doc install plex](https://hub.docker.com/r/linuxserver/plex).
* [Doc install Jellyfin](https://hub.docker.com/r/linuxserver/jellyfin).
