# Documentation des données — Licenciements dans la tech et l'IA (2020–2026)

## Source

Le jeu de données provient de Kaggle :

- **Titre :** Global AI & Tech Layoffs Dataset (2020–2026)
- **Auteur :** prajitdatta
- **URL :** https://www.kaggle.com/datasets/prajitdatta/global-ai-and-tech-layoffs-dataset-20202026
- **Licence :** consulter la page Kaggle pour les conditions d'utilisation et la licence applicables

## Fichier brut

Le fichier CSV brut n'est pas redistribué dans ce dépôt pour respecter les conditions de diffusion de la source.

**Nom attendu :** `tech_market_raw.csv`

**Emplacement :** le fichier doit être placé manuellement à la racine du projet ou référencé dans Power BI Desktop lors de l'ouverture du fichier `.pbix`.

## Contenu du jeu de données

| Nombre | Description |
|---|---|
| 1 850 | Événements de licenciement |
| 74 | Entreprises distinctes |
| 18 | Pays distincts |
| 2020–2026 | Période couverte par les dates d'annonce |

## Variables

| Colonne | Description | Type |
|---|---|---|
| `event_id` | Identifiant unique de l'événement | Texte |
| `company` | Nom de l'entreprise | Texte |
| `industry` | Secteur d'activité (libellé parfois composé, ex. « Fintech / AI ») | Texte |
| `hq_country` | Pays du siège social | Texte |
| `hq_city` | Ville du siège social | Texte |
| `continent` | Continent du siège social | Texte |
| `date_announced` | Date d'annonce du licenciement | Date |
| `founded_year` | Année de création de l'entreprise | Nombre entier |
| `company_size_est` | Taille estimée de l'entreprise (effectif) | Nombre entier |
| `company_status` | Statut juridique de l'entreprise (ex. Private, Public) | Texte |

## Unité d'analyse

Chaque ligne représente un **événement de licenciement**. Le fichier ne contient **pas** le nombre de personnes licenciées par événement. Toutes les analyses comptent des événements, non des salariés.

## Traitement appliqué dans ce projet

Les étapes de nettoyage et de modélisation sont décrites dans `rapport_final.md` et résumées dans `README.md` :

1. Import du CSV dans Power BI Desktop
2. Nettoyage dans Power Query (typage, doublons, valeurs vides, espaces, colonne `Age_Entreprise`)
3. Création des dimensions `Dim_Pays`, `Dim_Secteur` et `Dim_Date`
4. Modèle en étoile avec relations un-à-plusieurs
5. Mesures DAX pour les indicateurs clés

## Reproductibilité

Pour reconstruire le tableau de bord :

1. Télécharger le CSV depuis la page Kaggle indiquée ci-dessus
2. L'enregistrer sous le nom `tech_market_raw.csv`
3. Ouvrir `powerbi/tech_ai_layoffs_dashboard.pbix` dans Power BI Desktop
4. Si nécessaire, mettre à jour le chemin de la source dans **Accueil → Transformer les données → Faits_Licenciements → Source**
5. Cliquer sur **Accueil → Actualiser**