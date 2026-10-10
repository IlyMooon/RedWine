# Politique de sécurité — RedWine

La sécurité des utilisateurs et l'intégrité du projet **RedWine** sont des priorités fondamentales. Ce document décrit la démarche à suivre pour signaler une vulnérabilité de façon responsable, ainsi que le périmètre de sécurité propre à Wine.

---

## 1. Rappel fondamental sur l'isolation et Wine

> [!WARNING]
> **Wine n'est pas un bac à sable (sandbox) de sécurité.**
> Wine est une couche de compatibilité qui traduit les appels système Windows en appels système macOS. Les processus Windows exécutés via RedWine s'exécutent avec les privilèges complets de votre compte utilisateur macOS. Par conséquent :
> - Ne lancez jamais d'exécutables Windows (`.exe`, `.msi`, `.bat`) provenant de sources inconnues ou non fiables.
> - Un binaire malveillant exécuté sous Wine peut lire, modifier ou supprimer vos fichiers personnels au même titre qu'une application macOS native.

---

## 2. Versions prises en charge

Seule la dernière version publiée sur la branche principale (`main`) de [IlyMooon/RedWine](https://github.com/IlyMooon/RedWine) bénéficie des correctifs de sécurité.

| Version | Prise en charge |
| :--- | :--- |
| Dernière version sur `main` | :white_check_mark: Oui |
| Versions antérieures / non maintenues | :x: Non |

---

## 3. Signalement responsable d'une vulnérabilité

Si vous découvrez une faille de sécurité touchant le code de RedWine (gestion des processus, privilèges, exécution de scripts non contrôlés, etc.) :

1. **Ne créez pas d'issue publique sur GitHub.**
2. Utilisez la fonctionnalité de **signalement privé de vulnérabilité** de GitHub (*Private Vulnerability Reporting*) sur la page [Security Advisories de RedWine](https://github.com/IlyMooon/RedWine/security/advisories/new) si elle est activée.
3. À défaut, contactez directement le mainteneur du dépôt par email à l'adresse suivante :
   `[CONTACT_À_COMPLÉTER : ex. adresse email de sécurité du mainteneur]`

### Informations utiles à fournir

Dans votre rapport, merci d'inclure :
- Une description précise de la vulnérabilité constatée.
- Les étapes détaillées permettant de reproduire le problème (avec un scénario ou un exemple de preuve de concept non destructif).
- L'impact potentiel sur le système de l'utilisateur ou la confidentialité de ses données.
- Vos suggestions d'atténuation ou de correctif le cas échéant.

---

## 4. Délais de traitement

- **Accusé de réception** : Une réponse initiale confirmant la prise en compte du signalement vous sera adressée sous 48 à 72 heures ouvrées.
- **Investigation et correctif** : La faille sera analysée en priorité. Une fois le correctif développé et testé, une nouvelle version sera publiée accompagnée de crédits pour le chercheur ayant effectué le signalement de manière responsable.
