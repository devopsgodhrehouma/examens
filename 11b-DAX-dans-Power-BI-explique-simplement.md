<a id="top"></a>

# Cours — Comprendre DAX dans Power BI simplement

## Table des matières

| #  | Section                                                      |
| -- | ------------------------------------------------------------ |
| 1  | [Power BI sans DAX : ce qu’on peut faire](#section-1)        |
| 2  | [Le vrai problème : afficher n’est pas analyser](#section-2) |
| 3  | [DAX, c’est quoi exactement ?](#section-3)                   |
| 4  | [Pourquoi DAX est important dans Power BI](#section-4)       |
| 5  | [Sans DAX, quelles sont les limites ?](#section-5)           |
| 6  | [Mesure, colonne calculée, table calculée](#section-6)       |
| 7  | [La notion la plus importante : le contexte](#section-7)     |
| 8  | [Les fonctions DAX essentielles](#section-8)                 |
| 9  | [Exemple complet avec ventes](#section-9)                    |
| 10 | [Résumé final à retenir](#section-10)                        |

---

<a id="section-1"></a>

## 1. Power BI sans DAX : ce qu’on peut faire

Avant de parler de DAX, il faut comprendre une chose importante :

**Power BI peut fonctionner sans que tu écrives du DAX.**

Tu peux déjà faire beaucoup de choses :

* importer un fichier Excel ou CSV ;
* connecter une base de données ;
* nettoyer les données avec Power Query ;
* créer des graphiques ;
* ajouter des filtres ;
* faire des tableaux ;
* afficher des sommes simples ;
* afficher des moyennes simples ;
* créer des segments par date, produit, région, client.

Par exemple, si tu as une colonne `Montant`, Power BI peut automatiquement afficher :

```text
Somme de Montant
```

Donc au début, un utilisateur peut croire :

> Je n’ai pas besoin de DAX. Power BI fait déjà les calculs.

Et c’est vrai pour les choses simples.

Mais dès que tu veux faire des calculs professionnels, personnalisés et intelligents, DAX devient nécessaire.

---

<a id="section-2"></a>

## 2. Le vrai problème : afficher n’est pas analyser

Power BI peut afficher des données.

Mais dans une entreprise, on ne veut pas seulement afficher les données.

On veut répondre à des questions comme :

* Est-ce que les ventes augmentent ?
* Quelle est la marge réelle ?
* Quel produit est le plus rentable ?
* Quel client rapporte le plus ?
* Quel pourcentage représente chaque catégorie ?
* Quelle est la croissance par rapport au mois précédent ?
* Est-ce que l’objectif est atteint ?
* Quelle est la différence entre le budget prévu et le résultat réel ?

Ces questions ne sont pas seulement de l’affichage.

Ce sont des **calculs d’analyse**.

Et c’est là que DAX intervient.

---

<a id="section-3"></a>

## 3. DAX, c’est quoi exactement ?

**DAX** veut dire :

```text
Data Analysis Expressions
```

En français :

```text
Expressions d’analyse de données
```

DAX est le langage de calcul utilisé dans Power BI.

Il sert à créer :

* des mesures ;
* des colonnes calculées ;
* des tables calculées ;
* des indicateurs de performance ;
* des pourcentages ;
* des comparaisons ;
* des calculs dynamiques selon les filtres.

### Vulgarisation simple

Power BI, c’est comme un tableau de bord de voiture.

| Élément           | Rôle                             |
| ----------------- | -------------------------------- |
| Données           | Le carburant                     |
| Power Query       | Le garage qui nettoie et prépare |
| Modèle de données | Le moteur bien assemblé          |
| DAX               | Le cerveau qui calcule           |
| Visualisations    | Le tableau de bord visible       |

Sans DAX, tu vois des chiffres.

Avec DAX, tu comprends ce que ces chiffres veulent dire.

---

<a id="section-4"></a>

## 4. Pourquoi DAX est important dans Power BI

DAX est important parce qu’il permet de créer des **indicateurs métier**.

Un indicateur métier, ce n’est pas juste une colonne dans un fichier.

C’est une information calculée qui aide à prendre une décision.

### Exemple simple

Tu as une table de ventes :

| Produit | Quantité | Prix unitaire |
| ------- | -------: | ------------: |
| Souris  |        3 |            20 |
| Clavier |        2 |            50 |
| Écran   |        1 |           200 |

Power BI voit les colonnes :

* Produit ;
* Quantité ;
* Prix unitaire.

Mais il ne sait pas automatiquement ce que tu veux appeler le **chiffre d’affaires**.

Tu dois lui dire :

```DAX
ChiffreAffaires = SUMX(Ventes, Ventes[Quantité] * Ventes[Prix unitaire])
```

Cette formule veut dire :

> Pour chaque ligne de la table Ventes, multiplie la quantité par le prix unitaire, puis additionne le tout.

Donc DAX permet de transformer des données brutes en indicateurs utiles.

---

<a id="section-5"></a>

## 5. Sans DAX, quelles sont les limites ?

Sans DAX, tu peux faire des rapports simples.

Mais tu es limité dès que tu veux faire des analyses sérieuses.

### 5.1 Tu peux afficher les ventes, mais pas toujours calculer la marge

Imaginons une table :

| Produit | Chiffre d’affaires | Coût |
| ------- | -----------------: | ---: |
| Souris  |                 60 |   30 |
| Clavier |                100 |   70 |

Tu veux calculer la marge :

```text
Marge = Chiffre d’affaires - Coût
```

En DAX :

```DAX
Marge = [ChiffreAffaires] - [CoûtTotal]
```

Sans DAX, tu peux afficher les ventes et les coûts.

Mais tu ne peux pas facilement créer un indicateur dynamique de marge.

---

### 5.2 Tu peux afficher des montants, mais pas des pourcentages intelligents

Exemple :

| Catégorie    | Ventes |
| ------------ | -----: |
| Informatique | 10 000 |
| Mobilier     |  5 000 |
| Accessoires  |  5 000 |

Tu veux savoir :

> Quelle part représente chaque catégorie dans le total ?

Résultat attendu :

| Catégorie    | Ventes | Pourcentage du total |
| ------------ | -----: | -------------------: |
| Informatique | 10 000 |                 50 % |
| Mobilier     |  5 000 |                 25 % |
| Accessoires  |  5 000 |                 25 % |

Avec DAX :

```DAX
PourcentageTotal =
DIVIDE(
    [TotalVentes],
    CALCULATE([TotalVentes], ALL(Produits[Catégorie]))
)
```

Sans DAX, ce genre de calcul devient vite difficile, surtout si les filtres changent.

---

### 5.3 Tu peux afficher une année, mais pas facilement comparer avec l’année précédente

Un vrai rapport professionnel demande souvent :

* ventes de cette année ;
* ventes de l’année précédente ;
* différence ;
* taux de croissance.

Exemple :

```DAX
VentesAnneePrecedente =
CALCULATE(
    [TotalVentes],
    SAMEPERIODLASTYEAR(Date[Date])
)
```

Puis :

```DAX
Croissance =
DIVIDE(
    [TotalVentes] - [VentesAnneePrecedente],
    [VentesAnneePrecedente]
)
```

Sans DAX, les comparaisons temporelles avancées sont très limitées.

---

### 5.4 Tu peux faire un graphique, mais pas créer des KPI professionnels

Un KPI, c’est un indicateur important pour l’entreprise.

Exemples :

* taux de conversion ;
* taux de marge ;
* panier moyen ;
* revenu moyen par client ;
* objectif atteint ou non ;
* taux de croissance ;
* classement des meilleurs produits ;
* nombre de clients actifs ;
* ventes cumulées ;
* écart budget/réel.

Ces indicateurs nécessitent souvent DAX.

---

<a id="section-6"></a>

## 6. Mesure, colonne calculée, table calculée

Dans Power BI, DAX peut être utilisé principalement à trois endroits.

---

## 6.1 La mesure

Une **mesure** est un calcul dynamique.

Elle change selon les filtres du rapport.

Exemple :

```DAX
TotalVentes = SUM(Ventes[Montant])
```

Si tu filtres sur l’année 2025, la mesure donne les ventes de 2025.

Si tu filtres sur Montréal, elle donne les ventes de Montréal.

Si tu filtres sur un produit, elle donne les ventes de ce produit.

### Vulgarisation

Une mesure, c’est comme une calculatrice intelligente.

Elle ne donne pas toujours le même résultat.

Elle regarde d’abord le contexte du rapport, puis elle calcule.

---

## 6.2 La colonne calculée

Une **colonne calculée** ajoute une nouvelle colonne dans la table.

Exemple :

```DAX
MontantLigne = Ventes[Quantité] * Ventes[PrixUnitaire]
```

Résultat :

| Produit | Quantité | PrixUnitaire | MontantLigne |
| ------- | -------: | -----------: | -----------: |
| Souris  |        3 |           20 |           60 |
| Clavier |        2 |           50 |          100 |

La colonne calculée est calculée ligne par ligne.

### Vulgarisation

Une colonne calculée, c’est comme ajouter une nouvelle colonne dans Excel.

Chaque ligne reçoit une valeur.

---

## 6.3 La table calculée

Une **table calculée** permet de créer une nouvelle table avec DAX.

Exemple :

```DAX
ProduitsRentables =
FILTER(
    Produits,
    Produits[Marge] > 0
)
```

Les tables calculées sont moins utilisées au début.

Pour les débutants, il faut surtout comprendre :

* les mesures ;
* les colonnes calculées.

---

## 6.4 Différence simple

| Élément          | Sert à quoi ?                      | Exemple                   |
| ---------------- | ---------------------------------- | ------------------------- |
| Mesure           | Calcul dynamique selon les filtres | Total des ventes          |
| Colonne calculée | Calcul ligne par ligne             | Quantité × Prix           |
| Table calculée   | Créer une nouvelle table           | Liste filtrée de produits |

### Règle simple

Pour un débutant :

> Si le résultat doit changer selon les filtres du rapport, utilise une mesure.

> Si tu veux ajouter une valeur fixe à chaque ligne, utilise une colonne calculée.

---

<a id="section-7"></a>

## 7. La notion la plus importante : le contexte

Le plus important en DAX, ce n’est pas seulement les fonctions.

Le plus important, c’est le **contexte**.

DAX calcule toujours dans un contexte.

### Exemple

Tu crées cette mesure :

```DAX
TotalVentes = SUM(Ventes[Montant])
```

Si tu mets cette mesure dans une carte Power BI, elle peut afficher :

```text
100 000 $
```

Mais si tu mets la même mesure dans un tableau par région :

| Région   | TotalVentes |
| -------- | ----------: |
| Montréal |      40 000 |
| Québec   |      30 000 |
| Laval    |      30 000 |

La formule est la même.

Mais le résultat change.

Pourquoi ?

Parce que le contexte change.

---

## 7.1 Le contexte de filtre

Le **contexte de filtre**, c’est l’ensemble des filtres actifs au moment du calcul.

Ces filtres peuvent venir :

* d’un segment ;
* d’un graphique ;
* d’un tableau ;
* d’une relation entre tables ;
* d’une ligne dans un visuel ;
* d’une formule DAX.

### Vulgarisation

Imagine que DAX porte des lunettes.

Si les lunettes montrent seulement Montréal, DAX calcule Montréal.

Si les lunettes montrent seulement 2025, DAX calcule 2025.

Si les lunettes montrent seulement le produit “Clavier”, DAX calcule le clavier.

La formule peut être identique, mais les lunettes changent.

---

## 7.2 Le contexte de ligne

Le **contexte de ligne**, c’est quand DAX calcule ligne par ligne.

Exemple :

```DAX
MontantLigne = Ventes[Quantité] * Ventes[PrixUnitaire]
```

Ici, DAX prend chaque ligne et fait le calcul.

| Quantité | PrixUnitaire | MontantLigne |
| -------: | -----------: | -----------: |
|        3 |           20 |           60 |
|        2 |           50 |          100 |
|        1 |          200 |          200 |

C’est comme Excel : chaque ligne a son propre calcul.

---

<a id="section-8"></a>

## 8. Les fonctions DAX essentielles

Tu n’as pas besoin d’apprendre 100 fonctions au début.

Il faut commencer avec quelques fonctions importantes.

---

## 8.1 SUM

Additionne une colonne.

```DAX
TotalVentes = SUM(Ventes[Montant])
```

Utilisation :

> Calculer le total des ventes.

---

## 8.2 AVERAGE

Calcule une moyenne.

```DAX
MoyenneVentes = AVERAGE(Ventes[Montant])
```

Utilisation :

> Calculer le montant moyen des ventes.

---

## 8.3 COUNT

Compte les lignes ou les valeurs.

```DAX
NombreVentes = COUNT(Ventes[Montant])
```

Utilisation :

> Compter le nombre de ventes enregistrées.

---

## 8.4 DISTINCTCOUNT

Compte les valeurs uniques.

```DAX
NombreClients = DISTINCTCOUNT(Ventes[ClientID])
```

Utilisation :

> Compter le nombre de clients différents.

Très utile quand un client peut avoir plusieurs achats.

---

## 8.5 DIVIDE

Permet de faire une division proprement.

```DAX
TauxMarge = DIVIDE([Marge], [ChiffreAffaires])
```

Pourquoi utiliser `DIVIDE` au lieu de `/` ?

Parce que `DIVIDE` gère mieux les divisions par zéro.

Exemple :

```text
Marge / Chiffre d’affaires
```

Si le chiffre d’affaires est 0, il peut y avoir une erreur.

Avec `DIVIDE`, Power BI gère cela plus proprement.

---

## 8.6 SUMX

`SUMX` calcule ligne par ligne, puis additionne.

Exemple :

```DAX
ChiffreAffaires =
SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Explication :

1. DAX prend une ligne.
2. Il calcule `Quantité × PrixUnitaire`.
3. Il passe à la ligne suivante.
4. Il additionne tous les résultats.

### Vulgarisation

`SUM` additionne une colonne déjà existante.

`SUMX` crée d’abord un calcul ligne par ligne, puis additionne.

---

## 8.7 CALCULATE

`CALCULATE` est une des fonctions les plus importantes de DAX.

Elle permet de modifier le contexte du calcul.

Exemple :

```DAX
VentesCanada =
CALCULATE(
    [TotalVentes],
    Clients[Pays] = "Canada"
)
```

Cette formule veut dire :

> Calcule les ventes, mais seulement pour le Canada.

### Vulgarisation

`CALCULATE`, c’est comme dire à Power BI :

> Fais le calcul, mais avec une condition spéciale.

Autre exemple :

```DAX
Ventes2025 =
CALCULATE(
    [TotalVentes],
    Date[Année] = 2025
)
```

Cela veut dire :

> Calcule le total des ventes, mais seulement pour l’année 2025.

---

## 8.8 ALL

`ALL` enlève un filtre.

Exemple :

```DAX
PourcentageTotal =
DIVIDE(
    [TotalVentes],
    CALCULATE([TotalVentes], ALL(Produits))
)
```

Cette formule sert à calculer la part d’un produit dans le total global.

### Vulgarisation

`ALL`, c’est comme dire :

> Ignore le filtre actuel et regarde le total complet.

---

<a id="section-9"></a>

## 9. Exemple complet avec ventes

Imaginons une table `Ventes`.

| Date       | Produit | Région   | Quantité | PrixUnitaire | CoûtUnitaire |
| ---------- | ------- | -------- | -------: | -----------: | -----------: |
| 2025-01-01 | Souris  | Montréal |        3 |           20 |           10 |
| 2025-01-02 | Clavier | Québec   |        2 |           50 |           30 |
| 2025-01-03 | Écran   | Montréal |        1 |          200 |          150 |

---

## 9.1 Calculer le chiffre d’affaires

```DAX
ChiffreAffaires =
SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[PrixUnitaire]
)
```

Explication simple :

> Je multiplie la quantité par le prix pour chaque vente, puis j’additionne.

---

## 9.2 Calculer le coût total

```DAX
CoutTotal =
SUMX(
    Ventes,
    Ventes[Quantité] * Ventes[CoutUnitaire]
)
```

Explication simple :

> Je calcule combien les produits ont coûté à l’entreprise.

---

## 9.3 Calculer la marge

```DAX
Marge =
[ChiffreAffaires] - [CoutTotal]
```

Explication simple :

> La marge, c’est ce qui reste après avoir retiré les coûts.

---

## 9.4 Calculer le taux de marge

```DAX
TauxMarge =
DIVIDE(
    [Marge],
    [ChiffreAffaires]
)
```

Explication simple :

> Le taux de marge montre quelle partie du chiffre d’affaires reste en marge.

Exemple :

```text
Chiffre d’affaires = 10 000
Marge = 2 500

Taux de marge = 2 500 / 10 000 = 25 %
```

---

## 9.5 Calculer le nombre de produits vendus

```DAX
TotalQuantite =
SUM(Ventes[Quantité])
```

Explication simple :

> J’additionne toutes les quantités vendues.

---

## 9.6 Calculer le panier moyen

```DAX
PanierMoyen =
DIVIDE(
    [ChiffreAffaires],
    DISTINCTCOUNT(Ventes[ClientID])
)
```

Explication simple :

> Le panier moyen indique combien chaque client dépense en moyenne.

---

## 9.7 Calculer les ventes pour Montréal seulement

```DAX
VentesMontreal =
CALCULATE(
    [ChiffreAffaires],
    Ventes[Région] = "Montréal"
)
```

Explication simple :

> Je calcule les ventes, mais uniquement pour Montréal.

---

## 9.8 Calculer le pourcentage de chaque région

```DAX
PourcentageRegion =
DIVIDE(
    [ChiffreAffaires],
    CALCULATE([ChiffreAffaires], ALL(Ventes[Région]))
)
```

Explication simple :

> Je compare les ventes de la région actuelle avec le total de toutes les régions.

Exemple :

| Région   | Ventes | Pourcentage |
| -------- | -----: | ----------: |
| Montréal | 40 000 |        40 % |
| Québec   | 35 000 |        35 % |
| Laval    | 25 000 |        25 % |

---

<a id="section-10"></a>

## 10. Résumé final à retenir

### Power BI sans DAX

Power BI sans DAX permet de :

* charger les données ;
* nettoyer les données ;
* créer des graphiques ;
* faire des filtres ;
* afficher des sommes simples ;
* faire des rapports simples.

Mais il devient limité pour les analyses avancées.

---

### Power BI avec DAX

Power BI avec DAX permet de :

* créer des indicateurs métier ;
* calculer des marges ;
* calculer des taux ;
* calculer des pourcentages ;
* comparer des périodes ;
* créer des KPI ;
* faire des calculs dynamiques ;
* contrôler le contexte des filtres ;
* produire des rapports professionnels.

---

## Phrase très simple à retenir

```text
Power Query prépare les données.
DAX analyse les données.
Power BI affiche les résultats.
```

---

## Différence entre Power Query et DAX

| Outil                   | Rôle                            |
| ----------------------- | ------------------------------- |
| Power Query             | Nettoyer, transformer, préparer |
| DAX                     | Calculer, analyser, comparer    |
| Visualisations Power BI | Afficher les résultats          |

### Exemple simple

Power Query sert à dire :

> Nettoie mes colonnes, supprime les erreurs, transforme les dates.

DAX sert à dire :

> Calcule ma marge, mon taux de croissance, mon pourcentage du total.

---

## Conclusion

DAX est important parce qu’il transforme Power BI en véritable outil d’analyse.

Sans DAX, Power BI permet surtout de présenter des données.

Avec DAX, Power BI permet de comprendre les données, créer des indicateurs, comparer les résultats et prendre de meilleures décisions.

La vraie puissance de Power BI commence quand on comprend que les données brutes ne suffisent pas.

Il faut les transformer en indicateurs.

Et c’est exactement le rôle de DAX.
