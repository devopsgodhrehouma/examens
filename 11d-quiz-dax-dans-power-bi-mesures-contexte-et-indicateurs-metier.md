# Quiz — Comprendre DAX dans Power BI : mesures, contexte et indicateurs métier

## Question 1 — Rôle général de DAX

Dans un rapport Power BI, une équipe souhaite aller au-delà de l’affichage simple des données et créer des indicateurs comme la marge, le taux de marge, la croissance annuelle et le pourcentage du total.

Quel est le rôle principal de DAX dans cette situation ?

A. Nettoyer les colonnes avant le chargement des données
B. Créer des visualisations automatiquement sans modèle de données
C. Calculer des indicateurs analytiques à partir du modèle de données
D. Remplacer complètement Power Query dans la préparation des données

---

## Question 2 — Power BI sans DAX

Une personne crée un rapport Power BI à partir d’un fichier Excel contenant une colonne `Montant`. Elle ajoute cette colonne dans une carte et Power BI affiche automatiquement une somme.

Comment peut-on qualifier ce type de calcul ?

A. Une mesure implicite
B. Une table calculée
C. Une relation entre tables
D. Une mesure temporelle avancée

---

## Question 3 — Limite d’un rapport sans DAX

Un rapport affiche les ventes par produit, mais il ne calcule pas la marge, le taux de marge ni l’écart avec les objectifs.

Quelle est la principale limite de ce rapport ?

A. Il contient trop de mesures explicites
B. Il affiche des données, mais ne produit pas encore une analyse métier complète
C. Il utilise trop de relations entre les tables
D. Il contient nécessairement une erreur dans Power Query

---

## Question 4 — Données brutes et indicateurs

Une table contient les colonnes `Quantité` et `PrixUnitaire`. Le chiffre d’affaires n’existe pas directement dans la table.

Quelle formule représente correctement le calcul du chiffre d’affaires ligne par ligne ?

A. Quantité + PrixUnitaire
B. Quantité - PrixUnitaire
C. Quantité × PrixUnitaire
D. Quantité / PrixUnitaire

---

## Question 5 — Power Query et DAX

Une colonne de dates est importée sous forme de texte et doit être convertie en type Date avant l’analyse.

Quel outil est le plus approprié pour cette transformation ?

A. DAX
B. Power Query
C. Une mesure rapide
D. Un graphique en barres

---

## Question 6 — Modèle de données

Une table `Ventes` contient `ProduitID`, et une table `Produits` contient aussi `ProduitID`. On souhaite relier les ventes à leurs produits.

Dans Power BI, cette opération relève principalement de quoi ?

A. La création d’une relation dans le modèle de données
B. La création d’une mesure implicite
C. La création d’un segment visuel
D. La modification du format monétaire

---

## Question 7 — DAX comme couche analytique

Dans une architecture Power BI bien structurée, quel est l’enchaînement le plus logique ?

A. DAX → Power Query → Visualisations → Modèle de données
B. Sources de données → Power Query → Modèle de données → DAX → Visualisations
C. Visualisations → DAX → Power Query → Sources de données
D. Modèle de données → Sources de données → DAX → Power Query

---

## Question 8 — Définition de DAX

Que signifie DAX ?

A. Data Automatic Exchange
B. Data Analysis Expressions
C. Digital Analytics Extension
D. Database Access Explorer

---

## Question 9 — Utilité professionnelle de DAX

Une direction souhaite connaître l’écart entre les ventes réelles et le budget prévu.

Pourquoi DAX est-il utile dans ce cas ?

A. Il permet de supprimer les lignes vides dans la source
B. Il permet de créer un calcul métier entre deux indicateurs
C. Il permet de remplacer toutes les visualisations Power BI
D. Il permet uniquement de modifier la couleur des graphiques

---

## Question 10 — Rapport descriptif et rapport analytique

Quelle phrase décrit le mieux la différence entre un rapport descriptif et un rapport analytique ?

A. Un rapport descriptif utilise uniquement des graphiques rouges, alors qu’un rapport analytique utilise des graphiques bleus
B. Un rapport descriptif affiche des données, alors qu’un rapport analytique calcule et interprète des indicateurs
C. Un rapport analytique ne peut pas contenir de tableaux
D. Un rapport descriptif nécessite toujours plus de DAX qu’un rapport analytique

---

## Question 11 — Mesure explicite

Quelle formule représente une mesure explicite correctement définie dans Power BI ?

A. `TotalVentes = SUM(Ventes[Montant])`
B. `Somme automatique dans une carte`
C. `Ventes[Montant]`
D. `Importer un fichier CSV`

---

## Question 12 — Mesure implicite

Une colonne numérique est glissée dans un visuel, et Power BI applique automatiquement une somme.

De quel type de mesure s’agit-il ?

A. Mesure explicite
B. Mesure implicite
C. Table calculée
D. Colonne relationnelle

---

## Question 13 — Mesure rapide

Une personne utilise l’interface de Power BI pour générer automatiquement une formule de pourcentage du total.

Comment appelle-t-on généralement ce type de mesure ?

A. Une mesure rapide
B. Une colonne importée
C. Une clé primaire
D. Une table de faits

---

## Question 14 — Meilleure pratique pour les rapports professionnels

Dans un rapport Power BI professionnel, quelle pratique est généralement recommandée ?

A. Utiliser uniquement les mesures implicites
B. Créer des mesures explicites avec des noms clairs
C. Éviter complètement DAX
D. Mettre tous les calculs dans les titres des graphiques

---

## Question 15 — Colonne calculée

Une formule DAX crée une nouvelle colonne dans la table `Ventes` pour calculer `Quantité × PrixUnitaire` sur chaque ligne.

De quel objet DAX s’agit-il ?

A. Une mesure
B. Une colonne calculée
C. Une table calculée
D. Une relation inactive

---

## Question 16 — Table calculée

Une formule DAX crée une nouvelle table contenant uniquement les produits dont la marge unitaire est positive.

De quel objet DAX s’agit-il ?

A. Une table calculée
B. Une mesure implicite
C. Un segment
D. Une moyenne automatique

---

## Question 17 — Mesure dynamique

Pourquoi une mesure est-elle considérée comme dynamique ?

A. Parce qu’elle est toujours stockée ligne par ligne dans la table
B. Parce qu’elle change selon les filtres, les segments et les visuels
C. Parce qu’elle remplace les relations du modèle
D. Parce qu’elle ne peut être utilisée que dans Power Query

---

## Question 18 — Colonne calculée ou mesure

On souhaite créer un indicateur `TotalVentes` qui doit changer selon l’année, la région et le produit sélectionnés dans le rapport.

Quel objet faut-il privilégier ?

A. Une mesure
B. Une colonne calculée
C. Une table calculée sans relation
D. Une colonne texte dans Power Query

---

## Question 19 — Valeur ligne par ligne

On souhaite créer une valeur fixe pour chaque ligne d’une table, par exemple un montant de ligne calculé à partir de la quantité et du prix unitaire.

Quel objet DAX est le plus adapté ?

A. Une colonne calculée
B. Une mesure rapide uniquement
C. Une visualisation cartographique
D. Une relation plusieurs-à-plusieurs

---

## Question 20 — Comparaison des objets DAX

Quelle affirmation est correcte ?

A. Une mesure ajoute toujours une colonne physique dans une table
B. Une colonne calculée réagit toujours aux segments comme une mesure
C. Une mesure est évaluée selon le contexte du rapport
D. Une table calculée est identique à un graphique

---

## Question 21 — Contexte de filtre

Une mesure `TotalVentes = SUM(Ventes[Montant])` affiche des résultats différents par région dans un tableau.

Quelle notion explique ce comportement ?

A. Le contexte de filtre
B. Le nettoyage automatique
C. La suppression des doublons
D. Le format de devise

---

## Question 22 — Contexte de ligne

Une colonne calculée évalue `Ventes[Quantité] * Ventes[PrixUnitaire]` pour chaque ligne.

Quelle notion DAX est principalement utilisée ici ?

A. Le contexte de ligne
B. Le contexte de rapport uniquement
C. Le format conditionnel
D. Le type de graphique

---

## Question 23 — Même mesure, résultats différents

La même mesure `TotalVentes` affiche 100 000 dans une carte, puis 40 000 pour Montréal dans un tableau par région.

Pourquoi ?

A. Parce que la formule DAX est automatiquement modifiée
B. Parce que le contexte de calcul change selon le visuel
C. Parce que Power Query recalcule la table à chaque clic
D. Parce que les mesures ne sont pas fiables

---

## Question 24 — Segment Power BI

Un utilisateur sélectionne l’année 2025 dans un segment. Les mesures du rapport se recalculent automatiquement.

Quel concept explique cette réaction ?

A. Le contexte de filtre
B. La table calculée
C. La suppression des colonnes
D. La fusion des requêtes

---

## Question 25 — Rôle de CALCULATE

Quel est le rôle principal de la fonction `CALCULATE` ?

A. Modifier le contexte de filtre d’un calcul
B. Importer des fichiers Excel
C. Créer automatiquement des graphiques
D. Supprimer les relations entre tables

---

## Question 26 — Exemple avec CALCULATE

Que signifie la formule suivante ?

```DAX
VentesMontreal =
CALCULATE(
    [TotalVentes],
    Ventes[Région] = "Montréal"
)
```

A. Elle supprime toutes les ventes de Montréal
B. Elle calcule les ventes uniquement dans le contexte de Montréal
C. Elle transforme Montréal en colonne calculée
D. Elle crée une nouvelle table appelée Montréal

---

## Question 27 — Fonction SUM

À quoi sert la fonction `SUM` ?

A. Additionner les valeurs d’une colonne numérique
B. Compter uniquement les valeurs distinctes
C. Diviser deux mesures avec gestion des erreurs
D. Retirer tous les filtres du rapport

---

## Question 28 — Fonction AVERAGE

À quoi sert la fonction `AVERAGE` ?

A. Calculer une moyenne
B. Créer une table de dates
C. Supprimer les valeurs vides
D. Modifier une relation entre tables

---

## Question 29 — Fonction DISTINCTCOUNT

Dans une table de ventes, un même client peut apparaître plusieurs fois. On souhaite compter chaque client une seule fois.

Quelle fonction est la plus appropriée ?

A. COUNT
B. SUM
C. DISTINCTCOUNT
D. AVERAGE

---

## Question 30 — Fonction DIVIDE

Pourquoi recommande-t-on souvent `DIVIDE` au lieu de l’opérateur `/` pour les ratios ?

A. Parce que `DIVIDE` permet de mieux gérer les divisions par zéro
B. Parce que `/` ne fonctionne jamais dans DAX
C. Parce que `DIVIDE` sert à créer des relations
D. Parce que `DIVIDE` transforme automatiquement les dates

---

## Question 31 — Fonction SUMX

Que fait la fonction `SUMX` ?

A. Elle additionne directement une colonne existante sans calcul intermédiaire
B. Elle parcourt une table ligne par ligne, calcule une expression, puis additionne les résultats
C. Elle supprime les filtres d’une colonne
D. Elle crée automatiquement un graphique combiné

---

## Question 32 — SUM ou SUMX

Une table contient `Quantité` et `PrixUnitaire`, mais pas de colonne `Montant`. On souhaite calculer le chiffre d’affaires total.

Quelle fonction est la plus appropriée ?

A. SUMX
B. DISTINCTCOUNT
C. COUNTA
D. ALL uniquement

---

## Question 33 — Fonction ALL

À quoi sert principalement la fonction `ALL` dans un calcul DAX ?

A. Retirer un filtre pour obtenir un total de référence
B. Additionner une colonne numérique
C. Calculer une moyenne simple
D. Changer le nom d’une table

---

## Question 34 — Pourcentage du total

On souhaite calculer la part de chaque région dans le chiffre d’affaires total.

Quelle logique est correcte ?

A. Diviser les ventes de la région par le total de toutes les régions
B. Additionner uniquement les régions sans ventes
C. Multiplier chaque région par son nom
D. Compter le nombre de colonnes de la table

---

## Question 35 — Fonction FILTER

Quel est le rôle de la fonction `FILTER` ?

A. Retourner une table filtrée selon une condition
B. Transformer un nombre en pourcentage
C. Supprimer une source de données
D. Modifier le type d’un fichier CSV

---

## Question 36 — Fonction IF

Quelle formule exprime correctement une condition simple ?

A. `IF([TotalVentes] >= [ObjectifVentes], "Objectif atteint", "Objectif non atteint")`
B. `SUM([Objectif atteint])`
C. `ALL("Objectif atteint")`
D. `COUNT("Objectif atteint", "Objectif non atteint")`

---

## Question 37 — Fonction SWITCH

Pourquoi utiliser `SWITCH(TRUE(), ...)` dans une mesure DAX ?

A. Pour gérer plusieurs conditions de manière plus lisible que plusieurs IF imbriqués
B. Pour remplacer Power Query
C. Pour créer une relation automatique entre deux tables
D. Pour importer des fichiers depuis SharePoint

---

## Question 38 — Chiffre d’affaires

Quelle mesure calcule correctement le chiffre d’affaires à partir de `Quantité` et `PrixUnitaire` ?

A.

```DAX
ChiffreAffaires =
SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

B.

```DAX
ChiffreAffaires =
DISTINCTCOUNT(Ventes[Produit])
```

C.

```DAX
ChiffreAffaires =
AVERAGE(Ventes[ClientID])
```

D.

```DAX
ChiffreAffaires =
ALL(Ventes[Région])
```

---

## Question 39 — Coût total

Quelle mesure calcule correctement le coût total à partir de `Quantité` et `CoutUnitaire` ?

A.

```DAX
CoutTotal =
SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[CoutUnitaire]
)
```

B.

```DAX
CoutTotal =
COUNT(Ventes[Produit])
```

C.

```DAX
CoutTotal =
ALL(Ventes[Date])
```

D.

```DAX
CoutTotal =
AVERAGE(Ventes[Région])
```

---

## Question 40 — Marge

Si `[ChiffreAffaires]` et `[CoutTotal]` existent déjà comme mesures, quelle formule calcule correctement la marge ?

A.

```DAX
Marge = [ChiffreAffaires] - [CoutTotal]
```

B.

```DAX
Marge = [ChiffreAffaires] + [CoutTotal]
```

C.

```DAX
Marge = DISTINCTCOUNT(Ventes[ClientID])
```

D.

```DAX
Marge = ALL(Ventes[Produit])
```

---

## Question 41 — Taux de marge

Quelle mesure calcule correctement le taux de marge ?

A.

```DAX
TauxMarge =
DIVIDE(
    [Marge],
    [ChiffreAffaires],
    0
)
```

B.

```DAX
TauxMarge =
SUM(Ventes[Produit])
```

C.

```DAX
TauxMarge =
COUNT(Ventes[Région])
```

D.

```DAX
TauxMarge =
ALL(Ventes[Montant])
```

---

## Question 42 — Panier moyen

Le panier moyen correspond au chiffre d’affaires moyen généré par client distinct.

Quelle formule est la plus appropriée ?

A.

```DAX
PanierMoyen =
DIVIDE(
    [ChiffreAffaires],
    [NombreClients],
    0
)
```

B.

```DAX
PanierMoyen =
SUM(Ventes[ClientID])
```

C.

```DAX
PanierMoyen =
ALL(Ventes[Produit])
```

D.

```DAX
PanierMoyen =
COUNT(Ventes[Date])
```

---

## Question 43 — Nombre de clients

Une table contient plusieurs ventes par client. Quelle mesure compte correctement le nombre de clients différents ?

A.

```DAX
NombreClients =
DISTINCTCOUNT(Ventes[ClientID])
```

B.

```DAX
NombreClients =
SUM(Ventes[ClientID])
```

C.

```DAX
NombreClients =
AVERAGE(Ventes[ClientID])
```

D.

```DAX
NombreClients =
ALL(Ventes[ClientID])
```

---

## Question 44 — Contribution régionale

Que fait la mesure suivante ?

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

A. Elle calcule la part de la région actuelle dans le chiffre d’affaires total
B. Elle supprime définitivement les régions de la table
C. Elle transforme chaque région en client
D. Elle calcule uniquement la moyenne des dates

---

## Question 45 — Comparaison temporelle

Pour calculer les ventes de l’année précédente avec `SAMEPERIODLASTYEAR`, quel élément est fortement recommandé dans le modèle Power BI ?

A. Une table de dates correctement reliée à la table de faits
B. Une colonne texte sans relation
C. Une mesure implicite uniquement
D. Une table sans clé ni date

---

## Question 46 — Croissance en valeur

Si `[ChiffreAffaires]` représente les ventes actuelles et `[VentesAnneePrecedente]` représente les ventes de l’année précédente, quelle formule calcule la croissance en valeur ?

A.

```DAX
CroissanceValeur =
[ChiffreAffaires] - [VentesAnneePrecedente]
```

B.

```DAX
CroissanceValeur =
[ChiffreAffaires] + [VentesAnneePrecedente]
```

C.

```DAX
CroissanceValeur =
DISTINCTCOUNT(Ventes[ClientID])
```

D.

```DAX
CroissanceValeur =
ALL('Date'[Date])
```

---

## Question 47 — Croissance en pourcentage

Quelle formule calcule correctement une croissance en pourcentage ?

A.

```DAX
CroissancePourcentage =
DIVIDE(
    [CroissanceValeur],
    [VentesAnneePrecedente],
    0
)
```

B.

```DAX
CroissancePourcentage =
SUM(Ventes[Produit])
```

C.

```DAX
CroissancePourcentage =
COUNT(Ventes[Région])
```

D.

```DAX
CroissancePourcentage =
ALL(Ventes[Montant])
```

---

## Question 48 — Organisation des mesures

Pourquoi est-il recommandé de créer des mesures de base comme `[ChiffreAffaires]` et `[CoutTotal]`, puis des mesures dérivées comme `[Marge]` et `[TauxMarge]` ?

A. Pour rendre les calculs plus lisibles, réutilisables et faciles à maintenir
B. Pour empêcher les filtres de fonctionner
C. Pour éviter d’utiliser le modèle de données
D. Pour rendre les visualisations impossibles à modifier

---

## Question 49 — Nom des mesures

Quel nom de mesure est le plus professionnel et le plus clair ?

A. `Mesure1`
B. `TestCalcul`
C. `TauxMarge`
D. `ABC123`

---

## Question 50 — Synthèse générale

Quelle phrase résume le mieux le rôle de DAX dans Power BI ?

A. DAX sert principalement à nettoyer les fichiers avant leur importation
B. DAX sert à calculer des indicateurs analytiques qui donnent du sens aux données dans un rapport Power BI
C. DAX sert uniquement à modifier les couleurs des graphiques
D. DAX remplace complètement Power BI, Power Query et le modèle de données
