<a id="top"></a>

# Tutoriel DAX Power BI pour débuter

## Objectif général du document

<details open>
<summary>Lire l’objectif du tutoriel</summary>

Ce document présente une introduction progressive à **DAX dans Power BI**. Il est conçu pour une personne qui découvre Power BI et qui souhaite comprendre les premières notions indispensables avant de construire un tableau de bord.

L’objectif n’est pas seulement de recopier des formules. L’objectif est de comprendre :

* ce que chaque formule calcule ;
* pourquoi cette formule est utilisée ;
* dans quel contexte elle doit être utilisée ;
* comment vérifier que le résultat obtenu est correct ;
* comment interpréter les résultats affichés dans Power BI.

À la fin de ce tutoriel, vous serez capable de :

* comprendre à quoi sert DAX dans Power BI ;
* distinguer Power Query, DAX et les visuels Power BI ;
* créer une table de données simple ;
* comprendre ce qu’est une table de faits ;
* comprendre ce qu’est une table de dimensions ;
* faire la différence entre une colonne calculée et une mesure ;
* créer des mesures DAX de base ;
* utiliser les fonctions `SUM`, `SUMX`, `DIVIDE`, `COUNTROWS`, `DISTINCTCOUNT`, `CALCULATE` et `REMOVEFILTERS` ;
* comprendre le contexte de filtre ;
* créer une table calendrier ;
* créer des relations entre les tables ;
* construire un mini tableau de bord de ventes ;
* vérifier vos résultats avec des valeurs attendues.

Le tutoriel avance volontairement étape par étape. Chaque partie introduit une notion, l’explique avec des mots simples, puis montre comment l’appliquer dans Power BI.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

## Sommaire

| # | Section |
|---:|---|
| 1 | [Comprendre à quoi sert DAX dans Power BI](#section-1) |
| 2 | [Comprendre la notion de table de faits](#section-2) |
| 3 | [Comprendre les tables de dimensions](#section-3) |
| 4 | [Créer les données de départ dans Power BI](#section-4) |
| 5 | [Vérifier les types de données](#section-5) |
| 6 | [Colonne calculée ou mesure : différence fondamentale](#section-6) |
| 7 | [Créer une première colonne calculée](#section-7) |
| 8 | [Créer une première mesure DAX avec SUM](#section-8) |
| 9 | [Créer une mesure plus professionnelle avec SUMX](#section-9) |
| 10 | [Créer les mesures principales du tableau de bord](#section-10) |
| 11 | [Comprendre le contexte de filtre](#section-11) |
| 12 | [Créer un tableau visuel par région](#section-12) |
| 13 | [CALCULATE : modifier le contexte de calcul](#section-13) |
| 14 | [Calculer le pourcentage du total](#section-14) |
| 15 | [IF : créer une mesure conditionnelle](#section-15) |
| 16 | [SWITCH : gérer plusieurs niveaux de performance](#section-16) |
| 17 | [COUNTROWS : compter les lignes](#section-17) |
| 18 | [DISTINCTCOUNT : compter les valeurs différentes](#section-18) |
| 19 | [Créer une table calendrier](#section-19) |
| 20 | [Ajouter des colonnes à la table calendrier](#section-20) |
| 21 | [Relier la table calendrier à la table Ventes](#section-21) |
| 22 | [Marquer la table calendrier comme table de dates](#section-22) |
| 23 | [Calculer le chiffre d’affaires cumulé](#section-23) |
| 24 | [Comparer avec le mois précédent](#section-24) |
| 25 | [Créer les visuels du tableau de bord](#section-25) |
| 26 | [Formater les mesures](#section-26) |
| 27 | [Tableau complet des mesures à créer](#section-27) |
| 28 | [Résultats attendus pour vérifier le travail](#section-28) |
| 29 | [Erreurs fréquentes à éviter](#section-29) |
| 30 | [Mini-projet final](#section-30) |
| 31 | [Travail à réaliser](#section-31) |
| 32 | [Résumé final à retenir](#section-32) |

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-1"></a>

# 1. Comprendre à quoi sert DAX dans Power BI

<details open>
<summary>Comprendre le rôle de DAX dans les rapports et tableaux de bord Power BI</summary>

DAX signifie **Data Analysis Expressions**. C’est le langage de calcul utilisé dans Power BI pour créer des formules, des mesures, des colonnes calculées et des indicateurs.

Power BI permet d’importer des données, de les transformer, de les relier et de les afficher sous forme de graphiques. Cependant, pour obtenir des indicateurs utiles comme le chiffre d’affaires, la marge, le taux de marge ou la part d’une région dans le total, il faut créer des calculs. C’est le rôle de DAX.

Dans Power BI, il faut distinguer trois éléments importants :

| Élément | Rôle principal | Exemple simple |
|---|---|---|
| Power Query | Importer, nettoyer et transformer les données | Supprimer une colonne inutile, corriger un type de données, fusionner des fichiers |
| DAX | Calculer les indicateurs et les mesures | Calculer le chiffre d’affaires, la marge, un pourcentage, un cumul |
| Visuels Power BI | Présenter les résultats | Carte KPI, tableau, graphique en colonnes, segment de filtre |

Une façon simple de retenir est la suivante :

```text
Power Query prépare les données.
DAX calcule les indicateurs.
Power BI affiche les résultats.
```

Prenons un exemple très simple. Vous avez une table de ventes avec des produits, des quantités et des prix unitaires.

| Produit | Quantité | Prix unitaire |
|---|---:|---:|
| PC | 2 | 1000 |
| Souris | 5 | 20 |

L’idée du calcul du chiffre d’affaires est la suivante :

```text
Chiffre d’affaires = Quantité × Prix unitaire
```

Pour la première ligne :

```text
2 × 1000 = 2000
```

Pour la deuxième ligne :

```text
5 × 20 = 100
```

Le chiffre d’affaires total serait donc :

```text
2000 + 100 = 2100
```

Dans Power BI, DAX permet de créer une mesure qui fait ce calcul automatiquement. La mesure peut ensuite être utilisée dans une carte, un tableau ou un graphique.

La force de DAX ne vient pas seulement du calcul. Elle vient surtout du fait que les mesures sont **dynamiques**.

La même mesure peut afficher :

* le chiffre d’affaires total ;
* le chiffre d’affaires d’une région ;
* le chiffre d’affaires d’un produit ;
* le chiffre d’affaires d’un mois ;
* le chiffre d’affaires d’une catégorie ;
* le chiffre d’affaires après sélection d’un filtre.

La formule ne change pas. Ce sont les filtres du rapport qui changent le résultat.

C’est une idée essentielle :

```text
DAX ne calcule pas seulement une valeur fixe.
DAX calcule une valeur selon le contexte du rapport.
```

Dans un tableau de bord, ce comportement est très important. Lorsque vous cliquez sur une région, un produit ou une période, les indicateurs se recalculent automatiquement.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-2"></a>

# 2. Comprendre la notion de table de faits

<details open>
<summary>Comprendre ce qu’est une table de faits avec un exemple de ventes</summary>

Avant de créer des formules DAX, il faut comprendre comment les données sont organisées dans un modèle Power BI.

Une **table de faits** contient les événements mesurables d’une activité. Elle contient généralement des nombres que l’on peut additionner, compter, comparer ou analyser.

Dans une entreprise, une table de faits peut représenter :

* des ventes ;
* des commandes ;
* des paiements ;
* des livraisons ;
* des inscriptions ;
* des clics sur un site web ;
* des consultations ;
* des dépenses ;
* des transactions.

Une table de faits répond souvent à des questions comme :

* combien a-t-on vendu ?
* combien cela a-t-il coûté ?
* quelle quantité a été vendue ?
* quelle marge a été réalisée ?
* à quelle date la vente a-t-elle eu lieu ?
* dans quelle région la vente a-t-elle été faite ?
* quel produit a été vendu ?

Dans ce tutoriel, la table principale s’appelle **Ventes**. Elle représente une table de faits, car elle contient les données mesurables de l’activité commerciale.

Chaque ligne de la table représente une vente.

Exemple :

| Date | Produit | Région | Quantité | PrixUnitaire | CoutUnitaire |
|---|---|---|---:|---:|---:|
| 2025-01-05 | PC | Québec | 2 | 1000 | 700 |

Cette ligne signifie :

```text
Le 5 janvier 2025, 2 PC ont été vendus au Québec.
Chaque PC a été vendu 1000.
Chaque PC a coûté 700.
```

À partir de cette seule ligne, on peut calculer plusieurs indicateurs :

```text
Chiffre d’affaires = 2 × 1000 = 2000
Coût total = 2 × 700 = 1400
Marge = 2000 - 1400 = 600
```

Cette ligne contient donc des informations importantes pour l’analyse.

Dans Power BI, la table de faits est souvent la table centrale du modèle. Les mesures DAX sont généralement créées à partir de cette table, parce qu’elle contient les valeurs à additionner ou à analyser.

À retenir :

```text
Une table de faits contient les événements mesurables.
Elle sert à calculer des indicateurs.
Elle répond souvent à la question : combien ?
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-3"></a>

# 3. Comprendre les tables de dimensions

<details open>
<summary>Comprendre la différence entre table de faits et table de dimensions</summary>

Dans un modèle Power BI professionnel, on ne place pas toujours toutes les informations dans une seule table. On organise souvent les données en plusieurs tables.

On distingue principalement :

| Type de table | Rôle | Question principale |
|---|---|---|
| Table de faits | Contient les valeurs mesurables | Combien ? |
| Table de dimensions | Contient les axes d’analyse | Par quoi analyser ? |

La table de faits contient les valeurs à calculer.

Exemples :

* quantité vendue ;
* prix unitaire ;
* coût unitaire ;
* montant de vente ;
* marge ;
* nombre de transactions.

Les tables de dimensions servent à analyser ces valeurs sous différents angles.

Exemples :

* par produit ;
* par région ;
* par catégorie ;
* par mois ;
* par année ;
* par client ;
* par vendeur ;
* par canal de vente.

Dans notre exemple, nous allons commencer avec une seule table appelée **Ventes**. C’est volontaire. Pour débuter, il est plus simple de travailler avec une seule table.

Cependant, dans un modèle plus avancé, on pourrait séparer les données comme ceci :

| Table | Type | Exemple de contenu |
|---|---|---|
| Ventes | Table de faits | Date, Produit, Quantité, Prix, Coût |
| Produits | Dimension | Produit, Catégorie, Marque |
| Régions | Dimension | Région, Pays, Zone |
| Calendrier | Dimension temporelle | Date, Mois, Trimestre, Année |

La table **Ventes** contient les transactions. Les autres tables permettent d’analyser ces transactions.

Exemple :

```text
La table Ventes dit combien a été vendu.
La table Produits permet d’analyser les ventes par produit ou catégorie.
La table Régions permet d’analyser les ventes par région.
La table Calendrier permet d’analyser les ventes par mois, trimestre ou année.
```

Dans ce tutoriel, la table **Calendrier** sera créée plus loin. Elle est très importante pour les analyses temporelles, comme le chiffre d’affaires par mois, le cumul annuel ou la comparaison avec le mois précédent.

À retenir :

```text
La table de faits contient les valeurs à mesurer.
Les tables de dimensions contiennent les axes d’analyse.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-4"></a>

# 4. Créer les données de départ dans Power BI

<details open>
<summary>Créer manuellement la table Ventes dans Power BI Desktop</summary>

Pour apprendre DAX correctement, il est préférable de commencer avec un petit jeu de données. Cela permet de vérifier les résultats à la main et de comprendre pourquoi une mesure donne un certain résultat.

Dans Power BI Desktop, suivez les étapes suivantes :

1. Ouvrez **Power BI Desktop**.
2. Cliquez sur l’onglet **Accueil**.
3. Cliquez sur **Entrer des données**.
4. Créez une table appelée **Ventes**.
5. Copiez les données suivantes dans la table.
6. Cliquez sur **Charger**.

Données à utiliser :

| Date | Produit | Catégorie | Région | Quantité | PrixUnitaire | CoutUnitaire |
|---|---|---|---|---:|---:|---:|
| 2025-01-05 | PC | Informatique | Québec | 2 | 1000 | 700 |
| 2025-01-10 | Souris | Accessoire | Québec | 10 | 25 | 10 |
| 2025-02-03 | Clavier | Accessoire | Ontario | 5 | 60 | 30 |
| 2025-02-18 | PC | Informatique | Ontario | 1 | 1000 | 700 |
| 2025-03-02 | Écran | Informatique | Québec | 3 | 300 | 180 |
| 2025-03-15 | Souris | Accessoire | Ontario | 8 | 25 | 10 |

Cette table contient six ventes.

Chaque ligne représente une transaction. Par exemple, la première ligne indique que deux PC ont été vendus au Québec le 5 janvier 2025.

Le nom des colonnes est important. Les formules DAX qui seront utilisées plus loin supposent que les colonnes portent exactement les noms suivants :

```text
Date
Produit
Catégorie
Région
Quantité
PrixUnitaire
CoutUnitaire
```

Il faut donc éviter de modifier les noms des colonnes, sinon les formules devront être adaptées.

Après avoir chargé les données, vérifiez que la table **Ventes** apparaît bien dans le panneau des champs de Power BI.

À retenir :

```text
Avant d’écrire des formules DAX, il faut s’assurer que les données sont correctement importées.
Un mauvais nom de colonne ou un mauvais type de données peut provoquer des erreurs.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-5"></a>

# 5. Vérifier les types de données

<details open>
<summary>Vérifier que les colonnes sont reconnues avec le bon type</summary>

Avant d’écrire les formules DAX, il faut vérifier les types de données. Cette étape est essentielle.

Power BI doit comprendre qu’une date est une date, qu’un texte est un texte et qu’un nombre est un nombre. Si Power BI interprète une colonne numérique comme du texte, les calculs peuvent échouer ou donner des résultats incorrects.

Dans Power BI, allez dans la vue **Données** ou dans la vue **Modèle**, puis vérifiez les colonnes de la table **Ventes**.

| Colonne | Type attendu | Pourquoi ce type est important |
|---|---|---|
| Date | Date | Nécessaire pour les analyses temporelles |
| Produit | Texte | Permet de regrouper les ventes par produit |
| Catégorie | Texte | Permet de regrouper les ventes par catégorie |
| Région | Texte | Permet de filtrer ou comparer par région |
| Quantité | Nombre entier | Nécessaire pour les additions et multiplications |
| PrixUnitaire | Nombre entier ou décimal | Nécessaire pour calculer le chiffre d’affaires |
| CoutUnitaire | Nombre entier ou décimal | Nécessaire pour calculer le coût total et la marge |

Exemple de problème fréquent :

```text
Si la colonne Quantité est considérée comme du texte,
Power BI ne peut pas correctement calculer Quantité × PrixUnitaire.
```

Autre exemple :

```text
Si la colonne Date est considérée comme du texte,
les fonctions de temps comme TOTALYTD ou DATEADD risquent de ne pas fonctionner correctement.
```

Il faut donc corriger les types avant de créer les mesures.

À vérifier avant de continuer :

* la colonne `Date` est au format Date ;
* la colonne `Quantité` est au format Nombre entier ;
* les colonnes `PrixUnitaire` et `CoutUnitaire` sont au format Nombre entier ou Nombre décimal ;
* les colonnes `Produit`, `Catégorie` et `Région` sont au format Texte.

À retenir :

```text
Un bon modèle commence par des données correctement typées.
Les formules DAX dépendent fortement de la qualité des données.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-6"></a>

# 6. Colonne calculée ou mesure : différence fondamentale

<details open>
<summary>Comprendre la différence entre une colonne calculée et une mesure</summary>

Dans Power BI, il existe deux façons fréquentes de créer des calculs :

* les **colonnes calculées** ;
* les **mesures**.

Cette différence est fondamentale. Beaucoup d’erreurs en DAX viennent d’une confusion entre les deux.

## 6.1 Colonne calculée

Une colonne calculée ajoute une nouvelle colonne dans une table.

Elle travaille ligne par ligne.

Exemple :

| Quantité | PrixUnitaire | Montant |
|---:|---:|---:|
| 2 | 1000 | 2000 |
| 10 | 25 | 250 |
| 5 | 60 | 300 |

La colonne `Montant` est calculée pour chaque ligne.

Elle ressemble à une formule Excel copiée sur toutes les lignes d’un tableau.

Exemple d’idée :

```text
Pour chaque ligne :
Montant = Quantité × PrixUnitaire
```

Une colonne calculée est utile quand on veut stocker une information ligne par ligne.

## 6.2 Mesure

Une mesure calcule un résultat global, dynamique et dépendant du contexte.

Exemple :

```text
CA total = 4450
```

Ce résultat peut changer automatiquement selon les filtres.

Si vous filtrez la région Québec, la mesure calcule seulement le chiffre d’affaires du Québec.

Si vous filtrez la région Ontario, la même mesure calcule seulement le chiffre d’affaires de l’Ontario.

La formule ne change pas. C’est le contexte du rapport qui change.

## 6.3 Comparaison simple

| Critère | Colonne calculée | Mesure |
|---|---|---|
| Où apparaît le résultat ? | Dans la table | Dans les visuels |
| Niveau de calcul | Ligne par ligne | Selon le contexte |
| Résultat stocké ? | Oui, dans le modèle | Non, calculé dynamiquement |
| Exemple | Montant par ligne | Chiffre d’affaires total |
| Usage fréquent | Catégoriser, préparer une colonne | KPI, total, ratio, graphique |

## 6.4 Quand utiliser quoi ?

| Besoin | À utiliser |
|---|---|
| Ajouter une valeur ligne par ligne dans une table | Colonne calculée |
| Calculer un total | Mesure |
| Calculer une moyenne | Mesure |
| Calculer un ratio | Mesure |
| Créer un KPI | Mesure |
| Créer un tableau de bord dynamique | Mesure |
| Créer une catégorie fixe par ligne | Colonne calculée |

Règle pratique :

```text
Pour les tableaux de bord, les mesures sont généralement préférables.
```

Cela ne veut pas dire que les colonnes calculées sont inutiles. Elles sont utiles dans certains cas. Mais pour les indicateurs dynamiques, les mesures sont plus adaptées.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-7"></a>

# 7. Créer une première colonne calculée

<details open>
<summary>Créer une colonne Montant pour comprendre le calcul ligne par ligne</summary>

Nous allons d’abord créer une colonne calculée simple. Le but est de comprendre le principe du calcul ligne par ligne.

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
prendre la quantité,
la multiplier par le prix unitaire,
puis stocker le résultat dans une nouvelle colonne appelée Montant.
```

Exemples de calculs :

| Ligne | Produit | Quantité | PrixUnitaire | Montant |
|---:|---|---:|---:|---:|
| 1 | PC | 2 | 1000 | 2000 |
| 2 | Souris | 10 | 25 | 250 |
| 3 | Clavier | 5 | 60 | 300 |
| 4 | PC | 1 | 1000 | 1000 |
| 5 | Écran | 3 | 300 | 900 |
| 6 | Souris | 8 | 25 | 200 |

Après la création de cette colonne, la table **Ventes** contient une nouvelle colonne appelée `Montant`.

Cette colonne est utile pour comprendre le calcul ligne par ligne.

Cependant, dans un tableau de bord professionnel, on évite souvent de créer trop de colonnes calculées si une mesure peut faire le même travail. C’est pourquoi nous allons ensuite créer une mesure.

À retenir :

```text
Une colonne calculée ajoute une colonne dans la table.
Elle calcule une valeur pour chaque ligne.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-8"></a>

# 8. Créer une première mesure DAX avec SUM

<details open>
<summary>Créer une mesure CA en additionnant la colonne Montant</summary>

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

Détail du calcul :

| Ligne | Produit | Calcul | Montant |
|---:|---|---|---:|
| 1 | PC | 2 × 1000 | 2000 |
| 2 | Souris | 10 × 25 | 250 |
| 3 | Clavier | 5 × 60 | 300 |
| 4 | PC | 1 × 1000 | 1000 |
| 5 | Écran | 3 × 300 | 900 |
| 6 | Souris | 8 × 25 | 200 |
| Total | | | 4450 |

La fonction `SUM` additionne une colonne numérique.

Elle fonctionne très bien lorsque la colonne à additionner existe déjà.

Dans notre cas, la colonne `Montant` existe parce que nous l’avons créée dans la section précédente.

À retenir :

```text
SUM additionne les valeurs d’une colonne.
```

Exemple :

```text
SUM(Ventes[Montant]) = somme de tous les montants de la colonne Montant
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-9"></a>

# 9. Créer une mesure plus professionnelle avec SUMX

<details open>
<summary>Créer le chiffre d’affaires directement sans colonne Montant</summary>

La mesure précédente fonctionne, mais elle dépend de la colonne calculée `Montant`.

En DAX, il est possible de créer directement une mesure qui calcule ligne par ligne puis additionne les résultats. Pour cela, on utilise `SUMX`.

Créez une nouvelle mesure :

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

La fonction `SUMX` signifie :

```text
Parcourir chaque ligne d’une table,
évaluer une expression pour chaque ligne,
puis additionner les résultats.
```

Dans notre cas, Power BI fait ceci :

| Ligne | Produit | Expression évaluée | Résultat |
|---:|---|---|---:|
| 1 | PC | 2 × 1000 | 2000 |
| 2 | Souris | 10 × 25 | 250 |
| 3 | Clavier | 5 × 60 | 300 |
| 4 | PC | 1 × 1000 | 1000 |
| 5 | Écran | 3 × 300 | 900 |
| 6 | Souris | 8 × 25 | 200 |
| Total | | | 4450 |

La différence entre `SUM` et `SUMX` est importante.

| Formule | Signification |
|---|---|
| `SUM(Ventes[Montant])` | Additionne une colonne déjà existante |
| `SUMX(Ventes, expression)` | Calcule une expression ligne par ligne, puis additionne |

`SUMX` est très utile lorsque la valeur à additionner n’existe pas encore dans une colonne.

Dans un tableau de bord professionnel, on privilégie souvent la mesure avec `SUMX`, car elle évite de créer une colonne supplémentaire si celle-ci n’est pas nécessaire.

À retenir :

```text
SUM additionne une colonne existante.
SUMX calcule d’abord ligne par ligne, puis additionne.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-10"></a>

# 10. Créer les mesures principales du tableau de bord

<details open>
<summary>Créer les indicateurs principaux : CA, coût, marge, taux de marge, ventes et quantité</summary>

Nous allons maintenant créer les principales mesures du tableau de bord.

Ces mesures serviront ensuite dans les cartes KPI, les tableaux et les graphiques.

## 10.1 Chiffre d’affaires

```DAX
CA = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Cette mesure calcule le total des ventes.

Elle multiplie la quantité par le prix unitaire pour chaque ligne, puis additionne les résultats.

Résultat attendu sans filtre :

```text
4450
```

## 10.2 Coût total

```DAX
Coût total = SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[CoutUnitaire]
)
```

Cette mesure calcule le coût total des produits vendus.

Elle multiplie la quantité par le coût unitaire pour chaque ligne, puis additionne les résultats.

Résultat attendu sans filtre :

```text
2870
```

Détail du calcul :

| Produit | Calcul | Coût |
|---|---|---:|
| PC Québec | 2 × 700 | 1400 |
| Souris Québec | 10 × 10 | 100 |
| Clavier Ontario | 5 × 30 | 150 |
| PC Ontario | 1 × 700 | 700 |
| Écran Québec | 3 × 180 | 540 |
| Souris Ontario | 8 × 10 | 80 |
| Total | | 2870 |

## 10.3 Marge

```DAX
Marge = [CA] - [Coût total]
```

Cette mesure calcule la différence entre le chiffre d’affaires et le coût total.

Résultat attendu sans filtre :

```text
1580
```

Explication :

```text
Marge = 4450 - 2870 = 1580
```

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

Explication :

```text
1580 / 4450 = 0,3551
0,3551 = 35,51 %
```

Il est préférable d’utiliser `DIVIDE` au lieu de `/`.

À éviter :

```DAX
Taux de marge = [Marge] / [CA]
```

À privilégier :

```DAX
Taux de marge = DIVIDE([Marge], [CA])
```

`DIVIDE` gère mieux les cas où le dénominateur est égal à zéro.

## 10.5 Nombre de ventes

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

Cette mesure compte le nombre de lignes dans la table `Ventes`.

Résultat attendu sans filtre :

```text
6
```

Chaque ligne représente une vente. Comme la table contient six lignes, le nombre de ventes est donc six.

## 10.6 Quantité vendue

```DAX
Quantité vendue = SUM(Ventes[Quantité])
```

Cette mesure additionne toutes les quantités vendues.

Résultat attendu sans filtre :

```text
29
```

Détail :

```text
2 + 10 + 5 + 1 + 3 + 8 = 29
```

## 10.7 Prix moyen pondéré

Il ne faut pas confondre la moyenne simple des prix unitaires et le prix moyen pondéré.

Moyenne simple :

```DAX
Prix moyen simple = AVERAGE(Ventes[PrixUnitaire])
```

Cette mesure calcule la moyenne des prix unitaires présents dans la table. Cependant, elle ne tient pas compte des quantités vendues.

Pour un tableau de bord de ventes, il est souvent plus pertinent de calculer le prix moyen pondéré :

```DAX
Prix moyen pondéré = DIVIDE(
    [CA],
    [Quantité vendue]
)
```

Cette mesure répond à la question :

```text
En moyenne, combien rapporte une unité vendue ?
```

Résultat attendu sans filtre :

```text
153,45 environ
```

Explication :

```text
4450 / 29 = 153,45
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-11"></a>

# 11. Comprendre le contexte de filtre

<details open>
<summary>Comprendre pourquoi une même mesure DAX peut donner plusieurs résultats</summary>

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

| Contexte appliqué | Résultat de `[CA]` | Explication |
|---|---:|---|
| Aucun filtre | 4450 | Toutes les lignes sont prises en compte |
| Région = Québec | 3150 | Seulement les ventes du Québec |
| Région = Ontario | 1300 | Seulement les ventes de l’Ontario |
| Produit = PC | 3000 | Seulement les ventes du produit PC |
| Catégorie = Accessoire | 750 | Seulement les ventes de la catégorie Accessoire |
| Catégorie = Informatique | 3700 | Seulement les ventes de la catégorie Informatique |

Les filtres peuvent venir de plusieurs endroits :

* un segment de filtre ;
* une sélection dans un graphique ;
* une ligne dans un tableau ;
* un filtre de page ;
* un filtre de rapport ;
* une relation entre tables ;
* une condition dans une formule DAX.

Exemple simple :

```text
Dans une carte, [CA] affiche 4450.
Dans un tableau par région, [CA] affiche une valeur différente pour chaque région.
```

Cela ne signifie pas que la mesure est instable. Cela signifie qu’elle est dynamique.

À retenir :

```text
Une mesure DAX donne un résultat selon les filtres actifs dans le rapport.
```

Phrase essentielle :

```text
DAX calcule toujours dans un contexte.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-12"></a>

# 12. Créer un tableau visuel par région

<details open>
<summary>Créer un tableau qui montre comment les mesures changent par région</summary>

Dans Power BI, créez un visuel de type **Tableau**.

Ajoutez les champs suivants :

* `Région` ;
* `[CA]` ;
* `[Coût total]` ;
* `[Marge]` ;
* `[Taux de marge]`.

Résultat attendu :

| Région | CA | Coût total | Marge | Taux de marge |
|---|---:|---:|---:|---:|
| Québec | 3150 | 2040 | 1110 | 35,24 % |
| Ontario | 1300 | 830 | 470 | 36,15 % |
| Total | 4450 | 2870 | 1580 | 35,51 % |

Ce tableau est important parce qu’il montre le fonctionnement du contexte de filtre.

La mesure `[CA]` est la même partout. Pourtant, elle affiche une valeur différente pour Québec et Ontario.

Pourquoi ?

Parce que chaque ligne du tableau applique un filtre implicite.

Quand Power BI affiche la ligne Québec, il applique automatiquement :

```text
Région = Québec
```

Quand Power BI affiche la ligne Ontario, il applique automatiquement :

```text
Région = Ontario
```

Le tableau devient donc un bon outil pour vérifier que les mesures fonctionnent correctement.

À retenir :

```text
Dans un tableau Power BI, chaque ligne crée souvent son propre contexte de filtre.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-13"></a>

# 13. CALCULATE : modifier le contexte de calcul

<details open>
<summary>Utiliser CALCULATE pour forcer un filtre dans une mesure</summary>

`CALCULATE` est l’une des fonctions les plus importantes de DAX.

Elle permet de calculer une expression dans un contexte de filtre modifié.

Autrement dit, `CALCULATE` permet de dire :

```text
Calcule cette mesure,
mais avec ce filtre précis.
```

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

## 13.2 Calculer le chiffre d’affaires de l’Ontario

```DAX
CA Ontario = CALCULATE(
    [CA],
    Ventes[Région] = "Ontario"
)
```

Traduction :

```text
Calcule le chiffre d’affaires,
mais seulement pour les lignes où la région est Ontario.
```

Résultat attendu :

```text
1300
```

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

## 13.5 Pourquoi CALCULATE est important

Sans `CALCULATE`, une mesure suit simplement les filtres présents dans le rapport.

Avec `CALCULATE`, vous pouvez modifier ou imposer un filtre.

Exemple :

```text
[CA] suit le filtre sélectionné dans le rapport.
[CA Québec] force toujours le calcul sur Québec.
```

À retenir :

```text
CALCULATE sert à recalculer une mesure dans un contexte modifié.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-14"></a>

# 14. Calculer le pourcentage du total

<details open>
<summary>Calculer la part de chaque région dans le chiffre d’affaires total</summary>

Une question fréquente dans un tableau de bord est la suivante :

```text
Quelle est la part de chaque région dans le chiffre d’affaires total ?
```

Pour répondre, il faut comparer deux valeurs :

* le chiffre d’affaires de la région actuelle ;
* le chiffre d’affaires total toutes régions confondues.

## 14.1 Mesure du total toutes régions

Créez la mesure suivante :

```DAX
CA total toutes régions = CALCULATE(
    [CA],
    REMOVEFILTERS(Ventes[Région])
)
```

Cette mesure calcule le chiffre d’affaires en ignorant le filtre sur la région.

Explication :

```text
Même si le tableau affiche Québec ou Ontario,
REMOVEFILTERS(Ventes[Région]) enlève le filtre sur la région.
La mesure retourne donc le total général.
```

## 14.2 Mesure du pourcentage du total

Créez ensuite :

```DAX
% du total région = DIVIDE(
    [CA],
    [CA total toutes régions]
)
```

Cette mesure divise le chiffre d’affaires de la région courante par le chiffre d’affaires total.

Dans un tableau par région, vous devez obtenir :

| Région | CA | CA total toutes régions | % du total région |
|---|---:|---:|---:|
| Québec | 3150 | 4450 | 70,79 % |
| Ontario | 1300 | 4450 | 29,21 % |
| Total | 4450 | 4450 | 100 % |

Explication :

```text
Pour Québec : 3150 / 4450 = 70,79 %
Pour Ontario : 1300 / 4450 = 29,21 %
```

Cette mesure est utile pour comprendre la contribution de chaque région au total.

À retenir :

```text
REMOVEFILTERS permet d’ignorer un filtre précis.
DIVIDE permet de calculer un ratio de façon plus sûre.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-15"></a>

# 15. IF : créer une mesure conditionnelle

<details open>
<summary>Créer une mesure qui affiche un texte selon le niveau de chiffre d’affaires</summary>

La fonction `IF` permet de créer une condition.

Elle fonctionne selon le principe suivant :

```text
Si une condition est vraie,
alors retourner une valeur.
Sinon,
retourner une autre valeur.
```

Créez la mesure suivante :

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

| Contexte | CA | Performance |
|---|---:|---|
| Total | 4450 | Bonne performance |
| Québec | 3150 | Bonne performance |
| Ontario | 1300 | Performance faible |

Cette mesure peut être utilisée dans un tableau pour donner une interprétation rapide du résultat.

Attention : le seuil de 3000 est un choix arbitraire dans ce tutoriel. Dans un vrai projet, le seuil doit être défini selon le contexte métier.

À retenir :

```text
IF permet de retourner un résultat selon une condition.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-16"></a>

# 16. SWITCH : gérer plusieurs niveaux de performance

<details open>
<summary>Utiliser SWITCH pour remplacer plusieurs conditions IF</summary>

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

Cette mesure teste plusieurs conditions dans l’ordre.

Traduction :

```text
Si CA >= 4000 : Excellent
Sinon si CA >= 2000 : Bon
Sinon si CA >= 1000 : Moyen
Sinon : Faible
```

Exemple de résultat :

| Contexte | CA | Niveau performance |
|---|---:|---|
| Total | 4450 | Excellent |
| Québec | 3150 | Bon |
| Ontario | 1300 | Moyen |

Pourquoi utiliser `SWITCH(TRUE())` ?

Parce que cette forme permet d’écrire plusieurs conditions logiques de manière lisible.

Sans `SWITCH`, il faudrait écrire plusieurs `IF` imbriqués, ce qui devient rapidement difficile à lire.

À retenir :

```text
SWITCH est pratique lorsque plusieurs niveaux ou catégories doivent être évalués.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-17"></a>

# 17. COUNTROWS : compter les lignes

<details open>
<summary>Utiliser COUNTROWS pour compter le nombre de ventes</summary>

La fonction `COUNTROWS` compte le nombre de lignes d’une table.

Créez la mesure suivante :

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

Cette mesure compte les lignes de la table `Ventes`.

Comme chaque ligne représente une vente, cette mesure permet de compter le nombre de ventes.

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

Pourquoi le résultat change-t-il ?

Parce que `COUNTROWS` respecte le contexte de filtre.

Si le rapport filtre uniquement les ventes du Québec, `COUNTROWS(Ventes)` compte uniquement les lignes du Québec.

À retenir :

```text
COUNTROWS compte les lignes visibles dans le contexte actuel.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-18"></a>

# 18. DISTINCTCOUNT : compter les valeurs différentes

<details open>
<summary>Utiliser DISTINCTCOUNT pour compter les produits différents</summary>

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

Cette mesure est différente d’un simple comptage de lignes.

Exemple :

```text
La table contient 6 lignes de vente.
Mais elle contient seulement 4 produits différents.
```

`DISTINCTCOUNT` est utile pour répondre à des questions comme :

* combien de produits différents ont été vendus ?
* combien de clients différents ont acheté ?
* combien de régions différentes sont présentes ?
* combien de catégories différentes existent ?

À retenir :

```text
DISTINCTCOUNT compte les valeurs uniques dans une colonne.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-19"></a>

# 19. Créer une table calendrier

<details open>
<summary>Créer une table Calendrier pour les analyses temporelles</summary>

Pour travailler correctement avec les dates, il est recommandé de créer une table calendrier.

Une table calendrier est une table qui contient une ligne pour chaque date d’une période.

Elle permet d’analyser les données par :

* jour ;
* mois ;
* trimestre ;
* année ;
* année-mois ;
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

Dans notre jeu de données :

```text
Première date : 2025-01-05
Dernière date : 2025-03-15
```

La table Calendrier contiendra donc toutes les dates entre ces deux dates.

Pourquoi ne pas utiliser directement la colonne `Ventes[Date]` ?

Parce que la table `Ventes` contient seulement les dates où il y a eu une vente. Une vraie table calendrier contient toutes les dates, même les jours sans vente. Cela rend les analyses temporelles plus fiables.

À retenir :

```text
Une table calendrier est une dimension temporelle.
Elle est recommandée pour les analyses par date dans Power BI.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-20"></a>

# 20. Ajouter des colonnes à la table calendrier

<details open>
<summary>Ajouter Année, Mois, Numéro du mois et Année-Mois</summary>

Après avoir créé la table **Calendrier**, il faut l’enrichir avec des colonnes utiles pour l’analyse.

Ces colonnes permettent d’afficher les données par année, mois ou période.

## 20.1 Année

Créez une nouvelle colonne dans la table **Calendrier** :

```DAX
Année = YEAR(Calendrier[Date])
```

Cette colonne extrait l’année à partir de la date.

Exemple :

```text
2025-01-05 → 2025
```

## 20.2 Mois

Créez ensuite :

```DAX
Mois = FORMAT(Calendrier[Date], "MMMM")
```

Cette colonne extrait le nom du mois.

Exemple :

```text
2025-01-05 → janvier
2025-02-03 → février
2025-03-15 → mars
```

## 20.3 Numéro du mois

Créez ensuite :

```DAX
Numéro mois = MONTH(Calendrier[Date])
```

Cette colonne extrait le numéro du mois.

Exemple :

```text
Janvier → 1
Février → 2
Mars → 3
```

Cette colonne est importante pour trier correctement les mois. Sans numéro de mois, Power BI peut trier les mois par ordre alphabétique au lieu de l’ordre chronologique.

## 20.4 Année-Mois

Créez enfin :

```DAX
Année-Mois = FORMAT(Calendrier[Date], "YYYY-MM")
```

Cette colonne est utile pour afficher les données mensuelles dans un graphique.

Exemple :

```text
2025-01
2025-02
2025-03
```

À retenir :

```text
La table Calendrier doit contenir des colonnes utiles pour analyser les données dans le temps.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-21"></a>

# 21. Relier la table calendrier à la table Ventes

<details open>
<summary>Créer la relation entre Calendrier[Date] et Ventes[Date]</summary>

Après avoir créé la table calendrier, il faut créer une relation entre la table **Calendrier** et la table **Ventes**.

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
* chaque vente possède une date ;
* la table Calendrier filtre la table Ventes.

Exemple :

```text
La date 2025-01-05 existe une seule fois dans Calendrier.
Elle peut correspondre à une ou plusieurs ventes dans Ventes.
```

La table Calendrier devient donc une dimension temporelle.

Cette relation est essentielle pour que les filtres de date fonctionnent correctement.

Par exemple, si vous utilisez le mois de février dans un graphique, Power BI doit être capable de filtrer les ventes qui appartiennent au mois de février.

À retenir :

```text
La table Calendrier doit être reliée à la table Ventes par la colonne Date.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-22"></a>

# 22. Marquer la table calendrier comme table de dates

<details open>
<summary>Indiquer à Power BI que Calendrier est la table officielle de dates</summary>

Dans Power BI, il est recommandé de marquer la table calendrier comme table de dates.

Cette étape aide Power BI à comprendre que la table **Calendrier** doit être utilisée pour les analyses temporelles.

Étapes :

1. Sélectionnez la table **Calendrier**.
2. Cliquez sur **Outils de table**.
3. Cliquez sur **Marquer comme table de dates**.
4. Choisissez la colonne `Date`.
5. Validez.

Pourquoi cette étape est-elle importante ?

Parce que certaines fonctions temporelles de DAX fonctionnent mieux lorsque Power BI connaît explicitement la table de dates.

Exemples de fonctions temporelles :

* `TOTALYTD` ;
* `DATEADD` ;
* `SAMEPERIODLASTYEAR` ;
* `DATESYTD` ;
* `PREVIOUSMONTH`.

À retenir :

```text
Marquer la table Calendrier comme table de dates améliore la fiabilité des analyses temporelles.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-23"></a>

# 23. Calculer le chiffre d’affaires cumulé

<details open>
<summary>Créer une mesure de chiffre d’affaires cumulé depuis le début de l’année</summary>

Le chiffre d’affaires cumulé permet de suivre l’évolution du CA depuis le début de l’année.

Cette mesure est utile dans les graphiques d’évolution, car elle montre la progression du chiffre d’affaires au fil du temps.

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

Exemple d’interprétation :

```text
En janvier, le cumul contient les ventes de janvier.
En février, le cumul contient janvier + février.
En mars, le cumul contient janvier + février + mars.
```

Cette mesure doit être utilisée avec une table Calendrier correctement reliée à la table Ventes.

À retenir :

```text
TOTALYTD calcule un cumul annuel jusqu’à la date courante du contexte.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-24"></a>

# 24. Comparer avec le mois précédent

<details open>
<summary>Créer des mesures pour comparer le CA avec le mois précédent</summary>

Dans un tableau de bord, il est fréquent de comparer une période avec la période précédente.

La question métier est simple :

```text
Est-ce que les ventes ont augmenté ou diminué par rapport au mois précédent ?
```

Pour répondre à cette question, il faut créer trois mesures :

* le chiffre d’affaires du mois précédent ;
* la variation en valeur ;
* la variation en pourcentage.

## 24.1 Chiffre d’affaires du mois précédent

Créez la mesure suivante :

```DAX
CA mois précédent = CALCULATE(
    [CA],
    DATEADD(Calendrier[Date], -1, MONTH)
)
```

Cette mesure récupère le chiffre d’affaires du mois précédent.

## 24.2 Variation en valeur

Créez ensuite :

```DAX
Variation CA = [CA] - [CA mois précédent]
```

Cette mesure calcule la différence entre le CA actuel et le CA du mois précédent.

Exemple :

```text
Si CA actuel = 1300
et CA mois précédent = 2250
alors Variation CA = 1300 - 2250 = -950
```

## 24.3 Variation en pourcentage

Créez enfin :

```DAX
Variation CA % = DIVIDE(
    [Variation CA],
    [CA mois précédent]
)
```

Cette mesure calcule la variation relative.

Exemple :

```text
Variation CA % = -950 / 2250 = -42,22 %
```

À retenir :

```text
DATEADD permet de décaler une période dans le temps.
CALCULATE applique ce décalage à une mesure.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-25"></a>

# 25. Créer les visuels du tableau de bord

<details open>
<summary>Construire les cartes KPI, tableaux, graphiques et segments</summary>

Une fois les mesures créées, vous pouvez construire un tableau de bord simple.

Le tableau de bord doit permettre de visualiser rapidement les principaux résultats.

## 25.1 Cartes KPI

Créez trois cartes :

| Carte | Champ à utiliser | Rôle |
|---|---|---|
| Carte 1 | `[CA]` | Afficher le chiffre d’affaires total |
| Carte 2 | `[Marge]` | Afficher la marge totale |
| Carte 3 | `[Taux de marge]` | Afficher la rentabilité globale |

Résultat attendu sans filtre :

| KPI | Résultat attendu |
|---|---:|
| CA | 4450 |
| Marge | 1580 |
| Taux de marge | 35,51 % |

## 25.2 Tableau par région

Créez un tableau avec :

* `Région` ;
* `[CA]` ;
* `[Coût total]` ;
* `[Marge]` ;
* `[% du total région]`.

Résultat attendu :

| Région | CA | Coût total | Marge | % du total région |
|---|---:|---:|---:|---:|
| Québec | 3150 | 2040 | 1110 | 70,79 % |
| Ontario | 1300 | 830 | 470 | 29,21 % |
| Total | 4450 | 2870 | 1580 | 100 % |

## 25.3 Graphique en colonnes par produit

Créez un graphique en colonnes avec :

| Zone du visuel | Champ |
|---|---|
| Axe | `Produit` |
| Valeurs | `[CA]` |

Résultat attendu par produit :

| Produit | CA |
|---|---:|
| PC | 3000 |
| Écran | 900 |
| Souris | 450 |
| Clavier | 300 |

## 25.4 Graphique par catégorie

Créez un graphique avec :

| Zone du visuel | Champ |
|---|---|
| Axe ou légende | `Catégorie` |
| Valeurs | `[CA]` |

Résultat attendu :

| Catégorie | CA |
|---|---:|
| Informatique | 3700 |
| Accessoire | 750 |

## 25.5 Segments de filtre

Ajoutez deux segments :

| Segment | Champ | Utilité |
|---|---|---|
| Segment 1 | `Région` | Filtrer le rapport par région |
| Segment 2 | `Produit` | Filtrer le rapport par produit |

Exemple :

```text
Si vous cliquez sur Québec,
les cartes, tableaux et graphiques affichent uniquement les données du Québec.
```

À retenir :

```text
Les visuels permettent de rendre les mesures lisibles et interactives.
Les segments permettent de modifier le contexte de filtre.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-26"></a>

# 26. Formater les mesures

<details open>
<summary>Appliquer les bons formats aux montants, pourcentages et volumes</summary>

Le formatage est important pour rendre le tableau de bord lisible et professionnel.

Une mesure peut être correcte mathématiquement, mais difficile à lire si elle est mal formatée.

Exemple :

```text
0,3551
```

Cette valeur est correcte, mais elle est moins lisible qu’un pourcentage affiché comme ceci :

```text
35,51 %
```

Sélectionnez chaque mesure et appliquez le bon format.

| Mesure | Format recommandé | Pourquoi |
|---|---|---|
| `[CA]` | Monétaire | Il s’agit d’un montant de ventes |
| `[Coût total]` | Monétaire | Il s’agit d’un coût |
| `[Marge]` | Monétaire | Il s’agit d’un montant de profit brut |
| `[Taux de marge]` | Pourcentage | Il s’agit d’un ratio |
| `[% du total région]` | Pourcentage | Il s’agit d’une part du total |
| `[Quantité vendue]` | Nombre entier | Il s’agit d’un volume |
| `[Nombre de ventes]` | Nombre entier | Il s’agit d’un nombre de lignes |
| `[Prix moyen pondéré]` | Monétaire ou nombre décimal | Il s’agit d’un prix moyen |
| `[Variation CA %]` | Pourcentage | Il s’agit d’une variation relative |

Un bon formatage permet de distinguer rapidement :

* les montants ;
* les pourcentages ;
* les quantités ;
* les ratios ;
* les variations.

À retenir :

```text
Le formatage ne change pas le calcul.
Il change la manière dont le résultat est affiché.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-27"></a>

# 27. Tableau complet des mesures à créer

<details open>
<summary>Regrouper toutes les mesures DAX du tutoriel</summary>

Voici la liste complète des mesures importantes du tutoriel.

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

## Nombre de ventes

```DAX
Nombre de ventes = COUNTROWS(Ventes)
```

## Quantité vendue

```DAX
Quantité vendue = SUM(Ventes[Quantité])
```

## Prix moyen pondéré

```DAX
Prix moyen pondéré = DIVIDE(
    [CA],
    [Quantité vendue]
)
```

## Nombre de produits

```DAX
Nombre de produits = DISTINCTCOUNT(Ventes[Produit])
```

## Chiffre d’affaires par région

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

## Chiffre d’affaires par catégorie

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

## Total toutes régions

```DAX
CA total toutes régions = CALCULATE(
    [CA],
    REMOVEFILTERS(Ventes[Région])
)
```

## Pourcentage du total

```DAX
% du total région = DIVIDE(
    [CA],
    [CA total toutes régions]
)
```

## Performance simple

```DAX
Performance = IF(
    [CA] >= 3000,
    "Bonne performance",
    "Performance faible"
)
```

## Niveau de performance

```DAX
Niveau performance = SWITCH(
    TRUE(),
    [CA] >= 4000, "Excellent",
    [CA] >= 2000, "Bon",
    [CA] >= 1000, "Moyen",
    "Faible"
)
```

## Chiffre d’affaires cumulé

```DAX
CA cumulé année = TOTALYTD(
    [CA],
    Calendrier[Date]
)
```

## Chiffre d’affaires du mois précédent

```DAX
CA mois précédent = CALCULATE(
    [CA],
    DATEADD(Calendrier[Date], -1, MONTH)
)
```

## Variation du chiffre d’affaires

```DAX
Variation CA = [CA] - [CA mois précédent]
```

## Variation du chiffre d’affaires en pourcentage

```DAX
Variation CA % = DIVIDE(
    [Variation CA],
    [CA mois précédent]
)
```

À retenir :

```text
Ces mesures forment la base d’un tableau de bord de ventes simple et dynamique.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-28"></a>

# 28. Résultats attendus pour vérifier le travail

<details open>
<summary>Comparer les résultats obtenus avec les résultats attendus</summary>

Utilisez ce tableau pour vérifier vos mesures.

| Indicateur | Résultat attendu |
|---|---:|
| CA | 4450 |
| Coût total | 2870 |
| Marge | 1580 |
| Taux de marge | 35,51 % |
| Nombre de ventes | 6 |
| Quantité vendue | 29 |
| Prix moyen pondéré | 153,45 |
| Nombre de produits | 4 |
| CA Québec | 3150 |
| CA Ontario | 1300 |
| CA Informatique | 3700 |
| CA Accessoire | 750 |
| % Québec | 70,79 % |
| % Ontario | 29,21 % |

Si vos résultats sont différents, vérifiez les points suivants :

* les données ont-elles été copiées correctement ?
* les colonnes numériques sont-elles bien au format nombre ?
* la colonne `Date` est-elle bien au format Date ?
* les noms des colonnes sont-ils identiques aux formules ?
* les accents dans les noms de mesures sont-ils respectés ?
* les mesures ont-elles été créées dans la bonne table ?
* le visuel contient-il un filtre actif ?
* un segment est-il sélectionné dans la page ?
* la relation entre `Calendrier[Date]` et `Ventes[Date]` est-elle correcte ?

Cette étape de vérification est importante. Elle permet de confirmer que les mesures sont correctes avant de construire un rapport plus complet.

À retenir :

```text
Un bon tableau de bord doit être validé avec des résultats attendus.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-29"></a>

# 29. Erreurs fréquentes à éviter

<details open>
<summary>Identifier les erreurs classiques au début de l’apprentissage de DAX</summary>

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

## 29.2 Ne pas comprendre le contexte de filtre

Une mesure peut changer selon :

* le filtre de page ;
* le segment sélectionné ;
* la région dans un tableau ;
* le produit dans un graphique ;
* la relation entre deux tables.

Ce n’est pas une anomalie. C’est le comportement normal de DAX.

## 29.3 Oublier la table calendrier

Pour les analyses par date, il est recommandé de créer une vraie table calendrier.

Sans table calendrier, les comparaisons temporelles peuvent être limitées ou incorrectes.

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

## 29.6 Mal nommer les colonnes ou les mesures

Si une colonne s’appelle `PrixUnitaire`, la formule doit utiliser exactement ce nom.

Exemple correct :

```DAX
Ventes[PrixUnitaire]
```

Exemple qui peut provoquer une erreur :

```DAX
Ventes[Prix Unitaire]
```

## 29.7 Confondre table et colonne

En DAX, une colonne est toujours appelée avec le nom de la table.

Exemple :

```DAX
Ventes[Quantité]
```

Cela signifie :

```text
La colonne Quantité qui se trouve dans la table Ventes.
```

À retenir :

```text
La plupart des erreurs DAX viennent d’un mauvais contexte, d’un mauvais type de données ou d’un mauvais nom de colonne.
```

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-30"></a>

# 30. Mini-projet final

<details open>
<summary>Créer un mini tableau de bord Power BI de ventes</summary>

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

## 30.1 Données à utiliser

Utilisez la table **Ventes** fournie au début du tutoriel.

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

## 30.3 Visuels obligatoires

Le rapport doit contenir :

| Visuel | Champs à utiliser |
|---|---|
| Carte 1 | `[CA]` |
| Carte 2 | `[Marge]` |
| Carte 3 | `[Taux de marge]` |
| Tableau | `Région`, `[CA]`, `[Marge]`, `[% du total région]` |
| Graphique en colonnes | `Produit` + `[CA]` |
| Graphique par catégorie | `Catégorie` + `[CA]` |
| Segment | `Région` |
| Segment | `Produit` |

## 30.4 Validation attendue

Le tableau de bord doit afficher les résultats suivants sans filtre :

| KPI | Résultat attendu |
|---|---:|
| CA | 4450 |
| Coût total | 2870 |
| Marge | 1580 |
| Taux de marge | 35,51 % |
| Nombre de ventes | 6 |
| Quantité vendue | 29 |
| Nombre de produits | 4 |

Si ces valeurs ne sont pas obtenues, il faut corriger les données, les types de colonnes ou les formules DAX.

## 30.5 Ce que le mini-projet doit démontrer

Le mini-projet doit montrer que vous êtes capable de :

* importer ou créer une table de données ;
* vérifier les types de colonnes ;
* identifier une table de faits ;
* créer des mesures DAX ;
* créer une table calendrier ;
* relier deux tables ;
* construire des visuels ;
* utiliser des segments de filtre ;
* vérifier les résultats obtenus ;
* expliquer brièvement les indicateurs créés.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-31"></a>

# 31. Travail à réaliser

<details open>
<summary>Consignes du travail à remettre</summary>

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

## Livrable attendu

Le rapport Power BI doit contenir :

* une page de tableau de bord claire ;
* les mesures DAX obligatoires ;
* les visuels demandés ;
* les segments de filtre ;
* une mise en forme lisible ;
* des résultats cohérents avec les valeurs attendues.

## Vérification avant la remise

Avant de remettre le travail, vérifiez que :

* le fichier Power BI s’ouvre correctement ;
* les visuels s’affichent correctement ;
* les cartes KPI donnent les bons résultats ;
* les segments filtrent bien les visuels ;
* les mesures DAX ne contiennent pas d’erreurs ;
* la table Calendrier est reliée à la table Ventes ;
* les formats monétaires et pourcentages sont appliqués.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

<a id="section-32"></a>

# 32. Résumé final à retenir

<details open>
<summary>Revoir les idées essentielles du tutoriel</summary>

Voici les idées essentielles du tutoriel.

## Power Query, DAX et Power BI

```text
Power Query prépare les données.
DAX calcule les indicateurs.
Power BI affiche les résultats.
```

## Table de faits et table de dimensions

```text
Une table de faits contient les valeurs mesurables.
Une table de dimensions contient les axes d’analyse.
```

## Colonne calculée et mesure

```text
Une colonne calculée travaille ligne par ligne.
Une mesure calcule un résultat dynamique selon le contexte.
```

## Fonctions DAX importantes

```text
SUM additionne une colonne.
SUMX calcule ligne par ligne puis additionne.
CALCULATE modifie le contexte de calcul.
DIVIDE effectue une division plus sûre.
COUNTROWS compte les lignes.
DISTINCTCOUNT compte les valeurs différentes.
REMOVEFILTERS enlève un filtre précis.
```

## Phrase la plus importante

```text
DAX ne calcule jamais dans le vide.
DAX calcule toujours dans un contexte.
```

Lorsque cette idée est comprise, les mesures Power BI deviennent beaucoup plus faciles à interpréter.

Un tableau de bord Power BI n’est pas seulement une collection de graphiques. C’est un outil d’analyse qui repose sur :

* des données propres ;
* un modèle cohérent ;
* des mesures DAX bien écrites ;
* des filtres maîtrisés ;
* des résultats vérifiés.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>

---

# Fin du tutoriel

<details open>
<summary>Dernière vérification</summary>

Avant de considérer le tutoriel terminé, assurez-vous que vous savez expliquer :

* ce que fait DAX ;
* ce qu’est une mesure ;
* ce qu’est une colonne calculée ;
* ce qu’est une table de faits ;
* ce qu’est une table de dimensions ;
* pourquoi le contexte de filtre change les résultats ;
* pourquoi `SUMX` est utile ;
* pourquoi `DIVIDE` est préférable pour les ratios ;
* pourquoi une table calendrier est importante ;
* comment vérifier les résultats d’un tableau de bord.

Si vous pouvez expliquer ces points avec vos propres mots, vous avez compris les bases nécessaires pour continuer avec des modèles Power BI plus avancés.

</details>

<p align="right"><a href="#top">Retour en haut</a></p>
