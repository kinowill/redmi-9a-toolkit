# Journal de validation

## Contrôles logiciels

- 45 tests unitaires et contrôles Ruff, mypy et Bandit (niveau moyen ou supérieur).
- CI sur Windows, Linux et macOS, avec Python 3.10 et 3.13.
- Construction des distributions wheel/sdist et installation éditable vérifiées.
- Les parcours d’écriture sont couverts par des transports simulés.

## Validation matérielle

`doctor` et `verify --root-check` ont été exécutés en lecture seule sur un
Redmi 9A sous LineageOS 20. Le plan a été vérifié hors ligne avec les tailles
et empreintes des images. Voir les [preuves techniques](docs/evidence/) et
les [limites du test](docs/VALIDATED_DEVICE.md).

Aucun essai matériel complet des commandes `unlock` et `install` du toolkit
n’a été réalisé.
