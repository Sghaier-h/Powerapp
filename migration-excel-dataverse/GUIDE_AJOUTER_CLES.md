# Guide : Ajouter des Clés Uniques dans Power Apps

## Qu'est-ce qu'une Clé Unique ?

Une **clé unique** (Key) dans Dataverse/Power Apps garantit qu'aucune valeur en double ne peut être enregistrée sur une ou plusieurs colonnes.

**Exemples :**
- **Clé simple** : Une seule colonne (ex: Code Commercial) doit être unique
- **Clé composée** : Plusieurs colonnes ensemble (ex: Modèle + Code Modèle + Code Dimensions) doivent être uniques en combinaison

## Comment Ajouter une Clé Unique

### Étape 1 : Créer les Colonnes

1. **Ouvrez votre table** dans Power Apps
2. **Créez toutes les colonnes** nécessaires pour la clé
3. **Assurez-vous** que les colonnes existent avant d'ajouter la clé

### Étape 2 : Accéder à la Section Clés

1. **Ouvrez votre table** dans Power Apps
2. **Dans le menu de la table**, cherchez :
   - **"Clés"** ou **"Keys"**
   - OU dans les **"..."** (trois points) > **"Clés"** ou **"Keys"**

3. **Cliquez sur "+ Ajouter clés"** ou **"+ Add Keys"**

### Étape 3 : Configurer la Clé Unique

1. **Nom de la clé** : Donnez un nom descriptif
   - Exemple pour une clé simple : `Clé_Code_Commercial`
   - Exemple pour une clé composée : `Clé_Modèle_CodeModèle_CodeDimensions`

2. **Sélectionnez les colonnes** à inclure dans la clé :
   - Pour une clé simple : Sélectionnez une seule colonne
   - Pour une clé composée : Sélectionnez plusieurs colonnes

3. **Type de clé** : Sélectionnez **"Clé unique"** ou **"Unique Key"**

4. **Enregistrez** la clé
5. **Publiez** la table

## Exemple 1 : Clé Unique Simple

### Table : Article
### Colonne : Code Commercial

**Objectif :** Garantir qu'aucun article ne peut avoir le même code commercial qu'un autre article.

**Étapes :**

1. **Ouvrez la table "Article"**

2. **Créez la colonne "Code Commercial"** :
   - Type : Texte
   - Requis : Non (ou Oui selon vos besoins)

3. **Allez dans "Clés"** (dans le menu de la table)

4. **Cliquez sur "+ Ajouter clés"**

5. **Remplissez :**
   - **Nom** : `Clé_Code_Commercial`
   - **Colonnes** : Sélectionner "Code Commercial"
   - **Type** : Clé unique

6. **Enregistrez** et **publiez**

### Résultat

Aucun enregistrement ne pourra avoir la même valeur dans la colonne "Code Commercial".

## Exemple 2 : Clé Unique Composée

### Table : Prix de Référence
### Colonnes : Code Modèle + Code Dimensions

**Objectif :** Garantir qu'aucune combinaison identique de (Code Modèle + Code Dimensions) ne peut exister.

**Étapes :**

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

Aucun enregistrement ne pourra avoir la même combinaison de :
- Code Modèle + Code Dimensions

**Exemples :**
- ✅ Code Modèle="001", Code Dimensions="50x50" → OK
- ✅ Code Modèle="001", Code Dimensions="60x60" → OK (différent)
- ❌ Code Modèle="001", Code Dimensions="50x50" → ERREUR (déjà existe)

## Exemple 3 : Clé Unique Composée Complexe

### Table : Tarif Sous-Traitance
### Colonnes : Sous-Traitant + Type Opération + Type Suivi + Type Deuxième + Date Effet

**Objectif :** Garantir qu'aucune combinaison identique de ces cinq colonnes ne peut exister (permet de gérer l'historique des tarifs).

**⚠️ IMPORTANT :** Avec 5 colonnes, vous recevrez probablement l'erreur "Index size exceeded". Utilisez la méthode alternative avec une colonne calculée. Voir le guide GUIDE_CLE_UNIQUE_COMPOSEE_ALTERNATIVE.md pour les instructions détaillées.

**Méthode Alternative (recommandée pour 5 colonnes) :**

1. Créer une colonne texte "Clé Unique Combinée"
2. Créer un Power Automate Flow qui remplit cette colonne avec : ID Sous-Traitant + "-" + Type Opération + "-" + Type Suivi + "-" + Type Deuxième + "-" + Date Effet (format texte)
3. Créer une clé unique simple sur "Clé Unique Combinée"

Voir GUIDE_CLE_UNIQUE_COMPOSEE_ALTERNATIVE.md pour les instructions complètes.

### Résultat

Aucun enregistrement ne pourra avoir la même combinaison de :
- Sous-Traitant + Type Opération + Type Suivi + Type Deuxième + Date Effet

Cela permet de gérer l'historique des tarifs : un même sous-traitant peut avoir plusieurs tarifs pour la même opération, mais avec des dates d'effet différentes.

## Localisation dans l'Interface Power Apps

### Où Trouver "Clés" ou "Keys"

L'option "Clés" se trouve généralement :

1. **Dans le menu de la table** (à gauche ou en haut)
   - Section "Clés" ou "Keys"

2. **Dans les propriétés de la table**
   - Cliquez sur "..." (trois points) > "Clés" ou "Keys"

3. **Dans l'onglet principal de la table**
   - Parfois il y a un onglet "Clés" visible directement

### Si vous ne trouvez pas "Clés"

**Vérifications :**

1. **Vérifiez vos permissions** :
   - Vous devez avoir le rôle "System Administrator" ou "System Customizer"
   - Voir le guide GUIDE_PERMISSIONS_ADMINISTRATEUR.md pour plus de détails

2. **Cherchez "Keys"** (en anglais) si l'interface est en anglais

3. **Vérifiez la version** de Power Apps (certaines versions peuvent avoir des limitations)

4. **Contactez votre administrateur** si nécessaire

## Différence entre Clé Unique et Index Unique

- **Clé unique (Key)** : Contrainte d'intégrité qui garantit l'unicité. Plus directe et simple à utiliser.
- **Index unique** : Index de base de données qui améliore les performances ET garantit l'unicité. Plus complexe à configurer.

**Recommandation :** Utilisez "Ajouter clés" pour les contraintes d'unicité. C'est plus simple et plus direct.

## Vérification

Pour vérifier qu'une clé unique est bien créée :

1. **Ouvrez la table**
2. **Allez dans "Clés"**
3. **Vous devriez voir** votre clé avec :
   - Le nom de la clé
   - Les colonnes sélectionnées
   - Le type "Clé unique"

4. **Testez** en essayant de créer deux enregistrements avec la même valeur (ou combinaison)
5. **Vous devriez recevoir une erreur** indiquant que la valeur doit être unique

## Points Importants

1. **Toutes les colonnes doivent exister** avant d'ajouter la clé
2. **La clé unique vérifie l'unicité** de la valeur ou de la combinaison
3. **Les valeurs NULL** peuvent être autorisées ou non selon la configuration
4. **Une fois créée**, la clé unique empêche les doublons automatiquement
5. **Vous ne pouvez pas modifier** une clé unique une fois créée (il faut la supprimer et la recréer)

## Dépannage

### Problème : Je ne trouve pas l'option "Clés"

**Solutions :**

1. **Vérifiez vos permissions** :
   - Vérifiez si vous avez le rôle "System Administrator"
   - Si non, demandez à votre administrateur de vous l'ajouter
   - Voir GUIDE_PERMISSIONS_ADMINISTRATEUR.md pour les instructions détaillées

2. **Cherchez dans les propriétés avancées** de la table

3. **Contactez votre administrateur** Power Apps pour obtenir les permissions

### Problème : Erreur lors de la création de la clé

**Causes possibles :**

1. **Des doublons existent déjà** dans les colonnes
   - **Solution :** Supprimez ou corrigez les doublons avant de créer la clé

2. **Des valeurs NULL** dans les colonnes
   - **Solution :** Remplissez toutes les valeurs NULL ou configurez la clé pour autoriser NULL

3. **Permissions insuffisantes**
   - **Solution :** Vérifiez vos permissions ou contactez l'administrateur

4. **Une clé similaire existe déjà**
   - **Solution :** Vérifiez les clés existantes et supprimez-les si nécessaire

## Résumé Rapide

**Pour ajouter une clé unique :**

1. Créer toutes les colonnes nécessaires
2. Ouvrir la table > Aller dans "Clés"
3. Cliquer sur "+ Ajouter clés"
4. Donner un nom à la clé
5. Sélectionner les colonnes (une pour clé simple, plusieurs pour clé composée)
6. Sélectionner "Clé unique" comme type
7. Enregistrer et publier

**Exemples :**
- Clé simple : Code Commercial dans la table Article
- Clé composée : Code Modèle + Code Dimensions dans la table Prix de Référence

---

**📅 Date :** 2026-01-14  
**✅ Guide d'ajout de clés uniques complété**
