### FRANÇAIS

# Solution de première place pour le défi d'identification du sel Kaggle TGS (b.e.s. et phalanx)

## Papier décrivant la solution:

**Segmentation semi-supervisée des corps de sel dans des images sismiques à l'aide d'un ensemble de réseaux de neurones convolutifs**
 ***Conférence allemande sur la reconnaissance de formes (GCPR), 2019***
*Yauhen Babakhin, Artsiom Sanakoyeu, Hirotoshi Kitamura*
https://arxiv.org/abs/1904.04445

Kaggle post sur la solution: [link](https://www.kaggle.com/c/tgs-salt-identification-challenge/discussion/69291).

## ENVIRONNEMENT

La solution est disponible sous forme de conteneur Docker. Les dépendances suivantes doivent être installées:

* Python 3.5.2
* CUDA 9.0
* cuddn 7
* pilotes nvidia v.384
* [Docker] (https://www.docker.com/)
* [nvidia-docker] (https://github.com/NVIDIA/nvidia-docker)

## CONFIGURATION DES DONNÉES

Téléchargez et décompressez [competition data](https://www.kaggle.com/c/tgs-salt-identification-challenge/data) dans le répertoire `data/`.
On pourrait spécifier le chemin local vers les nouvelles images de test dans le fichier `SETTINGS.json` (champ `NEW_TEST_IMAGES_DATA`). Les données du test de compétition sont utilisées par défaut.

Le Dossier devrait ressembler a ceci après téléchargement des données:
![plot](/readmeimage/datafolder.JPG)

## CONFIGURATION DES POIDS

Pour obtenir les poids des modèles de la phase finale, téléchargez-les depuis [google drive](https://drive.google.com/file/d/12iXDUhBTC6596MLAC2aiN-GDVqBbGBWh/view?usp=sharing) et décompressez-les dans les répertoires correspondant  `bes/weights/` et `phalanx/weights`.

## CONFIGURATION DU DOCKER

Pour créer et démarrer une exécution de conteneur Docker:
```bash
docker cd
./build.sh
./run.sh
```

## CONSTRUCTION DE MODÈLE

1. Former des modèles à partir de zéro

    a) Entraîne tous les modèles à partir de zéro

    b) Attendez-vous à ce que cela dure environ 16 jours sur une seule GTX1080Ti
    
2. Faire des prédictions

    a) Utilise les poids des modèles d'étape finale pour faire des prédictions

    b) Attendez-vous à ce que cela dure 3,5 heures pour 18000 images de test sur une seule GTX1080Ti

Les commandes pour exécuter chaque build sont présentées ci-dessous:

### 1. modèles de train (crée des poids de modèle en bes/poids et phalanx/poids)
```bash
./train.sh
```

### 2. faire une prédiction (crée des prédictions / test_prediction.csv)
```bash
./predict.sh
```

## NOTES COMPLÉMENTAIRES

1. Les poids du modèle sont enregistrés dans bes/poids et phalanx/poids pour b.e.s. et modèles de phalanx respectivement

2. Les prédictions des modèles individuels avant l'assemblage sont stockées dans bes/predictions (beaucoup d'images .png) et phalanx/predictions (fichiers .npy)

3. Les scripts pour générer les plis initiaux et les mosaïques de puzzle se trouvent dans bes / datasets: generate_folds.py et Generate_Mosaic.R

## CITATION
Si vous trouvez ce code utile, veuillez citer notre article:

```
@journal{tgsSaltBodiesSegmentation2019,
  title={Semi-Supervised Segmentation of Salt Bodies in Seismic Images using an Ensemble of Convolutional Neural Networks},
  author={Babakhin, Yauhen, and Sanakoyeu, Artsiom, and Kitamura, Hirotoshi},
  journal={German Conference on Pattern Recognition (GCPR)},
  year={2019}
}
```

### ENGLISH

# 1st Place Solution for the Kaggle TGS Salt Identification Challenge (b.e.s. & phalanx)

## Paper describing the solution: 

**Semi-Supervised Segmentation of Salt Bodies in Seismic Images using an Ensemble of Convolutional Neural Networks**  
 ***German Conference on Pattern Recognition (GCPR), 2019***  
*Yauhen Babakhin, Artsiom Sanakoyeu, Hirotoshi Kitamura*   
https://arxiv.org/abs/1904.04445 

Kaggle post about the solution: [link](https://www.kaggle.com/c/tgs-salt-identification-challenge/discussion/69291).

## ENVIRONMENT

The solution is available as a Docker container. The following dependecies should be installed:

* Python 3.5.2
* CUDA 9.0
* cuddn 7
* nvidia drivers v.384
* [Docker](https://www.docker.com/)
* [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)

## DATA SETUP

Download and unzip [competition data](https://www.kaggle.com/c/tgs-salt-identification-challenge/data) into `data/` directory.
One could specify local path to the new test images in `SETTINGS.json` file (`NEW_TEST_IMAGES_DATA` field). The competition test data is used by default.

## WEIGHTS SETUP

To get the weights from the final stage models download them from [google drive](https://drive.google.com/file/d/12iXDUhBTC6596MLAC2aiN-GDVqBbGBWh/view?usp=sharing) and unzip into corresponding `bes/weights/` and `phalanx/weights` directories.

## DOCKER SETUP

To build and start a docker container run:
```bash
cd docker 
./build.sh
./run.sh
```

## MODEL BUILD

1. train models from scratch

    a) trains all models from scratch

    b) expect this to run for about 16 days on a single GTX1080Ti
    
2. make prediction

    a) uses weights from the final stage models to make predictions

    b) expect this to run for 3.5 hours for 18,000 test images on a single GTX1080Ti

Commands to run each build are presented below:

### 1. train models (creates model weights in bes/weights and phalanx/weights)
```bash
./train.sh
```

### 2. make prediction (creates predictions/test_prediction.csv)
```bash
./predict.sh
```

## ADDITIONAL NOTES

1. Model weights are saved in bes/weights and phalanx/weights for b.e.s. and phalanx models respectively

2. Individual model predictions before ensembling are stored in bes/predictions (lots of .png images) and phalanx/predictions (.npy files)

3. Scripts to generate initial folds and jigsaw mosaics are located in bes/datasets: generate_folds.py and Generate_Mosaic.R

## CITATION
If you find this code useful, please cite our paper:

```
@journal{tgsSaltBodiesSegmentation2019,
  title={Semi-Supervised Segmentation of Salt Bodies in Seismic Images using an Ensemble of Convolutional Neural Networks},
  author={Babakhin, Yauhen, and Sanakoyeu, Artsiom, and Kitamura, Hirotoshi},
  journal={German Conference on Pattern Recognition (GCPR)},
  year={2019}
}
```
