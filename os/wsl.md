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

## Git

Git arrive de base avec Ubuntu. Il peut être nécessaire de le mettre à jour :

1. Mettre à jour linux : `sudo apt update && sudo apt upgrade`.
2. Installer ou mettre à jour Git : `sudo apt-get install git`.
3. [Configuration de Git Credential Manager](https://learn.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-git#git-credential-manager-setup)
4. [Génération d’une nouvelle clé SSH](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux#generating-a-new-ssh-key)
5. [Ajout d’une nouvelle clé SSH à mon compte](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account)

*Source: [Démarrer avec Git sur le sous-système Windows pour Linux](https://learn.microsoft.com/fr-fr/windows/wsl/tutorials/wsl-git).*
