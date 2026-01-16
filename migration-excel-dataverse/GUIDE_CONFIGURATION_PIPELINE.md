# Guide : Configuration du Pipeline Azure DevOps / GitHub Actions

## ✅ Problème Résolu

**Erreur initiale :** `Could not read GitHub repository 'Sghaier-h/Powerapp' on ref 'main': Git Repository is empty.`

**Solution :** Le dépôt GitHub a été initialisé avec un commit initial. Le dépôt n'est plus vide.

## 🔍 Vérification

Le dépôt GitHub contient maintenant :
- ✅ README_POWERAPP.md
- ✅ migration-excel-dataverse/GUIDE_GIT_DATAVERSE_OFFICIEL.md
- ✅ migration-excel-dataverse/GUIDE_GIT_POWERAPPS.md
- ✅ Commits d'historique

## 🚀 Configuration du Pipeline

### Pour Azure DevOps

1. **Allez dans votre projet Azure DevOps**
2. **Pipelines** > **Nouveau pipeline**
3. **Sélectionnez "GitHub"** comme source
4. **Autorisez Azure DevOps** à accéder à votre dépôt GitHub
5. **Sélectionnez le dépôt** : `Sghaier-h/Powerapp`
6. **Branche** : `main`
7. **Configurez le pipeline** selon vos besoins

### Pour GitHub Actions

1. **Allez sur GitHub** : https://github.com/Sghaier-h/Powerapp
2. **Onglet "Actions"**
3. **"Set up a workflow yourself"** ou choisissez un template
4. **Créez le fichier** `.github/workflows/pipeline.yml`

## 📝 Exemple de Pipeline GitHub Actions

Créez le fichier `.github/workflows/powerapps-pipeline.yml` :

```yaml
name: Power Apps Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
    
    - name: Install dependencies
      run: |
        if [ -f package.json ]; then
          npm install
        fi
    
    - name: Run tests
      run: |
        echo "Tests à implémenter"
    
    - name: Build
      run: |
        echo "Build à implémenter"
```

## 📝 Exemple de Pipeline Azure DevOps

Créez un fichier `azure-pipelines.yml` à la racine :

```yaml
trigger:
  branches:
    include:
    - main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '18.x'
  displayName: 'Install Node.js'

- script: |
    if [ -f package.json ]; then
      npm install
    fi
  displayName: 'Install dependencies'

- script: |
    echo "Build et tests à implémenter"
  displayName: 'Build and Test'
```

## ✅ Vérification Post-Configuration

Après avoir configuré le pipeline :

1. **Vérifiez que le dépôt n'est plus vide** :
   ```bash
   git ls-remote https://github.com/Sghaier-h/Powerapp.git
   ```

2. **Testez le pipeline** :
   - Faites un petit changement
   - Commitez et poussez
   - Vérifiez que le pipeline se déclenche

## 🔄 Workflow Recommandé

1. **Développement** → Commit local
2. **Push vers GitHub** → Déclenche le pipeline
3. **Pipeline exécute** → Tests, build, déploiement
4. **Notification** → Succès ou échec

## 📚 Prochaines Étapes

1. ✅ Dépôt GitHub initialisé (fait)
2. ⏳ Configurer le pipeline selon vos besoins
3. ⏳ Ajouter les étapes de build/test
4. ⏳ Configurer le déploiement automatique (optionnel)

---

**📅 Date :** 2026-01-14  
**✅ Guide de configuration pipeline complété**
