# Railway

## Installer un projet directus

1. New project
2. Provision MySQL database
3. Une fois crée, cliquer sur la card et voir l'onglet `Connect` : il contient les infos de notre base qui vont servir à initialiser directus.
4. Créer un nouveau projet directus. Pour ça suivre la doc [directus - nouveau projet railway](../cms/directus.md#nouveau-projet-railway)
5. Dans Railway, cliquer sur le bouton `New` > Github repo > sélectionner le repo directus
6. Le projet Git apparait avec la mention `Ne deploys for this service`. Nous allons paraméter directus :
   1. Cliquer sur la card de notre repo Git
   2. Onglet `Variables` :
      1. `NIXPACKS_NODE_VERSION` : `18`, on force la version 18 de node, obligatoire
      2. `PORT` : Port se trouvant dans le `.env`
   3. Onglet `Settings` :
      1. Bloc `Environment` :
         1. Link to a repo branch
         2. Generate domain
      2. Bloc `Deploy` :
         1. `Start command` > `npx directus start`
