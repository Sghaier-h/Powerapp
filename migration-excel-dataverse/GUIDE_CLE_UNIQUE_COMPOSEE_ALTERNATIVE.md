# Guide : Clé Unique Composée - Méthode Alternative (Colonne Calculée)

## Problème : Erreur "Index size exceeded"

Lors de la création d'une clé unique composée sur plusieurs colonnes texte, vous pouvez recevoir l'erreur :

**"Index size exceeded the size limit of 1700 bytes. The key is too large. Try removing some columns or making the strings in string columns shorter."**

Cette erreur se produit lorsque la taille totale des colonnes dépasse 1700 bytes.

## Solution : Colonne Calculée + Clé Unique Simple

Au lieu de créer une clé unique composée directement sur plusieurs colonnes, utilisez cette méthode :

1. **Créer une colonne calculée** qui combine toutes les valeurs
2. **Créer une clé unique simple** sur cette colonne calculée
3. **Remplir automatiquement** cette colonne via Power Automate Flow

## Exemple 1 : Table Prix de Référence

### Objectif
Garantir qu'aucune combinaison identique de (Code Modèle + Code Dimensions) ne peut exister.

**Note :** Pour cette table, la clé unique composée directe fonctionne bien avec seulement 2 colonnes. La méthode alternative avec colonne calculée n'est nécessaire que si vous recevez l'erreur "Index size exceeded".

### Méthode Directe (Recommandée)

1. **Ouvrez la table "Prix de Référence"**

2. **Créez les colonnes** :
   - Modèle : Texte
   - Code Modèle : Texte
   - Code Dimensions : Texte

3. **Allez dans "Clés"** (dans le menu de la table)

4. **Cliquez sur "+ Ajouter clés"**

5. **Remplissez :**
   - **Nom** : `Clé_CodeModèle_CodeDimensions`
   - **Colonnes** : Sélectionner "Code Modèle", "Code Dimensions"
   - **Type** : Clé unique

6. **Enregistrez** et **publiez**

### Résultat

- La clé unique garantit qu'aucune combinaison identique de (Code Modèle + Code Dimensions) ne peut exister
- Exemples : "001-50x50" est unique, "001-60x60" est différent et autorisé

## Exemple 2 : Table Tarif Sous-Traitance

### Objectif
Garantir qu'aucune combinaison identique de (Sous-Traitant + Type Opération + Type Suivi + Type Deuxième + Date Effet) ne peut exister.

### Étape 1 : Créer la Colonne Calculée

1. **Ouvrez la table "Tarif Sous-Traitance"**

2. **Créez une nouvelle colonne** :
   - **Nom d'affichage** : `Clé Unique Combinée`
   - **Type de données** : Texte
   - **Requis** : Non
   - **Longueur maximale** : 500 caractères

3. **Enregistrez** la colonne

### Étape 2 : Créer le Power Automate Flow

**Déclencheur :** Lors de création ou modification d'un enregistrement dans la table "Tarif Sous-Traitance"

**Actions :**

1. **Initialiser une variable** : `CléCombinée` (Type : Texte)

2. **Composer la clé** :
   ```
   ID du Sous-Traitant (depuis la colonne Recherche) & "-" & 
   Type Opération (depuis l'enregistrement) & "-" & 
   Type Suivi (depuis l'enregistrement) & "-" & 
   Type Deuxième (depuis l'enregistrement) & "-" & 
   Date Effet formatée en texte (depuis l'enregistrement, format : YYYY-MM-DD HH:mm:ss)
   ```

3. **Mettre à jour l'enregistrement** :
   - Table : Tarif Sous-Traitance
   - ID : ID de l'enregistrement déclencheur
   - Colonne "Clé Unique Combinée" : Variable `CléCombinée`

**Note :** Pour extraire l'ID depuis une colonne Recherche, utilisez l'action "Obtenir les propriétés" ou accédez directement à la propriété `_soustraitant_value` dans Power Automate.

### Étape 3 : Créer la Clé Unique Simple

1. **Ouvrez la table "Tarif Sous-Traitance"**

2. **Allez dans "Clés"**

3. **Cliquez sur "+ Ajouter clés"**

4. **Remplissez :**
   - **Nom** : `Clé_Unique_Combinée`
   - **Colonnes** : Sélectionner uniquement "Clé Unique Combinée"
   - **Type** : Clé unique

5. **Enregistrez** et **publiez**

### Résultat

- La colonne "Clé Unique Combinée" sera automatiquement remplie à chaque création/modification
- La clé unique garantit qu'aucune combinaison identique ne peut exister
- Exemple de valeur : "12345-Ourlet-Première-Standard-2025-01-15 10:30:00"

## Avantages de cette Méthode

1. **Évite l'erreur de taille** : La colonne combinée est plus petite que plusieurs colonnes séparées
2. **Plus simple** : Une seule clé unique simple au lieu d'une clé composée
3. **Automatique** : Le Power Automate Flow remplit la colonne automatiquement
4. **Flexible** : Vous pouvez ajuster le format de la combinaison si nécessaire

## Points Importants

1. **La colonne calculée doit être remplie** avant de créer la clé unique
2. **Le Power Automate Flow doit être actif** pour que la colonne soit toujours à jour
3. **Le format de la combinaison** doit être cohérent (utiliser le même séparateur, ex: "-")
4. **Pour les colonnes Recherche**, extraire l'ID (GUID) plutôt que le nom d'affichage
5. **Pour les dates**, utiliser un format texte cohérent (ex: YYYY-MM-DD HH:mm:ss)

## Dépannage

### Problème : La colonne "Clé Unique Combinée" reste vide

**Solutions :**
1. Vérifiez que le Power Automate Flow est actif
2. Testez le Flow manuellement avec un enregistrement de test
3. Vérifiez les expressions dans le Flow (syntaxe correcte)
4. Vérifiez les permissions du Flow

### Problème : Erreur lors de la création de la clé unique

**Solutions :**
1. Vérifiez que la colonne "Clé Unique Combinée" contient des valeurs
2. Vérifiez qu'il n'y a pas de doublons dans cette colonne
3. Si des doublons existent, corrigez-les avant de créer la clé

### Problème : Le Flow ne se déclenche pas

**Solutions :**
1. Vérifiez que le Flow est activé
2. Vérifiez les permissions du Flow
3. Vérifiez que le déclencheur est correctement configuré
4. Testez le Flow manuellement

## Résumé Rapide

**Pour créer une clé unique composée avec cette méthode alternative :**

1. Créer une colonne texte "Clé Unique Combinée"
2. Créer un Power Automate Flow qui remplit cette colonne avec la combinaison des valeurs
3. Tester le Flow pour s'assurer qu'il fonctionne
4. Créer une clé unique simple sur la colonne "Clé Unique Combinée"
5. Publier la table

**Format de combinaison recommandé :**
- Utiliser "-" comme séparateur
- Pour les dates : Format YYYY-MM-DD HH:mm:ss
- Pour les colonnes Recherche : Utiliser l'ID (GUID)

---

**📅 Date :** 2026-01-14  
**✅ Guide de clé unique composée alternative complété**
