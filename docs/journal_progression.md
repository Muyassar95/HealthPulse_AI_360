# HealthPulse AI 360 — Journal de progression

**Projet :** Public Health, Prevention & Territorial Intelligence  
**Durée prévisionnelle :** 60 jours  
**Stack :** Python, Pandas, SQL, Plotly, GeoPandas, Power BI, Streamlit, Machine Learning  
**Objectif :** Développer une plateforme reproductible d'analyse des inégalités territoriales de santé, avec un premier axe consacré au diabète.

---

## 1. Suivi global

| Jour | Travaux | Statut |
|---|---|---|
| J1 | Environnement Python et bases Pandas | Terminé — exercices validés |
| J2 | Découverte API CNAM et import des données | À confirmer |
| J3 | Extraction diabète 2024 et contrôles qualité | À valider |
| J4 | Référentiel géographique et jointure CNAM–COG | À confirmer |
| J5 | Population INSEE, indicateurs d'âge, jointure et Plotly | En cours de validation |
| J6 | Analyse statistique exploratoire | À commencer |

**Légende :** Terminé / En cours / À vérifier / À commencer.

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


---

## 4. Bilan par jalon

### Bilan J1–J5

**Acquis confirmés :**
- Bases de manipulation et de filtrage avec Pandas.
- Première compréhension des requêtes API.
- Identification des dimensions sanitaires et géographiques.
- Découverte des données démographiques INSEE.

**Travaux à consolider :**
- Validation des jointures multi-sources.
- Contrôles de granularité.
- Automatisation des tests qualité.
- Visualisations interactives Plotly.

**Priorité suivante :** Finaliser les livrables du J5 avant de commencer les analyses statistiques du J6.

---

## 5. Compétences pour le portfolio

| Compétence | Preuve attendue |
|---|---|
| Acquisition de données sanitaires | Notebook API CNAM |
| Préparation et nettoyage | Contrôles J3 |
| Harmonisation géographique | Jointure J4 |
| Feature Engineering démographique | Indicateurs J5 |
| Data Visualization | Graphiques Plotly exportés |
| Documentation reproductible | Notebooks et journal de qualité |

**Règle :** Une compétence ne sera présentée comme réalisée dans le portfolio que lorsque son résultat et sa preuve auront été vérifiés.

---

## 6. Prochaine révision

**Jalon :** J10  
**À examiner :** Avancement des notebooks, qualité des données, difficultés récurrentes, autonomie Python et priorités pour J11–J15.
