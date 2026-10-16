# Licenciements dans la tech et l'IA (2020–2026) — Tableau de bord Power BI

## 🇫🇷 Français

### Présentation

Ce projet transforme un jeu de données public d'événements de licenciement dans la tech et l'IA en un tableau de bord Power BI interactif de quatre pages. Il suit une démarche de Business Intelligence complète : import et nettoyage avec Power Query, modèle de données en étoile, mesures DAX, restitution adaptée à deux publics (lecture exécutive et lecture analytique) et documentation explicite des limites.

Le jeu de données couvre 1 850 événements pour 74 entreprises et 18 pays. Le projet est **descriptif** : il ne produit ni prédiction ni modèle de Machine Learning.

Le rapport détaillé est disponible dans [rapport_final.md](./rapport_final.md).

### Contexte et problématique

Les annonces de licenciement dans la tech sont souvent commentées à partir de chiffres isolés. Le projet examine la question suivante :

> Comment structurer un pipeline Power Query et un modèle de données en étoile pour explorer l'évolution des licenciements dans la tech (temps, géographie, secteurs, entreprises liées à l'IA) et en restituer une lecture claire et honnête sur ses limites ?

### Données

Source : [Global AI & Tech Layoffs Dataset (2020–2026)](https://www.kaggle.com/datasets/prajitdatta/global-ai-and-tech-layoffs-dataset-20202026), publié sur Kaggle par prajitdatta. Les conditions d'utilisation et la licence sont indiquées sur la page du jeu de données. Le fichier brut n'est pas redistribué dans ce dépôt (voir [data/README_donnees.md](./data/README_donnees.md)).

| Colonne | Description |
|---|---|
| `event_id` | Identifiant de l'événement |
| `company` | Entreprise |
| `industry` | Secteur d'activité (libellé parfois composé, par exemple « Fintech / AI ») |
| `hq_country`, `hq_city`, `continent` | Localisation du siège |
| `date_announced` | Date d'annonce |
| `founded_year` | Année de création de l'entreprise |
| `company_size_est` | Taille estimée de l'entreprise |
| `company_status` | Statut de l'entreprise |

L'unité d'analyse est **l'événement de licenciement** : le fichier ne contient pas le nombre de personnes concernées.

### Méthodologie

1. **Import** du CSV dans Power BI Desktop.
2. **Nettoyage dans Power Query** : promotion des en-têtes, typage des colonnes, suppression des doublons sur `event_id`, remplacement des valeurs vides par « Inconnu », suppression des espaces superflus, création de `Age_Entreprise` (année de l'événement moins année de création).

### Mesures DAX principales

| Mesure | Rôle |
|---|---|
| `Total_Evenements` | Nombre d'événements distincts |
| `Nb_Entreprises`, `Nb_Pays` | Nombre d'entreprises et de pays distincts |
| `Part_IA` | Part des événements dans des secteurs dont le libellé contient « AI » ou « Artificial » |
| `Age_Moyen` | Âge moyen des entreprises au moment de l'événement |

### Résultats

Valeurs lues dans le tableau de bord (sélection complète) :

| Indicateur | Valeur |
|---|---|
| Événements | 1 850 |
| Entreprises / pays | 74 / 18 |
| Part des événements dans des secteurs liés à l'IA | 19 % |
| Secteur principal le plus fréquent | E-Commerce (176 événements) |
| Pays le plus fréquent | États-Unis (1 012 événements, soit environ 55 % du total) |
| Âge moyen des entreprises à l'événement | 19,7 ans (secteurs liés à l'IA) contre 29,2 ans (autres secteurs) |

### Visualisations

**Vue exécutive**

![Vue exécutive](./outputs/figures/01_vue_executive.png)

**Analyse géographique**

![Analyse géographique](./outputs/figures/02_analyse_geographique.png)

**IA et reste du marché**


### Structure du projet

```text
Projet4_Dashboard_PowerBI_Tech_AI_Layoffs/
├── data/
│   ├── README_donnees.csv                  # jeu de données brut (à télécharger sur Kaggle)
│   └── README_donnees.md                   # source, licence, emplacement du CSV
├── powerbi/
│   └── tech_ai_layoffs_dashboard.pbix     # fichier Power BI Desktop
├── outputs/
│   ├── figures/
│   │   ├── 01_vue_executive.png
│   │   ├── 02_analyse_geographique.png
│   │   ├── 03_ia_et_reste_du_marche.png
│   │   ├── 04_modele_en_etoile.png
│   │   ├── 05_power_query_etapes.png
│   │   └── 06_page_methodologie.png
│   └── rapport/
│       └── tech_ai_layoffs_dashboard.pdf  # export PDF du tableau de bord
├── rapport_final.md
├── README.md
└── requirements_or_info.txt               # prérequis et ouverture du fichier
```

### Ouvrir le projet

Prérequis : Power BI Desktop (gratuit, Windows).

### Compétences démontrées

| Compétence | Mise en œuvre dans le projet |
|---|---|
| Import et nettoyage (ETL) | Power Query : types, doublons, valeurs vides, colonne calculée |
| Modélisation dimensionnelle | Schéma en étoile, relations un-à-plusieurs, table de dates |
| DAX | Mesures de comptage distinct, part, moyennes, classement avec `TOPN` |
| Conception de rapports | Deux publics (exécutif, analytique), navigation, segments |
| Esprit critique sur les données | Limites documentées : échantillon, régularité, concentration géographique |
| Formation associée | Parcours Microsoft Learn Power BI : modules « Explore the analytics process », « Importez des données dans Power BI », « Configurer un modèle sémantique », « Scope report design requirements » |

### Lien avec la Data Science et l'IA

Ce projet relève de la Business Intelligence, pas du Machine Learning. Il illustre la phase qui précède et accompagne la modélisation : préparer des données propres, les structurer dans un modèle fiable et en produire une lecture vérifiable. L'indicateur `Est_IA` est une règle lexicale appliquée au libellé du secteur ; il sert à comparer deux groupes, pas à classer les entreprises de façon exacte. Un prolongement naturel serait une analyse temporelle en Python sur les mêmes données.

### Limites et usage responsable

- **Échantillon restreint** : 74 entreprises, ce qui ne représente pas l'ensemble du marché technologique mondial.
- **Régularité inhabituelle** : 1 850 événements pour 74 entreprises représentent en moyenne 25 événements par entreprise, un chiffre très régulier pour des licenciements réels. La constitution du jeu de données n'est pas vérifiée ici : les résultats sont descriptifs.
- **Concentration géographique** : environ 55 % des événements concernent les États-Unis et aucun pays d'Afrique n'est présent.
- **Unité d'analyse** : le fichier compte des événements, pas des personnes licenciées.
- **Année 2026 incomplète** : la baisse apparente en 2026 ne reflète pas une tendance.

---

## 🇬🇧 English

### Overview

This project turns a public dataset of tech and AI layoff events into a four-page interactive Power BI dashboard. It follows a complete Business Intelligence workflow: import and cleaning with Power Query, a star-schema data model, DAX measures, reports designed for two audiences (executive and analytical), and explicit documentation of the dataset's limits.

The dataset contains 1,850 events across 74 companies and 18 countries. The project is **descriptive**: it produces no prediction and no Machine Learning model. Read the detailed report in [rapport_final.md](./rapport_final.md).

### Data and method

Source: the Kaggle dataset *Global AI & Tech Layoffs Dataset (2020–2026)* by prajitdatta; usage terms are listed on its Kaggle page and the raw file is not redistributed here. The unit of analysis is the layoff **event**; the file does not include the number of people affected.

Cleaning in Power Query covers header promotion, typing, duplicate removal on `event_id`, replacement of empty values, trimming and a calculated `Age_Entreprise` column. The model is a star schema: one fact table (`Faits_Licenciements`) and three dimensions (`Dim_Pays`, `Dim_Secteur`, `Dim_Date`) linked by one-to-many relationships with single-direction filtering. DAX measures cover event counts, distinct companies and countries, the share of AI-related sectors, average age and size, and top sector and country.

### Recorded results

On the full selection: 1,850 events, 74 companies, 18 countries; 19% of events fall in AI-related sectors; the most frequent main sector is E-Commerce (176 events); the United States accounts for 1,012 events (about 55%). Companies in AI-related sectors are on average younger at the time of the event (19.7 years against 29.2). Event volume is lowest in 2021, peaks in 2023 and declines until 2025; 2026 is incomplete.

### Limitations

The sample is limited to 74 companies. The dataset averages exactly 25 events per company, an unusually regular figure for real layoffs, and its construction is not verified here, so results are descriptive. About 55% of events concern the United States and no African country is represented. The `Est_IA` flag is a lexical rule on the sector label. Comparisons do not establish causality between AI and employment.

### Open the project

Install Power BI Desktop (free, Windows), download the Kaggle file and save it as `tech_market_raw.csv`, open `powerbi/tech_ai_layoffs_dashboard.pbix`, update the source path in **Transform data → Faits_Licenciements → Source** if needed, then refresh.

### Author

**Kawtar Boughal** — [LinkedIn](https://www.linkedin.com/in/kawtar-boughal02) · [GitHub](https://github.com/kawtarboughal02)
- **Indicateur `Est_IA` heuristique** : un secteur peut être mal classé selon son libellé.
- **Taille estimée** : `company_size_est` est une estimation dont l'unité n'est pas documentée dans le fichier.
- **Aucune causalité** : les comparaisons ne permettent pas de conclure sur l'effet de l'IA sur l'emploi.
- **Diffusion** : le tableau de bord est fourni en fichier Power BI Desktop et en PDF ; il n'est pas publié en ligne.

### Auteure

**Kawtar Boughal** — [LinkedIn](https://www.linkedin.com/in/kawtar-boughal02) · [GitHub](https://github.com/kawtarboughal02)

1. Télécharger le jeu de données depuis Kaggle (voir `data/README_donnees.md`) et l'enregistrer sous le nom `tech_market_raw.csv`.
2. Ouvrir `powerbi/tech_ai_layoffs_dashboard.pbix`.
3. Si Power BI signale une source introuvable : **Accueil → Transformer les données**, sélectionner `Faits_Licenciements`, ouvrir l'étape **Source** et indiquer le chemin du CSV.
4. **Accueil → Actualiser**.
![IA et reste du marché](./outputs/figures/03_ia_et_reste_du_marche.png)

Le tableau de bord complet est également disponible au format PDF : [outputs/rapport/tech_ai_layoffs_dashboard.pdf](./outputs/rapport/tech_ai_layoffs_dashboard.pdf).

### Pages du tableau de bord

- **Vue exécutive** : six indicateurs clés (événements, entreprises, pays, part IA, secteur et pays dominants), classement des secteurs, évolution annuelle, segments année et continent.
- **Analyse géographique** : classement des pays, relation entre nombre d'entreprises et nombre d'événements par pays, segment par secteur.
- **IA et reste du marché** : évolution annuelle comparée, âge moyen et taille moyenne selon l'appartenance à un secteur lié à l'IA.
- **Méthodologie** : source, nettoyage, modélisation et limites.
| Taille estimée moyenne | environ 59 000 (secteurs liés à l'IA) contre environ 81 000 (autres secteurs) |

Lecture descriptive : le volume d'événements est faible en 2021, atteint son maximum en 2023 (plus de 400 événements) puis diminue jusqu'en 2025 ; 2026 est une année incomplète. Les secteurs liés à l'IA concentrent une part minoritaire des événements, avec des entreprises en moyenne plus jeunes.

Ces constats décrivent l'échantillon étudié. Ils n'établissent aucun lien de cause à effet entre l'IA et les licenciements.
| `Taille_Moyenne` | Taille estimée moyenne des entreprises |
| `Top_Secteur`, `Top_Pays` | Secteur et pays comptant le plus d'événements dans la sélection |
3. **Tables de dimension** créées par référence à la table de faits : `Dim_Pays` (pays et continent) et `Dim_Secteur` (secteur, indicateur `Est_IA`, `Secteur_Principal`).
4. **Table de dates** `Dim_Date` générée en DAX et marquée comme table de dates.
5. **Relations un-à-plusieurs** à filtre unique entre chaque dimension et la table de faits.
6. **Mesures DAX** : volumes, entreprises, pays, part des secteurs liés à l'IA, âge et taille moyens, secteur et pays dominants.
7. **Quatre pages** : vue exécutive, analyse géographique, comparaison IA et reste du marché, méthodologie.

### Modèle de données (schéma en étoile)

![Modèle en étoile](./outputs/figures/04_modele_en_etoile.png)

| Relation | Cardinalité | Filtre |
|---|---|---|
| `Dim_Pays[hq_country]` → `Faits_Licenciements[hq_country]` | Un à plusieurs | Unique |
| `Dim_Secteur[industry]` → `Faits_Licenciements[industry]` | Un à plusieurs | Unique |
| `Dim_Date[Date]` → `Faits_Licenciements[date_announced]` | Un à plusieurs | Unique |

Étapes de nettoyage appliquées à la table de faits :

![Étapes Power Query](./outputs/figures/05_power_query_etapes.png)
