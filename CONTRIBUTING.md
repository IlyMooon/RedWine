# Guide de contribution à RedWine

Merci de l'intérêt que vous portez au projet **RedWine** ! Les contributions sont les bienvenues, qu'il s'agisse de corriger un bug, d'améliorer la documentation ou de proposer de nouvelles fonctionnalités.

---

## 1. Environnement de développement et prérequis

Pour développer et compiler RedWine sur votre machine :

- **Système d'exploitation** : macOS 14.0 (Sonoma) ou version ultérieure.
- **Matériel** : Mac avec puce Apple Silicon (M1/M2/M3/M4).
- **Environnement de développement** : Xcode 15 ou supérieur (avec les outils de ligne de commande Xcode).
- **Linter Swift** : [SwiftLint](https://github.com/realm/SwiftLint) est requis pour compiler le projet via Xcode.
  Installez-le avec Homebrew :
  ```bash
  brew install swiftlint
  ```
- **Gestionnaire de dépendances** : Toutes les dépendances externes sont gérées automatiquement via le gestionnaire de paquets Swift (Swift Package Manager / SPM) intégré à Xcode.

---

## 2. Processus de contribution

1. **Forkez** le dépôt [IlyMooon/RedWine](https://github.com/IlyMooon/RedWine) sur votre compte GitHub personnel.
2. **Clonez** votre fork localement :
   ```bash
   git clone https://github.com/VOTRE_UTILISATEUR/RedWine.git
   cd RedWine
   ```
3. **Créez une branche de travail** dédiée à partir de `main` avec un nom explicite :
   ```bash
   git checkout -b feat/nom-de-fonctionnalite
   # ou
   git checkout -b fix/nom-du-bug
   ```
4. **Implémentez** vos modifications avec soin en respectant le style de code et les tests.
5. **Vérifiez la compilation et le linting** localement avant de soumettre.
6. **Poussez** votre branche sur votre fork et ouvrez une **Pull Request** visant la branche `main` de **IlyMooon/RedWine** (n'ouvrez jamais de PR vers le projet d'origine Whisky-App).

---

## 3. Conventions de style et de code

- **SwiftLint** : Le projet utilise une configuration stricte ([.swiftlint.yml](.swiftlint.yml)). Toute violation déclenche une erreur de compilation dans Xcode et bloque la CI.
- **Indentation** : Indentation avec **4 espaces** (pas de tabulations).
- **En-têtes de fichiers et Licence** : RedWine est distribué sous licence **GNU GPL v3.0**. Tout nouveau fichier Swift doit comporter l'en-tête de licence GPLv3 conforme aux directives du fichier `.swiftlint.yml`.
- **Localisation** : Les chaînes de caractères visibles dans l'interface doivent être ajoutées au fichier `Localizable.xcstrings` du projet.

---

## 4. Conventions de commits

Nous suivons les conventions [Conventional Commits](https://www.conventionalcommits.org/) :

- `feat:` pour une nouvelle fonctionnalité utilisateur.
- `fix:` pour une correction de bug.
- `docs:` pour des modifications de documentation (README, guides, commentaires).
- `refactor:` pour une réorganisation de code sans changement fonctionnel.
- `test:` pour l'ajout ou la mise à jour de tests.
- `build:` / `chore:` pour des changements relatifs au système de build, aux workflows GitHub ou à la configuration.

*Exemple :* `fix(ui): corriger le gel de la vue de configuration d'une bouteille`

---

## 5. Compilation et validation locale

Pour compiler et vérifier le projet depuis le terminal :

```bash
# Vérifier la conformité SwiftLint
swiftlint --strict

# Compiler le projet complet (Debug)
xcodebuild build -project Whisky.xcodeproj -scheme Whisky -configuration Debug CODE_SIGNING_ALLOWED=NO

# Compiler la version Release
xcodebuild build -project Whisky.xcodeproj -scheme Whisky -configuration Release
```

---

## 6. Soumettre une Pull Request

- Remplissez méticuleusement le formulaire de Pull Request défini dans [.github/PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md).
- Si votre PR apporte des modifications graphiques (UI), joignez des captures d'écran avant / après.
- Assurez-vous que l'ensemble des vérifications CI (SwiftLint) passe au vert.
- Tout comportement suspect, introduction de code propriétaire sans droit ou non-respect de la licence GPLv3 entraînera le rejet de la PR.

---

## 7. Signaler un bug ou proposer une idée

- Pour signaler un bug, utilisez le modèle dédié sur GitHub : [Rapport de bug](https://github.com/IlyMooon/RedWine/issues/new?template=bug.yml). Veillez à inclure vos versions logicielles et les journaux Wine (`Cmd + L`).
- Pour proposer une nouvelle idée, utilisez le formulaire : [Demande de fonctionnalité](https://github.com/IlyMooon/RedWine/issues/new?template=feature-request.yml).
