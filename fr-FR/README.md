# SilentSafe

SilentSafe est un logiciel de protection de la sécurité pour appareils personnels, produit par **SilentStudio**.

- **Version** : v1.0.0
- **Plateforme** : Windows

> Ce dépôt est uniquement destiné à la présentation du projet et ne contient **pas de code source**.

## Fonctionnalités

- Analyse de sécurité des fichiers (multithread + accélération Rust)
- Surveillance du système en temps réel (enregistré en tant que service Windows ; redémarrage automatique en cas d'échec ; la protection continue même après la fermeture de l'application)
- Gestion de la quarantaine
- Protection comportementale (processus / registre / réseau)
- Détection approfondie des injections (ETW-TI)
- Expérience à la Kaspersky : protection activée par défaut, uniquement les résultats, détails techniques masqués

## Pile technologique

Python + PySide6 + QFluentWidgets + moteur d'analyse C++ + extension d'accélération Rust

---

## Droits d'auteur

**Copyright © SilentStudio**

Certains composants publics de ce logiciel (par exemple, des exemples de SDK, certaines parties du code front-end ou des modules contribués par la communauté) peuvent être soumis à la GNU Affero General Public License (AGPL) v3.0 et à ses conditions complémentaires lorsque des conditions spécifiques sont remplies.

Les moteurs principaux (par exemple, SilentSecurityEngine), les services cloud (SSDBS) et toute partie non explicitement marquée comme Open Source sont protégés par les lois sur le droit d'auteur. Toute reproduction, modification, ingénierie inverse ou distribution commerciale non autorisée de ces parties est strictement interdite sans le consentement écrit préalable de SilentStudio.

---

## Équipe

SilentStudio, en tant qu'organisation mère de SilentCodeTeams, supervise le développement et les opérations des sous-équipes suivantes :

- SilentSafeGroup
- SilentNet.
- SilentCodeTeamsDev.

**Produced by SilentStudio.**
