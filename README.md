# Prédiction de l’Efficacité Énergétique des Bâtiments

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg?style=flat&logo=python&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange.svg?style=flat&logo=jupyter)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-0.24+-orange.svg?style=flat&logo=scikit-learn&logoColor=white)
![Statut](https://img.shields.io/badge/Statut-Complété-success.svg?style=flat)
![Licence](https://img.shields.io/badge/Licence-MIT-green.svg?style=flat)

## Objectif

Ce projet universitaire (Master MLAIM-S2) vise à prédire la charge de chauffage (Heating Load - Y1) et de refroidissement (Cooling Load - Y2) des bâtiments résidentiels à partir de leurs caractéristiques de conception. Pour cela, nous comparons deux approches de réseaux de neurones :
* 🧠 **Extreme Learning Machine (ELM)**
* 🔁 **Backpropagation (BP) via `MLPRegressor`**

## Contenu du dépôt

* `ENB2012_data_clean.csv` : Dataset utilisé (Energy Efficiency Data Set) nettoyé prêt à l'emploi.
* `Notebook_Prediction_Energie_Batiments.ipynb` : Notebook Jupyter contenant l'intégralité du code (prétraitement, entraînement des modèles ELM et BP, évaluation et visualisation).
* `Rapport.pdf` : Rapport détaillé du projet, de la méthodologie, et de l'analyse des résultats architecturaux.
* `README.md` : Ce fichier.

## Description du dataset

* 📦 **768 échantillons** représentant des bâtiments virtuels[cite: 2].
* 🔢 **8 variables d’entrée** (Compacité relative, Surface totale, Surface des murs, Surface du toit, Hauteur, Orientation, etc.)[cite: 2].
* 🎯 **2 cibles à prédire :**
  * **Y1** : Heating Load (charge de chauffage)[cite: 2]
  * **Y2** : Cooling Load (charge de refroidissement)[cite: 2]

## Méthodologie

1. **Chargement & Prétraitement :**
   * Normalisation des données avec `StandardScaler`.
   * Séparation en jeu d’entraînement (70%) et de test (30%).
2. **Entraînement et Optimisation :**
   * **ELM :** Test de plusieurs architectures (50, 100, 200 neurones) et fonctions d'activation (tanh, relu, sigmoid, linear).
   * **BP :** Recherche par grille (Grid Search) sur les couches cachées `(50,)`, `(100,)`, `(50, 50)` et les activations (ReLU, tanh, logistic).
3. **Évaluation :**
   * Métriques : RMSE, MAE, R².

## Résultats finaux

| Modèle Optimal | Target | RMSE | MAE | R² |
| :--- | :---: | :---: | :---: | :---: |
| **ELM (200 neurones, Sigmoid)** | Y1 | 1.3112 | 1.0111 | 0.9830 |
| **ELM (200 neurones, Sigmoid)** | Y2 | 2.0716 | 1.4577 | 0.9524 |
| **BP (Couches 50-50, ReLU)** | Y1 | 0.7288 | 0.5153 | 0.9948 |
| **BP (Couches 50-50, ReLU)** | Y2 | 1.4830 | 1.0540 | 0.9756 |

*(Note : Les résultats ci-dessus sont extraits de l'évaluation sur le jeu de test)*.

## Comment exécuter

Cloner ce dépôt, puis installer les dépendances requises :
```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```
Lancer ensuite Jupyter Notebook pour ouvrir et exécuter le fichier `Notebook_Prediction_Energie_Batiments.ipynb` :

```bash
jupyter notebook
```
## Conclusions

* **Performance des Modèles :** Le modèle BP (architecture 50,50 avec ReLU) offre la meilleure précision prédictive (RMSE le plus bas et R² le plus élevé) pour les deux cibles. L'ELM s'est néanmoins révélé être une excellente alternative, offrant des prédictions visuellement plus lisses et un temps d'entraînement réduit.
* **Analyse Architecturale :** Les deux variables influençant le plus fortement les charges de chauffage et de refroidissement sont la hauteur globale (`Overall_Height`) et la surface du toit (`Roof_Area`). 


