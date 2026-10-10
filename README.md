<div align="center">

# RedWine 🍷
**Un lanceur graphique moderne pour Wine sous macOS, propulsé par SwiftUI**

[![Licence : GPL-3.0](https://img.shields.io/badge/licence-GPL--3.0-blue.svg)](LICENSE)
[![Plateforme : macOS](https://img.shields.io/badge/plateforme-macOS%20(Apple%20Silicon)-lightgrey.svg)](#prérequis-et-compatibilité)
[![SwiftLint CI](https://github.com/IlyMooon/RedWine/actions/workflows/SwiftLint.yml/badge.svg)](https://github.com/IlyMooon/RedWine/actions/workflows/SwiftLint.yml)

[🇬🇧 English](README.en.md) | **[🇫🇷 Français](README.md)**

</div>

---

## 1. Aperçu

**RedWine** est une application macOS native conçue pour créer et gérer des environnements d'exécution Windows isolés (« bouteilles » Wine), et exécuter des logiciels ou jeux Windows (`.exe`, `.msi`, `.bat`) directement sur Mac, sans nécessiter de machine virtuelle lourde ni d'installation complète de Windows.

Conçu avec SwiftUI et s'intégrant au système d'exploitation macOS, RedWine met l'accent sur l'ergonomie, la simplicité de configuration et l'exploitation des technologies graphiques d'Apple.

---

## 2. Fonctionnalités

Toutes les fonctionnalités listées ci-dessous sont intégrées dans le code source de l'application :

- **Gestionnaire de bouteilles Wine** :
  - Création, configuration et suppression d'environnements Wine indépendants.
  - Choix de la version de Windows émulée (Windows 7, Windows 10, Windows 11).
  - Accès direct au disque `C:`, au dossier utilisateur et au panneau de configuration Wine (`winecfg`).
- **Lancement et association de fichiers** :
  - Prise en charge des exécutables Windows (`.exe`), installateurs (`.msi`) et scripts batch (`.bat`).
  - Lancement par double-clic dans le Finder, glisser-déposer sur l'interface ou sélection manuelle.
- **Accélération graphique 3D** :
  - Traduction Direct3D 9/10/11 vers Vulkan via **DXVK**, puis vers Metal via **MoltenVK**.
  - Intégration de **D3DMetal** (Apple Game Porting Toolkit).
  - Bascule de synchronisation **msync** pour des performances multithread accrues.
  - Option d'activation du Metal Performance HUD pour afficher les métriques en jeu en direct.
- **Intégration Winetricks** :
  - Interface graphique permettant d'installer des composants d'exécution Windows courants (runtimes Visual C++, .NET Framework, polices Microsoft).
- **Console de journaux en direct** :
  - Raccourci `Cmd + L` pour afficher la console de débogage capturant les flux `stdout` et `stderr` de Wine en temps réel.
- **Extension Finder (Vignettes)** :
  - Module `WhiskyThumbnail` permettant d'extraire et d'afficher les icônes réelles contenues dans les en-têtes PE des fichiers `.exe` directement dans le Finder.
- **Outil en ligne de commande** :
  - Utilitaire `WhiskyCmd` inclus pour automatiser ou scripter la gestion des bouteilles depuis le Terminal.

---

## 3. Prérequis et compatibilité

Les prérequis suivants sont vérifiés dans la configuration du projet Xcode :

| Composant | Prérequis |
| :--- | :--- |
| **Système d'exploitation** | **macOS 14.0 (Sonoma)** ou version ultérieure (`MACOSX_DEPLOYMENT_TARGET = 14.0`). |
| **Architecture processeur** | **Apple Silicon exclusivement (M1, M2, M3, M4)** (`ARCHS = arm64`). Les Mac Intel (x86_64) ne sont pas pris en charge par cette cible. |
| **Rosetta 2** | Indispensable pour permettre l'exécution des binaires Windows 64 bits et 32 bits (via WoW64). |
| **Espace disque** | Prévoir au minimum 2 à 5 Go d'espace libre selon le nombre de bouteilles créées et les composants installés. |

---

## 4. Installation

### Téléchargement des releases
Si une version précompilée est mise à disposition, rendez-vous sur la page des [Releases de RedWine](https://github.com/IlyMooon/RedWine/releases), téléchargez l'archive ou l'image disque `.dmg`, puis glissez `RedWine.app` dans votre dossier `/Applications`.

> [!NOTE]
> Ne pas utiliser la commande Homebrew du projet d'origine (`brew install --cask whisky`), car celle-ci installerait l'application d'origine obsolète et non RedWine.

### Compilation depuis les sources
Si aucune version compilée n'est disponible ou si vous souhaitez exécuter le code le plus récent, suivez les instructions de la section [Compiler depuis les sources](#6-compiler-depuis-les-sources).

---

## 5. Prise en main

1. **Premier lancement** : Ouvrez l'application. Si le composant de compatibilité Wine n'est pas encore installé, l'assistant d'installation vous guide pour initialiser les bibliothèques.
2. **Créer une bouteille** :
   - Cliquez sur le bouton `+` ou « Créer une bouteille ».
   - Donnez-lui un nom (ex. *Jeux*, *Outils*) et sélectionnez la version de Windows cible (ex. *Windows 10*).
3. **Lancer un programme** :
   - Cliquez sur « Exécuter... » et choisissez un installateur (`setup.exe`) ou un fichier exécutable.
   - Les programmes installés sont automatiquement épinglés dans l'interface de la bouteille pour un accès rapide.
4. **Configuration graphique et réglages** :
   - Ouvrez la vue de configuration de la bouteille pour activer DXVK, msync ou le HUD Metal selon les besoins de votre jeu ou logiciel.
5. **Surveillance et débogage** :
   - En cas d'erreur ou de fermeture inattendue d'un programme, pressez `Cmd + L` pour inspecter les journaux Wine.

---

## 6. Compiler depuis les sources

### Outils requis
- Un Mac avec puce Apple Silicon sous macOS 14.0 Sonoma ou supérieur.
- **Xcode 15** ou version ultérieure (disponible sur le Mac App Store ou le portail Apple Developer).
- Les outils en ligne de commande Xcode :
  ```bash
  xcode-select --install
  ```
- **SwiftLint** (obligatoire pour compiler le projet Xcode en local) :
  ```bash
  brew install swiftlint
  ```

### Étapes de compilation

1. **Cloner le dépôt** :
   ```bash
   git clone https://github.com/IlyMooon/RedWine.git
   cd RedWine
   ```

2. **Résolution des dépendances** :
   Les dépendances SPM (`Sparkle`, `swift-argument-parser`, `SwiftyTextTable`, `Progress.swift`, `SemanticVersion`) sont automatiquement résolues lors de l'ouverture du projet dans Xcode ou lors de la compilation en ligne de commande.

3. **Compiler l'application via le terminal** :
   ```bash
   # Compilation en mode Release
   xcodebuild build -project Whisky.xcodeproj -scheme Whisky -configuration Release

   # Ou compilation de développement sans signature de code :
   xcodebuild build -project Whisky.xcodeproj -scheme Whisky -configuration Debug CODE_SIGNING_ALLOWED=NO
   ```

4. **Lancer les vérifications SwiftLint** :
   ```bash
   swiftlint --strict
   ```

---

## 7. Structure du dépôt

```text
├── Whisky/                 Application principale macOS (interface SwiftUI, vues, AppDelegate, ressources)
├── WhiskyKit/              Framework Swift interne (moteur Wine, gestion des bouteilles, extraction PE, réglages)
├── WhiskyCmd/              Utilitaire en ligne de commande (CLI)
├── WhiskyThumbnail/        Extension QuickLook / Vignettes pour le Finder
├── Libraries/              Binaires tiers embarqués (cabextract)
├── images/                 Ressources graphiques locales
├── .github/                Modèles d'issues, de PR et flux d'intégration continue (CI)
├── LICENSE                 Texte intégral de la licence GNU General Public License v3.0
├── CONTRIBUTING.md         Guide de contribution, conventions de branches et de commits
├── CODE_OF_CONDUCT.md      Code de conduite de la communauté
├── SECURITY.md             Politique de signalement responsable des vulnérabilités
└── CHANGELOG.md            Historique des versions (format Keep a Changelog)
```

> [!NOTE]
> *Pourquoi certains dossiers et cibles s'appellent-ils encore « Whisky » ?*
> Ces noms internes proviennent du projet parent. Afin de garantir une stricte intégrité du code source, d'éviter les ruptures de compilation et de préserver la compatibilité interne du projet Xcode, ces identifiants n'ont pas été renommés arbitrairement.

---

## 8. Limites connues et compatibilité

RedWine est une couche de compatibilité et ne garantit pas le fonctionnement de tous les logiciels Windows :

- **Systèmes anti-triche au niveau noyau (Kernel-level Anti-Cheat)** : Les jeux nécessitant un pilote noyau Windows propriétaire (tels que Riot Vanguard, BattlEye, Easy Anti-Cheat, Ricochet) ne peuvent pas fonctionner sous Wine.
- **Jeux avec DRM restrictifs** : Certains mécanismes de protection contre la copie refusent de s'exécuter dans des environnements émulés.
- **Applications 16 bits DOS / Windows 3.1** : Non prises en charge par le sous-système WoW64 64 bits.
- **DirectX 12** : Le support varie selon les fonctionnalités Metal de votre Mac et la couche D3DMetal / VKD3D disponible.
- **Serveurs de données amonts** : Les serveurs de téléchargement du runtime gérés par le projet parent d'origine sont hors ligne. Le téléchargement automatique du runtime nécessite un hébergement actif de substitution ou une installation manuelle des bibliothèques Wine.

---

## 9. Sécurité

> [!WARNING]
> **Wine ne constitue pas un bac à sable (sandbox) de sécurité.**
> Les processus Windows lancés via RedWine disposent des mêmes permissions d'accès au système de fichiers et au réseau que votre compte utilisateur macOS. N'exécutez jamais d'exécutables provenant de sources suspectes ou inconnues.

Pour signaler une vulnérabilité de façon responsable, veuillez consulter notre [Politique de sécurité](SECURITY.md).

---

## 10. Contribuer et communauté

Les contributions, retours d'expérience et rapports d'anomalies sont les bienvenus :

- Pour proposer une modification, lisez attentivement le [Guide de contribution](CONTRIBUTING.md).
- Pour signaler un bug, utilisez le modèle officiel [Rapport de bug](https://github.com/IlyMooon/RedWine/issues/new?template=bug.yml).
- Pour suggérer une amélioration, ouvrez une [Demande de fonctionnalité](https://github.com/IlyMooon/RedWine/issues/new?template=feature-request.yml).
- L'ensemble des échanges au sein du projet est régi par notre [Code de conduite](CODE_OF_CONDUCT.md).

---

## 11. Crédits et remerciements

RedWine est rendu possible grâce au travail remarquable de plusieurs projets et mainteneurs de la communauté open source :

- [msync](https://github.com/marzent/wine-msync) par marzent
- [DXVK-macOS](https://github.com/Gcenx/DXVK-macOS) par Gcenx et doitsujin
- [MoltenVK](https://github.com/KhronosGroup/MoltenVK) par KhronosGroup
- [Sparkle](https://github.com/sparkle-project/Sparkle) par le projet Sparkle
- [swift-argument-parser](https://github.com/apple/swift-argument-parser) par Apple
- [SwiftyTextTable](https://github.com/scottrhoyt/SwiftyTextTable) par scottrhoyt
- [Progress.swift](https://github.com/jkandzi/Progress.swift) par jkandzi
- [SemanticVersion](https://github.com/SwiftPackageIndex/SemanticVersion) par SwiftPackageIndex
- [CrossOver](https://www.codeweavers.com/crossover) et [WineHQ](https://www.winehq.org/) par CodeWeavers et la communauté Wine
- D3DMetal par Apple

Nous tenons à exprimer notre profonde gratitude à **CodeWeavers** pour leur engagement historique et continu dans le développement de Wine, sans lequel cette application n'existerait pas.

---

## 12. Origine du projet

**RedWine** est un fork indépendant du projet [Whisky-App/Whisky](https://github.com/Whisky-App/Whisky), initialement conçu et développé par Isaac Marovitz et ses contributeurs.

- **Statut du projet d'origine** : Le projet d'origine a été archivé et n'est plus activement maintenu par son auteur.
- **Rôle de RedWine** : Ce fork a été créé pour assurer la pérennité, la clarté et l'évolution du projet en modernisant sa documentation, son organisation communautaire et en maintenant sa compatibilité.
- **Indépendance** : RedWine est un projet autonome. Il n'est ni affilié, ni sponsorisé, ni approuvé par les auteurs originaux de Whisky.

---

## 13. Licence

Ce projet est distribué sous les termes de la licence **GNU General Public License v3.0 (GPL-3.0)**.  
Consultez le fichier [LICENSE](LICENSE) pour prendre connaissance de l'intégralité du texte légal et des conditions d'utilisation.
