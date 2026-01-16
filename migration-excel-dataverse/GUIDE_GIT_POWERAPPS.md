# Guide : Intégration Git avec Power Apps

## 🎯 Objectif

Versionner vos solutions Power Apps (applications, flows, tables, etc.) avec Git pour :
- **Historique des changements** : Voir qui a modifié quoi et quand
- **Collaboration** : Travailler en équipe sans conflits
- **Sauvegarde** : Avoir une copie de sécurité de votre code
- **Déploiement** : Gérer les environnements (Dev, Test, Production)
- **Rollback** : Revenir en arrière en cas de problème

## ✅ Avantages de l'Intégration Git avec Power Apps

1. **Versioning Natif** : Power Apps supporte maintenant Git nativement
2. **Solutions Complètes** : Versionner toute la solution (apps, flows, tables, etc.)
3. **Collaboration** : Plusieurs développeurs peuvent travailler ensemble
4. **CI/CD** : Automatiser les déploiements entre environnements
5. **Documentation** : Le code source sert de documentation

## 📋 Prérequis

1. **Compte Power Apps** avec permissions administrateur
2. **Dépôt Git** (GitHub, Azure DevOps, ou Git local)
3. **Power Platform CLI** (pac CLI) installé
4. **Accès à l'environnement Power Apps**

## 🔧 Méthode 1 : Intégration Git Native Power Apps via Interface (Recommandée - Officielle Microsoft)

**⚠️ NOUVEAU :** Microsoft a maintenant une intégration Git native directement dans l'interface Power Apps ! Voir `GUIDE_GIT_DATAVERSE_OFFICIEL.md` pour la méthode officielle recommandée.

Cette méthode utilise l'interface Power Apps directement, sans besoin de CLI.

## 🔧 Méthode 1B : Intégration via Power Platform CLI (Alternative)

### Étape 1 : Installer Power Platform CLI

```powershell
# Installer via winget
winget install Microsoft.PowerPlatform.CLI

# OU via npm
npm install -g @microsoft/powerplatform-cli
```

### Étape 2 : Se Connecter à Power Apps

```powershell
# Se connecter à votre environnement
pac auth create --name "LaPlumeArtisanale" --url https://[votre-environnement].crm.dynamics.com

# OU pour Power Apps (si différent)
pac auth create --name "LaPlumeArtisanale" --url https://[votre-environnement].powerapps.com
```

### Étape 3 : Initialiser le Projet Git

```powershell
# Aller dans le dossier du projet
cd "d:\OneDrive - FLYING TEX\PROJET\migration-excel-dataverse"

# Initialiser un projet Power Platform
pac solution init --publisher-name "LaPlumeArtisanale" --publisher-prefix "lpa"

# Cela crée un dossier avec la structure :
# - Solution/
#   - Solution.xml
#   - Customizations.xml
#   - etc.
```

### Étape 4 : Exporter la Solution vers Git

```powershell
# Exporter la solution depuis Power Apps
pac solution export --name "La Plume Artisanale" --path ./solution --managed false

# Cela exporte tous les composants :
# - Applications
# - Flows
# - Tables
# - Choix options
# - etc.
```

### Étape 5 : Initialiser Git (si pas déjà fait)

```powershell
# Initialiser Git
git init

# Créer .gitignore pour Power Platform
@"
# Power Platform
*.zip
*.dll
*.pdb
bin/
obj/
*.suo
*.user
.vs/
"@ | Out-File -FilePath .gitignore -Encoding UTF8

# Ajouter les fichiers
git add .
git commit -m "Initial commit - Solution Power Apps La Plume Artisanale"
```

## 🔧 Méthode 2 : Intégration via Azure DevOps (Avancée)

### Avantages
- **Pipelines CI/CD** intégrés
- **Gestion des environnements** automatisée
- **Tests automatisés** possibles
- **Déploiements automatiques**

### Configuration

1. **Créer un projet Azure DevOps**
2. **Configurer le dépôt Git**
3. **Créer un pipeline YAML** pour exporter/importer les solutions
4. **Configurer les variables d'environnement** (Dev, Test, Prod)

## 🔧 Méthode 3 : Export Manuel + Git (Simple)

### Pour les Débutants

1. **Exporter manuellement** la solution depuis Power Apps
   - Power Apps > Solutions > Exporter
   - Format : Non géré (Unmanaged)

2. **Extraire le ZIP** dans un dossier Git

3. **Versionner avec Git** :
   ```powershell
   git add .
   git commit -m "Export solution Power Apps"
   ```

## 📁 Structure Recommandée du Dépôt Git

```
PROJET/
├── .gitignore
├── README.md
├── migration-excel-dataverse/
│   ├── INSTRUCTION_COPILOT_CREATION_TABLES.md
│   ├── GUIDE_*.md
│   └── ...
├── powerapps-solutions/
│   ├── La-Plume-Artisanale/
│   │   ├── Solution.xml
│   │   ├── Customizations.xml
│   │   ├── Workflows/
│   │   ├── Apps/
│   │   └── Tables/
│   └── ...
└── scripts/
    ├── export-solution.ps1
    └── import-solution.ps1
```

## 🔄 Workflow Recommandé

### Développement Quotidien

1. **Créer une branche** pour votre fonctionnalité :
   ```powershell
   git checkout -b feature/nouvelle-fonctionnalite
   ```

2. **Développer** dans Power Apps

3. **Exporter** la solution :
   ```powershell
   pac solution export --name "La Plume Artisanale" --path ./powerapps-solutions/La-Plume-Artisanale
   ```

4. **Commit** les changements :
   ```powershell
   git add .
   git commit -m "Ajout fonctionnalité X"
   ```

5. **Push** vers le dépôt :
   ```powershell
   git push origin feature/nouvelle-fonctionnalite
   ```

6. **Créer une Pull Request** pour review

7. **Merge** dans la branche principale

### Déploiement

1. **Exporter** depuis l'environnement de développement
2. **Importer** dans l'environnement de test :
   ```powershell
   pac solution import --path ./powerapps-solutions/La-Plume-Artisanale.zip --environment [test-env]
   ```
3. **Tester**
4. **Importer** dans la production si OK

## 📝 Scripts PowerShell Utiles

### Script d'Export Automatique

```powershell
# export-solution.ps1
param(
    [string]$SolutionName = "La Plume Artisanale",
    [string]$ExportPath = "./powerapps-solutions/$SolutionName"
)

Write-Host "Export de la solution $SolutionName..." -ForegroundColor Green

# Exporter la solution
pac solution export --name $SolutionName --path $ExportPath --managed false

if ($LASTEXITCODE -eq 0) {
    Write-Host "✅ Export réussi" -ForegroundColor Green
    
    # Commit automatique
    git add $ExportPath
    git commit -m "Export solution $SolutionName - $(Get-Date -Format 'yyyy-MM-dd HH:mm')"
    
    Write-Host "✅ Changements commités" -ForegroundColor Green
} else {
    Write-Host "❌ Erreur lors de l'export" -ForegroundColor Red
}
```

### Script d'Import Automatique

```powershell
# import-solution.ps1
param(
    [string]$SolutionPath = "./powerapps-solutions/La-Plume-Artisanale.zip",
    [string]$EnvironmentUrl
)

Write-Host "Import de la solution vers $EnvironmentUrl..." -ForegroundColor Green

pac solution import --path $SolutionPath --environment $EnvironmentUrl

if ($LASTEXITCODE -eq 0) {
    Write-Host "✅ Import réussi" -ForegroundColor Green
} else {
    Write-Host "❌ Erreur lors de l'import" -ForegroundColor Red
}
```

## 🔐 Sécurité et Bonnes Pratiques

### 1. Ne pas Versionner les Secrets

Créer un fichier `.gitignore` :
```
# Secrets
*.env
*.secrets
connectionStrings.json
appsettings.json
```

### 2. Utiliser des Variables d'Environnement

Pour les connexions et clés API, utiliser des variables d'environnement ou Azure Key Vault.

### 3. Gérer les Permissions

- **Développeurs** : Accès en lecture/écriture au dépôt Git
- **Testeurs** : Accès en lecture seule
- **Administrateurs** : Accès complet

## 🔗 Intégration avec OneDrive

### Option 1 : OneDrive comme Stockage de Fichiers

- **Documentation** : Stocker les guides et instructions
- **Images/Assets** : Stocker les logos, photos, etc.
- **Exports** : Sauvegarder les exports de solutions

### Option 2 : OneDrive comme Dépôt Git

**Non recommandé** : OneDrive n'est pas optimisé pour Git (problèmes de synchronisation, conflits).

**Meilleure approche** :
- **GitHub/Azure DevOps** : Pour le versioning
- **OneDrive** : Pour la documentation et les fichiers de référence

## 📊 Comparaison des Méthodes

| Méthode | Complexité | Avantages | Inconvénients |
|---------|-----------|-----------|---------------|
| **Git Native Power Apps** | Moyenne | Intégration native, CLI puissant | Nécessite CLI, courbe d'apprentissage |
| **Azure DevOps** | Élevée | CI/CD, gestion avancée | Configuration complexe |
| **Export Manuel + Git** | Faible | Simple, rapide | Processus manuel, risque d'erreur |

## ✅ Checklist de Mise en Place

- [ ] Installer Power Platform CLI
- [ ] Se connecter à l'environnement Power Apps
- [ ] Initialiser le projet Git
- [ ] Exporter la solution initiale
- [ ] Configurer .gitignore
- [ ] Créer la structure de dossiers
- [ ] Créer les scripts d'export/import
- [ ] Documenter le workflow
- [ ] Former l'équipe
- [ ] Configurer les branches (main, dev, feature/*)

## 🚀 Prochaines Étapes

1. **Installer Power Platform CLI**
2. **Exporter votre solution actuelle**
3. **Initialiser Git** (déjà fait ✅)
4. **Créer les scripts d'automatisation**
5. **Configurer le workflow de collaboration**

## 📚 Ressources

- [Documentation Power Platform CLI](https://learn.microsoft.com/en-us/power-platform/developer/cli/introduction)
- [Git pour Power Apps](https://learn.microsoft.com/en-us/power-platform/alm/devops-build-tools)
- [Azure DevOps pour Power Apps](https://learn.microsoft.com/en-us/power-platform/alm/devops-build-tools)

---

**📅 Date :** 2026-01-14  
**✅ Guide d'intégration Git avec Power Apps complété**
