# AssurPrime – Crédit Agricole Assurances

Prédiction de la prime d’assurance incendie pour les exploitations agricoles.  
Projet réalisé dans le cadre du challenge **AssurPrime – Crédit Agricole Assurances** (2024–2025), à l’Université Gustave Eiffel (M2 Proba Stat des Nouvelles Données).

---

##  Objectif
Développer un pipeline de modélisation pour prédire la **prime d’assurance** basée sur :
- La **fréquence** des sinistres (`FREQ`)
- Le **coût moyen** (`CM`)
- La **charge estimée** (`CHARGE_PRED` = FREQ × CM × Année d’assurance)

---

##  Méthodologie complète

###  Nettoyage & préparation des données
- Remplissage intelligent des valeurs manquantes avec un modèle supervisé (`XGBoostClassifier`) :
  - Conversion des colonnes numériques en classes discrètes pour permettre l’utilisation d’un classifieur.
  - Gestion du **fort déséquilibre** (classes contenant jusqu’à 90% de zéros) par :
    - **Sous-échantillonnage** de la classe majoritaire.
    - **Pondération** pendant l’entraînement (`sample_weight`).
  - Injection des valeurs prédites pour remplacer les `NaN` de façon robuste.

- Traitement des variables catégorielles et numériques :
  - Encodage automatique (`enable_categorical=True`)
  - Standardisation avant clustering

---

###  Modélisation
- **Régression de Poisson** sur la fréquence (`FREQ_PRED`)
- **Régression Tweedie** sur le coût moyen (`CM_PRED`)
- **Calcul de la charge estimée** pour chaque client
- **Clustering KMeans** sur la charge (`CHARGE_PRED`) pour créer des segments clients :
  - Très faible, Faible, Moyenne, Forte charge
  - Visualisation en 3D avec `plotly` : FREQ, CM, Année_Assurance

---

##  Analyse et visualisation
- Utilisation de **matplotlib**, **seaborn**, **plotly** pour l’exploration graphique.
- Cartographie interactive des clients par charge estimée.
- Segmentation des clients pour une politique de tarification adaptée.
- Visualisation dans Power BI (non présent dans le repo, à usage interne).

---

##  Contenu du repo
- `notebook.ipynb` : Notebook principal contenant l’ensemble des traitements
- `soumission_clients.csv` : Fichier de soumission au challenge (ID, prédictions, cluster)
- `README.md` : Documentation du projet

---

##  Stack technologique
- Python : `pandas`, `xgboost`, `scikit-learn`, `seaborn`, `matplotlib`, `plotly`
- Google Colab pour développement
- GitHub pour versioning

---

##  Réalisé par
**ABDELLI KHALID**  
Université Gustave Eiffel – Master 2 Proba Stat des Nouvelles Données  
Année universitaire **2024 – 2025**
