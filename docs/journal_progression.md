# HealthPulse AI 360 — Journal de progression

**Projet :** Public Health, Prevention & Territorial Intelligence  
**Durée prévisionnelle :** 60 jours  
**Stack :** Python, Pandas, SQL, Plotly, GeoPandas, Power BI, Streamlit, Machine Learning  
**Objectif :** Développer une plateforme reproductible d'analyse des inégalités territoriales de santé, avec un premier axe consacré au diabète.

---

## 1. Suivi global

| Jour | Travaux | Statut |
|---|---|---|
| J1 | Environnement Python et bases Pandas | Terminé |
| J2 | Découverte API CNAM et import des données | Terminé |
| J3 | Extraction diabète 2024 et contrôles qualité | Terminé |
| J4 | Référentiel géographique et jointure CNAM–COG | Terminé |
| J5 | Population INSEE, indicateurs d'âge, jointure et Plotly | Terminé |
| J6 | Analyse statistique exploratoire | Terminé |

---

## 2. Progression quotidienne

### J1 — Prise en main Python et Pandas

**Travaux :** Création d'un DataFrame fictif sur le diabète, calculs statistiques, filtrage, tri et recherche des valeurs manquantes.

**Résultats vérifiés :** Évaluation finale de consolidation Pandas : 20/20.

**Difficulté :** Compréhension de la différence entre Series et DataFrame, notamment pour le tri.

**Compétences :** `head()`, `mean()`, `sum()`, `sort_values()`, filtres booléens et `isna()`.

**Preuve :** `notebooks/J01_environnement_python.ipynb`

### J2 — Découverte des données sanitaires CNAM

**Travaux :** Initiation à l'API Data ameli, exploration des réponses JSON et conversion en DataFrame Pandas.

**Résultat :** Premières requêtes et exploration des variables du jeu de données `effectifs`.

**À vérifier :** Exhaustivité et validation des données récupérées au J2.

**Compétences travaillées :** Requests, API REST, JSON, Pandas.

**Preuve :** `notebooks/J02_acquisition_diabete.ipynb`

### J3 — Extraction et préparation des données sur le diabète

**Travaux :** Filtrage sur le diabète et l'année 2024, export CSV et identification des totaux géographiques.

**Difficultés rencontrées :**
- Comparaison incompatible entre une date et un entier.
- Limitation du nombre d'observations par requête.
- Identification des codes de total `dept = 999` et `region = 99`.

**Solutions étudiées :** `year(annee)`, export CSV filtré, filtres booléens.

**À vérifier :** Contrôles qualité finaux et sélection de la granularité départementale globale.

**Preuve :** `notebooks/J03_diabete_2024_qualite.ipynb`

### J4 — Référentiel géographique des départements

**Travaux prévus :** Intégration du COG 2024, harmonisation des identifiants et jointure CNAM–INSEE.

**Compétences travaillées :** `rename()`, `merge()`, contrôle des clés et des correspondances.

**À confirmer :** Nombre de correspondances, absence de doublons et fichier final validé.

**Preuve attendue :** `notebooks/J04_referentiel_departements.ipynb`

### J5 — Enrichissement démographique et visualisation

**Travaux :**
- Exploration du classeur INSEE contenant un onglet par année.
- Identification des données départementales de 2024.
- Repérage des classes d'âge et des catégories de sexe.
- Préparation des indicateurs de vieillissement.
- Préparation de la jointure entre les données CNAM et INSEE.
- Introduction de Plotly pour les graphiques interactifs.

**Résultat vérifié :** Structure du classeur INSEE identifiée.

**À valider :**
- Cohérence des calculs démographiques.
- Jointure CNAM–INSEE et couverture départementale.
- Unicité département–année.
- Visualisations Plotly effectivement réalisées.
- Export du CSV enrichi.

**Preuve :** `notebooks/J05_demographie_departements.ipynb`


### J6 — Analyse statistique exploratoire et visualisations interactives

**Travaux :**
- Exploration des données départementales CNAM–INSEE de 2024.
- Étude des distributions démographiques : part des 60 ans ou plus, des 75 ans ou plus et des femmes.
- Calcul des statistiques descriptives : moyenne, médiane, écart-type et quartiles.
- Introduction de la méthode IQR pour détecter les observations atypiques.
- Préparation d'histogrammes et de boxplots interactifs avec Plotly, ainsi que d'une analyse complémentaire avec Seaborn.
- Exploration facultative de l'indicateur de prévalence du diabète fourni par la CNAM.

**Résultat vérifié :**
- Aucun résultat chiffré du notebook J6 n'a encore été communiqué pour vérification.
- Médiane de la part des 60 ans ou plus : **30.94 %**.
- Écart interquartile (IQR) : **6.81**.
- Nombre de départements atypiques détectés : **2**.
- Graphiques effectivement réalisés : **2**.

**À valider :**
- Exhaustivité et unicité des observations départementales.
- Cohérence des types numériques et traitement des valeurs manquantes.
- Résultats des statistiques descriptives et pertinence des observations atypiques.
- Définition, unité et comparabilité de la prévalence CNAM.
- Reproductibilité du notebook et export effectif des graphiques interactifs.

**Preuve :**
- `notebooks/J06_analyse_exploratoire.ipynb`
- `outputs/figures/j06_histogramme_60_plus.html`
- `outputs/figures/j06_boxplot_60_plus.html`
- `outputs/figures/j06_statistiques_descriptives.csv`
- `outputs/figures/j06_observations_atypiques.csv`

*Les fichiers de preuve sont à confirmer selon les exports effectivement réalisés.*

**Statut :** À valider avant passage au J7.
