# Instruction pour Copilot : Création des Tables Dataverse

## Contexte du Projet

Projet : Migration Excel vers Dataverse et Power Apps
Organisation : La Plume Artisanale
Solution Power Apps : La Plume Artisanale
Total de tables à créer : 37 tables

IMPORTANT : Avant de créer les tables, vous devez configurer le préfixe lpa dans Power Apps. Voir le guide GUIDE_CONFIGURATION_PREFIXE_LPA.md pour les instructions détaillées.

## Objectif

Créer toutes les 37 tables Dataverse nécessaires pour le système de production textile, organisées en 10 phases, avec toutes les colonnes, relations, choix options, et clés uniques requis.

## Instructions Générales

1. Créer les tables dans l'ordre des phases (Phase 1 puis Phase 2, etc.)
2. Pour chaque table, utiliser le nom d'affichage exact indiqué
3. Le système générera automatiquement le nom logique avec le préfixe lpa
4. Créer toutes les colonnes listées pour chaque table
5. Configurer les choix options avec les valeurs exactes indiquées
6. Configurer les relations après avoir créé les deux tables concernées
7. Publier chaque table après création

## Phase 1 : Tables de Référence

### Table 1 : Opérateur

Nom d'affichage : Opérateur
Pluriel : Opérateurs
Clé primaire : Code (colonne texte, unique, requis)

Colonnes à créer :
- Nom : Texte, Requis
- Code : Texte, Requis, Unique, Clé primaire
- Rôle : Choix, Requis
  Valeurs du choix Rôle : Tisseur, Coupeur, Magasinier, Superviseur, Administrateur
- Parc : Choix
  Valeurs du choix Parc : Parc01, Parc02, Parc03, Dimatex, Neji
- Actif : Oui/Non, Requis, Valeur par défaut : Oui

---

### Table 2 : Machine

Nom d'affichage : Machine
Pluriel : Machines
Clé primaire : Num Machine (colonne texte, unique, requis)

Colonnes à créer :
- Num Machine : Texte, Requis, Unique, Clé primaire
- Numéro de série : Texte
- Type Machine : Choix, Requis
  Valeurs du choix Type Machine : CADRE, JACQUARD, ÉPONGE
- Parc : Choix
  Valeurs du choix Parc : Parc01, Parc02, Parc03, Dimatex, Neji
- État : Choix, Requis
  Valeurs du choix État : En fonction, Arrêt, Maintenance
- Laize : Nombre entier
- Vitesse : Nombre entier
- Nombre Sélecteurs : Nombre entier
- Num Série Ratière : Texte
- Type Ratière : Texte
- Système : Texte
- Unité : Texte
- Laize Machine : Nombre
- Laize Actuelle : Nombre
- Longueur Peigne : Nombre
- Nombre Fil Par Cm : Nombre
- Nombre Fil Chaine : Nombre
- Sélecteur Couleur Installé : Texte
- Cable Satin : Texte
- Type de Programme : Texte
- Vitesse Duite par Minute : Nombre
- Compteur : Nombre
- Unité Compteur : Texte

---

### Table 3 : Client

Nom d'affichage : Client
Pluriel : Clients
Clé primaire : Code Client (colonne texte, unique, requis)

Colonnes à créer :
- Code Client : Texte, Requis, Unique, Clé primaire
- Nom Client : Texte, Requis
- Adresse : Texte multiligne
- Téléphone : Texte
- Email : Email
- Actif : Oui/Non, Requis, Valeur par défaut : Oui

---

### Table 4 : Sous-Traitant

Nom d'affichage : Sous-Traitant
Pluriel : Sous-Traitants
Clé primaire : Nom Sous-Traitant (colonne texte, unique, requis)

Colonnes à créer :
- Nom Sous-Traitant : Texte, Requis, Unique, Clé primaire
- Code Sous-Traitant : Texte
- Type Opération : Choix
  Valeurs du choix Type Opération : Ourlet, Repassage, Autre
- Adresse : Texte multiligne
- Actif : Oui/Non, Requis, Valeur par défaut : Oui
- Prénom : Texte
- Num Téléphone : Texte
- Recto CIN : Image
- Verso CIN : Image
- Total Sortis : Nombre, Calculé
- Total Retour : Nombre, Calculé
- Reste A Retourner : Nombre, Calculé

---

### Table 5 : Entrepôt

Nom d'affichage : Entrepôt
Pluriel : Entrepôts
Clé primaire : Code Entrepôt (colonne texte, unique, requis)

Colonnes à créer :
- Code Entrepôt : Texte, Requis, Unique, Clé primaire
- Nom Entrepôt : Texte, Requis
- Type Entrepôt : Choix, Requis
  Valeurs du choix Type Entrepôt : Usine, Magasin, Sous-Traitant
- Adresse : Texte multiligne
- Actif : Oui/Non, Requis, Valeur par défaut : Oui
- Responsable : Texte

IMPORTANT : Créer d'abord l'entrepôt Usine avec code USINE

---

## Phase 2 : Tables Articles et Catalogue

### Table 6 : Article de Référence

Nom d'affichage : Article de Référence
Pluriel : Articles de Référence
Clé primaire : Ref Fabrication (colonne texte, unique, requis)

Colonnes à créer :
- Ref Fabrication : Texte, Requis, Unique, Clé primaire
- Code Commercial : Texte
- Modèle : Texte
- Dimensions : Texte
- Nombre Couleur : Nombre entier
- Sélecteur 01 : Texte
- Sélecteur 02 : Texte
- Sélecteur 03 : Texte
- Sélecteur 04 : Texte
- Sélecteur 05 : Texte
- Sélecteur 06 : Texte
- Description : Texte multiligne
- Actif : Oui/Non, Requis, Valeur par défaut : Oui

Clé unique à ajouter : Dans la table Article, aller dans la section Clés (Keys), cliquer sur "Ajouter clés" ou "Add Keys", créer une nouvelle clé unique nommée "Clé_Code_Commercial", sélectionner la colonne Code Commercial, et enregistrer. Cette clé garantit qu'aucun article ne peut avoir le même code commercial qu'un autre article.

---

### Table 7 : Caractéristique

Nom d'affichage : Caractéristique
Pluriel : Caractéristiques
Clé primaire : Dimensions (colonne texte, unique, requis)

Colonnes à créer :
- Dimensions : Texte, Requis, Unique, Clé primaire
- Code Dimensions : Texte
- Largeur : Nombre
- Longueur : Nombre

---

### Table 8 : Prix de Référence

Nom d'affichage : Prix de Référence
Pluriel : Prix de Référence
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée) (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Modèle : Texte, Requis
- Code Modèle : Texte
- Code Dimensions : Texte
- Prix Revient : Monnaie
- Prix Vente : Monnaie

Clé unique composée à ajouter : Dans la table Prix de Référence, aller dans la section Clés (Keys), cliquer sur "Ajouter clés" ou "Add Keys", créer une nouvelle clé unique nommée "Clé_CodeModèle_CodeDimensions", sélectionner les deux colonnes (Code Modèle, Code Dimensions), et enregistrer. Cette clé garantit qu'aucune combinaison identique de ces deux colonnes ne peut exister.

---

### Table 9 : Bill of Materials

Nom d'affichage : Bill of Materials
Pluriel : Bills of Materials
Clé primaire : Code Paramétrage (colonne texte, unique, requis)

Colonnes à créer :
- Code Paramétrage : Texte, Requis, Unique, Clé primaire
- Produit : Texte
- Modèle : Texte
- Code Dimensions : Texte
- Type Finition : Texte
- Type Fabrication : Texte
- Nombre Couleur : Nombre entier
- Actif : Oui/Non, Requis, Valeur par défaut : Oui

---

### Table 10 : Composant BOM

Nom d'affichage : Composant BOM
Pluriel : Composants BOM
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- BOM : Recherche vers table Bill of Materials, Requis
- ID Composant : Texte, Requis
- Qté par Unité : Nombre, Requis
- Description : Texte multiligne
- Dimensions : Texte
- Largeur Tissage : Nombre
- Longueur Tissage : Nombre
- Duites par CM : Nombre
- Consommation S01 : Nombre
- Consommation S02 : Nombre
- Consommation S03 : Nombre
- Consommation S04 : Nombre
- Consommation S05 : Nombre
- Consommation S06 : Nombre
- Consommation S07 : Nombre
- Consommation S08 : Nombre

Relation à créer : Dans la table Composant BOM, créer une colonne de type Recherche nommée "BOM" qui pointe vers la table Bill of Materials. Cette relation est obligatoire pour lier les composants à leur BOM parent.

---

## Phase 3 : Tables Production

### Table 11 : Ordre de Fabrication

Nom d'affichage : Ordre de Fabrication
Pluriel : Ordres de Fabrication
Clé primaire : Num OF (colonne texte, unique, requis)

Colonnes à créer :
- Num OF : Texte, Requis, Unique, Clé primaire
- Modèle : Texte
- Code Commercial : Texte
- Article : Recherche vers table Article de Référence
- Quantité : Nombre, Requis
- Quantité Fabriquée : Nombre
- Statut : Choix, Requis
  Valeurs du choix Statut : En attente, En cours, Terminé, Annulé
- Date Livraison : Date et heure
- Priorité : Choix
  Valeurs du choix Priorité : Haute, Normale, Basse
- Client : Recherche vers table Client
- Machine : Recherche vers table Machine
- Imprimé : Oui/Non, Valeur par défaut : Non
- Date Impression : Date et heure
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relations à créer :
- Dans la table Ordre de Fabrication, créer une colonne de type Recherche nommée "Client" qui pointe vers la table Client
- Dans la table Ordre de Fabrication, créer une colonne de type Recherche nommée "Machine" qui pointe vers la table Machine
- Dans la table Ordre de Fabrication, créer une colonne de type Recherche nommée "Article" qui pointe vers la table Article de Référence

Note : Les relations se créent du côté de la table enfant (Ordre de Fabrication). Le nom d'affichage de la colonne de recherche peut être le nom simple de la table parente (Client, Machine, Article). Les relations sont obligatoires pour utiliser les fonctionnalités de recherche et filtrage dans Power Apps.

---

### Table 12 : Sous-OF

Nom d'affichage : Sous-OF
Pluriel : Sous-OF
Clé primaire : Num Sous-OF (colonne texte, unique, requis)

Colonnes à créer :
- Num Sous-OF : Texte, Requis, Unique, Clé primaire
- OF : Recherche vers table Ordre de Fabrication, Requis
- Suffixe : Texte
- Composant : Texte
- Quantité : Nombre, Requis
- Pièces par Package : Nombre, Requis
- Statut : Choix, Requis
  Valeurs du choix Statut : En attente, En cours, Terminé
- Plié : Oui/Non, Valeur par défaut : Non
- Date Pliage : Date et heure
- Emballé : Oui/Non, Valeur par défaut : Non
- Date Emballage : Date et heure
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relation à créer : Dans la table Sous-OF, créer une colonne de type Recherche nommée "OF" qui pointe vers la table Ordre de Fabrication. Cette relation est obligatoire pour lier les sous-OF à leur ordre de fabrication parent.

---

### Table 13 : Numéro de Tissage

Nom d'affichage : Numéro de Tissage
Pluriel : Numéros de Tissage
Clé primaire : Num Tissage (colonne texte, unique, requis)

Colonnes à créer :
- Num Tissage : Texte, Requis, Unique, Clé primaire
- Sous-OF : Recherche vers table Sous-OF, Requis
- Machine : Recherche vers table Machine
- Opérateur : Recherche vers table Opérateur
- Métrage : Nombre
- Statut : Choix, Requis
  Valeurs du choix Statut : En cours, Terminé, Annulé
- Date Début : Date et heure
- Date Fin : Date et heure
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relation à créer : Dans la table Numéro de Tissage, créer une colonne de type Recherche nommée "Sous-OF" qui pointe vers la table Sous-OF. Cette relation est obligatoire pour lier les numéros de tissage à leur sous-OF parent.

---

### Table 14 : Opération Tissage

Nom d'affichage : Opération Tissage
Pluriel : Opérations Tissage
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Num Tissage : Recherche vers table Numéro de Tissage, Requis
- Type Opération : Choix, Requis
  Valeurs du choix Type Opération : Départ, Pause, Reprise, Terminé, Autre
- Machine : Recherche vers table Machine
- Opérateur : Recherche vers table Opérateur
- Compteur : Nombre
- Date : Date et heure, Requis
- Note : Texte multiligne
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relation à créer : Dans la table Opération Tissage, créer une colonne de type Recherche nommée "Num Tissage" qui pointe vers la table Numéro de Tissage. Cette relation est obligatoire pour lier les opérations à leur numéro de tissage parent.

---

### Table 15 : Opération Coupe

Nom d'affichage : Opération Coupe
Pluriel : Opérations Coupe
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Num Tissage : Recherche vers table Numéro de Tissage, Requis
- Quantité Totale Coupée : Nombre, Requis
- Quantité Deuxième : Nombre
- Quantité Surplus : Nombre
- Statut Surplus : Choix
  Valeurs du choix Statut Surplus : Standard, Erreur Couleur, Erreur Dimensions
- Déchet : Nombre
- Ourlet : Nombre
- Deuxième Approuvée : Nombre
- Opérateur : Recherche vers table Opérateur
- Date : Date et heure, Requis
- Statut : Choix, Requis
  Valeurs du choix Statut : En cours, Terminé
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relation à créer : Dans la table Opération Coupe, créer une colonne de type Recherche nommée "Num Tissage" qui pointe vers la table Numéro de Tissage. Cette relation est obligatoire pour lier les opérations de coupe à leur numéro de tissage parent.

---

### Table 16 : Étiquette de Suivis

Nom d'affichage : Étiquette de Suivis
Pluriel : Étiquettes de Suivis
Clé primaire : Num Suivis (colonne texte, unique, requis)

Colonnes à créer :
- Num Suivis : Texte, Requis, Unique, Clé primaire
- Sous-OF : Recherche vers table Sous-OF, Requis
- Quantité : Nombre, Requis
- Type Suivi : Choix, Requis
  Valeurs du choix Type Suivi : Première, Deuxième
- Date Création : Date et heure, Requis
- Statut : Choix, Requis
  Valeurs du choix Statut : Créé, En cours, Terminé
- Opérateur : Recherche vers table Opérateur

Format Num Suivis : OF250222-1 pour Première ou OF250222-Deu-1 pour Deuxième

Relation à créer : Dans la table Étiquette de Suivis, créer une colonne de type Recherche nommée "Sous-OF" qui pointe vers la table Sous-OF. Cette relation est obligatoire pour lier les étiquettes à leur sous-OF parent.

---

## Phase 4 : Tables Matières Premières

### Table 17 : QR Code Matière Première

Nom d'affichage : QR Code Matière Première
Pluriel : QR Codes Matières Premières
Clé primaire : QR MP (colonne texte, unique, requis)

Colonnes à créer :
- QR MP : Texte, Requis, Unique, Clé primaire
- Nom MP : Texte
- Code MP : Texte
- Couleur : Texte
- Stock E1 : Nombre, Calculé
- Stock E2 : Nombre, Calculé
- Stock E3 : Nombre, Calculé
- Stock Usine : Nombre, Calculé
- Stock Fabrication : Nombre, Calculé
- Stock Final : Nombre, Calculé
- Réservé : Nombre
- Stock Disponible : Nombre, Calculé
- Stock Minimal : Nombre
- Stock Maximal : Nombre
- Entrepôt : Choix
  Valeurs du choix Entrepôt : E1, E2, E3, Usine, Fabrication
- Statut : Choix, Requis
  Valeurs du choix Statut : Disponible, Réservé, Épuisé

---

### Table 18 : Mouvement Matière Première

Nom d'affichage : Mouvement Matière Première
Pluriel : Mouvements Matières Premières
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- QR MP : Recherche vers table QR Code Matière Première, Requis
- Type Opération : Choix, Requis
  Valeurs du choix Type Opération : Réception, Transfert, Sortie, Inventaire, Autre
- Départ : Choix, Requis
  Valeurs du choix Départ : E1, E2, E3, Usine, Fabrication
- Destination : Choix, Requis
  Valeurs du choix Destination : E1, E2, E3, Usine, Fabrication
- Poids : Nombre, Requis
- Num OF : Recherche vers table Ordre de Fabrication
- Sélecteur : Choix
  Valeurs du choix Sélecteur : S01, S02, S03, S04, S05, S06, S07, S08
- Opérateur : Recherche vers table Opérateur
- Terminal : Texte
- Date : Date et heure, Requis
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relations à créer :
- Dans la table Mouvement Matière Première, créer une colonne de type Recherche nommée "QR MP" qui pointe vers la table QR Code Matière Première. Cette relation est obligatoire.
- Dans la table Mouvement Matière Première, créer une colonne de type Recherche nommée "Num OF" qui pointe vers la table Ordre de Fabrication. Cette relation est optionnelle mais recommandée.

---

## Phase 5 : Tables Sous-Traitance

### Table 19 : Mouvement Sous-Traitance

Nom d'affichage : Mouvement Sous-Traitance
Pluriel : Mouvements Sous-Traitance
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Num OF : Recherche vers table Ordre de Fabrication, Requis
- Num Suivis : Texte, Requis
- Sous-Traitant : Texte, Requis
- Type Opération : Choix, Requis
  Valeurs du choix Type Opération : Sortie, Retour
- Type Suivi : Choix, Requis
  Valeurs du choix Type Suivi : Première, Deuxième
- Type Deuxième : Choix
  Valeurs du choix Type Deuxième : Standard, Erreur Couleur, Erreur Dimensions
- Qté Sortis : Nombre
- Qté Retour : Nombre
- Date : Date et heure, Requis
- Opérateur : Recherche vers table Opérateur
- Ref Fabrication : Texte
- Description : Texte multiligne
- Dimensions : Texte
- Num Commande : Texte
- Num Client : Texte
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relation à créer : Dans la table Mouvement Sous-Traitance, créer une colonne de type Recherche nommée "Num OF" qui pointe vers la table Ordre de Fabrication. Cette relation est obligatoire pour lier les mouvements à leur ordre de fabrication.

---

### Table 20 : Qualité Sous-Traitance

Nom d'affichage : Qualité Sous-Traitance
Pluriel : Qualités Sous-Traitance
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Num OF : Recherche vers table Ordre de Fabrication, Requis
- Num Suivis : Texte, Requis
- Sous-Traitant : Texte, Requis
- Type Opération : Choix, Requis
  Valeurs du choix Type Opération : Ourlet, Repassage, Autre
- Type Suivi : Choix, Requis
  Valeurs du choix Type Suivi : Première, Deuxième
- Type Deuxième : Choix
  Valeurs du choix Type Deuxième : Standard, Erreur Couleur, Erreur Dimensions
- Deuxième Externe : Nombre
- Deuxième Approuvée : Nombre
- Ourlet : Nombre
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)

Relation à créer : Dans la table Qualité Sous-Traitance, créer une colonne de type Recherche nommée "Num OF" qui pointe vers la table Ordre de Fabrication. Cette relation est obligatoire pour lier les contrôles qualité à leur ordre de fabrication.

---

### Table 21 : Tarif Sous-Traitance

Nom d'affichage : Tarif Sous-Traitance
Pluriel : Tarifs Sous-Traitance
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Sous-Traitant : Recherche vers table Sous-Traitant, Requis
- Type Opération : Choix, Requis
  Valeurs du choix Type Opération : Ourlet, Repassage, Autre
- Type Suivi : Choix, Requis
  Valeurs du choix Type Suivi : Première, Deuxième
- Type Deuxième : Choix
  Valeurs du choix Type Deuxième : Standard, Erreur Couleur, Erreur Dimensions
- Prix Unitaire : Monnaie, Requis
- Date Effet : Date et heure, Requis
- Date Fin : Date et heure
- Actif : Oui/Non, Requis, Valeur par défaut : Oui
- Description : Texte multiligne
- Remarque : Texte multiligne
- Clé Unique Combinée : Texte, Longueur maximale 500 caractères, Requis Non (cette colonne sera remplie automatiquement via Power Automate Flow, voir note ci-dessous)

Relation à créer : Dans la table Tarif Sous-Traitance, créer une colonne de type Recherche nommée "Sous-Traitant" qui pointe vers la table Sous-Traitant. Cette relation est obligatoire pour lier les tarifs à leur sous-traitant.

Note importante : Pour éviter l'erreur "Index size exceeded", au lieu de créer une clé unique composée directement sur plusieurs colonnes, créer une colonne texte "Clé Unique Combinée" (Type : Texte, Longueur maximale : 500 caractères, Requis : Non). Cette colonne sera remplie automatiquement via un Power Automate Flow lors de la création/modification d'un enregistrement avec la formule : ID du Sous-Traitant (depuis la colonne Recherche, extraire le GUID) + "-" + Type Opération + "-" + Type Suivi + "-" + Type Deuxième + "-" + Date Effet formatée en texte (format : YYYY-MM-DD HH:mm:ss). Ensuite, créer une clé unique simple sur cette colonne "Clé Unique Combinée" dans la section Clés (Keys) de la table. Voir le guide GUIDE_CLE_UNIQUE_COMPOSEE_ALTERNATIVE.md pour les instructions détaillées sur la création du Power Automate Flow. Cette méthode garantit qu'aucune combinaison identique de (Sous-Traitant + Type Opération + Type Suivi + Type Deuxième + Date Effet) ne peut exister (permet de gérer l'historique des tarifs).

---

### Table 22 : Suivi Sous-Traitance (OPTIONNEL)

Nom d'affichage : Suivi Sous-Traitance
Pluriel : Suivis Sous-Traitance
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Description : Table pré-calculée pour améliorer les performances

Colonnes à créer :
- Num OF : Recherche vers table Ordre de Fabrication, Requis
- Sous-Traitant : Texte, Requis
- Type Opération : Choix, Requis
- Type Suivi : Choix, Requis
- Année : Nombre
- Mois : Nombre
- Semaine : Nombre
- Qté Fabriquée : Nombre
- Total Sortis : Nombre
- Total Retour : Nombre
- Reste A Retourner : Nombre
- Deuxième Externe : Nombre
- Deuxième Approuvée : Nombre
- Ourlet : Nombre
- Alerte Interne : Choix
  Valeurs du choix Alerte Interne : Erreur Saisie, A Vérifier, Reste à Sortir, Tout Sorti, Pas de Coupe, Non Défini
- Alerte Sous-Traitant : Choix
  Valeurs du choix Alerte Sous-Traitant : Retourné, Danger, Alerte, Retard, Attention, En Cours, Non Défini
- Prix Unitaire : Monnaie
- Prix Total Calculé : Monnaie

Relation à créer : Dans la table Suivi Sous-Traitance, créer une colonne de type Recherche nommée "Num OF" qui pointe vers la table Ordre de Fabrication. Cette relation est obligatoire. Note : Cette table est optionnelle (pré-calculée pour performance).

---

## Phase 6 : Tables Stocks et Transferts

### Table 23 : Stock Entrepôt

Nom d'affichage : Stock Entrepôt
Pluriel : Stocks Entrepôts
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Entrepôt : Recherche vers table Entrepôt, Requis
- Article : Recherche vers table Article de Référence
- Num Tissage : Recherche vers table Numéro de Tissage
- Num Suivis : Texte
- Quantité Disponible : Nombre, Requis
- Quantité Réservée : Nombre
- Quantité Totale : Nombre
- Type Suivi : Choix, Requis
  Valeurs du choix Type Suivi : Première, Deuxième, Deuxième Erreur Couleur, Deuxième Erreur Dimensions
- Type Deuxième : Choix
  Valeurs du choix Type Deuxième : Standard, Erreur Couleur, Erreur Dimensions
- Date Dernière Entrée : Date et heure
- Date Dernière Sortie : Date et heure
- Prix Unitaire : Monnaie
- Valeur Stock : Monnaie

Relations à créer :
- Dans la table Stock Entrepôt, créer une colonne de type Recherche nommée "Entrepôt" qui pointe vers la table Entrepôt. Cette relation est obligatoire.
- Dans la table Stock Entrepôt, créer une colonne de type Recherche nommée "Article" qui pointe vers la table Article de Référence. Cette relation est optionnelle mais recommandée.

---

### Table 24 : Transfert Entrepôt

Nom d'affichage : Transfert Entrepôt
Pluriel : Transferts Entrepôts
Clé primaire : Num Transfert (colonne texte, unique, requis)

Colonnes à créer :
- Num Transfert : Texte, Requis, Unique, Clé primaire
- Entrepôt Origine : Recherche vers table Entrepôt, Requis
- Entrepôt Destination : Recherche vers table Entrepôt, Requis
- Article : Recherche vers table Article de Référence
- Num Suivis : Texte
- Quantité : Nombre, Requis
- Type Transfert : Choix, Requis
  Valeurs du choix Type Transfert : Retour Sous-Traitant, Réapprovisionnement, Réallocation
- Date Demande : Date et heure, Requis
- Date Expédition : Date et heure
- Date Réception : Date et heure
- Statut : Choix, Requis
  Valeurs du choix Statut : Demandé, En Transit, Reçu, Annulé
- Opérateur Expéditeur : Recherche vers table Opérateur
- Opérateur Destinataire : Recherche vers table Opérateur
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)
- Type : Choix
  Valeurs du choix Type : Retour Sous-Traitant, Réapprovisionnement, Réallocation
- Mouvement : Texte
- Ref Commercial : Recherche vers table Article de Référence
- Modèle : Texte

Format Num Transfert : TRF-2025-001
Relations à créer :
- Dans la table Transfert Entrepôt, créer une colonne de type Recherche nommée "Entrepôt Origine" qui pointe vers la table Entrepôt. Cette relation est obligatoire.
- Dans la table Transfert Entrepôt, créer une colonne de type Recherche nommée "Entrepôt Destination" qui pointe vers la table Entrepôt. Cette relation est obligatoire.

---

## Phase 7 : Tables Produits Finis

### Table 25 : Commande

Nom d'affichage : Commande
Pluriel : Commandes
Clé primaire : Num Commande (colonne texte, unique, requis)

Colonnes à créer :
- Num Commande : Texte, Requis, Unique, Clé primaire
- Client : Recherche vers table Client, Requis
- Date Commande : Date et heure, Requis
- Date Livraison Prévue : Date et heure
- Quantité : Nombre, Requis
- Quantité Emballée : Nombre
- Statut : Choix, Requis
  Valeurs du choix Statut : En attente, En cours, Emballée, Expédiée, Annulée
- Priorité : Choix
  Valeurs du choix Priorité : Haute, Normale, Basse
- Remarque : Texte multiligne

Relation à créer : Dans la table Commande, créer une colonne de type Recherche nommée "Client" qui pointe vers la table Client. Cette relation est obligatoire pour lier les commandes à leur client.

---

### Table 26 : Colisage

Nom d'affichage : Colisage
Pluriel : Colisages
Clé primaire : Num Colis (colonne texte, unique, requis)

Colonnes à créer :
- Num Colis : Texte, Requis, Unique, Clé primaire
- QR Commande : Texte
- Num Suivis : Texte
- Quantité : Nombre, Requis
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)
- Note : Texte multiligne
- Terminal : Texte
- Date : Date et heure, Requis
- Emplacement : Texte
- Facture Export : Texte
- Bon de Livraison : Texte
- ID Commande : Recherche vers table Commande
- Num Client : Recherche vers table Client
- Ref Commercial : Recherche vers table Article de Référence
- Modèle : Texte
- Dimensions : Texte

Relations à créer :
- Dans la table Colisage, créer une colonne de type Recherche nommée "ID Commande" qui pointe vers la table Commande. Cette relation est optionnelle mais recommandée.
- Dans la table Colisage, créer une colonne de type Recherche nommée "Num Client" qui pointe vers la table Client. Cette relation est optionnelle mais recommandée.
- Dans la table Colisage, créer une colonne de type Recherche nommée "Ref Commercial" qui pointe vers la table Article de Référence. Cette relation est optionnelle mais recommandée.

---

### Table 27 : Palette

Nom d'affichage : Palette
Pluriel : Palettes
Clé primaire : Num Palette (colonne texte, unique, requis)

Colonnes à créer :
- Num Palette : Texte, Requis, Unique, Clé primaire
- Num Colis : Recherche vers table Colisage
- Num Facture Export : Texte
- Transporteur : Texte
- Date Création : Date et heure, Requis
- Date Expédition : Date et heure
- Statut : Choix, Requis
  Valeurs du choix Statut : En cours, Complète, Expédiée
- Nombre Colis : Nombre, Calculé
- Opérateur : Recherche vers table Opérateur
- Remarque : Texte multiligne
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)
- Terminale : Texte

Format Num Palette : PAL-001
Relation à créer : Dans la table Palette, créer une colonne de type Recherche nommée "Num Colis" qui pointe vers la table Colisage. Cette relation est optionnelle mais recommandée pour lier les palettes aux colis.

---

## Phase 8 : Tables Utilitaires

### Table 28 : Journal des Erreurs

Nom d'affichage : Journal des Erreurs
Pluriel : Journaux des Erreurs
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Date Heure : Date et heure, Requis
- Poste : Choix, Requis
  Valeurs du choix Poste : Secrétariat, MP Préparation, Tissage, Coupe, Magasin Sous-Traitant, Pliage/Emballage, Magasinier MP, Magasinier Produits Finis
- Opérateur : Recherche vers table Opérateur
- Type Erreur : Choix, Requis
  Valeurs du choix Type Erreur : Scan double, Retour sans sortie, Quantité incohérente, QR code invalide, Date incohérente, Opération logique invalide, Autre
- Message : Texte multiligne, Requis
- Données : Texte multiligne (JSON)
- Résolue : Oui/Non, Requis, Valeur par défaut : Non
- Date Résolution : Date et heure
- Résolution : Texte multiligne

---

## Phase 9 : Tables Supplémentaires Identifiées

### Table 29 : Mouvement Fourniture

Nom d'affichage : Mouvement Fourniture
Pluriel : Mouvements Fournitures
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- QR Fourniture : Recherche vers table Fourniture, Requis
- Type Opération : Choix, Requis
  Valeurs du choix Type Opération : Entrée, Sortie
- Qte Entrée : Nombre
- Qte Sortis : Nombre
- Photo : URL (dans Power Apps, sélectionner le type "URL" sous "Une seule ligne de texte" dans la liste des types de données. Si le type "Image" est disponible dans votre version, utilisez-le à la place. Sinon, utilisez "URL" pour stocker les liens vers les images stockées dans SharePoint, OneDrive, ou autre stockage cloud)
- Note : Texte multiligne
- Terminal : Texte
- Date : Date et heure, Requis
- ID Commande : Recherche vers table Commande
- Num Client : Recherche vers table Client
- Type : Texte
- Référence : Texte
- Libellé : Texte

Relations :
- Fourniture vers Mouvement Fourniture (1 vers plusieurs)
- Commande vers Mouvement Fourniture (1 vers plusieurs)
- Client vers Mouvement Fourniture (1 vers plusieurs)

---

### Table 30 : Fourniture

Nom d'affichage : Fourniture
Pluriel : Fournitures
Clé primaire : QR Fourniture (colonne texte, unique, requis)

Colonnes à créer :
- QR Fourniture : Texte, Requis, Unique, Clé primaire
- Type : Texte
- Référence : Texte
- Libellé : Texte
- Stock : Nombre
- Prix Achat : Monnaie
- Valeur : Monnaie, Calculé (Stock multiplié par Prix Achat)

Relations à créer :
- Dans la table Mouvement Fourniture, créer une colonne de type Recherche nommée "QR Fourniture" qui pointe vers la table Fourniture. Cette relation est obligatoire.
- Dans la table Mouvement Fourniture, créer une colonne de type Recherche nommée "ID Commande" qui pointe vers la table Commande. Cette relation est optionnelle.
- Dans la table Mouvement Fourniture, créer une colonne de type Recherche nommée "Num Client" qui pointe vers la table Client. Cette relation est optionnelle.

---

### Table 31 : Equipe de Fabrication

Nom d'affichage : Equipe de Fabrication
Pluriel : Equipes de Fabrication
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Nom : Texte, Requis
- Fonction : Texte
- Parc Machine : Texte
- Equipe : Texte
- Horaire Journalière : Nombre
- Jours Semaine : Nombre
- Taux Horaire : Monnaie

---

### Table 32 : Opération de Fabrication

Nom d'affichage : Opération de Fabrication
Pluriel : Opérations de Fabrication
Clé primaire : Code Opération (colonne texte, unique, requis)

Colonnes à créer :
- Code Opération : Texte, Requis, Unique, Clé primaire
- Opération : Texte, Requis
- Unité : Texte

---

### Table 33 : Matière Première

Nom d'affichage : Matière Première
Pluriel : Matières Premières
Clé primaire : QR MP (colonne texte, unique, requis)

Colonnes à créer :
- QR MP : Texte, Requis, Unique, Clé primaire
- Numéro Métrique : Texte
- Code Couleur : Texte
- Code Fabrication MP : Texte
- Couleur : Texte
- Num de Lot : Texte
- Stock Minimal : Nombre
- Stock Disponible : Nombre, Calculé
- Stock Final : Nombre, Calculé
- Demande Transfert Usine : Nombre
- Demande Achat : Nombre
- Statut Achat : Choix
  Valeurs du choix Statut Achat : En attente, Commandé, Reçu, Annulé

---

### Table 34 : Base Commandes

Nom d'affichage : Base Commandes
Pluriel : Bases Commandes
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Description : Table consolidée (peut être une vue calculée)

Colonnes à créer :
- Source : Texte
- Etat : Choix
- ID Commande : Texte
- Num OF : Recherche vers table Ordre de Fabrication
- Num Commande : Recherche vers table Commande
- Num Client : Recherche vers table Client
- Ref Commercial : Recherche vers table Article de Référence
- ID Composant : Recherche vers table Composant BOM
- Qté Commandé : Nombre
- Qté Réservé : Nombre
- Qté Composant à Fabriquer : Nombre
- QTE Fabriquer Coupe : Nombre
- Etat Préparation MP : Choix
- Etat Tissage : Choix
- Etat Coupe : Choix

Relations à créer :
- Dans la table Base Commandes, créer une colonne de type Recherche nommée "Num OF" qui pointe vers la table Ordre de Fabrication. Cette relation est optionnelle mais recommandée.
- Dans la table Base Commandes, créer une colonne de type Recherche nommée "Num Commande" qui pointe vers la table Commande. Cette relation est optionnelle mais recommandée.
- Dans la table Base Commandes, créer une colonne de type Recherche nommée "Num Client" qui pointe vers la table Client. Cette relation est optionnelle mais recommandée.
- Dans la table Base Commandes, créer une colonne de type Recherche nommée "Ref Commercial" qui pointe vers la table Article de Référence. Cette relation est optionnelle mais recommandée.
- Dans la table Base Commandes, créer une colonne de type Recherche nommée "ID Composant" qui pointe vers la table Composant BOM. Cette relation est optionnelle mais recommandée.

Note : La table Base Commandes peut être une vue calculée plutôt qu'une table physique. Dans ce cas, les relations sont gérées automatiquement par la vue.

---

### Table 35 : Rendement Tissage

Nom d'affichage : Rendement Tissage
Pluriel : Rendements Tissage
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Num OF : Recherche vers table Ordre de Fabrication, Requis
- Personne : Recherche vers table Opérateur, Requis
- Date Tissage : Date et heure
- QTE : Nombre
- QTE Deuxième : Nombre
- Déchet : Nombre
- Ourlet : Nombre
- Deuxième Approuvée : Nombre
- Type Deuxième : Choix
  Valeurs du choix Type Deuxième : Standard, Erreur Couleur, Erreur Dimensions
- Prix Revient : Monnaie
- Prix Vente : Monnaie
- Total Revient DT : Monnaie, Calculé
- Total Vente DT : Monnaie, Calculé
- Perte Déchet DT : Monnaie, Calculé
- Perte Deuxième DT : Monnaie, Calculé
- Perte Ourlet DT : Monnaie, Calculé
- Perte Totale DT : Monnaie, Calculé
- Gain Approuvé DT : Monnaie, Calculé
- Qte Totale Brute : Nombre, Calculé
- Taux Perte : Nombre, Calculé (pourcentage)
- Marge Nette DT : Monnaie, Calculé
- Alerte Prix : Oui/Non

Relations à créer :
- Dans la table Rendement Tissage, créer une colonne de type Recherche nommée "Num OF" qui pointe vers la table Ordre de Fabrication. Cette relation est obligatoire.
- Dans la table Rendement Tissage, créer une colonne de type Recherche nommée "Personne" qui pointe vers la table Opérateur. Cette relation est obligatoire.

---

### Table 36 : Récapitulatif Rendement

Nom d'affichage : Récapitulatif Rendement
Pluriel : Récapitulatifs Rendement
Clé primaire : GUID automatique (option par défaut, aucune action requise, le système crée automatiquement une colonne GUID cachée)

Colonnes à créer :
- Personne : Recherche vers table Opérateur, Requis
- Période : Texte
- Type Période : Choix, Requis
  Valeurs du choix Type Période : Jour, Semaine, Mois, Global
- Dimensions : Texte
- Qte Première : Nombre
- Qte Deuxième : Nombre
- Qte Déchet : Nombre
- Qte Ourlet : Nombre
- Qte Deuxième Approuvée : Nombre
- Perte Déchet DT : Monnaie
- Perte Deuxième DT : Monnaie
- Perte Ourlet DT : Monnaie
- Perte Totale DT : Monnaie
- Gain Approuvé DT : Monnaie
- Taux Qualité : Nombre (pourcentage)
- Perte Nette DT : Monnaie

Relation à créer : Dans la table Récapitulatif Rendement, créer une colonne de type Recherche nommée "Personne" qui pointe vers la table Opérateur. Cette relation est obligatoire.

---

## Phase 10 : Extensions Tables Existantes

Note : Les extensions sont déjà incluses dans les tables ci-dessus (colonnes supplémentaires marquées dans les tables Machine et Sous-Traitant).

---

## Résumé des Relations

Toutes les relations sont détaillées dans chaque table ci-dessus. Les relations se créent en ajoutant une colonne de type Recherche dans la table enfant qui pointe vers la table parente.

Règle générale : Le nom d'affichage de la colonne de recherche est le nom simple de la table parente (ex: "Client", "Machine", "Article", "OF", "Sous-OF", "Num Tissage", etc.).

Les relations obligatoires sont marquées comme "obligatoire" dans les instructions de chaque table. Les relations optionnelles sont marquées comme "optionnelle mais recommandée".

Voir le guide GUIDE_RELATIONS_POWERAPPS.md pour les instructions détaillées sur la création de relations.

---

## Points Importants

1. Ordre de Création : Créer les tables dans l'ordre des phases (1 puis 2, etc.)

2. Entrepôt Usine : Créer d'abord l'entrepôt Usine avec code USINE dans la table Entrepôt

3. Clés Primaires : Utiliser les colonnes texte comme clés primaires quand spécifié, sinon utiliser GUID automatique

4. Clés Uniques : 
   - Pour une colonne unique : Aller dans la section Clés (Keys) de la table, cliquer sur "Ajouter clés" ou "Add Keys", créer une nouvelle clé unique, sélectionner la colonne, et enregistrer
   - Pour une clé unique composée (plusieurs colonnes) : Aller dans la section Clés (Keys) de la table, cliquer sur "Ajouter clés" ou "Add Keys", créer une nouvelle clé unique, sélectionner toutes les colonnes nécessaires, et enregistrer. Si vous recevez l'erreur "Index size exceeded", utiliser la méthode alternative : créer une colonne calculée "Clé Unique Combinée" qui combine toutes les valeurs avec un séparateur (ex: "-"), puis créer une clé unique simple sur cette colonne. Cette colonne sera remplie automatiquement via Power Automate Flow. Voir les instructions détaillées dans la table Tarif Sous-Traitance pour un exemple.

5. Relations : Configurer les relations après avoir créé les deux tables concernées. Les relations 1 vers plusieurs se créent du côté table enfant en créant une colonne de type Recherche. Le nom d'affichage de la colonne de recherche peut être le nom simple de la table parente (ex: "Client", "Machine", "Article"). Les relations obligatoires sont nécessaires pour utiliser les fonctionnalités de recherche et filtrage dans Power Apps. Les relations optionnelles sont recommandées mais pas strictement nécessaires.

6. Choix Options : Créer tous les choix options avec les valeurs exactes spécifiées, respecter la casse et les accents

7. Colonnes Calculées : Marquer les colonnes comme calculées quand spécifié. Les calculs seront implémentés via Power Automate Flows

8. Valeurs par Défaut : Configurer les valeurs par défaut pour les colonnes Oui/Non (ex: Actif = Oui)

---

## Format de Sortie Attendu

Pour chaque table, générer :
1. Nom d'affichage de la table
2. Pluriel de la table
3. Clé primaire (colonne ou GUID)
4. Liste des colonnes avec nom d'affichage, type de données, requis, valeur par défaut si applicable
5. Choix options avec toutes les valeurs
6. Clés uniques si applicable
7. Relations (nom de la table parente)

---

## Checklist de Validation

Après création de chaque table, vérifier :
- Table créée avec le bon nom d'affichage
- Clé primaire configurée
- Toutes les colonnes créées avec les bons types
- Colonnes requises marquées comme requises
- Choix options créés avec toutes les valeurs
- Clés uniques configurées
- Relations configurées (si table parente existe)
- Table publiée

---

## Résultat Final Attendu

37 tables Dataverse créées dans la solution La Plume Artisanale, organisées en 10 phases, avec toutes les colonnes, relations, choix options, et clés uniques configurées, prêtes pour la migration des données Excel.

---

Date : 2026-01-14
Instruction complète pour Copilot
