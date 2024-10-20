# Windows

[← Retour à l'accueil](/README.md)

## Installation

- [Comment installer Linux sur Windows avec WSL](https://learn.microsoft.com/fr-fr/windows/wsl/install)

### Mise à jour de Linux

Mettre régulièrement à jour la ditribution Linux est important.

Utiliser les commandes `sudo apt update && sudo apt upgrade`.

### Sous-installations

Pour ajouter wget (pour récupérer du contenu à partir de serveurs web) et ca-certificates (pour autoriser les applications ssl à vérifier l’authenticité des connexions SSL), entrer : `sudo apt-get install wget ca-certificates`.

## Lancer le sous système

Utiliser la commande `wsl install` ou bien lancer Ubuntu depuis le menu démarrer.

## Mot de passe Linux oublié

1. Depuis un terminal, aller à la racine de WSL : `wsl -u root`
2. Réinitialiser le mot de passe via : `passwd <usernamse>`

## Commandes utiles

- `explorer.exe .` : Affiche le contenu du fichier dans l'explorateur windows.
