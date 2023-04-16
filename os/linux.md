# Guidelines et cheatsheet pour linux

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

* `bin`: **binaries**: contient des commandes
* `sbin`: **super bin**: contient des commandes plus puissant. Il faut des droits particulier pour les utiliser.
* `usr`: **user**
* `home`: Là où sont stockés les utilisateurs (excepté `root`).
* `root`: Dossier de l'utilisateur `root`
* `dev`: Là où sont rangés les "devices"
* `etc`: etcetera ou "etsy". Là où sont rangés les fichiers de configuration, `network` par exemple
* `media`: Là où sont ajoutés les périphériques ("drives") montés (clé usb par ex)
* `mnt`: Comme `media` mais pour les périphériques montés manuellement

### Dossier "user"

Contient une autre intération de `bin` et `sbin` mais plus puissantes. Actuellement c'est ces commandes qui sont appelées quand elles sont utilisées dans la console (`which ls` par exemple)

Autre sous dossiers `local` (commandes crées), `lib` (fichiers de bibliothèques partagées), `games`, ...

### ligne de commande

Si la ligne du terminal se termine par `$`, on est loggé comme un utilisateur. Si la ligne se termine par `#`, on est logué en tant que `root`
