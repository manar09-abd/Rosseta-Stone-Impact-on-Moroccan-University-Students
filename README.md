# 🌐 Impact de Rosetta Stone sur les étudiants marocains — Étude BI
 
> **Projet universitaire BI** · Licence Audit, Contrôle & Business Intelligence  
> Tafilalt Business School — Faculté Polydisciplinaire Errachidia · 2022–2023  
> Encadré par : **Mr. Farhaoui Youssef**
 
---
 
## 🎯 Objectif du projet
 
Analyser l'**adoption, la perception et l'impact** de la plateforme Rosetta Stone auprès des étudiants de trois universités marocaines, à travers un **pipeline ETL complet** (collecte → transformation → stockage → visualisation) et une approche analytique quantitative.
 
---
 
## 🏫 Périmètre de l'étude
 
| Université | Ville |
|---|---|
| Université Moulay Ismaïl | Meknès |
| Université Ibn Tofaïl | Kénitra |
| Université Sidi Mohamed Ben Abdellah | Fès |
 
**Taille de l'échantillon : 127 répondants**
 
---
 
## 📌 Résultats clés — Scores moyens (sur 5)
 
| Dimension mesurée | Score moyen |
|---|---|
| 🧠 Connaissance de la plateforme | **2,9 / 5** |
| 🤝 Soutien et ressources | **2,7 / 5** |
| 💻 Expérience d'utilisation | **2,4 / 5** |
| 📚 Impact sur l'apprentissage linguistique | **2,3 / 5** |
| 💡 Motivation et satisfaction | **2,2 / 5** |
| 🔄 Usage régulier | **2,1 / 5** |
 
### Points saillants
- 🏆 **Université Moulay Ismaïl** : niveaux de motivation et satisfaction les plus élevés, notamment chez les femmes
- 📈 **3ème année de licence** : meilleure expérience d'utilisation — représente **+50%** de l'échantillon
- ⚠️ **Gap important** entre connaissance de la plateforme (2,9) et usage régulier (2,1)
---
 
## ⚙️ Pipeline ETL — 6 étapes
 
```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│  ÉTAPE 1        │    │  ÉTAPE 2         │    │  ÉTAPE 3            │
│  Collecte       │───►│  Préparation     │───►│  Analyse            │
│                 │    │                  │    │  descriptive        │
│  Google Forms   │    │  • Suppression   │    │                     │
│  127 réponses   │    │    doublons      │    │  • Hypothèses H₀/H₁ │
│  Diffusion via  │    │  • Imputation    │    │  • Démographie      │
│  réseaux univ.  │    │    valeurs mq    │    │  • Statistiques     │
└─────────────────┘    │  • Standardisat. │    │    descriptives     │
                       └──────────────────┘    └─────────────────────┘
                                                         │
                                                         ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│  ÉTAPE 6        │    │  ÉTAPE 5         │    │  ÉTAPE 4            │
│  Visualisation  │◄───│  Stockage        │◄───│  Transformation     │
│                 │    │                  │    │                     │
│  • Sphinx       │    │  MySQL Workbench │    │  Talend             │
│  • Power BI     │    │  Base :          │    │  • tDBInput         │
│                 │    │  plateforme_edu  │    │  • tMap             │
│                 │    │  3 tables        │    │  • tDBOutput        │
└─────────────────┘    └──────────────────┘    └─────────────────────┘
```
 
---
 
## 🔬 Hypothèses testées (H₀ / H₁)
 
### Hypothèse 1 — Fréquence d'utilisation
- **H₀** : Il n'existe pas de différence significative dans la fréquence d'utilisation selon le genre ou l'âge
- **H₁** : Il existe une différence significative dans la fréquence d'utilisation selon le genre ou l'âge
### Hypothèse 2 — Motivation
- **H₀** : La motivation des étudiants n'est pas influencée par le soutien des enseignants et des pairs
- **H₁** : La motivation des étudiants est significativement influencée par le soutien des enseignants et des pairs
### Hypothèse 3 — Compétences linguistiques
- **H₀** : Rosetta Stone n'améliore pas significativement les compétences linguistiques
- **H₁** : Rosetta Stone améliore significativement les compétences linguistiques des étudiants
---
 
## 🗄️ Modèle de base de données (MySQL)
 
```sql
-- Base de données : plateforme_education
 
-- Table principale
CREATE TABLE utilisation_plateforme (
    ID_Utilisation    INT PRIMARY KEY,
    ID_Etudiant       INT,
    ID_Universite     INT,
    Connaissance_plateforme   INT,   -- score /5
    Experience_utilisation    INT,   -- score /5
    Impact_apprentissage      INT,   -- score /5
    Motivation_satisfaction   INT,   -- score /5
    Usage_regulier            INT,   -- score /5
    Soutien_ressources        INT,   -- score /5
    Recommandation            INT,
    Acceptation_reelle        INT
);
 
-- Table dimension étudiant
CREATE TABLE dimension_etudiant (
    ID_Etudiant       INT PRIMARY KEY,
    Sexe              ENUM('femme', 'homme'),
    Tranche_age       VARCHAR(20),   -- '18-22 ans' / '23-27 ans'
    Niveau_etudes     VARCHAR(50),
    ID_Universite     INT
);
 
-- Table dimension université
CREATE TABLE dimension_universite (
    ID_Universite     INT PRIMARY KEY,
    Nom_Universite    VARCHAR(100)
);
```
 
---
 
## 📊 Visualisations produites
 
### Avec Sphinx (analyse statistique)
- Distribution par genre (65,3% femmes / 34,7% hommes)
- Répartition par tranche d'âge (majorité 18-22 ans : 83,7%)
- Répartition par niveau d'études (3ème année licence : 81,2%)
- Scores moyens avec écarts-types pour chaque dimension
### Avec Power BI (dashboards interactifs)
- Motivation et satisfaction par université, sexe et niveau d'études
- Expérience d'utilisation par université et niveau d'études
- Corrélation connaissance × expérience × impact apprentissage
- Recommandation par soutien et ressources selon l'université
---
 
## 🎯 Recommandations produites
 
1. **Renforcer l'onboarding** — combler le gap entre connaissance (2,9) et usage réel (2,1)
2. **Soutien interuniversitaire** — homogénéiser les résultats entre établissements
3. **Cibler les 1ère et 2ème années** — profils les moins engagés avec accompagnement dédié
4. **Gérer les attentes des utilisateurs avancés** — un niveau de connaissance élevé peut générer une déception si la plateforme ne répond pas aux besoins avancés
---
 
## 🛠️ Stack technique
 
| Outil | Usage |
|---|---|
| **Google Forms** | Collecte du questionnaire (127 réponses) |
| **Excel** | Préparation et nettoyage des données |
| **Talend** | Pipeline ETL (tDBInput · tMap · tDBOutput) |
| **MySQL Workbench** | Stockage et requêtage des données |
| **Sphinx** | Analyse statistique descriptive |
| **Power BI** | Dashboards interactifs et visualisations |
 
---
 
## 👥 Équipe
 
| Nom | Rôle |
|---|---|
| **Manar Abdellaoui** | Pipeline ETL · MySQL · Power BI · Analyse |
| **Noura Youssfi** | Collecte · Préparation · Sphinx · Analyse |
| **Bouchrae Benchaibi** | Collecte · Interprétation · Recommandations |
 
> Encadré par **Mr. Farhaoui Youssef** — Tafilalt Business School, FP Errachidia
 
---
 
## 📁 Structure du repo
 
```
RosettaStone-Impact-Study-BI/
│
├── README.md
├── report/
│   └── Rosetta_Impact_Rapport.pdf
├── etl/
│   ├── talend_pipeline.png
│   └── mysql_schema.png
├── visualizations/
│   ├── sphinx_page1.png
│   ├── sphinx_page2.png
│   └── powerbi_dashboard.png
└── data/
    └── questionnaire_anonymized.csv
```
 
---
 
## 🔗 Liens utiles
 
- 🌐 [LinkedIn — Manar Abdellaoui](https://www.linkedin.com/in/manarabdellaoui)
- 💻 [GitHub — manar09-abd](https://github.com/manar09-abd)
---
 
*Licence Audit, Contrôle & Business Intelligence · Tafilalt Business School · FP Errachidia · 2022–2023*
