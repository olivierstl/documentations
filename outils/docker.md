# Docker

Docker est une plate-forme de conteneurs logicielle conçue pour développer, expédier et exécuter des applications utilisant la technologie des conteneurs. Docker est disponible en deux versions : une édition d'entreprise et une édition communautaire

## Définitions

### Conteneur

Contrairement à une machine virtuelle qui fournit la virtualisation matérielle, un conteneur fournit une virtualisation légère au niveau du système d'exploitation par l'abstraction de l'« espace utilisateur ». Les conteneurs partagent le noyau du système hôte avec d'autres conteneurs. Un conteneur, qui s'exécute sur le système d'exploitation hôte, est une unité logicielle standard qui rassemble le code et toutes ses dépendances, afin que les applications puissent s'exécuter rapidement et de manière fiable d'un environnement à un autre. Les conteneurs ne sont pas persistants et sont lancés à partir d'images.

### Image

Ensemble de logiciels à exécuter en tant que conteneur contenant un ensemble d'instructions pour la création d'un conteneur pouvant être exécuté sur la plate-forme Docker. Les images ne sont pas modifiables ; pour apporter des modifications à une image, il faut en créer une nouvelle.

### Volume

Docker volume est un mécanisme de fichiers géré par Docker permettant de sauvegarder des données générées lors de l’exécution d’un conteneur. Il permet également de monter les données dont le conteneur a besoin à l’intérieur de ce dernier pour qu’il puisse fonctionner correctement lors de son lancement.

Les volumes ne dépendent pas du cycle de vie du conteneur. Ainsi, on peut l’utiliser lors de la réexécution du conteneur ou le partager à d’autres conteneurs qui en ont besoin. C’est donc le moyen le plus adéquat pour faire persister des données au sein de Docker.

## Commandes

* `docker ps` : liste les conteneurs en route ([docs](https://docs.docker.com/engine/reference/commandline/ps/))
* `docker images` : liste des images disponibles sur l'ordi ([docs](https://docs.docker.com/engine/reference/commandline/images/))
* `docker stop CONTAINER_ID` : stope le conteneur `CONTAINER_ID` ([docs](https://docs.docker.com/engine/reference/commandline/stop/))
* `docker run [OPTIONS] IMAGE` : lance le conteneur avec les options ([docs](https://docs.docker.com/engine/reference/commandline/run/))
  * options : `-d / --detached`: detached, `-it`: interactive, `-p`: port, 
* `docker volume ls` : permet de lister les volumes
* `docker build` : permet de créer une image docker
  * options : `-t [NAME]` , `-it`: interactive, `-p`: port,  

## Docker file

* `FROM` : permet de définir l'image source pour créer notre conteneur
* `RUN` : permet d’exécuter des commandes dans votre conteneur
* `ADD` : permet d'ajouter des fichiers dans votre conteneur
* `WORKDIR` : se déplacer dans un répertoire (équivalent de `cd`)
* `EXPOSE` : permet de définir les ports d'écoute par défaut
* `VOLUME` : permet de définir les volumes utilisable
* `CMD` : permet de définir la commande par défaut lors de l’exécution de vos conteneurs Docker

### Fichier .dockerignore 

Ajouter un fichier `.dockerignore` permet d'indiquer à docker les répertoires à ignorer (et ne pas copier).
