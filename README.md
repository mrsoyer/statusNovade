# Projet Novade - État et Analyse des Problèmes
*Mise à jour du 16 décembre 2024*

## Introduction

Le projet Novade représente une migration complexe d'infrastructure technique, passant d'une solution éprouvée (n8n/Segment/BigQuery) vers une nouvelle architecture (Databricks/Azure/Amplitude). Cette transition implique la centralisation et le traitement de données provenant de multiples sources (Salesforce, Drift, plan de tracking) avec un double objectif de stockage et d'analyse.

### Contexte Actuel
- **Progression** : 25% du projet réalisé
- **État** : Blocages techniques majeurs
- **Priorité** : Résolution urgente des problèmes d'autorisation

### Défis Principaux
1. Problèmes d'autorisation multiples (Databricks, Azure, Salesforce)
2. Incompatibilités environnement local/Databricks
3. Accès limité aux logs et monitoring
4. Complexité de la migration multi-plateformes

### Impact Business
- Retard sur le planning initial
- Risque sur la qualité des données
- Nécessité d'ajustements budgétaires
- Complexité technique sous-estimée

<style>
.section {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    margin: 10px 0;
    background-color: #fff;
}

.section summary {
    font-weight: bold;
    cursor: pointer;
    padding: 8px;
    background-color: #f8f9fa;
    border-radius: 6px;
}

.section summary:hover {
    background-color: #e9ecef;
}

.status-critical {
    color: #dc3545;
    font-weight: bold;
}

.status-warning {
    color: #ffc107;
    font-weight: bold;
}

.status-success {
    color: #28a745;
    font-weight: bold;
}
</style>

<div class="section">
<details>
<summary>📊 Présentation du Projet</summary>

### Contexte
Projet de migration et centralisation des données pour Novade, impliquant une transition complexe d'architecture technique.

### Ancienne Architecture
- **Stack Technique** : n8n, Segment, BigQuery, Salesforce
- **Fonctionnement** : Solution fonctionnelle et stable
- **Gestion des Données** : Centralisée et automatisée

### Nouvelle Architecture
- **Workflow** : Databricks
- **Base de Données** : Databricks
- **Webhooks** : Microsoft Azure
- **Dashboard & Centralisation** : Amplitude
- **Intégrations** : Multiples sources de données

### Sources de Données
- Plan de tracking
- Salesforce
- Drift
- Données historiques BigQuery

### Objectifs Principaux
1. Migration complète de l'infrastructure
2. Centralisation des données dans Databricks
3. Mise en place des automatisations
4. Maintien de la continuité de service
5. Optimisation des performances

### Défis Techniques
- Migration complexe multi-plateformes
- Gestion des autorisations multiples
- Compatibilité environnement local/cloud
- Stabilité de l'infrastructure
- Synchronisation temps réel

### Contraintes Spécifiques
- Exécution depuis la racine du projet
- Fichiers Python dans `local_workspace`
- Configuration via fichiers à la racine
- Logs en anglais, communication en français
</details>
</div>

<div class="section">
<details>
<summary>📊 Liste des Tâches</summary>

### 1. Webhook Amplitude → Databricks
- Création d'un script Azure Function pour capturer les événements Amplitude
- Configuration de l'appel API pour déclencher un script Python Notebook dans Databricks
- Implémentation de la validation des données avant stockage
- Test du webhook pour vérifier la réception des données Amplitude
- Gestion des erreurs via logs et alertes

### 2. Scripts Périodiques d'Organisation des Données
- Écriture des scripts Python pour organiser les données brutes en tables finales
- Planification des jobs périodiques dans Databricks
- Implémentation des tests de vérification d'intégrité des données
- Automatisation des alertes en cas de problèmes

### 3. Création des Tables pour Amplitude
- Identification des types de données à stocker dans les tables pour Amplitude
- Création des tables temporaires pour stocker les données brutes Amplitude
- Création des tables finales pour organiser les données
- Définition des schémas pour chaque table
- Mise en place des index et optimisation des performances
- Test d'insertion et d'organisation des données

### 4. Récupération des Événements Drift → Amplitude
- Écriture d'un script pour récupérer les événements Drift
- Planification du script sur Databricks pour exécution périodique
- Envoi des données Drift vers Amplitude
- Test de réception des données dans Amplitude et Databricks

### 5. Récupération des Données Salesforce → Amplitude
- Écriture d'un script pour récupérer les événements et utilisateurs de Salesforce
- Planification du script sur Databricks pour exécution périodique
- Envoi des données Salesforce vers Amplitude
- Test de réception des données dans Amplitude et Databricks

### 6. Migration des Scripts n8n → Databricks
- Réécriture de chaque script n8n en Python pour Databricks
- Test de chaque script Python sur Databricks
- Planification des scripts dans un scheduler
- Automatisation de la gestion des erreurs et alertes

### 7. Migration des Données BigQuery → Amplitude
- Export des données existantes depuis BigQuery
- Création d'un script pour envoyer les données vers Amplitude
- Configuration d'Amplitude pour rediriger les données vers Databricks
- Test de réception des données dans Amplitude et Databricks

### 8. Tracking en Double sur Amplitude
- Analyse des scripts de tracking actuels sur novade.com
- Duplication du tracking existant en double via Amplitude
- Test et validation du tracking en parallèle

### 9. Configuration et Test de l'Infrastructure
- Configuration des tests pour valider le bon fonctionnement des intégrations
- Validation des performances et de l'intégrité des données
- Réalisation des tests de charge pour l'infrastructure
- Mise en place des tableaux de bord de monitoring

### 10. Création de la Documentation
- Rédaction de la documentation technique complète
- Formation des équipes techniques de Novade

### 11. Gestion de Projet
- Planification
- Suivi
- Communication
- Clôture du projet
</details>
</div>

<div class="section">
<details>
<summary>📊 État Actuel du Projet</summary>

### Vue d'Ensemble
- **Phase en cours** : Migration n8n → Databricks/Amplitude
- **Statut** : <span class="status-critical">Bloqué - Problèmes techniques critiques</span>
- **Priorité** : Haute
- **Progrès** : ~25%

### Contexte Initial
- Migration depuis stack n8n/Segment/BigQuery/Salesforce
- Nouvelle stack : Databricks/Azure/Amplitude
- Sources de données : Plan de tracking, Salesforce, Drift

### Blocages Majeurs
1. **Problèmes d'Autorisation** <span class="status-critical">(CRITIQUE)</span>
   - Accès Databricks incomplet (création cluster)
   - Logs Azure inaccessibles
   - Permissions Salesforce partielles
   - Configuration Amplitude incomplète

2. **Environnement de Développement** <span class="status-warning">(INSTABLE)</span>
   - Incompatibilités local/Databricks
   - Dépendances complexes (Spark, Java)
   - Clusters instables (redémarrages fréquents)
   - Organisation du code non structurée

### État des Composants
- **Webhook Amplitude** : 
  - Base fonctionnelle ✅
  - Gestion d'erreurs bloquée ⛔
  - Tests incomplets ⚠️

- **Scripts Périodiques** :
  - En cours de revue 🔄
  - Problèmes de permissions ⛔
  - Tests à implémenter ⚠️

- **Tables Amplitude** :
  - Création en cours 🔄
  - Schémas définis ✅
  - Performance non optimisée ⚠️

### Métriques Actuelles
- **Volumétrie** : ~37 000 contacts à traiter
- **Performance** : Non mesurable (environnement instable)
- **Taux d'erreur** : Non mesurable (logs inaccessibles)
- **Couverture de tests** : 0%

### Solutions Temporaires en Place
1. **Environnement Local**
   - Développement en local avec GitHub
   - Déploiement vers Databricks
   - Tests locaux avant push

2. **Contournements**
   - Mode développement local sans Spark
   - Tests manuels des composants
   - Documentation détaillée des problèmes

### Impact sur le Planning
- Retard significatif sur le planning initial
- Blocages techniques multiples
- Dépendances sur les autorisations
- Complexité accrue de la maintenance
</details>
</div>

<div class="section">
<details>
<summary>🚨 Problèmes Majeurs Identifiés</summary>

### 1. Problèmes d'Autorisation et d'Accès
- **Databricks**
  - Permissions insuffisantes pour la création de clusters
  - Accès limité aux notebooks et à une partie de la db
  - Problèmes de connexion avec l'environnement local

- **Azure**
  - Pas d'accès aux logs des fonctions
  - Limitations sur la configuration des webhooks
  - Problèmes de monitoring des événements
  - Restrictions sur la gestion des erreurs

- **Salesforce & Amplitude**
  - Autorisations partielles sur Salesforce
  - Configuration incomplète d'Amplitude
  - Problèmes de tokens et d'authentification
  - Limitations sur les API

### 2. Problèmes d'Architecture et d'Infrastructure
- **Environnement Local vs Databricks**
  - Incompatibilités de versions Spark
  - Conflits de dépendances Java
  - Problèmes de configuration des clusters
  - Redémarrages fréquents des clusters Databricks

- **Stack Technique**
  - Migration complexe depuis n8n/Segment/BigQuery
  - Double destination (Amplitude + Databricks)
  - Synchronisation multi-sources complexe
  - Gestion des formats de données hétérogènes

### 3. Problèmes de Développement
- **Organisation du Code**
  - Structure de projet désorganisée
  - Tests dispersés et non standardisés
  - Documentation fragmentée
  - Manque de cohérence dans les nomenclatures

- **Gestion des Données**
  - Validation des données incomplète
  - Problèmes de mapping des champs
  - Gestion des doublons complexe
  - Schémas dynamiques difficiles à maintenir

### 4. Problèmes de Performance et Monitoring
- **Performances**
  - Temps de traitement non optimisés
  - Latence webhook non mesurée
  - Problèmes de scalabilité
  - Gestion des lots inefficace

- **Monitoring**
  - Absence de métriques clés
  - Pas de tableaux de bord de suivi
  - Alerting non configuré
  - Logs incomplets ou inaccessibles

### 5. Problèmes de Gestion de Projet
- **Planning**
  - Retards significatifs sur le planning initial
  - Dépendances bloquantes non identifiées
  - Estimation incorrecte des temps de développement
  - Impact des problèmes d'autorisation sur les délais

- **Communication**
  - Difficultés de coordination avec les équipes techniques
  - Problèmes d'escalade des incidents
  - Documentation insuffisante pour les équipes
  - Manque de visibilité sur l'avancement

### Impact sur le Projet
- **Délais**
  - Retard sur l'import initial des données
  - Blocage sur les développements critiques
  - Report des phases de test
  - Ralentissement général du projet

- **Qualité**
  - Risques sur l'intégrité des données
  - Tests incomplets
  - Documentation partielle
  - Dette technique croissante
</details>
</div>

<div class="section">
<details>
<summary>🎯 Plan d'Action Immédiat</summary>

### Phase 1 : Résolution des Blocages (48h)
1. **Gestion des Autorisations** (Urgent)
   - [ ] Inventaire des accès manquants par plateforme
     - Databricks : création clusters, accès DB
     - Azure : accès logs, configuration webhooks
     - Salesforce : permissions API
     - Amplitude : droits d'administration
   - [ ] Escalade aux équipes concernées
   - [ ] Suivi des demandes d'accès
   - [ ] Documentation des accès obtenus

2. **Stabilisation Environnement Local** (Prioritaire)
   - [ ] Standardisation de l'environnement
     - Python depuis la racine
     - Fichiers exécutables dans `local_workspace`
     - Configuration à la racine
   - [ ] Gestion des dépendances
     - Versions Spark compatibles
     - Configuration Java
     - Requirements.txt à jour
   - [ ] Tests de compatibilité
     - Validation locale
     - Tests sur Databricks
     - Vérification des connexions

3. **Réorganisation du Code** (Important)
   - [ ] Structure du projet
     - Séparation claire webhook/salesforce
     - Organisation des tests
     - Centralisation des configurations
   - [ ] Documentation
     - README par composant
     - Guide de déploiement
     - Procédures de test

### Phase 2 : Développement Sécurisé (72h)
1. **Mise en Place Tests**
   - [ ] Tests unitaires de base
     - Validation payload
     - Transformation données
     - Gestion erreurs
   - [ ] Tests d'intégration
     - Connexion Databricks
     - Envoi Amplitude
     - Webhooks Azure

2. **Sécurisation Données**
   - [ ] Validation données
     - Schémas obligatoires
     - Formats attendus
     - Gestion doublons
   - [ ] Monitoring
     - Logs détaillés
     - Métriques de base
     - Alertes critiques

3. **Optimisation Performance**
   - [ ] Traitement par lots
     - Taille optimale
     - Gestion mémoire
     - Parallélisation
   - [ ] Gestion erreurs
     - Retry pattern
     - Circuit breaker
     - Logging avancé

### Métriques de Suivi
- **Critères de Succès**
  - Environnement local stable et documenté
  - Tests de base fonctionnels
  - Accès et permissions résolus
  - Premiers imports réussis

- **Points de Contrôle**
  - Validation quotidienne des accès
  - Tests automatisés
  - Métriques de performance
  - Documentation à jour

### Communication
- Daily avec équipe technique
- Points hebdomadaires stakeholders
- Documentation des blocages
- Suivi des escalades

### Livrables Attendus
1. **48h**
   - Inventaire complet des accès
   - Environnement local stable
   - Structure projet claire

2. **72h**
   - Tests de base fonctionnels
   - Premier import test réussi
   - Documentation technique initiale
</details>
</div>

<div class="section">
<details>
<summary>📋 Tâches en Cours</summary>

### 1. Webhook Amplitude → Databricks (En Review)
- [x] Création script Azure Function
  - Endpoint webhook fonctionnel
  - Structure de base en place
  - Tests initiaux validés
- [x] Configuration API Databricks
  - Connexion établie
  - Paramètres de base configurés
- [x] Validation données
  - Format payload vérifié
  - Schémas définis
- [ ] Gestion des erreurs (Bloqué)
  - Accès logs manquant
  - Monitoring à configurer
  - Alertes à mettre en place

### 2. Tables et Données (En Cours)
- [ ] Tables Amplitude
  - [x] Identification des types de données
  - [ ] Tables temporaires en création
  - [ ] Tables finales en préparation
  - [ ] Schémas en cours de définition
  - [ ] Tests d'insertion à faire

- [ ] Organisation des Données
  - [x] Scripts de base ��crits
  - [ ] Jobs périodiques en attente
  - [ ] Tests d'intégrité à implémenter
  - [ ] Alertes à configurer

### 3. Intégrations Sources (Mixte)
#### Salesforce (En Révision)
- [x] Script de récupération
  - [x] Contacts
  - [x] Leads
  - [x] Opportunités
- [x] Planification (5min)
- [ ] Double destination
  - [ ] Envoi Amplitude (Problèmes)
  - [ ] Stockage Databricks (À valider)

#### Problèmes Identifiés
- Format des événements non conforme aux spécifications Amplitude
- Problèmes de performance sur les requêtes Salesforce
- Gestion des erreurs insuffisante
- Monitoring incomplet des envois

#### Actions Correctives
- [ ] Révision du format des événements
  - [ ] Structure contact
  - [ ] Structure identify
  - [ ] Validation JSON
- [ ] Optimisation des requêtes
  - [ ] Limitation des champs
  - [ ] Gestion du rate limiting
  - [ ] Batch processing
- [ ] Amélioration monitoring
  - [ ] Logs détaillés
  - [ ] Métriques de performance
  - [ ] Alertes en cas d'échec

#### Prochaines Étapes
1. Correction du format des événements
2. Tests avec petit volume (100 contacts)
3. Validation complète des données
4. Déploiement progressif

#### Drift (En Cours)
- [ ] Récupération événements
  - [ ] Analyse des types d'événements
  - [ ] Format de données défini
  - [ ] Script de récupération en cours
  - [ ] Tests unitaires à faire

#### Synchronisation
- [ ] Configuration Amplitude
- [ ] Tests connexion

### 4. Migration n8n (En Cours)
- [ ] Analyse des workflows
  - [x] Identification des scripts
  - [ ] Documentation des flux
  - [ ] Points d'intégration
- [ ] Conversion
  - [ ] Scripts Python
  - [ ] Tests unitaires
  - [ ] Validation fonctionnelle

### 5. Infrastructure (En Cours)
- [ ] Tests et Validation
  - [ ] Tests intégration
  - [ ] Tests performance
  - [ ] Tests charge
- [ ] Monitoring
  - [ ] Dashboards
  - [ ] Alertes
  - [ ] Logs

### Points de Blocage Actuels
1. **Autorisations** (Critique)
   - Création clusters Databricks
   - Accès logs Azure
   - Configuration complète Amplitude

2. **Environnement** (Important)
   - Incompatibilités versions
   - Configuration Spark
   - Stabilité clusters

3. **Tests** (À Démarrer)
   - Framework à mettre en place
   - Environnement de test à configurer
   - Données de test à préparer

### Prochaines Actions (24-48h)
1. **Priorité 1**
   - Résolution accès Databricks
   - Stabilisation environnement local
   - Tests basiques webhook

2. **Priorité 2**
   - Finalisation tables Amplitude
   - Tests intégration Drift
   - Documentation technique

### Métriques Actuelles
- **Webhook** : 80% complété
- **Tables** : 40% complété
- **Intégrations** : 60% complété
- **Tests** : 20% complété
</details>
</div>

<div class="section">
<details>
<summary>🔄 Intégrations en Attente</summary>

### 1. Drift → Amplitude (En Cours)
#### État Actuel
- [ ] Récupération événements
  - [ ] Analyse des types d'événements
  - [ ] Format de données défini
  - [ ] Script de récupération en cours
  - [ ] Tests unitaires à faire

#### Blocages
- Accès API Drift incomplet
- Format des données à valider
- Tests environnement à configurer

#### Prochaines Étapes
- Finalisation script récupération
- Tests avec données réelles
- Documentation technique

### 2. Salesforce → Amplitude (En Révision)
#### État Actuel
- [x] Script de récupération
  - [x] Contacts
  - [x] Leads
  - [x] Opportunités
- [x] Planification (5min)
- [ ] Double destination
  - [ ] Envoi Amplitude (Problèmes)
  - [ ] Stockage Databricks (À valider)

#### Problèmes Identifiés
- Format des événements non conforme aux spécifications Amplitude
- Problèmes de performance sur les requêtes Salesforce
- Gestion des erreurs insuffisante
- Monitoring incomplet des envois

#### Actions Correctives
- [ ] Révision du format des événements
  - [ ] Structure contact
  - [ ] Structure identify
  - [ ] Validation JSON
- [ ] Optimisation des requêtes
  - [ ] Limitation des champs
  - [ ] Gestion du rate limiting
  - [ ] Batch processing
- [ ] Amélioration monitoring
  - [ ] Logs détaillés
  - [ ] Métriques de performance
  - [ ] Alertes en cas d'échec

#### Prochaines Étapes
1. Correction du format des événements
2. Tests avec petit volume (100 contacts)
3. Validation complète des données
4. Déploiement progressif

### 3. BigQuery → Amplitude/Databricks (En Attente)
#### À Faire
- [ ] Export données historiques
  - [ ] Analyse volumétrie
  - [ ] Script d'export
  - [ ] Validation données
- [ ] Migration
  - [ ] Transformation données
  - [ ] Import Amplitude
  - [ ] Vérification intégrité

#### Prérequis
- Accès BigQuery à configurer
- Format de mapping à définir
- Environnement de test à préparer

### 4. Plan de Tracking → Amplitude (Bloqué)
#### État Actuel
- [ ] Analyse existant
  - [ ] Scripts actuels
  - [ ] Points de tracking
  - [ ] Format données
- [ ] Migration
  - [ ] Nouveau format
  - [ ] Tests parallèles
  - [ ] Validation données

#### Blocages
- Documentation incomplète
- Accès configurations actuelles
- Environnement de test

### 5. Migration n8n → Databricks (En Cours)
#### En Cours
- [ ] Analyse des workflows
  - [x] Identification des scripts
  - [ ] Documentation des flux
  - [ ] Points d'intégration
- [ ] Conversion
  - [ ] Scripts Python
  - [ ] Tests unitaires
  - [ ] Validation fonctionnelle

#### Risques Identifiés
- Complexité des workflows
- Dépendances multiples
- Tests incomplets

### Points de Vigilance Généraux
1. **Données**
   - Validation des formats
   - Gestion des doublons
   - Intégrité des données

2. **Performance**
   - Temps de traitement
   - Utilisation ressources
   - Gestion des erreurs

3. **Monitoring**
   - Alertes en place
   - Logs accessibles
   - Tableaux de bord

### Prochaines Actions Prioritaires
1. **Immédiat (24h)**
   - Finalisation Drift
   - Tests BigQuery
   - Documentation workflows

2. **Court Terme (72h)**
   - Migration plan de tracking
   - Validation complète Salesforce
   - Tests d'intégration
</details>
</div>

<div class="section">
<details>
<summary>⚠️ Points de Vigilance Critiques</summary>

### 1. Problèmes d'Autorisation (URGENT)
- **Databricks**
  - [ ] Création de clusters bloquée
  - [ ] Accès limité aux notebooks
  - [ ] Permissions DB incomplètes
  - [ ] Configuration des jobs restreinte

- **Azure**
  - [ ] Logs inaccessibles
  - [ ] Configuration webhook limitée
  - [ ] Monitoring incomplet
  - [ ] Gestion des erreurs impossible

- **Amplitude & Salesforce**
  - [ ] Tokens d'authentification à sécuriser
  - [ ] Permissions API à compléter
  - [ ] Webhooks à configurer
  - [ ] Rate limiting à gérer

### 2. Environnement de Développement (CRITIQUE)
- **Incompatibilités**
  - [ ] Versions Spark local/Databricks
  - [ ] Dépendances Java
  - [ ] Configurations Python
  - [ ] Packages système

- **Stabilité**
  - [ ] Redémarrages fréquents des clusters
  - [ ] Connexions instables
  - [ ] Pertes de session
  - [ ] Timeouts fréquents

### 3. Organisation du Code (IMPORTANT)
- **Structure**
  - [ ] Réorganiser les fichiers Python
  - [ ] Centraliser les configurations
  - [ ] Standardiser les logs
  - [ ] Nettoyer les tests

- **Documentation**
  - [ ] Mise à jour des README
  - [ ] Documentation des API
  - [ ] Guides de déploiement
  - [ ] Procédures de test

### 4. Performance et Données (CRITIQUE)
- **Validation**
  - [ ] Format des événements
  - [ ] Champs obligatoires
  - [ ] Gestion des doublons
  - [ ] Intégrité des données

- **Monitoring**
  - [ ] Temps de traitement
  - [ ] Taux d'erreur
  - [ ] Utilisation ressources
  - [ ] Alertes

### Actions Prioritaires (24-48h)
1. **Autorisations (URGENT)**
   - Escalade problèmes d'accès
   - Documentation des besoins
   - Tests de validation
   - Mise en place workarounds

2. **Environnement (CRITIQUE)**
   - Standardisation configuration
   - Tests de compatibilité
   - Documentation déploiement
   - Procédures de recovery

3. **Code (IMPORTANT)**
   - Restructuration projet
   - Nettoyage dépendances
   - Mise à jour documentation
   - Organisation tests

### Métriques à Surveiller
- **Performance**
  - Temps traitement < 2min/1000 records
  - Latence webhook < 1s
  - CPU cluster < 80%
  - Mémoire < 70%

- **Qualité**
  - Taux erreur < 0.1%
  - Couverture tests > 80%
  - Doublons = 0%
  - Data loss = 0%

### Rappels Critiques
- Exécuter depuis la racine du projet
- Vérifier les configurations avant déploiement
- Tester sur petit volume avant production
- Documenter tous les changements
- Maintenir les logs à jour
- Sauvegarder les données critiques

</details>
</div>

<div class="section">
<details>
<summary>📝 Recommandations</summary>

### 1. Actions Immédiates (24-48h)
#### 1.1 Stabilisation Environnement
- **Local**
  - [ ] Standardiser l'environnement Python
  - [ ] Nettoyer les dépendances conflictuelles
  - [ ] Centraliser les fichiers de configuration
  - [ ] Organiser les scripts dans `local_workspace`

- **Databricks**
  - [ ] Documenter les erreurs de connexion
  - [ ] Créer un cluster de développement stable
  - [ ] Tester les connexions de base
  - [ ] Valider les permissions minimales

#### 1.2 Gestion des Accès
- **Escalade Prioritaire**
  - [ ] Liste exhaustive des accès manquants
  - [ ] Demande formelle par plateforme
  - [ ] Suivi quotidien des tickets
  - [ ] Tests de validation post-accès

- **Solutions Temporaires**
  - [ ] Développement en mode dégradé
  - [ ] Tests locaux simulés
  - [ ] Documentation des workarounds
  - [ ] Plan de migration vers solution finale

### 2. Actions à Court Terme (1-2 semaines)
#### 2.1 Organisation du Code
- **Structure**
  - [ ] Séparation claire des composants
  - [ ] Standardisation des logs
  - [ ] Gestion centralisée des configurations
  - [ ] Tests unitaires de base

- **Documentation**
  - [ ] Guide d'installation
  - [ ] Procédures de déploiement
  - [ ] Points de contrôle critiques
  - [ ] Troubleshooting guide

#### 2.2 Monitoring et Tests
- **Base Monitoring**
  - [ ] Logs essentiels
  - [ ] Métriques de performance
  - [ ] Alertes critiques
  - [ ] Dashboard basique

- **Tests Fondamentaux**
  - [ ] Validation des données
  - [ ] Tests de connexion
  - [ ] Vérification des formats
  - [ ] Tests d'intégration simples

### 3. Actions à Moyen Terme (2-4 semaines)
#### 3.1 Optimisation
- **Performance**
  - [ ] Optimisation des requêtes
  - [ ] Gestion du batch processing
  - [ ] Configuration des clusters
  - [ ] Monitoring avancé

- **Sécurité**
  - [ ] Migration vers Key Vault
  - [ ] Gestion des secrets
  - [ ] Validation des accès
  - [ ] Audit des logs

#### 3.2 Automatisation
- **Déploiement**
  - [ ] Pipeline CI/CD
  - [ ] Tests automatisés
  - [ ] Déploiement continu
  - [ ] Rollback automatique

- **Maintenance**
  - [ ] Scripts de maintenance
  - [ ] Backup automatique
  - [ ] Nettoyage données
  - [ ] Rotation des logs

### 4. Actions à Long Terme (1-2 mois)
#### 4.1 Industrialisation
- **Infrastructure**
  - [ ] Architecture haute disponibilité
  - [ ] Scaling automatique
  - [ ] Disaster recovery
  - [ ] Monitoring complet

- **Documentation**
  - [ ] Documentation technique complète
  - [ ] Guides utilisateurs
  - [ ] Procédures d'exploitation
  - [ ] Plans de maintenance

### Points de Vigilance
1. **Priorités**
   - Stabilité avant fonctionnalités
   - Tests avant déploiement
   - Documentation continue
   - Communication régulière

2. **Risques**
   - Dépendances externes
   - Compatibilité versions
   - Performance données
   - Sécurité accès

3. **Contrôle**
   - Validation étape par étape
   - Tests réguliers
   - Métriques claires
   - Feedback utilisateurs

### Métriques de Succès
- **Technique**
  - Uptime > 99.9%
  - Latence < 1s
  - Erreurs < 0.1%
  - Tests > 80%

- **Projet**
  - Délais respectés
  - Budget maintenu
  - Satisfaction utilisateurs
  - Documentation complète

</details>
</div>

<div class="section">
<details>
<summary>🔍 Configuration Requise</summary>

### 1. Structure du Projet
```plaintext
project_root/
├── .env                    # Variables d'environnement (ne pas commiter)
├── config/
│   ├── databricks.yaml     # Configuration Databricks (ne pas commiter)
│   ├── amplitude.yaml      # Configuration Amplitude (ne pas commiter)
│   └── azure.yaml         # Configuration Azure (ne pas commiter)
├── local_workspace/
│   ├── webhook/
│   ├── salesforce_sync/
│   └── drift_sync/
└── tests/
```

### 2. Prérequis Système
- Python 3.8+
- Java 8+ (pour Spark local)
- Git
- Accès Internet stable
- RAM minimale : 8GB
- Espace disque : 20GB

### 3. Fichiers de Configuration
#### 3.1 Structure .env
```plaintext
# Databricks
DATABRICKS_HOST=xxx
DATABRICKS_TOKEN=xxx
DATABRICKS_CLUSTER_ID=xxx

# Amplitude
AMPLITUDE_API_KEY=xxx

# Azure
AZURE_FUNCTION_URL=xxx

# Salesforce
SF_USERNAME=xxx
SF_PASSWORD=xxx
SF_TOKEN=xxx
```

### 4. Dépendances Python
```plaintext
# requirements.txt
databricks-connect>=13.0
requests>=2.28.0
python-dotenv>=0.19.0
simple-salesforce>=1.12.0
amplitude-analytics>=1.1.0
azure-functions>=1.12.0
```

### 5. Points de Configuration Importants
- **Exécution** : Toujours depuis la racine du projet
- **Fichiers Python** : Dans `local_workspace`
- **Logs** : En anglais, niveau INFO minimum
- **Tests** : Dans le dossier `tests`
- **Configuration** : Fichiers à la racine

### 6. Accès Requis
- **Databricks**
  - Accès Workspace
  - Permissions Cluster
  - Accès Tables

- **Azure**
  - Accès Function App
  - Permissions Logs
  - Configuration Webhook

- **Amplitude**
  - Clé API
  - Accès Dashboard
  - Permissions Projet

### 7. Sécurité
- Ne jamais commiter les fichiers `.env`
- Ne pas partager les tokens
- Utiliser des secrets sécurisés
- Restreindre les accès IP si possible
- Rotation régulière des clés

### 8. Rappels Critiques
- Vérifier les configurations avant déploiement
- Tester en local avant push
- Sauvegarder les configurations sensibles
- Documenter les changements
- Maintenir les accès à jour

</details>
</div>

<div class="section">
<details>
<summary>📅 Planning Proposé</summary>

### Planning d'Exécution sur 6 Semaines

### Semaine 1 : Setup & Configuration
#### Jour 1-2 : Environnement
- [ ] Clone du repository
- [ ] Installation environnement local
  ```bash
  # Dans project_root/
  python -m venv venv
  source venv/bin/activate  # ou venv\Scripts\activate sous Windows
  pip install -r requirements.txt
  ```
- [ ] Vérification des accès
  - Databricks
  - Azure
  - Amplitude
  - Salesforce

#### Jour 3-4 : Architecture
- [ ] Analyse du code existant
  - `webhook.py`
  - `historical_import.py`
  - Scripts de synchronisation
- [ ] Tests des composants existants
- [ ] Documentation des problèmes rencontrés

#### Jour 5 : Tests Initiaux
- [ ] Test connexions
- [ ] Validation formats données
- [ ] Vérification logs

### Semaine 2 : Infrastructure
#### Jour 1-2 : Databricks
- [ ] Configuration cluster dev
  ```python
  # Example cluster config
  {
    "spark_version": "13.3.x-scala2.12",
    "node_type_id": "Standard_DS3_v2",
    "num_workers": 1
  }
  ```
- [ ] Tests connexion locale
- [ ] Validation tables

#### Jour 3-4 : Webhooks & Azure
- [ ] Setup Azure Functions
- [ ] Tests webhooks
- [ ] Validation payload

#### Jour 5 : Monitoring
- [ ] Setup logs
- [ ] Configuration alertes
- [ ] Tests monitoring

### Semaine 3 : Développement Core
#### Jour 1-2 : Import Données
```python
# Structure import attendue
def import_data(source, destination):
    """
    source: 'salesforce', 'drift', 'bigquery'
    destination: 'amplitude', 'databricks'
    """
    pass
```
- [ ] Import test Salesforce
- [ ] Import test Drift
- [ ] Validation données

#### Jour 3-4 : Synchronisation
- [ ] Setup jobs périodiques
- [ ] Tests synchronisation
- [ ] Gestion erreurs

#### Jour 5 : Tests & Documentation
- [ ] Tests unitaires
- [ ] Tests intégration
- [ ] Documentation technique

### Semaine 4 : Intégrations
#### Priorités par Source
1. **Salesforce** (2 jours)
   - Format événements
   - Synchronisation 5min
   - Validation données

2. **Drift** (2 jours)
   - Structure données
   - Tests connexion
   - Import initial

3. **BigQuery** (1 jour)
   - Export données
   - Import Amplitude
   - Validation

### Semaine 5 : Optimisation & Tests
#### Performance (3 jours)
- [ ] Optimisation requêtes
- [ ] Gestion batch
- [ ] Tests charge
```python
# Exemple batch processing
def process_batch(records, batch_size=1000):
    for i in range(0, len(records), batch_size):
        batch = records[i:i + batch_size]
        try:
            process_records(batch)
        except Exception as e:
            log_error(e, batch)
```

#### Tests (2 jours)
- [ ] Tests bout en bout
- [ ] Tests charge
- [ ] Documentation tests

### Semaine 6 : Finalisation
#### Documentation (3 jours)
- [ ] Guide technique
- [ ] Procédures maintenance
- [ ] Troubleshooting

#### Déploiement (2 jours)
- [ ] Validation finale
- [ ] Mise en production
- [ ] Monitoring post-déploiement

### Points de Contrôle Quotidiens
- Validation connexions
- Vérification logs
- Tests basiques
- Push code commenté

### Métriques de Progression
- **Setup** : Environnement fonctionnel
- **Dev** : Tests passent
- **Prod** : Données synchronisées
- **Docs** : Documentation à jour

### Contacts Clés
- **Support Databricks** : À définir
- **Support Azure** : À définir
- **Support Amplitude** : À définir
- **Équipe Novade** : À définir

### Rappels Importants
- Exécuter depuis la racine
- Vérifier `.env` avant tests
- Documenter les erreurs
- Commits clairs et documentés
- Tests avant push

</details>
</div>

<div class="section">
<details>
<summary>💰 Budget et Facturation</summary>

### Vue d'Ensemble Financière
- **Budget Initial** : 21 375,00 € HT
- **Acompte Novade (50%)** : 10 687,50 € HT
- **Montant Reçu par Thomas** : 6 000,00 € HT
- **Reste à Facturer** : 10 687,50 € HT
- **Marge Tyrscale** : 7 125,00 € HT

### Répartition Initiale
- **Jours Prévus** : 24 jours
- **Gestion de Projet** : 4,5 jours (non consommés)
- **Développement** : 19,5 jours

### État Actuel
- **Complexité Additionnelle**
  - Problèmes d'autorisations multiples
  - Architecture technique plus complexe que prévue
  - Intégrations supplémentaires nécessaires
  - Environnement de développement complexe

### Proposition d'Ajustement
- **Enveloppe Supplémentaire** : 5 000,00 € HT
  - Livrable à la finalisation complète du projet
  - Justifié par la complexité technique imprévue
  - Couvre les développements additionnels nécessaires

### Justification
1. **Complexité Technique**
   - Migration multi-plateformes complexe
   - Problèmes d'autorisations non anticipés
   - Architecture technique plus sophistiquée

2. **Travail Supplémentaire**
   - Développement d'environnement local
   - Gestion des incompatibilités
   - Tests et validations additionnels
   - Documentation extensive

3. **Reconnaissance Client**
   - Novade conscient des problèmes d'autorisation
   - Impact sur le planning initial
   - Complexité technique reconnue

### Options de Financement
1. **Solution Proposée**
   - Enveloppe supplémentaire : 5 000,00 € HT
   - Paiement à la livraison finale
   - Garantie de finalisation complète

2. **Alternative**
   - Utilisation partielle de la marge Tyrscale
   - Maintien du budget initial
   - Ajustement du périmètre

### État des Paiements
1. **Déjà Reçu**
   - Acompte Novade : 10 687,50 € HT
   - Versement Thomas : 6 000,00 € HT

2. **À Venir**
   - Solde Novade : 10 687,50 € HT
   - Bonus finalisation (si accepté) : 5 000,00 € HT

### Points de Discussion
- Reconnaissance de la complexité technique
- Validation de l'enveloppe supplémentaire
- Planning de facturation ajusté
- Garanties de livraison

</details>
</div>
