# Guide : Permissions Administrateur Système dans Power Apps

## Qu'est-ce qu'un Administrateur Système ?

Un **Administrateur Système** (System Administrator) est un rôle dans Power Apps/Dataverse qui donne les permissions complètes pour :
- Créer et modifier des tables
- Créer des index
- Configurer les relations
- Gérer les solutions
- Accéder à toutes les fonctionnalités avancées

## Comment Vérifier vos Permissions

### Méthode 1 : Vérifier dans Power Apps

1. **Connectez-vous** à [make.powerapps.com](https://make.powerapps.com)
2. **Cliquez sur votre profil** (en haut à droite)
3. **Sélectionnez "Paramètres"** ou "Settings"
4. **Cherchez "Sécurité"** ou "Security"
5. **Regardez vos rôles** ou "Roles"

**Si vous voyez "System Administrator"** → Vous avez les permissions ✅

**Si vous ne voyez pas "System Administrator"** → Vous n'avez pas les permissions ❌

### Méthode 2 : Vérifier dans le Centre d'Administration Power Platform

1. **Allez sur** [admin.powerplatform.microsoft.com](https://admin.powerplatform.microsoft.com)
2. **Dans le menu de gauche**, cherchez "Environnements" ou "Environments"
3. **Sélectionnez votre environnement**
4. **Allez dans "Sécurité"** ou "Security" > "Utilisateurs" ou "Users"
5. **Cherchez votre nom**
6. **Regardez vos rôles de sécurité**

### Méthode 3 : Tester Directement

**Test simple :** Essayez de créer un index dans une table.

1. **Ouvrez une table** dans votre solution
2. **Cherchez l'option "Index"** dans le menu
3. **Si vous voyez "Index"** et pouvez créer un index → Vous avez les permissions ✅
4. **Si vous ne voyez pas "Index"** ou avez une erreur → Vous n'avez pas les permissions ❌

## Comment Obtenir les Permissions

### Option 1 : Demander à votre Administrateur

1. **Identifiez votre administrateur Power Apps** :
   - Votre responsable IT
   - L'administrateur de votre organisation
   - Le propriétaire de l'environnement Power Apps

2. **Demandez-lui** :
   - "Pouvez-vous m'ajouter le rôle System Administrator dans l'environnement Power Apps ?"
   - OU : "J'ai besoin de permissions pour créer des index dans Dataverse"

3. **L'administrateur doit** :
   - Aller dans le Centre d'Administration Power Platform
   - Sélectionner votre environnement
   - Aller dans Sécurité > Utilisateurs
   - Vous trouver et vous assigner le rôle "System Administrator"

### Option 2 : Si vous êtes Propriétaire de l'Environnement

Si vous avez créé l'environnement vous-même, vous devriez automatiquement avoir les permissions.

**Vérification :**
1. Allez dans [admin.powerplatform.microsoft.com](https://admin.powerplatform.microsoft.com)
2. Vérifiez si vous voyez votre environnement dans la liste
3. Si oui, vous êtes probablement propriétaire et avez les permissions

### Option 3 : Demander le Rôle "Maker" ou "Environment Maker"

Si vous ne pouvez pas obtenir "System Administrator", demandez au minimum :

- **"Environment Maker"** : Permet de créer des tables et solutions
- **"Maker"** : Permet de créer des applications

**Note :** Ces rôles peuvent ne pas donner accès aux index. Le rôle "System Administrator" est généralement requis pour les index.

## Étapes pour l'Administrateur

Si vous êtes administrateur ou si vous devez expliquer à votre administrateur :

### Ajouter le Rôle System Administrator

1. **Connectez-vous** à [admin.powerplatform.microsoft.com](https://admin.powerplatform.microsoft.com)

2. **Allez dans "Environnements"** ou "Environments"

3. **Sélectionnez l'environnement** concerné (ex: "Production" ou "Développement")

4. **Cliquez sur "Sécurité"** ou "Security" > **"Utilisateurs"** ou "Users"

5. **Cherchez l'utilisateur** (vous ou la personne concernée)

6. **Cliquez sur l'utilisateur** > **"Gérer les rôles"** ou "Manage roles"

7. **Cochez "System Administrator"**

8. **Enregistrez**

### Rôles Disponibles

- **System Administrator** : Permissions complètes (recommandé pour créer des index)
- **System Customizer** : Peut personnaliser mais pas tout
- **Environment Maker** : Peut créer des tables et applications
- **Maker** : Peut créer des applications

## Vérification après Attribution du Rôle

Après que l'administrateur vous ait attribué le rôle :

1. **Déconnectez-vous** de Power Apps
2. **Reconnectez-vous** (pour rafraîchir les permissions)
3. **Essayez de créer un index** dans une table
4. **Vous devriez maintenant voir** l'option "Index"

## Si vous ne pouvez pas Obtenir les Permissions

### Alternative 1 : Utiliser une Colonne Calculée

Au lieu d'un index unique composé, créez une colonne calculée :

1. **Créer une colonne "Clé Unique"** :
   - Type : Texte
   - Formule : `Modèle & "-" & Code Modèle & "-" & Code Dimensions`

2. **Créer un index unique** sur cette colonne "Clé Unique"
   - Cela peut être fait avec moins de permissions

### Alternative 2 : Validation via Power Automate

Créer un Flow Power Automate qui :

1. **Déclencheur** : Lors de création/modification d'un enregistrement
2. **Actions** :
   - Vérifier si la combinaison existe déjà
   - Si oui, annuler la création et envoyer une erreur
   - Si non, autoriser la création

### Alternative 3 : Demander à l'Administrateur de Créer l'Index

1. **Documentez** exactement quel index vous voulez créer
2. **Demandez à l'administrateur** de le créer pour vous
3. **Une fois créé**, vous pourrez utiliser la table normalement

## Résumé Rapide

**Pour vérifier vos permissions :**

1. Power Apps > Profil > Paramètres > Sécurité > Rôles
2. OU : Centre d'Administration Power Platform > Environnements > Sécurité > Utilisateurs

**Pour obtenir les permissions :**

1. Demander à votre administrateur de vous ajouter le rôle "System Administrator"
2. OU : Si vous êtes propriétaire de l'environnement, vous devriez déjà avoir les permissions

**Si vous ne pouvez pas obtenir les permissions :**

1. Utiliser une colonne calculée avec index unique simple
2. OU : Demander à l'administrateur de créer l'index pour vous

---

**📅 Date :** 2026-01-14  
**✅ Guide de permissions administrateur complété**
