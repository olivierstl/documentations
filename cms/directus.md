# Directus

## Nouveau projet railway

Documentation [self hosted](https://docs.directus.io/self-hosted/cli.html).

Cette liste d'étapes correspond à l'installation de directus via la webapp [railway](https://railway.app/).

1. Créer un nouveau repo sur git
2. Créer un nouveau dossier de travail
3. Initialiser git `git init` dans ce nouveau dossier
4. Ajouter la remote de votre nouveau repo `git remote add origin [ADDRESSE_REPO_GIT]`
5. Ne pas oublier d'ajouter un fichier `.gitignore` si ce n'est pas déjà fait
6. Dans le dossier, initialiser directus avec `npx directus init`
   1. `Choose database client` : MySQL
   2. `Host` : Railway > DB > Connect > MYSQLHOST
   3. `Port` : Railway > DB > Connect > MYSQLPORT
   4. `Name` : Railway > DB > Connect > MYSQLDATABASE
   5. `User` : Railway > DB > Connect > MYSQLUSER
   6. `Password` : Railway > DB > Connect > MYSQLPASSWORD
   7. `Email` : mail du compte admin directus généré par l'initialisation de directus
   8. `Password` : mot de passe admin directus généré par l'initialisation de directus

Une fois l'opération terminée, un fichier de configuration `.env` a été généré.

Commit et pusher le projet sur le repo.

### Erreur d'authentification

Après avoir renseigné les infos d'accès à la base de données, il y a de fortes chances que la CLI renvoie une erreur console :

```shell
Something went wrong while seeding the database:

[ER_NOT_SUPPORTED_AUTH_MODE] ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client
```

### Solution

Créer un service phpMyAdmin en local via docker-compose et l'image suivante :

```yml
version: '3.1'

services:
  phpmyadmin-remote:
    image: phpmyadmin
    restart: unless-stopped
    ports:
      - 7000:80
    environment:
      PMA_HOST: Railway > DB > Connect > MYSQLHOST
      PMA_PORT: Railway > DB > Connect > MYSQLPORT
```

Executer la commande `docker-compose up -d` et se rendre sur l'url locale du container. Pour se connecter à l'interface phpMyAdmin, utiliser les infos railway:

* `User` : Railway > DB > Connect > MYSQLUSER
* `Password` : Railway > DB > Connect > MYSQLPASSWORD

Se rendre dans l'onglet `Comptes utilisateurs` et cliquer sur `Editer les privilèges` de l'utilisteur root. Dans l'édition, se rendre dans l'onglet `Change password`, copier le mot de passe depuis railway pour conserver le même (Railway > DB > Connect > MYSQLPASSWORD) et mettre le Hachage du mot de passe en `Authentification MySQL native`.

Répéter l'opération pour le second utilisateur root.

Relancer la commande `npx directus init` et suivre les étapes au dessus.

## Installer directus sur un VPS

### Fichier docker compose

Exemple dans la [documentation directus](https://docs.directus.io/self-hosted/docker-guide.html#docker-compose).

Version mysql perso :

```YAML
version: '3.8'
services:
  olivetced-database:
    container_name: olivetced-database
    image: mysql:8
    command: --default-authentication-plugin=mysql_native_password
    ports:
      - 5101:${MYSQL_PORT}
    cap_add:
      - SYS_NICE
    volumes:
      - mysql-data:/var/lib/mysql
    networks:
      - directus
    environment:
      MYSQL_ROOT_PASSWORD: '${MYSQL_ROOT_PASSWORD}'
      MYSQL_DATABASE: '${MYSQL_DATABASE}'
    healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost", "-uroot", "-ppass"]
      interval: 5s
      timeout: 5s
      retries: 20

  olivetced-directus:
    container_name: olivetced-directus
    image: directus/directus:latest
    ports:
      - 8055:8055
    volumes:
      # By default, uploads are stored in /directus/uploads
      # Always make sure your volumes matches the storage root when using
      # local driver
      - ./uploads:/directus/uploads
      # Make sure to also mount the volume when using SQLite
      # - ./database:/directus/database
      # If you want to load extensions from the host
      - ./extensions:/directus/extensions
    networks:
      - directus
    depends_on:
      olivetced-database:
        condition: service_healthy
    environment:
      KEY: '255d861b-5ea1-5996-9aa3-922530ec40b1'
      SECRET: '6116487b-cda1-52c2-b5b5-c8022c45e263'

      DB_CLIENT: 'mysql'
      DB_HOST: '${MYSQL_HOST}'
      DB_PORT: '${MYSQL_PORT}'
      DB_DATABASE: '${MYSQL_DATABASE}'
      DB_USER: 'root'
      DB_PASSWORD: '${MYSQL_ROOT_PASSWORD}'

      ADMIN_EMAIL: '${DIRECTUS_ADMIN_EMAIL}'
      ADMIN_PASSWORD: '${DIRECTUS_ADMIN_PASSWORD}'

      # Make sure to set this in production
      # (see https://docs.directus.io/self-hosted/config-options#general)
      PUBLIC_URL: 'https://admin.olivetced.fr'

networks:
  directus:

volumes:
  mysql-data:
```

### Soucis rencontrés

#### Compose foireux

Lancer le compose initial générait des soucis aléatoire de plantage de directus. Après quelques recherches il s'avérait que le `depends_on` de sur le service de la base mysql ne suffisait pas. Le conteneur était initialisé mais pas encore la base, ce qui faisait planter directus.

J'ai du ajouter une condition `healthcheck` pour vérifier que la base était bien initialisée, avant de monter directus.

#### Droits d'écriture

Changer les droits d'écriture pour pemettre à directus d'écrire sur le disque (upload de fichiers) : `docker exec -u root IDCONTAINER chown -R node:node /directus/extensions /directus/uploads` (possible d'ajouter `/directus/database` au besoin). [Source](https://github.com/directus/directus/discussions/6480#discussioncomment-917708)

## API

Documentation de l'API [directus](https://docs.directus.io/reference/query.html)

## Liens utiles

* [Ajouter auto slug à la sauvegarde / modification](https://github.com/directus/directus/discussions/15195)
* [Déclencher action git depuis flow](https://github.com/directus/directus/discussions/12591#discussioncomment-4596707)

### Typescript

Pour générer le typage de son api directus, utiliser les commandes fournies dans le module [directus-typescript-gen](https://github.com/elierotenberg/directus-typescript-gen)
