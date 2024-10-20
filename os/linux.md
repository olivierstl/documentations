# Guidelines et cheatsheet pour linux

[← Retour à l'accueil](/README.md)

## Commandes utiles

* `pwd`: **Print work directory**. Affiche le chemin du dossier courant
* `ls`: **List**. Liste du contenu du dossier courant
* `cd _path`: **Change directory**. Se déplacer vers un autre dossier
* `whoami`: **Current user**. Affiche l'utilisateur courant
* `clear`: Vide le terminal
* `cat`: **Concatenate**. Affiche le contenu du fichier dans la console
* `cp _filetocopy _nameofthecopy`: **Copy**. Crée une copie de fichier
* `sudo _command`: ****. Force une commande avec les permissions de root
* `rm`: **Remove**. Supprime un fichier
* `adduser _name`: Ajoute un utilisateur (*sbin command*)
* `which _file`: Affiche le chemin de la commande appelée

* `man _command`: **Manuel**. Documentation de la commande-h
* `_command -h | --help`: sous commandes possibles
* `apropos _keyword`: recherche de commandes

* `ps`: **Process status**. Liste les processus en cours
* `id`: donne des informations sur l'utilisateur et la machine
* `hostname`: nom de la machine
* `uname _modfier`: fait des trucs
* `ifconfig`: Informations réseau
* `ip`: Plus d'informations réseau
* `netstat`: Statut du réseau
* `ss`: **Session status**. Informations de session
* `ps`: **Process status**. Information sur les process
* `who`: Qui d'autre est loggé sur le système
* `env`: Variables d'environnement
* `lsblk`: **List blocks**. Informations disques durs
* `lsusb`: **List usb**. Périphériques usb pluggés
* `lsof`: **List open files**. Fichier ouverts

## Raccourcis

* `ctrl + C`: Coupe la commande en cours

## Fonctionnement de linux

Tout est fichier au sein de linux: dossiers, fichiers mais aussi le disque dur, une imprimante. Et même les commandes linux.

### Dossiers à la racine

* `bin`: **binaries**: contient des commandes.
* `sbin`: **super bin**: contient des commandes plus puissant. Il faut des droits particulier pour les utiliser.
* `usr`: **unix system resources**: contient des programmes, des données et des documents utilisés par les utilisateurs du système
  * `usr/bin`: contient des exécutables et des commandes utilisées par les utilisateurs du système.
  * `usr/include`: contient des fichiers d'en-tête utilisés par les compilateurs pour inclure du code dans les programmes.
  * `usr/lib` , `usr/lib64`: contient des bibliothèques (librairies) utilisées par les programmes (32 et 64 bits)
  * `usr/local`: contient des programmes et des données installées localement sur le système, par un administrateur, non installés par le gestionnaire de paquets
  * `usr/sbin`: contient des exécutables et des commandes utilisées par l'admin système
  * `usr/share`: contient des données partagées utilisées par les programmes (fichiers de langue, images, polices de caractères ...)
  * `usr/src`: contient le code source des programmes installés
* `home`: Là où sont stockés les utilisateurs (excepté `root`).
* `root`: Dossier de l'utilisateur `root`.
* `dev`: **device**: Là où sont rangés les periphériques.
* `etc`: **editing text config** ou "etsy". Là où sont rangés les fichiers de configuration, `network` par exemple
* `media`: Là où sont ajoutés les périphériques amovibles ("drives") montés (ex: clé usb).
* `mnt`: **mount**: Comme `media` mais pour les périphériques de systèmes de fichiers montés manuellement (disquette, CD-ROM…)..
* `var`: **variable**: fichiers variables tels que journaux et bases de données.
  * `var/cache`: contient des données mises en cache par les programmes et le système, telles que les paquets de logiciels téléchargés (apt, yum, dnf, emerge suivant votre distribution).
  * `var/lib`: contient des données utilisées par les programmes du système, telles que les bases de données (mysql) par exemple.
  * `var/log`: contient des fichiers de log, avec un sous dossier par service installé.
  * `var/run`: contient des fichiers temporaires utilisés par les programmes en cours d'exécution (fichiers .pid, ...).
  * `var/spool`: contient des fichiers en attente d'être traités par les programmes système, tels que les impressions et les tâches cron.
  * `var/tmp`: contient des fichiers temporaires utilisés par les programmes. Par rapport à /tmp ces fichiers tomporaires ne sont pas épurés automatiquement.

### Dossier "user"

Contient une autre intération de `bin` et `sbin` mais plus puissantes. Actuellement ce sont ces commandes qui sont appelées quand elles sont utilisées dans la console (`which ls` par exemple)

Autre sous dossiers `local` (commandes crées), `lib` (fichiers de bibliothèques partagées), `games`, ...

### ligne de commande

Si la ligne du terminal se termine par `$`, on est loggé comme un utilisateur. Si la ligne se termine par `#`, on est logué en tant que `root`

### Droits: Utilisateurs, Groupes, Permissions

Ressource : [Droits sous Linux : Utilisateurs, Groupes, Permissions](https://www.linuxtricks.fr/wiki/droits-sous-linux-utilisateurs-groupes-permissions)

Seuls root et le propriétaire d'un fichier peuvent changer ses permissions d'accès.

#### Lexique

* Utilisateur :Utilisateur connecté au système. La liste des utilisateurs est disponible dans le fichier /etc/passwd
* Groupe :Groupe appartenant au système. La liste des groupes est disponible dans le fichier /etc/group
* Utilisateur Propriétaire (noté u comme user) :Utilisateur qui est en possession du fichier
*Groupe Propriétaire (noté g comme group):Groupe d'utilisateurs qui est en possession du fichier
*Autres Utilisateurs (noté o comme other):Utilisateurs qui ne sont ni propriétaire du fichier, ni faisant partie du groupe propriétaire.
* Tous (noté a comme all):Utilisateur propriétaire + Groupe propriétaire + Autres utilisateurs.
* Lecture (noté r comme **R**ead).
* Écriture (noté w comme **W**rite).
* Exécution (noté x comme e**X**ecution).

#### Droits des fichiers

* Lecture (noté r) : on peut par exemple lire le fichier avec un logiciel.
* Écriture (noté w) : on peut modifier le fichier et le vider de son contenu.
* Exécution (noté x) : on peut exécuter le fichier s'il est prévu pour, c'est-à-dire si c'est un fichier exécutable (script, programme).

#### Droits des dossiers

* Lecture (noté r) : il autorise l'affichage du contenu du répertoire (la liste des fichiers présents à la racine de ce répertoire).
* Écriture (noté w) : il autorise la création, la suppression et le changement de nom des fichiers qu'il contient, quels que soient les droits d'accès des fichiers de ce répertoire (même s'ils ne possèdent pas eux-mêmes le droit en écriture). Néanmoins le droit spécial sticky bit permet de passer outre ce comportement.
* Exécution (noté x) : il autorise l'accès (le traverser) au répertoire.

## Installations

### Git

Git arrive de base avec Ubuntu. Il peut être nécessaire de le mettre à jour :

1. Mettre à jour linux : `sudo apt update && sudo apt upgrade`.
2. Installer ou mettre à jour Git : `sudo apt-get install git`.
3. [Configuration de Git Credential Manager](https://learn.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-git#git-credential-manager-setup)
4. [Génération d’une nouvelle clé SSH](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux#generating-a-new-ssh-key)
5. [Ajout d’une nouvelle clé SSH à mon compte](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account)

*Source: [Démarrer avec Git sur le sous-système Windows pour Linux](https://learn.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-git).*

### Installer nvm, node.js et npm

#### NVM

1. Installer cURL (outil utilisé pour télécharger du contenu à partir d’Internet dans la ligne de commande) : `sudo apt-get install curl`.
2. Installer nvm : `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash`.
3. Tester l'installation : `command -v nvm`. Doit retourner "nvm".
4. Installer la version LTS stable actuelle de Node.js : `nvm install --lts`.
5. Vérifier les installations de node et npm avec `node --version` et `npm --version`.

[Supprimer NVM](https://github.com/nvm-sh/nvm?tab=readme-ov-file#uninstalling--removal)

*Source: [Installer nvm, node.js et npm](https://learn.microsoft.com/fr-fr/windows/dev-environment/javascript/nodejs-on-wsl#install-nvm-nodejs-and-npm).*
