# Examen théorique — Power BI et DAX

**Nom :** ___________________________
**Prénom :** ________________________
**Groupe :** _________________________
**Date :** ___________________________

**Durée suggérée :** 1 h 30
**Total :** 100 points
**Barème :** 2 points par bonne réponse

## Consignes

Pour chaque numéro, choisissez une seule bonne réponse parmi A, B, C ou D.

---

# Partie 1 — Power BI, Power Query et modèle de données

## 1.

Dans Power BI, le rôle principal de Power Query est de :

A. Créer des mesures DAX
B. Nettoyer, transformer et préparer les données
C. Créer uniquement des graphiques
D. Publier automatiquement le rapport

---

## 2.

Dans un projet Power BI, DAX intervient généralement :

A. Avant l’importation des données
B. Après la préparation des données et la création du modèle
C. Avant Power Query
D. Uniquement lors de l’installation de Power BI

---

## 3.

Quelle affirmation est correcte ?

A. Power Query sert à créer les indicateurs métier
B. DAX sert uniquement à nettoyer les données
C. Le modèle de données organise les relations entre les tables
D. Les visualisations remplacent les mesures DAX

---

## 4.

Une source de données dans Power BI peut être :

A. Seulement un fichier Excel
B. Seulement une base SQL
C. Excel, CSV, SQL, SharePoint, API ou autre source
D. Seulement un fichier PowerPoint

---

## 5.

La correction du type d’une colonne de date doit généralement être faite dans :

A. Power Query
B. Le menu des couleurs
C. Le titre du rapport
D. La légende d’un graphique

---

## 6.

Le modèle de données sert principalement à :

A. Modifier le logo du rapport
B. Organiser les tables et leurs relations
C. Supprimer Power Query
D. Remplacer les graphiques

---

## 7.

Une relation entre une table `Ventes` et une table `Date` permet surtout de :

A. Faire des analyses temporelles fiables
B. Changer automatiquement les couleurs
C. Supprimer les mesures
D. Compresser le fichier Power BI

---

## 8.

Quelle phrase résume correctement l’architecture Power BI ?

A. DAX prépare les données, Power Query affiche les graphiques
B. Power Query prépare les données, le modèle organise les tables, DAX calcule les indicateurs
C. Les visualisations nettoient les données
D. Le modèle de données remplace Power Query

---

## 9.

Une bonne pratique consiste à faire le nettoyage des données dans :

A. Les visualisations
B. Power Query
C. Les segments
D. Les cartes KPI

---

## 10.

Dans un rapport Power BI professionnel, les visualisations servent principalement à :

A. Préparer les données brutes
B. Présenter les résultats de manière claire
C. Créer les relations entre les tables
D. Installer les connecteurs

---

# Partie 2 — DAX et indicateurs analytiques

## 11.

DAX signifie :

A. Data Automatic Extension
B. Data Analysis Expressions
C. Data Access Explorer
D. Dynamic Application Excel

---

## 12.

Le rôle principal de DAX est de :

A. Créer des calculs et des indicateurs analytiques
B. Supprimer les fichiers inutiles
C. Installer Power BI Desktop
D. Remplacer complètement Power Query

---

## 13.

Un rapport sans DAX peut être limité parce que :

A. Il ne peut jamais afficher de graphique
B. Il ne peut pas toujours représenter la logique métier précise
C. Il ne peut pas importer de fichiers CSV
D. Il ne peut pas contenir de tableau

---

## 14.

Une mesure DAX permet principalement de :

A. Calculer une valeur dynamique selon le contexte
B. Modifier le nom d’un fichier source
C. Supprimer une base de données
D. Changer le mot de passe Power BI

---

## 15.

Une donnée brute représente généralement :

A. Une information enregistrée dans un système
B. Une mesure DAX toujours complète
C. Une visualisation déjà interprétée
D. Un rapport finalisé

---

## 16.

Un indicateur métier est utile parce qu’il permet de :

A. Transformer des données en information exploitable
B. Supprimer automatiquement les erreurs humaines
C. Empêcher les filtres de fonctionner
D. Remplacer toutes les tables

---

## 17.

Parmi les exemples suivants, lequel est un indicateur analytique ?

A. Le nom du fichier Power BI
B. Le taux de marge
C. La couleur du graphique
D. La taille de la page

---

## 18.

Quel indicateur permet de mesurer le revenu généré par les ventes ?

A. Le coût total
B. Le chiffre d’affaires
C. Le nombre de colonnes
D. Le nom de la table

---

## 19.

Quel indicateur permet d’évaluer la rentabilité en pourcentage ?

A. Le taux de marge
B. Le nombre de pages
C. Le format de date
D. La police du titre

---

## 20.

Pourquoi DAX est-il important dans un rapport analytique ?

A. Parce qu’il permet de créer des indicateurs dynamiques
B. Parce qu’il interdit les graphiques
C. Parce qu’il remplace les données
D. Parce qu’il supprime les segments

---

# Partie 3 — Mesures, colonnes calculées et tables calculées

## 21.

Une mesure DAX est généralement :

A. Dynamique et sensible aux filtres
B. Toujours fixe et indépendante du rapport
C. Une colonne obligatoire dans la source
D. Une image dans le rapport

---

## 22.

Une colonne calculée est généralement calculée :

A. Ligne par ligne
B. Seulement dans une carte KPI
C. Seulement après la publication du rapport
D. Sans utiliser de table

---

## 23.

Une table calculée permet de :

A. Créer une nouvelle table à partir d’une expression DAX
B. Modifier les couleurs du rapport
C. Supprimer les relations
D. Remplacer Power BI Desktop

---

## 24.

Quel élément est recommandé pour créer un KPI qui change selon les filtres ?

A. Une mesure
B. Une image
C. Une page vide
D. Une colonne supprimée

---

## 25.

Quand faut-il généralement privilégier une mesure plutôt qu’une colonne calculée ?

A. Quand le calcul doit réagir aux filtres du rapport
B. Quand le calcul doit être un texte fixe
C. Quand on veut supprimer les données
D. Quand on veut modifier le thème Power BI

---

## 26.

La formule suivante représente plutôt :

```DAX
MontantLigne = Ventes[Quantité] * Ventes[PrixUnitaire]
```

A. Une colonne calculée ligne par ligne
B. Un segment
C. Une relation entre tables
D. Un filtre de page

---

## 27.

La formule suivante représente plutôt :

```DAX
TotalVentes = SUM(Ventes[Montant])
```

A. Une mesure
B. Une image
C. Une source CSV
D. Une relation inactive

---

## 28.

Dans un rapport professionnel, il est préférable de nommer une mesure :

A. `Mesure1`
B. `Calcul2`
C. `TauxMarge`
D. `Test`

---

## 29.

Une bonne organisation des mesures consiste à :

A. Créer des mesures de base puis des mesures dérivées
B. Tout mettre dans une seule formule très longue
C. Ne jamais nommer les mesures
D. Supprimer les indicateurs après création

---

## 30.

Pourquoi les mesures explicites sont-elles recommandées ?

A. Elles sont claires, réutilisables et maintenables
B. Elles empêchent les filtres de fonctionner
C. Elles remplacent tous les fichiers sources
D. Elles ne peuvent pas être utilisées dans les visuels

---

# Partie 4 — Fonctions DAX fondamentales

## 31.

Quelle fonction DAX additionne les valeurs d’une colonne numérique ?

A. `SUM()`
B. `COUNT()`
C. `FORMAT()`
D. `IF()`

---

## 32.

Quelle fonction DAX calcule une moyenne ?

A. `SUM()`
B. `AVERAGE()`
C. `DISTINCTCOUNT()`
D. `ALL()`

---

## 33.

Quelle fonction DAX compte les valeurs distinctes ?

A. `COUNT()`
B. `COUNTA()`
C. `DISTINCTCOUNT()`
D. `SUMX()`

---

## 34.

Quelle fonction DAX est recommandée pour éviter les problèmes de division par zéro ?

A. `DIVIDE()`
B. `SUM()`
C. `MONTH()`
D. `YEAR()`

---

## 35.

Quelle fonction DAX permet de parcourir une table ligne par ligne et d’additionner les résultats ?

A. `SUMX()`
B. `COUNT()`
C. `ALL()`
D. `FORMAT()`

---

## 36.

Quelle fonction DAX permet de modifier le contexte de filtre ?

A. `CALCULATE()`
B. `SUM()`
C. `COUNT()`
D. `AVERAGE()`

---

## 37.

Quelle fonction DAX permet souvent de retirer un filtre dans un calcul ?

A. `ALL()`
B. `IF()`
C. `SWITCH()`
D. `COUNTA()`

---

## 38.

Quelle formule est correcte pour calculer le chiffre d’affaires ?

A. `SUM(Ventes[Produit])`
B. `SUMX(Ventes, Ventes[Quantité] * Ventes[PrixUnitaire])`
C. `COUNT(Ventes[Région])`
D. `AVERAGE(Ventes[ClientID])`

---

## 39.

Quelle formule est correcte pour calculer le coût total ?

A. `SUMX(Ventes, Ventes[Quantité] * Ventes[CoutUnitaire])`
B. `COUNT(Ventes[Produit])`
C. `SUM(Ventes[Région])`
D. `FORMAT(Ventes[Date], "mmmm")`

---

## 40.

Quelle formule est correcte pour calculer la marge ?

A. `[ChiffreAffaires] + [CoutTotal]`
B. `[CoutTotal] - [ChiffreAffaires]`
C. `[ChiffreAffaires] - [CoutTotal]`
D. `[ChiffreAffaires] * [CoutTotal]`

---

# Partie 5 — Contexte de calcul et analyse métier

## 41.

Le contexte de filtre correspond à :

A. L’ensemble des filtres actifs au moment du calcul
B. La taille du fichier Power BI
C. Le nom de l’utilisateur
D. La couleur des graphiques

---

## 42.

Si une mesure `TotalVentes` est placée dans un tableau par région, elle calcule :

A. Le même total général sur toutes les lignes
B. Le total des ventes pour chaque région
C. Le nombre de relations du modèle
D. Le nombre de pages du rapport

---

## 43.

Le contexte de ligne apparaît surtout lorsque :

A. Un calcul est évalué ligne par ligne
B. Un rapport est publié
C. Une page est renommée
D. Une couleur est changée

---

## 44.

Pourquoi une même mesure peut-elle donner des résultats différents dans une carte, un tableau ou un graphique ?

A. Parce qu’elle dépend du contexte de calcul
B. Parce qu’elle est toujours fausse
C. Parce qu’elle ne fonctionne qu’une seule fois
D. Parce qu’elle ignore toutes les tables

---

## 45.

La fonction `CALCULATE` est importante parce qu’elle permet de :

A. Modifier le contexte dans lequel une mesure est calculée
B. Supprimer Power Query
C. Changer le format du fichier
D. Remplacer les visualisations

---

## 46.

La fonction `ALL` est souvent utilisée pour calculer :

A. Un pourcentage du total
B. Une image de fond
C. Une relation automatique
D. Un nom de page

---

## 47.

La mesure suivante sert à calculer :

```DAX
PartRegion =
DIVIDE(
    [ChiffreAffaires],
    CALCULATE(
        [ChiffreAffaires],
        ALL(Ventes[Région])
    ),
    0
)
```

A. La contribution d’une région au chiffre d’affaires total
B. Le nombre de produits vendus
C. Le coût unitaire moyen
D. Le nombre de colonnes dans la table

---

## 48.

Dans un rapport commercial, le panier moyen peut être calculé par :

A. `ChiffreAffaires / NombreClients`
B. `CoutTotal / Région`
C. `Produit / Date`
D. `NombrePages / NombreGraphiques`

---

## 49.

Un bon rapport Power BI doit permettre de :

A. Afficher des chiffres sans interprétation
B. Analyser, comparer et soutenir la décision
C. Masquer tous les indicateurs
D. Éviter toute mesure DAX

---

## 50.

Quelle phrase est la plus correcte ?

A. Power BI sert seulement à faire de beaux graphiques
B. DAX transforme les données brutes en indicateurs exploitables
C. Power Query remplace toutes les mesures
D. Les filtres empêchent l’analyse

