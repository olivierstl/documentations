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

## API

Documentation de l'API [directus](https://docs.directus.io/reference/query.html)

## Liens utiles

* [Ajouter auto slug à la sauvegarde / modification](https://github.com/directus/directus/discussions/15195)

### Typescript

Pour générer le typage de son api directus, utiliser les commandes fournies dans le module [directus-typescript-gen](https://github.com/elierotenberg/directus-typescript-gen)
