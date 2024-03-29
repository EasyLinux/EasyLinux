# vaultWarden

## Contexte

Pour des raisons de sécurité, il a été décidé de supprimer la capacité d'enregistrement des mots de passe dans les navigateurs de nos collaborateurs.
Il se pose dès lors une question : comment permettre le stockage de mot de passe fort aux utilisteurs ? La réponse est dans ce qui suit : à savoir, la mise à disposition de vaultWarden.

> **NB:** vaultWarden est mis à disposition des collaborateurs, mais n'est pas un outil 'officiel' du groupe : il n'est pas lié à l'AD du groupe

## vaultWarden

**Vaultwarden** est un gestionnaire de mot de passe gratuit, OpenSource et SelfHosted basé sur **Bitwarden**. il inclut pas mal de fonctionnalités intéressantes tels que :

- Une application pour Windows, Mac et Linux
- Une application iOS et Android
- Une extension de navigateurs
- La gestion du 2FA
- Gestion de notes sécurisés, d'identités et de moyens de payements
- Classements par collections, dossiers et favoris
- Un générateur de mot de passe
- La possibilité de partager des mots de passe avec d’autres utilisateurs internes et externes
- Une gestion des droits avancées
- Le chiffrement des données stockées
- Support de la Yubikey et de Duo
- Et plein de petites configurations utiles !

Vous pouvez retrouver le Github du projet [ici](https://github.com/dani-garcia/vaultwarden).


## Implémentation

La mise en oeuvre de vaultWarden suit l'implémentation calssique d'une application au sein du groupe, cette application est définie [ici](https://gitea-p10s.alias.asten/app-catalog/vaultwarden).   
Dans le cadre de notre usage, plusieurs modifications seront apportées afin d'augmenter significativement la sécurité de l'ensemble.

- **l'accès d'administration est désactivé par défaut** : la variable d'environnement ADMIN_TOKEN n'est positionnée que sur demande, lors des actions d'administration. Sans cette variable, vaultwarden n'autorise pas d'accès à ses modules d'administration.
- **gestion** : un container interragit avec l'interface d'administration, ce container n'est pas accessible en dehors de la zone de sécurité du groupe.
- **micro services**: chaque fonction est implémentée dans un module (pod) à part.