# Journal des modifications (Changelog)

Toutes les modifications notables apportées au projet **RedWine** sont consignées dans ce document.

Le format est basé sur [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) et ce projet adhère aux principes de [Semantic Versioning](https://semver.org/lang/fr/).

---

## [Non publié]

### Ajouté
- Initialisation et restructuration du fork **RedWine** à partir de Whisky (commit `fd5480a7`).
- Refonte intégrale et bilingue de la documentation : `README.md` (français) et `README.en.md` (anglais) avec sélecteur de langue.
- Guide de contribution dédié ([CONTRIBUTING.md](CONTRIBUTING.md)) incluant les prérequis de build (Xcode 15, macOS Sonoma, SwiftLint) et les conventions Conventional Commits.
- Politique de sécurité et de signalement responsable des vulnérabilités ([SECURITY.md](SECURITY.md)).
- Modèles d'issues GitHub en français pour le signalement de bugs ([.github/ISSUE_TEMPLATE/bug.yml](.github/ISSUE_TEMPLATE/bug.yml)) et les suggestions d'améliorations ([.github/ISSUE_TEMPLATE/feature-request.yml](.github/ISSUE_TEMPLATE/feature-request.yml)).
- Modèle de Pull Request structuré ([.github/PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md)).

### Modifié
- Mise à jour du Code de Conduite ([CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)) pour dissocier les canaux de modération du projet d'origine.
- Clarification de la licence effective du projet : **GNU General Public License v3.0 (GPL-3.0)**.
- Renforcement des règles du fichier [.gitignore](.gitignore) pour les environnements macOS et Xcode modernes.

### Supprimé
- Suppression des liens externes obsolètes pointant vers l'infrastructure du projet d'origine (Discord, Crowdin, site web d'origine).
- Retrait de la commande Homebrew du projet parent dans la documentation pour éviter d'installer une version obsolète.
- Suppression du fichier de sponsoring amont [.github/FUNDING.yml](.github/FUNDING.yml) et des liens d'affiliation tiers.
- Suppression du workflow de publication amont [.github/workflows/Release.yml](.github/workflows/Release.yml) (non fonctionnel sans secrets et ciblant des dépôts externes).
