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
- Protection activée par défaut ; l'interface n'affiche que les résultats et masque les détails techniques

## Pile technologique

Python + PySide6 + QFluentWidgets + moteur d'analyse C++ + extension d'accélération Rust

## Architecture

- **Couche UI** : Python + PySide6 + QFluentWidgets ; navigation multipage (Accueil / Conseils / Analyse / Protection / Comportement / Quarantaine / Avis / Paramètres) ; thème clair/sombre et couleur d'accent ; bascule de langue instantanée (zh/en).
- **Moteur d'analyse** : C++ (SilentSecurityEngine), analyse parallèle multithread, sortie du progrès et des résultats au format JSONL ; modes fichier / dossier / disque complet.
- **Accélération** : Rust (`ss_rust.pyd`, PyO3) analyse et agrège la sortie JSONL du moteur par lots, environ 3x plus rapide que l'analyse ligne par ligne en Python ; repli automatique sur du Python pur lorsqu'il est absent (sémantique identique).
- **Surveillance en temps réel** : Windows `ReadDirectoryChangesW` piloté par événements, récursif sur tous les disques fixes ; les menaces de signature confirmées sont supprimées automatiquement et les alertes heuristiques sont mises en quarantaine.
- **Protection comportementale** : création de processus via ETW (0 latence, derrière `NtCreateProcess` ; repli sur l'analyse périodique si indisponible) ; autorun du registre et connexions sortantes par différence d'instantanés ; les événements portent PID / PID parent / chaîne de comportement.
- **Service système** : le moteur est enregistré en tant que service Windows (SCM, démarrage automatique) avec une politique de redémarrage en cas d'échec (5 s / 10 s / 60 s) ; découplé du processus UI — la protection continue après la sortie et le SCM le relance si le processus est terminé.
- **Bac à sable** : les exécutables à haut risque qui échouent à la quarantaine sont automatiquement lancés dans un processus isolé, réévalués selon le comportement échantillonné, puis remis en quarantaine en cas de verdict malveillant.
- **Vérification de signature** : validation hors ligne d'Authenticode via WinVerifyTrust + extraction du signataire (sans vérification de révocation, sans réseau) ; les signatures valides de Microsoft / Google sont entièrement approuvées, les autres signatures valides sont dégradées en affichant le signataire.
- **Détection approfondie des injections** : ETW-TI (session noyau AutoLogger, Windows 11).
- **Modèle de communication** : UI et moteur découplés via JSONL — tube stdout pour les analyses ; en mode service, les événements de surveillance/comportement sont écrits dans des fichiers et lus de manière incrémentale par l'UI.
- **Quarantaine** : les fichiers sont déplacés vers un répertoire de quarantaine et renommés pour empêcher la ré-exécution ; liste / restauration / suppression pris en charge ; la quarantaine et les journaux sont exclus de l'analyse.

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
