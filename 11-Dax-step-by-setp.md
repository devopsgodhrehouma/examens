# Tutoriel DAX Power BI pour débuter

## Objectif du document

Ce document présente une introduction progressive à DAX dans Power BI. Il est conçu pour une personne qui découvre Power BI, les mesures, les colonnes calculées, les tables de faits, les tables de dimensions et les premiers indicateurs de tableau de bord.

L’objectif n’est pas seulement de copier des formules, mais de comprendre ce que chaque formule calcule, pourquoi elle est utilisée et comment vérifier que le résultat obtenu est correct.

À la fin du tutoriel, vous serez capable de :

* comprendre le rôle de DAX dans Power BI ;
* distinguer Power Query, DAX et les visuels Power BI ;
* créer une table de données simple ;
* comprendre ce qu’est une table de faits ;
* comprendre la différence entre une colonne calculée et une mesure ;
* créer des mesures DAX de base ;
* utiliser `SUM`, `SUMX`, `DIVIDE`, `COUNTROWS`, `DISTINCTCOUNT`, `CALCULATE` et `REMOVEFILTERS` ;
* comprendre le contexte de filtre ;
* créer une table calendrier ;
* construire un mini tableau de bord de ventes ;
* vérifier vos résultats avec des valeurs attendues.

Lien du travail à implémenter à la fin du tutoriel :

[https://www.youtube.com/watch?v=waG_JhBgUpM](https://www.youtube.com/watch?v=waG_JhBgUpM)

Lien des données :

[https://onedrive.live.com/?redeem=aHR0cHM6Ly8xZHJ2Lm1zL3UvcyFBbXhyb2ZaWmxaLXdoTUlnUzlXSlM3QndTZkhCYnc_ZT0wejNuUW4&id=B09F9559F6A16B6C!74016&cid=B09F9559F6A16B6C](https://onedrive.live.com/?redeem=aHR0cHM6Ly8xZHJ2Lm1zL3UvcyFBbXhyb2ZaWmxaLXdoTUlnUzlXSlM3QndTZkhCYnc_ZT0wejNuUW4&id=B09F9559F6A16B6C!74016&cid=B09F9559F6A16B6C)

<br/>



<details> 
<summary> # 1. Comprendre le rôle de DAX dans Power BI  </summary>

DAX signifie **Data Analysis Expressions**. C’est le langage de calcul utilisé dans Power BI pour créer des formules, des indicateurs, des mesures, des colonnes calculées et des analyses dynamiques.

Dans Power BI, il faut bien distinguer trois éléments :

| Élément     | Rôle principal                                                        |
| ----------- | --------------------------------------------------------------------- |
| Power Query | Importer, nettoyer et transformer les données                         |
| DAX         | Calculer les indicateurs et les mesures                               |
| Power BI    | Présenter les résultats sous forme de rapports et de tableaux de bord |

Une façon simple de retenir est la suivante :

```text
Power Query prépare les données.
DAX calcule les indicateurs.
Power BI affiche les résultats.
```

Exemple simple :

Vous avez une table de ventes avec des produits, des quantités et des prix.

| Produit | Quantité | Prix unitaire |
| ------- | -------: | ------------: |
| PC      |        2 |          1000 |
| Souris  |        5 |            20 |

Avec DAX, vous pouvez calculer le chiffre d’affaires :

```DAX
Chiffre d'affaires = Quantité × Prix unitaire
```

Mais dans Power BI, ce calcul peut changer automatiquement selon le contexte :

* l’année sélectionnée ;
* le mois sélectionné ;
* la région sélectionnée ;
* le produit sélectionné ;
* la catégorie sélectionnée ;
* le client sélectionné.

C’est l’une des grandes forces de DAX : une même mesure peut donner des résultats différents selon les filtres appliqués dans le rapport.

</details>

# 2. Comprendre la notion de table de faits

Avant de créer des formules DAX, il faut comprendre ce qu’est une **table de faits**.

Une table de faits contient les événements mesurables d’une activité. Elle répond généralement à des questions comme :

* combien a-t-on vendu ?
* combien cela a-t-il coûté ?
* quelle quantité a été vendue ?
* quelle marge a été réalisée ?
* à quelle date la vente a-t-elle eu lieu ?
* dans quelle région la vente a-t-elle été faite ?

Dans ce tutoriel, la table principale s’appelle **Ventes**. Elle représente une table de faits, car elle contient les données mesurables de l’activité commerciale.

Chaque ligne de la table représente une vente.

Exemple :

| Date       | Produit | Région | Quantité | PrixUnitaire | CoutUnitaire |
| ---------- | ------- | ------ | -------: | -----------: | -----------: |
| 2025-01-05 | PC      | Québec |        2 |         1000 |          700 |

Cette ligne signifie :

```text
Le 5 janvier 2025, 2 PC ont été vendus au Québec.
Chaque PC a été vendu 1000.
Chaque PC a coûté 700.
```

À partir de cette ligne, on peut calculer :

```text
Chiffre d’affaires = 2 × 1000 = 2000
Coût total = 2 × 700 = 1400
Marge = 2000 - 1400 = 600
```

---

# 3. Comprendre les tables de dimensions

Dans un modèle Power BI plus professionnel, on sépare souvent les données en plusieurs tables.

On distingue principalement :

| Type de table       | Rôle                            |
| ------------------- | ------------------------------- |
| Table de faits      | Contient les valeurs mesurables |
| Table de dimensions | Contient les axes d’analyse     |

La table de faits répond à la question :

```text
Combien ?
```

Exemples :

* combien vendu ?
* combien gagné ?
* combien coûté ?
* quelle quantité ?
* quelle marge ?

Les tables de dimensions répondent aux questions :

```text
Par quoi analyser ?
```

Exemples :

* par produit ;
* par région ;
* par catégorie ;
* par mois ;
* par année ;
* par client.

Dans notre exemple, nous allons commencer avec une seule table appelée **Ventes**. C’est volontaire, pour simplifier l’apprentissage.

Cependant, dans un modèle plus avancé, on pourrait avoir :

| Table      | Type                 | Exemple de contenu                  |
| ---------- | -------------------- | ----------------------------------- |
| Ventes     | Table de faits       | Date, Produit, Quantité, Prix, Coût |
| Produits   | Dimension            | Produit, Catégorie, Marque          |
| Régions    | Dimension            | Région, Pays, Zone                  |
| Calendrier | Dimension temporelle | Date, Mois, Trimestre, Année        |

Dans ce tutoriel, la table **Calendrier** sera créée plus loin, car elle est essentielle pour les analyses par date.

---

# 4. Créer les données de départ dans Power BI

Ouvrez Power BI Desktop, puis suivez les étapes suivantes :

1. Cliquez sur **Accueil**.
2. Cliquez sur **Entrer des données**.
3. Créez une table appelée **Ventes**.
4. Copiez les données suivantes.

| Date       | Produit | Catégorie    | Région  | Quantité | PrixUnitaire | CoutUnitaire |
| ---------- | ------- | ------------ | ------- | -------: | -----------: | -----------: |
| 2025-01-05 | PC      | Informatique | Québec  |        2 |         1000 |          700 |
| 2025-01-10 | Souris  | Accessoire   | Québec  |       10 |           25 |           10 |
| 2025-02-03 | Clavier | Accessoire   | Ontario |        5 |           60 |           30 |
| 2025-02-18 | PC      | Informatique | Ontario |        1 |         1000 |          700 |
| 2025-03-02 | Écran   | Informatique | Québec  |        3 |          300 |          180 |
| 2025-03-15 | Souris  | Accessoire   | Ontario |        8 |           25 |           10 |

Après avoir collé les données, cliquez sur **Charger**.

---

# 5. Vérifier les types de données

Avant d’écrire les formules DAX, il faut vérifier les types de données. Cette étape est très importante, car une mauvaise détection du type peut provoquer des erreurs dans les calculs.

Dans Power BI, allez dans la vue **Données** ou dans la vue **Modèle**, puis vérifiez les colonnes de la table **Ventes**.

| Colonne      | Type attendu                    |
| ------------ | ------------------------------- |
| Date         | Date                            |
| Produit      | Texte                           |
| Catégorie    | Texte                           |
| Région       | Texte                           |
| Quantité     | Nombre entier                   |
| PrixUnitaire | Nombre entier ou nombre décimal |
| CoutUnitaire | Nombre entier ou nombre décimal |

Si la colonne `Date` est interprétée comme du texte, les calculs temporels risquent de ne pas fonctionner correctement.

Si les colonnes `Quantité`, `PrixUnitaire` ou `CoutUnitaire` sont interprétées comme du texte, les formules de multiplication et d’addition risquent de produire des erreurs.

---

# 6. Colonne calculée ou mesure : différence fondamentale

Dans Power BI, il existe deux façons fréquentes de créer des calculs :

* les colonnes calculées ;
* les mesures.

Il est essentiel de comprendre la différence entre les deux.

---

## 6.1 Colonne calculée

Une **colonne calculée** ajoute une nouvelle colonne dans une table.

Elle travaille ligne par ligne.

Exemple :

| Quantité | PrixUnitaire | Montant |
| -------: | -----------: | ------: |
|        2 |         1000 |    2000 |
|       10 |           25 |     250 |
|        5 |           60 |     300 |

La colonne `Montant` est calculée pour chaque ligne.

Elle ressemble beaucoup à une formule Excel copiée sur toutes les lignes d’un tableau.

---

## 6.2 Mesure

Une **mesure** calcule un résultat global, dynamique et dépendant du contexte.

Exemple :

```DAX
CA = 4450
```

Ce résultat peut changer automatiquement selon les filtres.

Si vous filtrez la région Québec, la mesure calcule seulement le chiffre d’affaires du Québec.

Si vous filtrez la région Ontario, la même mesure calcule seulement le chiffre d’affaires de l’Ontario.

La formule ne change pas. C’est le contexte qui change.

---

## 6.3 Quand utiliser une colonne calculée ou une mesure ?

| Besoin                                            | À utiliser       |
| ------------------------------------------------- | ---------------- |
| Ajouter une valeur ligne par ligne dans une table | Colonne calculée |
| Calculer un total                                 | Mesure           |
| Calculer une moyenne                              | Mesure           |
| Calculer un ratio                                 | Mesure           |
| Créer un KPI                                      | Mesure           |
| Créer un tableau de bord dynamique                | Mesure           |
| Créer une catégorie fixe par ligne                | Colonne calculée |

Règle pratique :

```text
Pour les tableaux de bord, les mesures sont généralement préférables.
```

---

# 7. Créer une première colonne calculée

Nous allons d’abord créer une colonne calculée simple pour comprendre le principe.

Dans Power BI :

1. Allez dans la table **Ventes**.
2. Cliquez sur **Nouvelle colonne**.
3. Écrivez la formule suivante.

```DAX
Montant = Ventes[Quantité] * Ventes[PrixUnitaire]
```

Cette formule signifie :

```text
Pour chaque ligne de la table Ventes,
multiplier la quantité par le prix unitaire.
```

Exemples :

```text
Ligne 1 : 2 × 1000 = 2000
Ligne 2 : 10 × 25 = 250
Ligne 3 : 5 × 60 = 300
```

Après la création de cette colonne, la table contient une nouvelle colonne appelée `Montant`.

---

# 8. Créer une première mesure DAX avec SUM

Nous allons maintenant créer une mesure qui additionne la colonne `Montant`.

Dans Power BI :

1. Cliquez avec le bouton droit sur la table **Ventes**.
2. Cliquez sur **Nouvelle mesure**.
3. Écrivez la formule suivante.

```DAX
CA = SUM(Ventes[Montant])
```

`CA` signifie **chiffre d’affaires**.

Cette mesure additionne toutes les valeurs de la colonne `Montant`.

Avec les données du tutoriel, le résultat attendu est :

```text
CA = 4450
```

Explication du calcul :

| Ligne | Produit | Calcul   | Montant |
| ----: | ------- | -------- | ------: |
|     1 | PC      | 2 × 1000 |    2000 |
|     2 | Souris  | 10 × 25  |     250 |
|     3 | Clavier | 5 × 60   |     300 |
|     4 | PC      | 1 × 1000 |    1000 |
|     5 | Écran   | 3 × 300  |     900 |
|     6 | Souris  | 8 × 25   |     200 |
| Total |         |          |    4450 |

---

# 9. Créer une mesure plus professionnelle avec SUMX

La mesure précédente fonctionne, mais elle dépend de la colonne calculée `Montant`.

En DAX, on peut créer directement une mesure sans ajouter de colonne physique dans la table.

Créez une nouvelle mesure :

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

`SUMX` signifie :

```text
Parcourir chaque ligne d’une table,
évaluer une expression pour chaque ligne,
puis additionner les résultats.
```

Dans notre cas, Power BI fait ceci :

```text
Ligne 1 : 2 × 1000 = 2000
Ligne 2 : 10 × 25 = 250
Ligne 3 : 5 × 60 = 300
Ligne 4 : 1 × 1000 = 1000
Ligne 5 : 3 × 300 = 900
Ligne 6 : 8 × 25 = 200
Total = 4450
```

Différence importante :

| Formule                    | Signification                                           |
| -------------------------- | ------------------------------------------------------- |
| `SUM(Ventes[Montant])`     | Additionne une colonne déjà existante                   |
| `SUMX(Ventes, expression)` | Calcule une expression ligne par ligne, puis additionne |

Dans un tableau de bord professionnel, on privilégie souvent la mesure avec `SUMX`, car elle évite de créer une colonne supplémentaire si celle-ci n’est pas nécessaire.

---

# 10. Créer les mesures principales du tableau de bord

Nous allons maintenant créer les mesures principales.

---

## 10.1 Chiffre d’affaires

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Cette mesure calcule le total des ventes.

Résultat attendu sans filtre :

```text
4450
```

---

## 10.2 Coût total

```DAX
Coût total = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[CoutUnitaire]
)
```

Cette mesure calcule le coût total des produits vendus.

Résultat attendu sans filtre :

```text
2870
```

Détail du calcul :

| Produit         | Calcul  | Coût |
| --------------- | ------- | ---: |
| PC Québec       | 2 × 700 | 1400 |
| Souris Québec   | 10 × 10 |  100 |
| Clavier Ontario | 5 × 30  |  150 |
| PC Ontario      | 1 × 700 |  700 |
| Écran Québec    | 3 × 180 |  540 |
| Souris Ontario  | 8 × 10  |   80 |
| Total           |         | 2870 |

---

## 10.3 Marge

```DAX
Marge = [CA] - [Coût total]
```

Cette mesure calcule la différence entre le chiffre d’affaires et le coût total.

Résultat attendu sans filtre :

```text
1580
```

---

## 10.4 Taux de marge

```DAX
Taux de marge = DIVIDE(
    [Marge],
    [CA]
)
```

Cette mesure calcule la part de la marge dans le chiffre d’affaires.

Résultat attendu sans filtre :

```text
35,51 % environ
```

Pourquoi utiliser `DIVIDE` au lieu de `/` ?

Parce que `DIVIDE` gère mieux les divisions par zéro.

À éviter :

```DAX
Taux de marge = [Marge] / [CA]
```

À privilégier :

```DAX
Taux de marge = DIVIDE([Marge], [CA])
```

Si `[CA]` vaut 0, `DIVIDE` évite une erreur ou un résultat incorrect.

---

## 10.5 Nombre de ventes

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

Cette mesure compte le nombre de lignes dans la table `Ventes`.

Résultat attendu sans filtre :

```text
6
```

Si vous appliquez un filtre sur Québec, Power BI comptera seulement les lignes correspondant au Québec.

---

## 10.6 Quantité vendue

```DAX
Quantité vendue = SUM(Ventes[Quantité])
```

Cette mesure additionne toutes les quantités vendues.

Résultat attendu sans filtre :

```text
29
```

---

## 10.7 Prix moyen pondéré

Il ne faut pas confondre la moyenne simple des prix unitaires et le prix moyen pondéré.

Moyenne simple :

```DAX
Prix moyen simple = AVERAGE(Ventes[PrixUnitaire])
```

Cette mesure calcule la moyenne des prix unitaires présents dans la table.

Mais cette moyenne ne tient pas compte des quantités vendues.

Pour un tableau de bord de ventes, il est souvent plus pertinent de calculer le prix moyen pondéré :

```DAX
Prix moyen pondéré = DIVIDE(
    [CA],
    [Quantité vendue]
)
```

Cette mesure répond à la question suivante :

```text
En moyenne, combien rapporte une unité vendue ?
```

Résultat attendu sans filtre :

```text
153,45 environ
```

---

# 11. Comprendre le contexte de filtre

Le contexte de filtre est l’une des notions les plus importantes en DAX.

Une mesure DAX ne calcule jamais dans le vide. Elle calcule toujours dans un contexte.

Prenons cette mesure :

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Si vous placez cette mesure dans une carte Power BI sans aucun filtre, elle affiche le chiffre d’affaires total.

Résultat :

```text
4450
```

Mais si vous ajoutez un filtre sur la région Québec, la même mesure calcule uniquement les ventes du Québec.

Résultat :

```text
3150
```

Si vous ajoutez un filtre sur la région Ontario, la même mesure calcule uniquement les ventes de l’Ontario.

Résultat :

```text
1300
```

La formule n’a pas changé. C’est le contexte qui a changé.

| Contexte appliqué        | Résultat de `[CA]` |
| ------------------------ | -----------------: |
| Aucun filtre             |               4450 |
| Région = Québec          |               3150 |
| Région = Ontario         |               1300 |
| Produit = PC             |               3000 |
| Catégorie = Accessoire   |                750 |
| Catégorie = Informatique |               3700 |

À retenir :

```text
Une mesure DAX donne un résultat selon les filtres actifs dans le rapport.
```

Ces filtres peuvent venir :

* d’un segment ;
* d’un tableau ;
* d’un graphique ;
* d’une page ;
* d’une relation entre tables ;
* d’un filtre explicite dans une formule DAX.

---

# 12. Créer un tableau visuel par région

Dans Power BI, créez un visuel de type **Tableau**.

Ajoutez les champs suivants :

* `Région` ;
* `[CA]` ;
* `[Coût total]` ;
* `[Marge]` ;
* `[Taux de marge]`.

Résultat attendu :

| Région  |   CA | Coût total | Marge | Taux de marge |
| ------- | ---: | ---------: | ----: | ------------: |
| Québec  | 3150 |       2040 |  1110 |       35,24 % |
| Ontario | 1300 |        830 |   470 |       36,15 % |
| Total   | 4450 |       2870 |  1580 |       35,51 % |

Ce tableau montre que la même mesure `[CA]` se recalcule automatiquement pour chaque région.

---

# 13. CALCULATE : modifier le contexte de calcul

`CALCULATE` est l’une des fonctions les plus importantes de DAX.

Elle permet de calculer une expression dans un contexte de filtre modifié.

Autrement dit, `CALCULATE` permet de dire :

```text
Calcule cette mesure,
mais avec ce filtre précis.
```

---

## 13.1 Calculer le chiffre d’affaires du Québec

```DAX
CA Québec = CALCULATE(
    [CA],
    Ventes[Région] = "Québec"
)
```

Traduction :

```text
Calcule le chiffre d’affaires,
mais seulement pour les lignes où la région est Québec.
```

Résultat attendu :

```text
3150
```

---

## 13.2 Calculer le chiffre d’affaires de l’Ontario

```DAX
CA Ontario = CALCULATE(
    [CA],
    Ventes[Région] = "Ontario"
)
```

Résultat attendu :

```text
1300
```

---

## 13.3 Calculer le chiffre d’affaires de la catégorie Informatique

```DAX
CA Informatique = CALCULATE(
    [CA],
    Ventes[Catégorie] = "Informatique"
)
```

Résultat attendu :

```text
3700
```

---

## 13.4 Calculer le chiffre d’affaires de la catégorie Accessoire

```DAX
CA Accessoire = CALCULATE(
    [CA],
    Ventes[Catégorie] = "Accessoire"
)
```

Résultat attendu :

```text
750
```

---

# 14. Calculer le pourcentage du total

Une question fréquente dans un tableau de bord est :

```text
Quelle est la part de chaque région dans le chiffre d’affaires total ?
```

Pour répondre, il faut comparer :

* le chiffre d’affaires de la région actuelle ;
* le chiffre d’affaires total toutes régions confondues.

---

## 14.1 Mesure du total toutes régions

Créez la mesure suivante :

```DAX
CA total toutes régions = CALCULATE(
    [CA],
    REMOVEFILTERS(Ventes[Région])
)
```

Cette mesure calcule le chiffre d’affaires en ignorant le filtre sur la région.

---

## 14.2 Mesure du pourcentage du total

Créez ensuite :

```DAX
% du total région = DIVIDE(
    [CA],
    [CA total toutes régions]
)
```

Dans un tableau par région, vous devez obtenir :

| Région  |   CA | CA total toutes régions | % du total région |
| ------- | ---: | ----------------------: | ----------------: |
| Québec  | 3150 |                    4450 |           70,79 % |
| Ontario | 1300 |                    4450 |           29,21 % |
| Total   | 4450 |                    4450 |             100 % |

Explication :

```text
Pour Québec : 3150 / 4450 = 70,79 %
Pour Ontario : 1300 / 4450 = 29,21 %
```

---

# 15. IF : créer une mesure conditionnelle

La fonction `IF` permet de créer une condition.

Exemple :

```DAX
Performance = IF(
    [CA] >= 3000,
    "Bonne performance",
    "Performance faible"
)
```

Traduction :

```text
Si le chiffre d’affaires est supérieur ou égal à 3000,
alors afficher Bonne performance.
Sinon, afficher Performance faible.
```

Dans notre exemple :

| Contexte |   CA | Performance        |
| -------- | ---: | ------------------ |
| Total    | 4450 | Bonne performance  |
| Québec   | 3150 | Bonne performance  |
| Ontario  | 1300 | Performance faible |

---

# 16. SWITCH : gérer plusieurs niveaux de performance

Quand il y a plusieurs conditions, `SWITCH` est souvent plus lisible que plusieurs `IF` imbriqués.

Créez cette mesure :

```DAX
Niveau performance = SWITCH(
    TRUE(),
    [CA] >= 4000, "Excellent",
    [CA] >= 2000, "Bon",
    [CA] >= 1000, "Moyen",
    "Faible"
)
```

Traduction :

```text
Si CA >= 4000 : Excellent
Sinon si CA >= 2000 : Bon
Sinon si CA >= 1000 : Moyen
Sinon : Faible
```

Exemple de résultat :

| Contexte |   CA | Niveau performance |
| -------- | ---: | ------------------ |
| Total    | 4450 | Excellent          |
| Québec   | 3150 | Bon                |
| Ontario  | 1300 | Moyen              |

---

# 17. COUNTROWS : compter les lignes

La fonction `COUNTROWS` compte le nombre de lignes d’une table.

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

Résultat attendu sans filtre :

```text
6
```

Avec un filtre sur Québec :

```text
3
```

Avec un filtre sur Ontario :

```text
3
```

La mesure respecte donc le contexte de filtre.

---

# 18. DISTINCTCOUNT : compter les valeurs différentes

La fonction `DISTINCTCOUNT` compte le nombre de valeurs différentes dans une colonne.

Créez cette mesure :

```DAX
Nombre de produits = DISTINCTCOUNT(Ventes[Produit])
```

Dans notre table, les produits sont :

```text
PC
Souris
Clavier
PC
Écran
Souris
```

Les produits différents sont :

```text
PC
Souris
Clavier
Écran
```

Résultat attendu :

```text
4
```

---

# 19. Créer une table calendrier

Pour travailler correctement avec les dates, il est recommandé de créer une table calendrier.

Une table calendrier permet d’analyser les données par :

* jour ;
* mois ;
* trimestre ;
* année ;
* période cumulée ;
* comparaison avec le mois précédent ;
* comparaison avec l’année précédente.

Dans Power BI :

1. Cliquez sur **Modélisation**.
2. Cliquez sur **Nouvelle table**.
3. Écrivez la formule suivante.

```DAX
Calendrier = CALENDAR(
    MIN(Ventes[Date]),
    MAX(Ventes[Date])
)
```

Cette formule crée une table contenant toutes les dates comprises entre la première date de vente et la dernière date de vente.

---

# 20. Ajouter des colonnes à la table calendrier

Dans la table **Calendrier**, créez les colonnes suivantes.

---

## 20.1 Année

```DAX
Année = YEAR(Calendrier[Date])
```

---

## 20.2 Mois

```DAX
Mois = FORMAT(Calendrier[Date], "MMMM")
```

---

## 20.3 Numéro du mois

```DAX
Numéro mois = MONTH(Calendrier[Date])
```

---

## 20.4 Année-mois

```DAX
Année-Mois = FORMAT(Calendrier[Date], "YYYY-MM")
```

Cette colonne est utile pour afficher les données mensuelles dans un graphique.

---

# 21. Relier la table calendrier à la table ventes

Après avoir créé la table calendrier, il faut créer une relation entre les deux tables.

Dans Power BI :

1. Allez dans la vue **Modèle**.
2. Repérez la table **Ventes**.
3. Repérez la table **Calendrier**.
4. Reliez `Calendrier[Date]` à `Ventes[Date]`.

La relation doit être :

```text
Calendrier[Date] 1  →  * Ventes[Date]
```

Cela signifie :

* une date dans la table Calendrier peut correspondre à plusieurs ventes ;
* chaque vente possède une date.

La table Calendrier devient donc une dimension temporelle.

---

# 22. Marquer la table calendrier comme table de dates

Dans Power BI, il est recommandé de marquer la table calendrier comme table de dates.

Étapes :

1. Sélectionnez la table **Calendrier**.
2. Cliquez sur **Outils de table**.
3. Cliquez sur **Marquer comme table de dates**.
4. Choisissez la colonne `Date`.
5. Validez.

Cette étape aide Power BI à comprendre que la table Calendrier doit être utilisée pour les analyses temporelles.

---

# 23. Calculer le chiffre d’affaires cumulé

Le chiffre d’affaires cumulé permet de suivre l’évolution du CA depuis le début de l’année.

Créez cette mesure :

```DAX
CA cumulé année = TOTALYTD(
    [CA],
    Calendrier[Date]
)
```

Traduction :

```text
Additionner le chiffre d’affaires depuis le début de l’année
jusqu’à la date actuellement affichée dans le rapport.
```

Cette mesure est utile pour les graphiques d’évolution.

---

# 24. Comparer avec le mois précédent

Pour comparer le chiffre d’affaires avec le mois précédent, créez la mesure suivante :

```DAX
CA mois précédent = CALCULATE(
    [CA],
    DATEADD(Calendrier[Date], -1, MONTH)
)
```

Cette mesure récupère le chiffre d’affaires du mois précédent.

Ensuite, créez la variation en valeur :

```DAX
Variation CA = [CA] - [CA mois précédent]
```

Puis la variation en pourcentage :

```DAX
Variation CA % = DIVIDE(
    [Variation CA],
    [CA mois précédent]
)
```

Ces mesures permettent de répondre à une question métier classique :

```text
Est-ce que les ventes ont augmenté ou diminué par rapport au mois précédent ?
```

---

# 25. Créer les visuels du tableau de bord

Une fois les mesures créées, vous pouvez construire un tableau de bord simple.

---

## 25.1 Cartes KPI

Créez trois cartes :

| Carte   | Champ à utiliser  |
| ------- | ----------------- |
| Carte 1 | `[CA]`            |
| Carte 2 | `[Marge]`         |
| Carte 3 | `[Taux de marge]` |

Résultat attendu :

| KPI           | Résultat attendu |
| ------------- | ---------------: |
| CA            |             4450 |
| Marge         |             1580 |
| Taux de marge |          35,51 % |

---

## 25.2 Tableau par région

Créez un tableau avec :

* `Région` ;
* `[CA]` ;
* `[Coût total]` ;
* `[Marge]` ;
* `[% du total région]`.

Résultat attendu :

| Région  |   CA | Coût total | Marge | % du total région |
| ------- | ---: | ---------: | ----: | ----------------: |
| Québec  | 3150 |       2040 |  1110 |           70,79 % |
| Ontario | 1300 |        830 |   470 |           29,21 % |
| Total   | 4450 |       2870 |  1580 |             100 % |

---

## 25.3 Graphique en colonnes par produit

Créez un graphique en colonnes avec :

| Zone du visuel | Champ     |
| -------------- | --------- |
| Axe            | `Produit` |
| Valeurs        | `[CA]`    |

Résultat attendu par produit :

| Produit |   CA |
| ------- | ---: |
| PC      | 3000 |
| Écran   |  900 |
| Souris  |  450 |
| Clavier |  300 |

---

## 25.4 Graphique par catégorie

Créez un graphique avec :

| Zone du visuel | Champ       |
| -------------- | ----------- |
| Légende ou axe | `Catégorie` |
| Valeurs        | `[CA]`      |

Résultat attendu :

| Catégorie    |   CA |
| ------------ | ---: |
| Informatique | 3700 |
| Accessoire   |  750 |

---

## 25.5 Segments de filtre

Ajoutez deux segments :

| Segment   | Champ     |
| --------- | --------- |
| Segment 1 | `Région`  |
| Segment 2 | `Produit` |

Ces segments permettent de filtrer dynamiquement tout le tableau de bord.

Exemple :

Si vous cliquez sur Québec, les cartes, les tableaux et les graphiques affichent uniquement les données du Québec.

---

# 26. Formater les mesures

Le formatage est important pour rendre le tableau de bord lisible et professionnel.

Sélectionnez chaque mesure et appliquez le bon format.

| Mesure                 | Format recommandé           |
| ---------------------- | --------------------------- |
| `[CA]`                 | Monétaire                   |
| `[Coût total]`         | Monétaire                   |
| `[Marge]`              | Monétaire                   |
| `[Taux de marge]`      | Pourcentage                 |
| `[% du total région]`  | Pourcentage                 |
| `[Quantité vendue]`    | Nombre entier               |
| `[Nombre de ventes]`   | Nombre entier               |
| `[Prix moyen pondéré]` | Monétaire ou nombre décimal |
| `[Variation CA %]`     | Pourcentage                 |

Un bon formatage permet de distinguer rapidement les montants, les pourcentages et les volumes.

---

# 27. Tableau complet des mesures à créer

Voici la liste complète des mesures importantes du tutoriel.

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

```DAX
Coût total = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[CoutUnitaire]
)
```

```DAX
Marge = [CA] - [Coût total]
```

```DAX
Taux de marge = DIVIDE(
    [Marge],
    [CA]
)
```

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

```DAX
Quantité vendue = SUM(Ventes[Quantité])
```

```DAX
Prix moyen pondéré = DIVIDE(
    [CA],
    [Quantité vendue]
)
```

```DAX
Nombre de produits = DISTINCTCOUNT(Ventes[Produit])
```

```DAX
CA Québec = CALCULATE(
    [CA],
    Ventes[Région] = "Québec"
)
```

```DAX
CA Ontario = CALCULATE(
    [CA],
    Ventes[Région] = "Ontario"
)
```

```DAX
CA Informatique = CALCULATE(
    [CA],
    Ventes[Catégorie] = "Informatique"
)
```

```DAX
CA Accessoire = CALCULATE(
    [CA],
    Ventes[Catégorie] = "Accessoire"
)
```

```DAX
CA total toutes régions = CALCULATE(
    [CA],
    REMOVEFILTERS(Ventes[Région])
)
```

```DAX
% du total région = DIVIDE(
    [CA],
    [CA total toutes régions]
)
```

```DAX
Performance = IF(
    [CA] >= 3000,
    "Bonne performance",
    "Performance faible"
)
```

```DAX
Niveau performance = SWITCH(
    TRUE(),
    [CA] >= 4000, "Excellent",
    [CA] >= 2000, "Bon",
    [CA] >= 1000, "Moyen",
    "Faible"
)
```

```DAX
CA cumulé année = TOTALYTD(
    [CA],
    Calendrier[Date]
)
```

```DAX
CA mois précédent = CALCULATE(
    [CA],
    DATEADD(Calendrier[Date], -1, MONTH)
)
```

```DAX
Variation CA = [CA] - [CA mois précédent]
```

```DAX
Variation CA % = DIVIDE(
    [Variation CA],
    [CA mois précédent]
)
```

---

# 28. Résultats attendus pour vérifier le travail

Utilisez ce tableau pour vérifier vos mesures.

| Indicateur         | Résultat attendu |
| ------------------ | ---------------: |
| CA                 |             4450 |
| Coût total         |             2870 |
| Marge              |             1580 |
| Taux de marge      |          35,51 % |
| Nombre de ventes   |                6 |
| Quantité vendue    |               29 |
| Prix moyen pondéré |           153,45 |
| Nombre de produits |                4 |
| CA Québec          |             3150 |
| CA Ontario         |             1300 |
| CA Informatique    |             3700 |
| CA Accessoire      |              750 |
| % Québec           |          70,79 % |
| % Ontario          |          29,21 % |

Si vos résultats sont différents, vérifiez les points suivants :

* les données ont-elles été copiées correctement ?
* les colonnes numériques sont-elles bien au format nombre ?
* la colonne Date est-elle bien au format Date ?
* les noms des colonnes sont-ils identiques aux formules ?
* les accents dans les noms de colonnes sont-ils respectés ?
* les mesures ont-elles été créées dans la bonne table ?
* le visuel contient-il un filtre actif ?

---

# 29. Erreurs fréquentes à éviter

## 29.1 Tout faire avec des colonnes calculées

Une erreur fréquente consiste à créer trop de colonnes calculées.

Exemple :

```DAX
Montant = Ventes[Quantité] * Ventes[PrixUnitaire]
```

Cette colonne est utile pour comprendre le fonctionnement ligne par ligne.

Mais pour un tableau de bord dynamique, il est souvent préférable d’utiliser une mesure :

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Les mesures sont plus adaptées aux KPI, aux filtres et aux visuels interactifs.

---

## 29.2 Ne pas comprendre le contexte de filtre

Une mesure peut changer selon :

* le filtre de page ;
* le segment sélectionné ;
* la région dans un tableau ;
* le produit dans un graphique ;
* la relation entre deux tables.

Ce n’est pas une anomalie. C’est le comportement normal de DAX.

---

## 29.3 Oublier la table calendrier

Pour les analyses par date, il est recommandé de créer une vraie table calendrier.

Sans table calendrier, les comparaisons temporelles peuvent être limitées ou incorrectes.

---

## 29.4 Utiliser `/` au lieu de `DIVIDE`

À éviter :

```DAX
Taux de marge = [Marge] / [CA]
```

À privilégier :

```DAX
Taux de marge = DIVIDE([Marge], [CA])
```

`DIVIDE` protège contre les problèmes de division par zéro.

---

## 29.5 Oublier de formater les mesures

Une mesure de pourcentage affichée sous forme décimale peut être difficile à lire.

Exemple :

```text
0,3551
```

Il faut la formater en pourcentage pour obtenir :

```text
35,51 %
```

---

# 30. Mini-projet final

## Objectif

Créer un mini tableau de bord Power BI permettant d’analyser les ventes par région, produit et catégorie.

Le tableau de bord doit permettre de répondre aux questions suivantes :

* Quel est le chiffre d’affaires total ?
* Quelle est la marge totale ?
* Quel est le taux de marge ?
* Quelle région génère le plus de chiffre d’affaires ?
* Quel produit génère le plus de ventes ?
* Quelle catégorie domine les ventes ?
* Quelle est la part de chaque région dans le total ?
* Comment les résultats changent-ils lorsqu’on applique un filtre ?

---

## 30.1 Données à utiliser

Utilisez la table **Ventes** fournie au début du tutoriel.

---

## 30.2 Mesures obligatoires

Le tableau de bord doit contenir au minimum les mesures suivantes :

* `[CA]` ;
* `[Coût total]` ;
* `[Marge]` ;
* `[Taux de marge]` ;
* `[Nombre de ventes]` ;
* `[Quantité vendue]` ;
* `[Prix moyen pondéré]` ;
* `[CA Québec]` ;
* `[CA Ontario]` ;
* `[CA total toutes régions]` ;
* `[% du total région]`.

---

## 30.3 Visuels obligatoires

Le rapport doit contenir :

| Visuel                  | Champs à utiliser                                  |
| ----------------------- | -------------------------------------------------- |
| Carte 1                 | `[CA]`                                             |
| Carte 2                 | `[Marge]`                                          |
| Carte 3                 | `[Taux de marge]`                                  |
| Tableau                 | `Région`, `[CA]`, `[Marge]`, `[% du total région]` |
| Graphique en colonnes   | `Produit` + `[CA]`                                 |
| Graphique par catégorie | `Catégorie` + `[CA]`                               |
| Segment                 | `Région`                                           |
| Segment                 | `Produit`                                          |

---

## 30.4 Validation attendue

Le tableau de bord doit afficher les résultats suivants sans filtre :

| KPI                | Résultat attendu |
| ------------------ | ---------------: |
| CA                 |             4450 |
| Coût total         |             2870 |
| Marge              |             1580 |
| Taux de marge      |          35,51 % |
| Nombre de ventes   |                6 |
| Quantité vendue    |               29 |
| Nombre de produits |                4 |

Si ces valeurs ne sont pas obtenues, il faut corriger les données, les types de colonnes ou les formules DAX.

---

# 31. Travail à réaliser

Vous devez reproduire le travail présenté dans la vidéo suivante :

[https://www.youtube.com/watch?v=waG_JhBgUpM](https://www.youtube.com/watch?v=waG_JhBgUpM)

Vous devez également utiliser les données fournies ici :

[https://onedrive.live.com/?redeem=aHR0cHM6Ly8xZHJ2Lm1zL3UvcyFBbXhyb2ZaWmxaLXdoTUlnUzlXSlM3QndTZkhCYnc_ZT0wejNuUW4&id=B09F9559F6A16B6C!74016&cid=B09F9559F6A16B6C](https://onedrive.live.com/?redeem=aHR0cHM6Ly8xZHJ2Lm1zL3UvcyFBbXhyb2ZaWmxaLXdoTUlnUzlXSlM3QndTZkhCYnc_ZT0wejNuUW4&id=B09F9559F6A16B6C!74016&cid=B09F9559F6A16B6C)

Le travail doit démontrer que vous êtes capable de :

* importer les données dans Power BI ;
* vérifier les types de données ;
* identifier la table de faits ;
* créer les mesures DAX principales ;
* créer une table calendrier ;
* relier les tables correctement ;
* créer des visuels pertinents ;
* utiliser des segments de filtre ;
* valider les résultats ;
* expliquer brièvement les mesures utilisées.

---

# 32. Résumé final à retenir

Voici les idées essentielles du tutoriel :

```text
Power Query prépare les données.
DAX calcule les indicateurs.
Power BI affiche les résultats.
```

```text
Une table de faits contient les valeurs mesurables.
Une table de dimensions contient les axes d’analyse.
```

```text
Une colonne calculée travaille ligne par ligne.
Une mesure calcule un résultat dynamique selon le contexte.
```

```text
SUM additionne une colonne.
SUMX calcule ligne par ligne puis additionne.
CALCULATE modifie le contexte de calcul.
DIVIDE effectue une division plus sûre.
COUNTROWS compte les lignes.
DISTINCTCOUNT compte les valeurs différentes.
REMOVEFILTERS enlève un filtre précis.
```

Phrase la plus importante à retenir :

```text
DAX ne calcule jamais dans le vide.
DAX calcule toujours dans un contexte.
```

Lorsque cette idée est comprise, les mesures Power BI deviennent beaucoup plus faciles à interpréter.
