# HealthPulse AI 360 : Cadrage du projet

**Nom complet :** HealthPulse AI 360 — Public Health, Prevention & Territorial Intelligence

**Domaine :** Data Science, Machine Learning, Deep Learning, santé publique et intelligence territoriale.

**Durée du MVP :** 60 jours — 2 heures par jour (environ 120 heures).

**Périmètre initial :** France métropolitaine, principalement à l'échelle départementale.

## 1. Présentation et objectifs

HealthPulse AI 360 est un projet professionnel de Data Science et d'intelligence artificielle consacré à l'analyse des indicateurs sanitaires et des inégalités territoriales de santé.

Il poursuit deux objectifs :

- **Court terme :** développer en 60 jours un MVP reproductible et démontrable sur GitHub, LinkedIn et lors d'entretiens Data Analyst / Data Scientist.
- **Long terme :** transformer le projet en plateforme B2B/B2G destinée aux collectivités, organismes de santé publique et cabinets d'études, avec une extension internationale.

Le projet doit évoluer progressivement sur plusieurs années, sans date de fin imposée.

## 2. Problématique du MVP

**Question centrale :**

Comment analyser les disparités territoriales du diabète en France et étudier leurs associations avec les caractéristiques sociodémographiques et l'accessibilité aux soins afin d'éclairer les besoins de prévention ?

Le MVP devra permettre de :

1. Cartographier les indicateurs territoriaux du diabète.
2. Étudier leurs évolutions temporelles.
3. Analyser leurs associations avec l'âge, les revenus, la pauvreté et l'accessibilité aux soins.
4. Développer et évaluer des modèles statistiques et prédictifs.
5. Identifier des territoires présentant des besoins potentiellement importants en prévention.
6. Présenter les résultats dans une plateforme interactive.

Les résultats seront exclusivement territoriaux et ne constitueront pas des diagnostics individuels.

## 3. Sources de données

**Sources prioritaires :**

- **Assurance Maladie — Data pathologies :** effectifs et indicateurs de prise en charge du diabète.
  https://data.ameli.fr
- **Santé publique France — Odissé :** indicateurs épidémiologiques et données de santé publique.
  https://odisse.santepubliquefrance.fr
- **INSEE :** population, âge, revenus, pauvreté, chômage et caractéristiques territoriales.
  https://www.insee.fr
- **DREES :** accessibilité potentielle localisée (APL) aux professionnels de santé.
  https://data.drees.solidarites-sante.gouv.fr

Les variables, millésimes, licences et niveaux géographiques seront vérifiés lors de l'acquisition.

**Échelle géographique retenue :** département, sous réserve de disponibilité des indicateurs sanitaires.

Aucune donnée communale ou IRIS sur le diabète ne sera inventée à partir de données départementales.

## 4. Indicateurs à construire

**Indicateurs sanitaires :**
- Effectifs de personnes prises en charge pour diabète.
- Prévalence du diabète pris en charge, si le dénominateur approprié est disponible.
- Évolution annuelle de la prévalence.
- Prévalence standardisée, si disponible.

**Indicateurs sociodémographiques :**
- Part des personnes de 65 ans et plus.
- Revenu médian.
- Taux de pauvreté.
- Taux de chômage.
- Densité de population.

**Indicateurs d'accessibilité :**
- Accessibilité aux médecins généralistes.
- Accessibilité aux infirmiers.
- Disparités territoriales d'accès aux soins.

Un indice exploratoire de besoins territoriaux de prévention pourra être construit avec des pondérations transparentes et des tests de sensibilité.

## 5. Technologies

**Python :** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost et PyTorch.

**SQL :** PostgreSQL, avec PostGIS si nécessaire.

**Business Intelligence :** Power BI.

**Application :** Streamlit.

**Développement :** Jupyter Notebook, Git et GitHub.

**Cartographie :** GeoPandas et éventuellement QGIS.

**Contraintes matérielles :**
- Windows.
- 16 Go de RAM.
- GPU AMD ou Intel.
- Modèles Machine Learning et Deep Learning exécutables sur CPU.
- Données filtrées et fichiers de taille raisonnable.

## 6. Architecture du projet

```text
HealthPulse_AI_360/
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│
├── notebooks/
│
├── src/
│   ├── collect_data.py
│   ├── clean_data.py
│   ├── build_indicators.py
│   ├── train_ml.py
│   └── train_pytorch.py
│
├── sql/
│
├── models/
│   ├── ml/
│   └── pytorch/
│
├── dashboards/
│
├── app/
│   └── streamlit_app.py
│
├── reports/
│
├── tests/
│
├── docs/
│   ├── cadrage_j0.md
│   ├── sources.csv
│   ├── methodology.md
│   └── ethics_and_limitations.md
│
├── README.md
├── requirements.txt
└── .gitignore
```

## 7. Machine Learning et Deep Learning

**Machine Learning :**
- Régression Ridge.
- Random Forest.
- XGBoost.
- Analyse des variables importantes.
- Comparaison avec un modèle de référence.

**Deep Learning :**
- PyTorch.
- Réseau neuronal dense simple.
- Entraînement sur CPU.
- Comparaison avec les modèles classiques.

**Évaluation :**
- MAE, RMSE et R² lorsque pertinents.
- Séparation entraînement/test adaptée aux territoires et aux périodes.
- Prévention des fuites de données.
- Analyse du surapprentissage.
- Documentation des limites et incertitudes.

Le Deep Learning sera expérimental si le volume de données ne permet pas une validation scientifique suffisante.

## 8. Calendrier des 60 jours

| Période | Travaux |
|---|---|
| J0 | Cadrage et architecture |
| J1–J7 | Environnement, sources et acquisition |
| J8–J14 | Nettoyage et analyse exploratoire |
| J15–J21 | PostgreSQL, SQL et statistiques |
| J22–J30 | Machine Learning |
| J31–J37 | Deep Learning avec PyTorch |
| J38–J45 | Dashboard Power BI |
| J46–J53 | Application Streamlit |
| J54–J60 | Documentation, tests et publication |

**Programme de la première semaine :**

- J1 : installation et configuration de Python/Jupyter.
- J2 : acquisition des données sur le diabète.
- J3 : acquisition des données INSEE.
- J4 : acquisition des données d'accessibilité aux soins.
- J5 : documentation des sources et variables.
- J6 : premiers contrôles de qualité.
- J7 : bilan de faisabilité et préparation du nettoyage.

Chaque journée comprendra un objectif, des tâches, des explications, des contrôles et un livrable.

## 9. Livrables attendus à J60

1. Dépôt GitHub professionnel.
2. Dataset territorial documenté.
3. Notebooks Python reproductibles.
4. Base PostgreSQL et scripts SQL.
5. Analyses statistiques et cartographiques.
6. Modèles Machine Learning évalués.
7. Prototype Deep Learning PyTorch.
8. Dashboard Power BI.
9. Application Streamlit.
10. README, méthodologie et présentation LinkedIn.

**Critères de réussite :** fiabilité des données, reproductibilité, validation statistique, interface fonctionnelle et documentation professionnelle.

## 10. Évolution internationale et commerciale

**Phase 1 — France :** MVP consacré au diabète et aux inégalités territoriales.

**Phase 2 — France :** extension à l'activité physique, la nutrition, le tabagisme, les addictions, le handicap et d'autres maladies chroniques.

**Phase 3 — Europe :** intégration progressive de données Eurostat et OMS, sous réserve de comparabilité.

**Phase 4 — International :** développement d'une plateforme SaaS B2B/B2G pour l'analyse territoriale et la prévention.

Des connexions pourront être établies avec FoodMarket AI et GeoMobility 360 AI lorsque les données seront compatibles.

## 11. Éthique et réglementation

- Utilisation prioritaire de données publiques agrégées.
- Respect du RGPD et des licences.
- Absence de diagnostic médical individuel.
- Distinction entre corrélation, prédiction et causalité.
- Documentation des biais et incertitudes.
- Prévention de la stigmatisation territoriale.
- Validation scientifique avant tout usage médical ou décisionnel sensible.

## 12. Conclusion du J0

HealthPulse AI 360 est défini comme un projet de Data Science appliquée à la santé publique, combinant statistiques, intelligence territoriale, Machine Learning, Deep Learning et visualisation interactive.

**Objectif final :** construire un MVP professionnel en 60 jours, puis le faire évoluer progressivement vers une solution internationale d'intelligence territoriale en santé publique.

**Prochaine étape : J1 — Configuration de l'environnement Python et Jupyter Notebook.**

Le passage à J1 nécessitera une validation explicite du J0.
