# Tutoriel DAX Power BI pour débutant

## 1. C’est quoi DAX ?

**DAX** signifie **Data Analysis Expressions**. C’est le langage utilisé dans Power BI pour créer des calculs, des mesures, des colonnes calculées et des indicateurs dynamiques. Microsoft le définit comme une bibliothèque de fonctions et d’opérateurs utilisée dans Power BI, Analysis Services et Power Pivot. ([Microsoft Learn][1])

> Travail à implémenter à la fin de ce tuto: https://www.youtube.com/watch?v=waG_JhBgUpM 

Très simplement :

> **Power Query prépare les données.**
> **DAX calcule les indicateurs.**
> **Power BI affiche les résultats.**

Exemple :

Tu as une table de ventes :

| Produit | Quantité | Prix |
| ------- | -------: | ---: |
| PC      |        2 | 1000 |
| Souris  |        5 |   20 |

Avec DAX, tu peux calculer :

```DAX
Chiffre d'affaires = Quantité × Prix
```

Mais dans Power BI, ce calcul peut changer automatiquement selon :

* l’année sélectionnée ;
* la région sélectionnée ;
* le produit sélectionné ;
* le client sélectionné.

C’est ça la puissance de DAX.

---

# 2. Créer un petit exemple dans Power BI

Dans Power BI Desktop :

1. Clique sur **Entrer des données**.
2. Crée une table appelée **Ventes**.
3. Copie ces données :

| Date       | Produit | Catégorie    | Région  | Quantité | PrixUnitaire | CoutUnitaire |
| ---------- | ------- | ------------ | ------- | -------: | -----------: | -----------: |
| 2025-01-05 | PC      | Informatique | Québec  |        2 |         1000 |          700 |
| 2025-01-10 | Souris  | Accessoire   | Québec  |       10 |           25 |           10 |
| 2025-02-03 | Clavier | Accessoire   | Ontario |        5 |           60 |           30 |
| 2025-02-18 | PC      | Informatique | Ontario |        1 |         1000 |          700 |
| 2025-03-02 | Écran   | Informatique | Québec  |        3 |          300 |          180 |
| 2025-03-15 | Souris  | Accessoire   | Ontario |        8 |           25 |           10 |

---

# 3. La première idée importante : colonne calculée ou mesure ?

Dans Power BI, tu vas souvent hésiter entre deux choses :

## Colonne calculée

Une **colonne calculée** ajoute une nouvelle colonne dans la table.

Exemple :

| Quantité | PrixUnitaire | Montant |
| -------: | -----------: | ------: |
|        2 |         1000 |    2000 |
|       10 |           25 |     250 |

Elle travaille **ligne par ligne**.

## Mesure

Une **mesure** calcule un résultat global.

Exemple :

```DAX
Chiffre d'affaires total = 4450
```

Mais ce résultat peut changer selon le filtre.

Si tu filtres Québec, la mesure donne seulement le chiffre d’affaires du Québec.

Si tu filtres Ontario, elle donne seulement celui de l’Ontario.

Donc :

| Besoin                                           | Utiliser         |
| ------------------------------------------------ | ---------------- |
| Calculer une valeur ligne par ligne              | Colonne calculée |
| Calculer un total, une moyenne, un ratio, un KPI | Mesure           |
| Faire un tableau de bord dynamique               | Mesure           |

---

# 4. Ta première colonne calculée

Dans Power BI :

1. Va dans la table **Ventes**.
2. Clique sur **Nouvelle colonne**.
3. Écris :

```DAX
Montant = Ventes[Quantité] * Ventes[PrixUnitaire]
```

Explication simple :

Power BI lit chaque ligne :

```text
Ligne 1 : 2 × 1000 = 2000
Ligne 2 : 10 × 25 = 250
Ligne 3 : 5 × 60 = 300
```

Ici, DAX agit comme Excel.

---

# 5. Ta première mesure DAX

Maintenant, crée une **mesure**.

Dans Power BI :

1. Clique droit sur la table **Ventes**.
2. Choisis **Nouvelle mesure**.
3. Écris :

```DAX
CA = SUM(Ventes[Montant])
```

**CA** signifie **chiffre d’affaires**.

Cette mesure additionne toute la colonne `Montant`.

Microsoft rappelle qu’une formule DAX utilise des tables, des colonnes, des opérateurs et des fonctions, et que le comportement dépend du contexte dans lequel la formule est utilisée. ([Microsoft Learn][2])

---

# 6. Version plus professionnelle : utiliser SUMX

Au lieu de créer une colonne `Montant`, on peut créer directement une mesure :

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

`SUMX` veut dire :

> Parcours chaque ligne de la table, calcule Quantité × PrixUnitaire, puis additionne tout.

Microsoft définit `SUMX` comme une fonction qui additionne une expression évaluée ligne par ligne sur une table. ([Microsoft Learn][3])

Image mentale :

```text
Power BI prend la ligne 1 : calcule le montant.
Power BI prend la ligne 2 : calcule le montant.
Power BI prend la ligne 3 : calcule le montant.
À la fin, il additionne tout.
```

Donc :

```DAX
SUM(Ventes[Montant])
```

veut dire :

> Additionne une colonne déjà existante.

Mais :

```DAX
SUMX(Ventes, Ventes[Quantité] * Ventes[PrixUnitaire])
```

veut dire :

> Calcule une expression ligne par ligne, puis additionne.

---

# 7. Créer les mesures principales

Crée maintenant ces mesures.

## Chiffre d’affaires

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

## Coût total

```DAX
Coût total = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[CoutUnitaire]
)
```

## Marge

```DAX
Marge = [CA] - [Coût total]
```

## Taux de marge

```DAX
Taux de marge = DIVIDE(
    [Marge],
    [CA]
)
```

Pourquoi utiliser `DIVIDE` au lieu de `/` ?

Parce que `DIVIDE` gère mieux les divisions par zéro.

Exemple dangereux :

```DAX
[Marge] / [CA]
```

Si `[CA] = 0`, tu peux avoir une erreur.

Version propre :

```DAX
DIVIDE([Marge], [CA])
```

---

# 8. Comprendre le contexte de filtre

C’est probablement **la notion la plus importante en DAX**.

Imagine que ta mesure est :

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Si tu mets cette mesure dans une carte Power BI, elle donne le total général.

Mais si tu ajoutes un filtre Région = Québec, alors la même mesure calcule seulement Québec.

La mesure ne change pas.

C’est le contexte qui change.

Exemple :

| Filtre appliqué        |    Résultat de `[CA]` |
| ---------------------- | --------------------: |
| Aucun filtre           |          Total global |
| Région = Québec        |          Total Québec |
| Région = Ontario       |         Total Ontario |
| Produit = PC           |          Total des PC |
| Catégorie = Accessoire | Total des accessoires |

Donc une mesure DAX est comme une personne intelligente qui dit :

> Donne-moi le contexte, et je te donne le bon résultat.

---

# 9. Créer un tableau visuel

Dans Power BI, crée un tableau avec :

* `Région`
* `[CA]`
* `[Coût total]`
* `[Marge]`
* `[Taux de marge]`

Tu obtiendras quelque chose comme :

| Région  |  CA | Coût total | Marge | Taux de marge |
| ------- | --: | ---------: | ----: | ------------: |
| Québec  | ... |        ... |   ... |           ... |
| Ontario | ... |        ... |   ... |           ... |

La même mesure `[CA]` se recalcule automatiquement pour chaque région.

---

# 10. CALCULATE : la fonction la plus importante de DAX

`CALCULATE` est la fonction reine de DAX.

Elle sert à dire :

> Calcule cette mesure, mais dans un contexte modifié.

Microsoft explique que `CALCULATE` évalue une expression dans un contexte de filtre modifié. ([Microsoft Learn][4])

Exemple :

```DAX
CA Québec = CALCULATE(
    [CA],
    Ventes[Région] = "Québec"
)
```

Traduction en français :

```text
Calcule le chiffre d’affaires,
mais seulement pour les lignes où Région = Québec.
```

Autre exemple :

```DAX
CA Informatique = CALCULATE(
    [CA],
    Ventes[Catégorie] = "Informatique"
)
```

Traduction :

```text
Calcule le chiffre d’affaires,
mais seulement pour la catégorie Informatique.
```

---

# 11. Pourcentage du total

Supposons que tu veux savoir :

> Québec représente combien du chiffre d’affaires total ?

Crée cette mesure :

```DAX
CA total toutes régions = CALCULATE(
    [CA],
    REMOVEFILTERS(Ventes[Région])
)
```

Puis :

```DAX
% du total région = DIVIDE(
    [CA],
    [CA total toutes régions]
)
```

Explication :

* `[CA]` respecte le filtre actuel.
* `[CA total toutes régions]` ignore le filtre Région.
* Donc le ratio donne la part de chaque région.

Exemple :

| Région  |   CA | CA total toutes régions | % du total |
| ------- | ---: | ----------------------: | ---------: |
| Québec  | 3150 |                    4450 |     70,8 % |
| Ontario | 1300 |                    4450 |     29,2 % |

---

# 12. IF : créer une logique conditionnelle

Tu peux créer une mesure qui classe la performance.

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
alors afficher "Bonne performance",
sinon afficher "Performance faible".
```

---

# 13. SWITCH : mieux que plusieurs IF

Quand il y a plusieurs conditions, `SWITCH` est plus propre.

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

---

# 14. COUNTROWS : compter les lignes

Pour compter le nombre de ventes :

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

Exemple :

Si ta table contient 6 lignes, le résultat sera 6.

Mais si tu filtres Québec, Power BI compte seulement les lignes du Québec.

---

# 15. DISTINCTCOUNT : compter sans doublons

Pour compter le nombre de produits différents :

```DAX
Nombre de produits = DISTINCTCOUNT(Ventes[Produit])
```

Si tu as :

```text
PC
Souris
Clavier
PC
Souris
Écran
```

Le résultat est :

```text
4 produits différents
```

Parce que PC et Souris apparaissent plusieurs fois.

---

# 16. AVERAGE : moyenne simple

Prix moyen :

```DAX
Prix moyen = AVERAGE(Ventes[PrixUnitaire])
```

Attention : c’est la moyenne des prix unitaires, pas forcément le prix moyen pondéré par quantité.

Pour un prix moyen plus intelligent :

```DAX
Prix moyen pondéré = DIVIDE(
    [CA],
    SUM(Ventes[Quantité])
)
```

Pourquoi ?

Parce que si tu vends beaucoup de souris et peu de PC, la quantité doit influencer la moyenne.

---

# 17. Créer une table calendrier

Pour travailler avec les dates, crée une table calendrier.

Dans Power BI :

1. Clique sur **Nouvelle table**.
2. Écris :

```DAX
Calendrier = CALENDAR(
    MIN(Ventes[Date]),
    MAX(Ventes[Date])
)
```

Ensuite, ajoute des colonnes :

```DAX
Année = YEAR(Calendrier[Date])
```

```DAX
Mois = FORMAT(Calendrier[Date], "MMMM")
```

```DAX
Numéro mois = MONTH(Calendrier[Date])
```

Après cela :

1. Va dans la vue **Modèle**.
2. Relie `Calendrier[Date]` à `Ventes[Date]`.
3. Marque `Calendrier` comme table de dates.

Microsoft indique que les fonctions de time intelligence manipulent des périodes comme jours, mois, trimestres et années, et qu’il faut marquer une table contenant une colonne de dates comme table de dates avant de les utiliser correctement. ([Microsoft Learn][5])

---

# 18. Calculer le CA cumulé

Exemple : chiffre d’affaires cumulé depuis le début de l’année.

```DAX
CA cumulé année = TOTALYTD(
    [CA],
    Calendrier[Date]
)
```

Traduction :

```text
Additionne le chiffre d’affaires depuis le début de l’année jusqu’à la date actuelle.
```

C’est utile pour faire des graphiques d’évolution.

---

# 19. Comparer avec le mois précédent

```DAX
CA mois précédent = CALCULATE(
    [CA],
    DATEADD(Calendrier[Date], -1, MONTH)
)
```

Puis :

```DAX
Variation CA = [CA] - [CA mois précédent]
```

Et :

```DAX
Variation CA % = DIVIDE(
    [Variation CA],
    [CA mois précédent]
)
```

Cela permet de répondre à une question métier très classique :

> Est-ce qu’on vend plus ou moins que le mois dernier ?

---

# 20. Les erreurs fréquentes des débutants

## Erreur 1 : tout faire en colonnes calculées

Mauvais réflexe :

```DAX
Montant = Quantité × Prix
```

Puis tout calculer avec des colonnes.

Meilleur réflexe :

```DAX
CA = SUMX(Ventes, Ventes[Quantité] * Ventes[PrixUnitaire])
```

Les mesures sont souvent préférables pour les KPI et tableaux de bord dynamiques.

## Erreur 2 : ne pas comprendre le filtre

Une mesure change selon :

* les segments ;
* les filtres ;
* les lignes du tableau ;
* les colonnes du graphique.

Ce n’est pas une erreur. C’est le fonctionnement normal de DAX.

## Erreur 3 : oublier la table calendrier

Pour les calculs par mois, trimestre, année ou comparaison temporelle, crée toujours une vraie table calendrier.

## Erreur 4 : utiliser `/` partout

À éviter :

```DAX
Taux = [Marge] / [CA]
```

Préférer :

```DAX
Taux = DIVIDE([Marge], [CA])
```

---

# 21. Mini-projet final

Objectif : créer un mini tableau de bord de ventes.

## Mesures à créer

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

---

# 22. Visuels à créer dans Power BI

Crée ces éléments :

| Visuel                | Champs à utiliser                                |
| --------------------- | ------------------------------------------------ |
| Carte 1               | `[CA]`                                           |
| Carte 2               | `[Marge]`                                        |
| Carte 3               | `[Taux de marge]`                                |
| Tableau               | Région, `[CA]`, `[Marge]`, `[% du total région]` |
| Graphique en colonnes | Produit + `[CA]`                                 |
| Graphique circulaire  | Catégorie + `[CA]`                               |
| Segment               | Région                                           |
| Segment               | Produit                                          |

---

# 23. Résumé ultra-simple

À retenir :

```text
SUM = additionner une colonne.
SUMX = calculer ligne par ligne puis additionner.
CALCULATE = changer le contexte de calcul.
DIVIDE = division propre.
COUNTROWS = compter les lignes.
DISTINCTCOUNT = compter les valeurs différentes.
FILTER / REMOVEFILTERS = contrôler les filtres.
```

> Vidéo :  https://www.youtube.com/watch?v=waG_JhBgUpM 

À RETENIR :

> **DAX ne calcule jamais dans le vide. Il calcule toujours dans un contexte.**

Quand tu comprends ça, tu commences vraiment à comprendre Power BI.

[1]: https://learn.microsoft.com/en-us/dax/ "Data Analysis Expressions (DAX) Reference - DAX | Microsoft Learn"
[2]: https://learn.microsoft.com/en-us/dax/dax-syntax-reference "DAX syntax - DAX | Microsoft Learn"
[3]: https://learn.microsoft.com/en-us/dax/sumx-function-dax "SUMX function (DAX) - DAX | Microsoft Learn"
[4]: https://learn.microsoft.com/en-us/dax/calculate-function-dax "CALCULATE function (DAX) - DAX | Microsoft Learn"
[5]: https://learn.microsoft.com/en-us/dax/time-intelligence-functions-dax "Time intelligence functions (DAX) - DAX | Microsoft Learn"
