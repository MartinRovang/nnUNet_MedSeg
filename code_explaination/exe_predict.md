
## Documentation pour `script_python.py`

---

### Vue d'ensemble

Le script `script_python.py` est conçu pour réaliser des prédictions en utilisant un modèle de deep learning avec la bibliothèque nnUNet. Il prend en entrée des images, les traite à travers un modèle pré-entraîné, et produit les résultats de la prédiction.

### Table des matières

- [Prérequis](#prérequis)
- [Exécution Principale](#exécution-principale)
- [Fonctions](#fonctions)
- [Utilisation](#utilisation)

---

### Prérequis

Assurez-vous d'avoir les bibliothèques suivantes installées :

- os
- sys
- shutil
- argparse
- subprocess
- re

---

### Exécution Principale

Le script commence par définir les chemins principaux et les variables nécessaires. Il vérifie ensuite si le dossier d'entrée contient des données pour la prédiction. Si des données sont présentes, il lance la prédiction en utilisant Docker et le modèle nnUNet. Après la prédiction, il nettoie les dossiers temporaires et affiche un message indiquant que la prédiction est terminée.

---

### Fonctions

#### list_model_available

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Affiche tous les modèles disponibles dans le dossier spécifié.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

```python
def list_model_available():
    print("All models available:")
    for folder in os.listdir(model_folder_path_result):
        print(f"{folder}")
```

---

#### create_folder

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Crée les dossiers nécessaires pour l'entrée et la sortie, et copie les fichiers d'entrée et les modèles dans les dossiers appropriés.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

---

#### remove_folder

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Supprime tous les dossiers temporaires et les fichiers inutiles après la prédiction.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

---

#### get_dataset_name

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Obtient le nom du dataset à partir du nom du modèle.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) `str`: Le nom du dataset.

---

#### get_fold_value

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Obtient la valeur du fold à partir du dossier du modèle.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) `str`: La valeur du fold.

---

#### extract_values

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Extrait les valeurs nécessaires à partir d'un fichier.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `file_path` (str): Le chemin du fichier à lire.
- ![Returns](https://img.shields.io/badge/-Returns-red) `tuple`: Les valeurs extraites.

---

#### remove_docker_container

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Supprime un conteneur Docker en utilisant son ID.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `id` (str): L'ID du conteneur Docker à supprimer.
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

---

#### gpu_available

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Vérifie la disponibilité des GPUs pour Docker.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) `list`: Les indices des GPUs disponibles.

---

#### exec_in_docker

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Exécute une commande dans le conteneur Docker.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue)
  - `cmd` (str): La commande à exécuter.
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

---

#### load_image

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Charge une image Docker.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

---

#### launch_docker_prediction

- ![Purpose](https://img.shields.io/badge/-Purpose-green) Lance la prédiction en utilisant Docker et le modèle nnUNet.
- ![Parameters](https://img.shields.io/badge/-Parameters-blue) Aucun
- ![Returns](https://img.shields.io/badge/-Returns-red) Aucun

---

### Utilisation

Pour utiliser ce script, placez vos données d'entrée dans le dossier spécifié et exécutez le script. Assurez-vous que toutes les dépendances sont installées et que Docker est configuré correctement sur votre machine.

