# Redmi 9A Community Toolkit — document maître

## Origine et portée autorisée

Toolkit communautaire pour le Redmi 9A. Les rapports publics se limitent aux
résultats techniques vérifiés. Les journaux privés, identifiants USB, clés,
firmwares et images de téléphone ne sont pas publiés.

Objectif : remplacer les essais répétitifs par un diagnostic, un audit local
d'images, un plan lisible et une installation contrôlée de bundles audités.
Aucun reflash ni effacement n'est nécessaire pour développer le toolkit ou
exécuter ses tests logiciels.

## Résultat attendu avant développement

- Python 3.10+, sans dépendance d'exécution ; Windows, Linux et macOS visés.
- Commandes de lecture par défaut ; installation distincte et explicitement destructive.
- Sélection d'un unique appareil, empreintes SHA256, architecture, modèle,
  firmware vendor, tailles et modes fastboot vérifiés avant écriture.
- Liste fermée des écritures : boot, vbmeta, system, puis remise à zéro Android.
- Préserver preloader, RPMB, partitions radio/calibration, vendor et product.
- Conserver l'authentification ADB ; aucune injection de clé ou désactivation SELinux.
- Aucun déverrouillage de compte, contournement d'activation ou relock automatique.
- Ne publier que du code original, des références et des preuves nettoyées.

## Choix et hypothèses

Choix retenu dans la portée demandée : orchestrateur Python et profils JSON,
plutôt qu'un script Windows lié au poste ou une image de téléphone redistribuée.
Les profils extensibles permettent d'étendre le support sans prétendre installer
n'importe quel OS sur n'importe quel appareil. Une ROM Linux native exige un portage.

Le premier profil cible M2006C3LG/dandelion, vendor MIUI EEA
V12.0.17.0.QCDEUXM, Android GSI ARM32/binder64/SAR. Le bootloader doit être
déjà déverrouillé pour l'installation. Sur demande explicite supplémentaire,
une commande de déverrouillage MediaTek distincte est ajoutée : version MTKClient
figée, Android identifié avant connexion BROM, GPT de référence, écriture unique
de 512 octets seccfg et relecture identique obligatoires. Ce nouvel adaptateur
n’a pas été exécuté sur le téléphone de référence.

Un manifeste de bundle est une configuration fournie par un opérateur de
confiance. Ses attestations d'audit ne prouvent pas qu'une image est sûre :
les SHA256 vérifient l'intégrité locale, pas la provenance ni la compatibilité.
Les sources et le contenu doivent être contrôlés avant de créer un bundle.

Fiabilité : arrêt au premier écart, jamais de reprise aveugle après un flash
partiel. Pas de service distant ni collecte. Performances : lecture SHA256 par
blocs, plafond d'extraction et aucune image entière chargée en mémoire.
Maintenance communautaire par profils et rapports de validation anonymisés.

## Contrôles prévus et états à distinguer

Tests unitaires : fichiers tronqués, CRC gzip, limites de taille, manifestes
incomplets, mauvaise architecture, appareils multiples, bootloader verrouillé,
mauvais fastboot, partitions trop petites, échec de flash et commandes interdites.
Analyse statique, installation du paquet et diagnostic réel en lecture seule.

Le succès de la procédure manuelle d'origine ne valide pas l'orchestrateur neuf.
Les trois états à renseigner dans VALIDATION_LOG.md : code local, publication
GitHub, exécution réelle sur téléphone.

État sécurité constaté : chiffrement Android `encrypted` / `file`, SELinux
Enforcing, ADB authentifié. Correctif système 2025-09-05 et ancien noyau/vendor
Xiaomi : aucune promesse de sécurité à jour. Le port Droidian dandelion a retiré
ses images à cause de blocages selon révision matérielle ; pas d'installation
Linux native dans ce périmètre sans un portage maintenu et une validation.

Sources de vérité du dépôt : ce document, ROADMAP.md, VALIDATION_LOG.md, code.
