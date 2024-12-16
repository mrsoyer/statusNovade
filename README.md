# Rapport de Suivi du Projet Novade

*Mise à jour du 16 décembre 2024*

---

## Introduction

Ce rapport présente l'état actuel du projet Novade, qui vise à migrer notre infrastructure technique vers une nouvelle architecture. L'objectif principal est de centraliser et de traiter les données provenant de diverses sources telles que Salesforce, Drift, et le plan de tracking, afin d'améliorer le stockage et l'analyse des données dans un environnement Databricks/Azure/Amplitude.

![Plan Novade](https://i.ibb.co/TYYdjMp/Capture-d-e-cran-2024-12-16-a-13-21-23.png)

### Points Clés et KPIs

- **Durée du Projet** : À ce jour, 16 jours de travail ont été consacrés sur les 24 jours prévus, soit 80% du temps alloué.
- **Progrès Réalisés** : La majorité des scripts de migration et d'intégration sont en place, avec des tests en cours pour assurer la stabilité et la performance.
- **Défis Majeurs** : Adaptation des workflows Databricks pour des automatisations complexes, et gestion des autorisations avec Amplitude, Azure, et Salesforce.
- **Solutions Envisagées** : Migration vers des solutions plus flexibles comme Azure Blob Storage et Synapse Analytics pour une meilleure gestion des données.

Ce document est conçu pour fournir une vue d'ensemble claire et accessible des progrès réalisés, des défis rencontrés et des solutions envisagées. Nous restons engagés à travailler en étroite collaboration avec toutes les parties prenantes pour assurer le succès de cette migration.

---

## 📊 Présentation du Projet

Le projet Novade consiste en la migration d'une solution éprouvée (n8n/Segment/BigQuery) vers une nouvelle architecture (Databricks/Azure/Amplitude). Cette transition a pour but de centraliser et de traiter les données provenant de diverses sources (Salesforce, Drift, plan de tracking) afin d'améliorer le stockage et l'analyse des données.

### Objectifs Principaux
- **Migration complète de l'infrastructure**
- **Centralisation des données dans Databricks**
- **Mise en place des automatisations**
- **Maintien de la continuité de service**
- **Optimisation des performances**

---

## 📅 Historique du Projet

### Timeline des Réunions et Progrès

#### Sprint 1 : Weekly - 12 Novembre
- **Travail réalisé** : Préparation des premiers scripts sur Databricks.
- **Problèmes rencontrés** :
  - Problème de création de destination Amplitude.
  - Problème d'autorisation sur GitHub.
- **Solutions trouvées** : Aucune solution définitive à ce stade.
- **Temps de travail** : 3 jours.

#### Sprint 2 : Weekly - 18 Novembre
- **Travail réalisé** : Mise en place du connecteur Amplitude vers Databricks et tests.
- **Problèmes rencontrés** :
  - Coût pour environ 1000 données : 400 €.
  - Problème d'autorisation Salesforce pour la création d'applications.
- **Solutions trouvées** : Aucune solution définitive à ce stade.
- **Temps de travail** : 3 jours.

#### Sprint 3 : Weekly - 26 Novembre
- **Travail réalisé** : Script de migration Salesforce, création et tests.
- **Problèmes rencontrés** :
  - Données antérieures à 1 mois ne s'importent pas dans Databricks.
  - Les données ne sont pas envoyées correctement.
- **Solutions trouvées** : Mise en place d'une double importation pour garantir que toutes les données nécessaires soient transférées.
- **Coût** : Environ 50 € pour 200 événements envoyés.
- **Temps de travail** : 3 jours.

#### Sprint 4 et 5 : Weekly - 10 Décembre
- **Travail réalisé** : Création d'un environnement local, déploiement sur Databricks ou Azure lorsque l'accès aux logs sera disponible. Création de compatibilité des scripts pour un double environnement.
- **Problèmes rencontrés** :
  - Architecture lourde due au triple environnement.
  - Rendre les scripts compatibles pour Azure/local et Databricks/local.
- **Solutions trouvées** : Création d'un environnement local pour effectuer les tests.
- **Temps de travail** : 7 jours.

#### Sprint 6 : Weekly - 17 Décembre
- **Travail réalisé** : Ajustements pour rendre compatibles les librairies Spark et Salesforce.
- **Problèmes rencontrés** :
  - Clusters Databricks instables, redémarrages fréquents.
- **Solutions trouvées** : Recherche d'une solution pour un cluster stable.
- **Temps de travail** : 3 jours.

---

## 🚨 Problèmes Majeurs Identifiés

1. **Problèmes d'Autorisation** : Accès limité aux ressources nécessaires sur Amplitude, Azure et Salesforce.
2. **Environnement de Développement** : Incompatibilités entre les environnements locaux et Databricks, entraînant des instabilités.
3. **Gestion des Données** : Difficultés dans la validation et l'intégration des données provenant de différentes sources.
4. **Limitations des Workflows Databricks** : Les workflows de Databricks, principalement conçus pour l'analyse de données et de petites automatisations périodiques, ne répondent pas efficacement aux exigences de notre projet de grande envergure qui nécessite des automatisations complexes et continues.

---

## 💡 Solutions Identifiées

Les solutions d'automatisation de Databricks qui m'ont été imposées sont beaucoup trop coûteuses et contraignantes. Databricks est principalement dédié à la création de notebooks pour l'analyse de données ou de petites automatisations. La création de connecteurs alourdit également le projet.

### Solution Proposée

Amplitude vient de créer une nouvelle destination de données Azure Blob Storage native. Voici comment nous pouvons procéder :

1. **Amplitude → Azure Blob Storage** : 
   - Exportez les données depuis Amplitude (événements, utilisateurs fusionnés) directement dans Azure Blob Storage grâce à l'intégration native. Les fichiers sont généralement en format JSON, CSV ou Parquet.

2. **Azure Blob Storage → Azure Synapse Analytics** : 
   - Chargez les données dans Synapse via :
     - **PolyBase** : Requêtes directes sur les fichiers Blob sans duplication.
     - **COPY INTO** : Importation des fichiers dans des tables internes pour des analyses plus rapides.
   - **Automatisation** : Utilisez Synapse Pipelines pour planifier et orchestrer les flux de données entre Blob Storage et Synapse.

### Choix de l'Automatisation

Pour l'automatisation, il faudra choisir entre deux options :

- **n8n** : Si vous optez pour n8n, cela permettra une intégration facile grâce à des scripts déjà réalisés. n8n est idéal pour des workflows visuels et des automatisations simples.
  
- **Python hébergé sur Azure Functions** : Cette option offre plus de flexibilité et de contrôle sur le traitement des données, mais nécessite une gestion plus technique. Cela peut être plus adapté si des traitements complexes sont nécessaires.

### Estimation du Temps

| Étape                                   | Durée estimée |
|-----------------------------------------|---------------|
| Exportation Amplitude → Blob Storage    | 3 heures      |
| Chargement Blob Storage → Synapse       | 4 heures      |
| Automatisation avec Synapse Pipelines    | 5 heures      |
| Vérifications et documentation          | 5 heures      |
| **Total estimé**                       | **17 heures** |

### Avantages

- **Workflow sur n8n** installé sur Azure : Adaptation facile grâce à des scripts déjà réalisés.
- **Python hébergé sur Azure Functions** : Flexibilité pour des traitements plus complexes.
- **Point d'alerte** : Afin de faciliter cette intégration, j'aurais besoin que tous les accès soient débloqués.

Cette solution peut être rapidement mise en place, sera beaucoup plus facile à maintenir et sera beaucoup moins coûteuse.

---

## ⚠️ Points de Vigilance

- **Suivi des Autorisations** : Continuer à surveiller l'accès aux ressources critiques pour éviter des blocages futurs.
- **Stabilité des Environnements** : Assurer que les environnements de développement et de production restent synchronisés et stables.
- **Documentation** : Maintenir une documentation à jour pour faciliter la communication entre les équipes et garantir la continuité des opérations.

---

Ce rapport vise à fournir une vue d'ensemble claire et concise de l'état du projet Novade, en mettant l'accent sur les défis et les solutions. Nous restons engagés à travailler en étroite collaboration avec toutes les parties prenantes pour assurer le succès de cette migration.
