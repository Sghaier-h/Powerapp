# Guide : Intégration Git avec Dataverse (Méthode Officielle Microsoft)

## 🎯 Vue d'Ensemble

Ce guide utilise la méthode **officielle Microsoft** pour connecter votre environnement Dataverse/Power Apps à Git via Azure DevOps. Cette méthode est intégrée directement dans l'interface Power Apps.

## ✅ Avantages de la Méthode Officielle

1. **Intégration Native** : Pas besoin de CLI, tout se fait depuis l'interface Power Apps
2. **Synchronisation Automatique** : Les modifications sont automatiquement détectées
3. **Interface Visuelle** : Panneau "Contrôle de code source" dans Power Apps
4. **Gestion des Branches** : Création et gestion des branches directement depuis Power Apps
5. **Validation et Push** : Tout se fait depuis l'interface, pas besoin de commandes

## 📋 Prérequis

### 1. Environnements Power Platform

- ✅ **Environnements gérés activés** : Les environnements de développement et cibles doivent être activés en tant qu'**Environnements gérés** dans le Centre d'Administration Power Platform
- ✅ **Rôle Administrateur système** : Vous devez avoir le rôle "System Administrator" dans l'environnement Dataverse

### 2. Azure DevOps

- ✅ **Abonnement Azure DevOps** : Un compte Azure DevOps avec un projet
- ✅ **Licences** : Licences pour les utilisateurs qui interagissent avec le contrôle de code source
- ✅ **Autorisations** : Les membres du groupe "Contributeurs" ont les autorisations nécessaires

### 3. Solution Power Apps

- ✅ **Solution personnalisée non gérée** : La solution par défaut et Common Data Service ne peuvent PAS être connectées à Git
- ✅ **Créer une solution personnalisée** : Ex: "La Plume Artisanale"

## 🚀 Étape 1 : Configuration d'Azure DevOps

### Créer un Projet Azure DevOps

1. **Connectez-vous** à [Azure DevOps](https://dev.azure.com)
2. **Sélectionnez votre organisation** (ou créez-en une)
3. **Cliquez sur "Nouveau projet"**
4. **Remplissez** :
   - **Nom du projet** : `La-Plume-Artisanale` (ou autre nom)
   - **Contrôle de version** : **Git** (important !)
   - **Visibilité** : Privé ou Public
5. **Cliquez sur "Créer"**

### Initialiser le Référentiel Git

1. **Dans le nouveau projet**, allez dans **"Référentiels"**
2. **Cliquez sur "Initialiser"** en bas de la page
3. Le référentiel par défaut est maintenant initialisé

### Configurer les Permissions

1. **Allez dans "Paramètres du projet"** > **"Permissions"**
2. **Vérifiez que tous les utilisateurs** qui apportent des modifications ont :
   - Accès au référentiel
   - Permission de valider les modifications
   - Licence Azure DevOps (plan de base disponible)

## 🔗 Étape 2 : Se Connecter à Git depuis Power Apps

### Méthode A : Liaison d'Environnement (Recommandée pour Démarrer)

**Avantages :**
- ✅ Processus unique pour lier tout l'environnement
- ✅ Toutes les solutions non gérées sont automatiquement synchronisées
- ✅ Pas besoin de configurer chaque solution individuellement
- ✅ Un seul dossier et une seule branche pour tout l'environnement

**Étapes :**

1. **Connectez-vous** à [Power Apps](https://make.powerapps.com)
2. **Allez dans "Solutions"** (menu de gauche)
3. **Cliquez sur "Se connecter à Git"** (en haut de la page Solutions)
4. **Sélectionnez "Environnement"** comme type de connexion
5. **Sélectionnez** :
   - **Organisation Azure DevOps** : Votre organisation
   - **Projet** : Votre projet (ex: "La-Plume-Artisanale")
   - **Référentiel** : Le référentiel Git
   - **Branche** : `main` ou `master` (ou créez-en une nouvelle)
   - **Dossier** : Nom du dossier (ex: `powerapps-solutions`)
6. **Cliquez sur "Se connecter"**

### Méthode B : Liaison de Solution (Plus de Flexibilité)

**Avantages :**
- ✅ Flexibilité pour organiser plusieurs solutions dans différents dossiers/référentiels
- ✅ Contrôle granulaire par solution

**Inconvénients :**
- ⚠️ Chaque nouvelle solution doit être configurée individuellement
- ⚠️ Plus de gestion nécessaire

**Étapes :**

1. **Connectez-vous** à [Power Apps](https://make.powerapps.com)
2. **Allez dans "Solutions"**
3. **Cliquez sur "Se connecter à Git"**
4. **Sélectionnez "Solution"** comme type de connexion
5. **Sélectionnez votre organisation et projet Azure DevOps**
6. **Cliquez sur "Se connecter"**

**Ensuite, pour chaque solution :**

1. **Dans la liste des solutions**, cliquez sur les **trois points verticaux** (⋮) à côté de la solution
2. **Sélectionnez "Connecter à Git"**
3. **Sélectionnez** :
   - **Branche** : Branche existante ou créez-en une nouvelle
   - **Dossier Git** : Nom du dossier pour cette solution (ex: `solution-la-plume`)
4. **Cliquez sur "Connecter"**

## ✅ Étape 3 : Valider votre Connexion

### Créer ou Modifier une Solution

1. **Ouvrez votre solution** dans Power Apps
2. **Apportez une modification** (ajoutez une table, modifiez une application, etc.)
3. **Dans le volet de gauche**, cliquez sur **"Contrôle de code source"**

### Voir les Modifications

Dans le panneau "Contrôle de code source", vous verrez :

- ✅ **Modifications détectées** : Liste des fichiers modifiés
- ✅ **Branche actuelle** : La branche à laquelle votre solution est liée
- ✅ **Boutons** :
  - **Valider** : Valider les modifications localement
  - **Pousser** : Envoyer les modifications vers Azure DevOps
  - **Extraire** : Récupérer les modifications depuis Azure DevOps

### Valider et Pousser

1. **Vérifiez les modifications** dans la liste
2. **Ajoutez un message de commit** (ex: "Ajout table Article")
3. **Cliquez sur "Valider"**
4. **Cliquez sur "Pousser"** pour envoyer vers Azure DevOps

## 🔄 Workflow Quotidien

### Développement

1. **Développer** dans Power Apps (créer/modifier des tables, apps, flows)
2. **Ouvrir "Contrôle de code source"** dans la solution
3. **Voir les modifications** détectées automatiquement
4. **Valider** avec un message descriptif
5. **Pousser** vers Azure DevOps

### Collaboration

1. **Avant de commencer** : **Extraire** les dernières modifications depuis Git
2. **Développer** vos fonctionnalités
3. **Valider et pousser** vos modifications
4. **Créer une Pull Request** dans Azure DevOps (optionnel, pour review)

### Déploiement

1. **Exporter** la solution depuis l'environnement de développement
2. **Importer** dans l'environnement de test
3. **Tester**
4. **Importer** dans la production si OK

## 🌿 Gestion des Branches

### Créer une Nouvelle Branche

1. **Dans "Contrôle de code source"**, cliquez sur la branche actuelle
2. **Sélectionnez "Créer une nouvelle branche"**
3. **Entrez le nom** (ex: `feature/nouvelle-fonctionnalite`)
4. **Créez la branche**

### Changer de Branche

1. **Dans "Contrôle de code source"**, cliquez sur la branche actuelle
2. **Sélectionnez une autre branche** existante
3. Les modifications sont automatiquement synchronisées

## 🔌 Connecter Plusieurs Environnements

Vous pouvez connecter plusieurs environnements de développement au même emplacement Git :

1. **Environnement Dev 1** → Branche `dev-1`
2. **Environnement Dev 2** → Branche `dev-2`
3. **Environnement Test** → Branche `test`
4. **Environnement Prod** → Branche `main`

**Avantages :**
- ✅ Isolation des développeurs
- ✅ Envoi rapide des modifications vers Git
- ✅ Extraction des modifications des autres

## 🔌 Déconnecter de Git

### Déconnecter Toutes les Solutions (Liaison d'Environnement)

1. **Dans "Solutions"**, cliquez sur **"Connexion à Git"**
2. **Sélectionnez "Déconnecter toutes les solutions de Git"**
3. **Confirmez** en cliquant sur "Continuer"

### Déconnecter une Solution Spécifique (Liaison de Solution)

1. **Dans "Solutions"** ou **"Contrôle de code source"**, cliquez sur **"Connexion Git"**
2. **Sélectionnez "Déconnecter la solution de Git"**
3. **Confirmez** en cliquant sur "Continuer"

## 📊 Comparaison : Liaison d'Environnement vs Liaison de Solution

| Critère | Liaison d'Environnement | Liaison de Solution |
|---------|------------------------|---------------------|
| **Configuration** | Une seule fois pour tout l'environnement | Par solution |
| **Nouvelles solutions** | Automatiquement synchronisées | Doivent être configurées |
| **Organisation** | Un seul dossier/branche | Plusieurs dossiers/branches possibles |
| **Flexibilité** | Moins flexible | Plus flexible |
| **Recommandation** | ✅ Pour démarrer | Pour organisation avancée |

## ⚠️ Points Importants

### Solutions qui ne peuvent PAS être connectées

- ❌ **Solution par défaut** : Ne peut pas être connectée à Git
- ❌ **Solution Common Data Service** : Ne peut pas être connectée à Git
- ✅ **Solutions personnalisées non gérées** : Peuvent être connectées

### Bonnes Pratiques

1. **Toujours utiliser des solutions personnalisées** pour le développement
2. **Créer des branches** pour chaque fonctionnalité
3. **Valider régulièrement** vos modifications
4. **Extraire avant de développer** pour avoir les dernières modifications
5. **Messages de commit descriptifs** : "Ajout table Article" plutôt que "Modifications"

## ✅ Checklist de Configuration

- [ ] Créer un projet Azure DevOps
- [ ] Initialiser le référentiel Git
- [ ] Configurer les permissions Azure DevOps
- [ ] Activer les environnements gérés dans Power Platform
- [ ] Vérifier le rôle System Administrator
- [ ] Créer une solution personnalisée non gérée
- [ ] Se connecter à Git (liaison d'environnement ou solution)
- [ ] Valider la connexion en créant une modification
- [ ] Voir les modifications dans "Contrôle de code source"
- [ ] Valider et pousser une première modification

## 🚀 Prochaines Étapes

1. **Configurer Azure DevOps** (si pas déjà fait)
2. **Se connecter à Git** depuis Power Apps
3. **Créer votre première solution personnalisée** "La Plume Artisanale"
4. **Valider et pousser** les modifications initiales
5. **Configurer les branches** pour le développement

## 📚 Ressources Officielles

- [Documentation Microsoft : Intégration Git avec Dataverse](https://learn.microsoft.com/fr-fr/power-platform/alm/git-integration)
- [Azure DevOps](https://dev.azure.com)
- [Power Apps](https://make.powerapps.com)

---

**📅 Date :** 2026-01-14  
**✅ Guide d'intégration Git Dataverse (Méthode Officielle) complété**
