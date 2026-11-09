# HealthPulse AI 360 — Compte rendu J4

**Projet :** HealthPulse AI 360 — Public Health, Prevention & Territorial Intelligence  
**Jour :** J4 / 60  
**Date :** 09 novembre 2026
**Environnement :** Windows 11, Python 3.13, JupyterLab  
**Bibliothèques :** Pandas, pathlib, Plotly Express  
**Notebook :** `J04_referentiel_departements.ipynb`  
**Statut :** Validé

---

## 1. Objectifs atteints

### 1.1. Objectif principal

L'objectif du J4 est d'enrichir les données départementales relatives au diabète, préparées au J3, avec le référentiel géographique officiel de l'INSEE.

Ce travail vise à construire une base territoriale cohérente, reproductible et exploitable pour les futures analyses des inégalités de santé en France.

### 1.2. Objectifs opérationnels

Les travaux du J4 portent sur :

- L'acquisition du Code officiel géographique (COG) 2024.
- L'exploration des identifiants départementaux.
- L'harmonisation des codes géographiques entre la CNAM et l'INSEE.
- La réalisation d'une jointure avec Pandas.
- Le contrôle des correspondances et des doublons.
- La création d'une première visualisation interactive avec Plotly.
- L'export d'un jeu de données enrichi.

### 1.3. Résultat attendu

Le résultat final est un fichier contenant les indicateurs sanitaires du diabète en 2024, associés aux noms officiels et aux codes régionaux des départements français.


---

## 2. Sources et données utilisées

### 2.1. Source sanitaire — CNAM

**Organisme :** Caisse nationale de l'Assurance Maladie  
**Portail :** Data ameli  
**Jeu de données :** Effectifs par pathologie  
**Année étudiée :** 2024  
**Pathologie :** Diabète  
**Granularité cible :** Département

Source : https://data.ameli.fr/explore/dataset/effectifs/

Le fichier exploité provient des traitements du J3. Il contient des observations sanitaires agrégées, qui doivent être correctement filtrées selon les dimensions géographiques et démographiques.

### 2.2. Source géographique — INSEE

**Organisme :** Institut national de la statistique et des études économiques  
**Référentiel :** Code officiel géographique 2024  
**Fichier :** `v_departement_2024.csv`

Source : https://www.insee.fr/fr/information/7766585

Les principales variables du référentiel sont :

| Variable | Signification |
|---|---|
| `DEP` | Code officiel du département |
| `REG` | Code de la région |
| `LIBELLE` | Nom officiel du département |
| `CHEFLIEU` | Code de la commune chef-lieu |

### 2.3. Organisation des fichiers

Les données sont organisées selon trois niveaux :

- `data/raw/` : conservation des données originales.
- `data/interim/` : données préparées et harmonisées.
- `data/processed/` : données validées pour les analyses ultérieures.

Cette organisation permet de conserver la traçabilité des transformations.

---

## 3. Méthodologie d'extraction et de traitement

### 3.1. Importation des données

Les deux jeux de données ont été préparés pour être importés dans Pandas.

Le référentiel INSEE fournit les informations administratives, tandis que le fichier CNAM contient les indicateurs sanitaires issus du J3.

Les données brutes sont conservées sans modification afin de garantir leur reproductibilité.

### 3.2. Vérification de la granularité

Avant la jointure, il est nécessaire de vérifier qu'une observation du fichier sanitaire correspond à un département pour l'année 2024, après sélection du bon niveau de pathologie, du sexe global et de l'âge global.

Les observations correspondant aux totaux géographiques `dept = 999` et `region = 99`, identifiées lors du J3, doivent être exclues du périmètre départemental.

La clé métier attendue pour le fichier sanitaire est le couple :

**Code département + année**

### 3.3. Harmonisation des identifiants

Les codes géographiques sont initialement stockés dans des colonnes différentes :

- CNAM : `dept`
- INSEE : `DEP`

Ces variables sont harmonisées sous le nom `code_dept`.

Les identifiants sont conservés sous forme de chaînes de caractères afin de préserver les zéros initiaux et les codes alphanumériques.

Une attention particulière est portée aux départements corses (`2A`, `2B`) et aux départements d'outre-mer.

### 3.4. Réalisation de la jointure

La jointure est effectuée avec la méthode `merge()` de Pandas.

Le type **LEFT JOIN** est privilégié afin de conserver les observations sanitaires de la CNAM, y compris lorsqu'une correspondance géographique n'est pas trouvée dans le référentiel INSEE.

Le paramètre `indicator=True` permet d'identifier l'origine des correspondances.

Le paramètre `validate` permet de vérifier la cardinalité attendue et de prévenir une multiplication accidentelle des observations.

### 3.5. Construction de la base enrichie

La base résultante doit notamment contenir :

| Variable | Description |
|---|---|
| `code_dept` | Code départemental harmonisé |
| `nom_departement` | Libellé officiel du département |
| `code_region_insee` | Code région INSEE |
| `annee` | Année de référence |
| `effectif_num` | Effectif numérique des personnes prises en charge |
| Autres variables CNAM | Indicateurs conservés et documentés |

Les noms exacts des variables sanitaires sont à confirmer selon le fichier issu du J3.

---

## 4. Contrôles de qualité

### 4.1. Contrôles géographiques

L'objectif est de vérifier la correspondance entre les identifiants géographiques des deux sources.

| Contrôle | Résultat |
|---|---|
| Départements distincts INSEE | Oui |
| Départements distincts CNAM | Oui |
| Correspondances réussies | Oui |
| Codes CNAM sans correspondance | Non |
| Doublons sur la clé INSEE | Oui |
| Doublons département-année CNAM | Oui |
| Lignes avant jointure | Oui |
| Lignes après jointure | Oui |
| Cohérence des codes régionaux | Oui |

### 4.2. Contrôle des correspondances

Les observations sans correspondance doivent être examinées avant toute suppression.

Une différence peut notamment provenir :

- D'un format géographique différent.
- D'un zéro initial manquant.
- D'un niveau d'agrégation incorrect.
- D'une différence de couverture territoriale.
- D'une incompatibilité entre référentiels.

### 4.3. Contrôle de cardinalité

La jointure ne doit pas provoquer de duplication involontaire des observations sanitaires.

Le nombre de lignes avant et après jointure est comparé.

L'unicité département-année est également vérifiée après fusion.

### 4.4. Bilan qualité

**Résultats obtenus :** [Présenter les chiffres réels issus des contrôles.]

**Anomalies restantes :** [Indiquer les éventuelles correspondances ou incohérences non résolues.]

**Conclusion :** La base ne pourra être considérée comme validée que lorsque la couverture géographique, la granularité et la cohérence des jointures auront été vérifiées.

---

## 5. Résultats exploratoires

### 5.1. Première visualisation interactive

Le J4 introduit Plotly Express pour produire une représentation interactive des données départementales.

Le graphique prévu représente les dix départements présentant les plus grands effectifs de personnes prises en charge pour un diabète en 2024.

Les principales fonctionnalités utilisées sont :

- Le survol interactif des observations.
- L'affichage des noms des départements.
- L'affichage des effectifs et des codes géographiques.
- La personnalisation des couleurs.
- La possibilité de zoomer et d'exporter le graphique.

### 5.2. Résultats obtenus

**Graphique réalisé :** Oui

**Principales observations :** 187 060 patients diabétiques sont prises en charge dans le département du Nord.

**Départements représentés :** Nord, Bouches-du-Rhône, Seine-Saint-Denis, Pas-de-Calais, Rhône, Paris, Gironde, Seine-et-Marne, La Réunion et Val-d'Oise.

**Emplacement du graphique :** `outputs/figures/j04_top10_diabete.html`

### 5.3. Interprétation

Les effectifs absolus ne permettent pas de comparer directement les niveaux de risque sanitaire entre départements.

Les écarts observés peuvent notamment être liés à la taille des populations et à leur composition démographique.

Une analyse des inégalités territoriales nécessite donc des indicateurs comparables, notamment des prévalences dont le dénominateur est clairement identifié.

---

## 6. Difficultés rencontrées et solutions

### Difficulté 1 — Hétérogénéité des noms de colonnes

**Problème :** Les deux jeux de données utilisent des noms de variables différents pour identifier les départements.

**Solution :** Harmonisation des colonnes avec `rename()` afin de construire une clé commune appelée `code_dept`.

**Enseignement :** Deux sources ne peuvent pas être jointes correctement sans identifier des clés géographiques compatibles.

### Difficulté 2 — Format des identifiants départementaux

**Problème :** Certains codes contiennent des zéros initiaux ou des lettres.

**Solution :** Conservation des identifiants sous forme de chaînes de caractères, puis harmonisation des espaces et de la casse.

**Enseignement :** Un identifiant administratif ne doit pas être traité automatiquement comme une variable numérique.

### Difficulté 3 — Risque de jointure incorrecte

**Problème :** Une jointure peut produire des correspondances manquantes ou multiplier les lignes lorsque les clés ne sont pas uniques.

**Solution :** Utilisation des paramètres `validate` et `indicator`, accompagnée de contrôles avant et après fusion.

**Enseignement :** Une jointure réussie techniquement ne garantit pas la validité des données produites.

### Difficulté 4 — Nouvelle bibliothèque de visualisation

**Problème :** La création d'un graphique interactif nécessite de comprendre les paramètres de Plotly Express.

**Solution envisagée :** Décomposer la visualisation en trois opérations : préparer le DataFrame, construire le graphique et personnaliser son affichage.

**Enseignement :** La préparation et la fiabilité des données sont prioritaires sur l'esthétique du graphique.


---

## 7. Limites scientifiques

### 7.1. Définition des indicateurs sanitaires

Les données de l'Assurance Maladie concernent les personnes identifiées comme prises en charge selon les critères de la cartographie des pathologies.

Elles ne correspondent pas nécessairement à la totalité des personnes vivant avec un diabète en France.

### 7.2. Comparabilité entre territoires

Les effectifs départementaux sont influencés par les volumes de population.

Un département comptant davantage de personnes prises en charge ne possède pas nécessairement une prévalence plus élevée.

### 7.3. Structure par âge

Les différences de structure démographique peuvent influencer les indicateurs sanitaires.

Les futures analyses devront distinguer les prévalences brutes des prévalences standardisées, lorsque les données nécessaires seront disponibles.

### 7.4. Couverture territoriale

Les périmètres et les populations couverts par la CNAM et l'INSEE doivent être vérifiés avant toute comparaison.

La présence d'un département dans le COG ne garantit pas la disponibilité de tous les indicateurs sanitaires pour ce territoire.

### 7.5. Interprétation statistique

Les futures associations entre diabète, pauvreté, vieillissement ou accessibilité aux soins ne devront pas être interprétées directement comme des relations causales.

---

## 8. Compétences acquises

### 8.1. Python et Pandas

Les compétences travaillées au J4 sont :

- L'importation de fichiers CSV.
- La manipulation de chaînes de caractères.
- Le renommage de colonnes avec `rename()`.
- La sélection de variables.
- La comparaison d'ensembles avec `set()`.
- Les jointures avec `merge()`.
- Le contrôle des doublons avec `duplicated()`.
- La vérification des valeurs manquantes.
- L'exportation des données avec `to_csv()`.

### 8.2. Data Engineering

- Harmonisation des clés de jointure.
- Vérification de la granularité.
- Contrôle de cardinalité.
- Analyse des correspondances manquantes.
- Organisation des données brutes et transformées.
- Documentation des traitements.

### 8.3. Data Visualization

- Découverte de Plotly Express.
- Construction d'un graphique interactif.
- Utilisation des informations de survol.
- Personnalisation d'une visualisation.
- Export au format HTML.

---

## 9. Perspectives pour J5

Le J5 sera consacré à la préparation des données démographiques et à l'approfondissement de l'analyse territoriale du diabète.

### 9.1. Intégration démographique

Les prochaines étapes viseront à identifier les populations départementales, leurs millésimes et leurs structures par âge.

Ces informations permettront de mieux contextualiser les écarts sanitaires observés.

### 9.2. Préparation des indicateurs

Les indicateurs à approfondir comprennent notamment :

- Les effectifs de personnes prises en charge pour un diabète.
- Les prévalences fournies par la CNAM.
- La population départementale.
- Les répartitions par âge et sexe.
- Les futurs indicateurs socio-économiques.

Les données INSEE ne seront pas utilisées automatiquement comme dénominateur des indicateurs CNAM : la compatibilité des populations de référence devra être démontrée.

### 9.3. Cartographie interactive

Le projet évoluera progressivement vers des cartes choroplèthes avec Plotly et GeoPandas.

Les cartes devront présenter des indicateurs comparables et inclure les territoires ultramarins lorsque leur couverture sera disponible.

### 9.4. Perspective à long terme

Ces développements alimenteront la future plateforme HealthPulse AI 360 :

- Centralisation des données territoriales.
- Analyse des inégalités de santé.
- Exploration statistique et géospatiale.
- Machine Learning et modèles prédictifs exploratoires.
- Dashboards Power BI et Streamlit.
- Documentation et déploiement reproductible.

---

## Bilan personnel du J4

**Principal apprentissage :** La préparation des identifiants géographiques et la vérification des jointures constituent des étapes fondamentales pour construire une base territoriale fiable.

**Progression par rapport au J3 :** Le J3 portait principalement sur l'extraction et la fiabilisation des données sanitaires. Le J4 introduit l'intégration de plusieurs sources grâce à une clé géographique commune.

**Prochaine priorité :** Préparer les données démographiques nécessaires aux analyses territoriales.

