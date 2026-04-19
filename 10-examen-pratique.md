<a id="top"></a>

# EXAMEN PRATIQUE — ANALYSE DE DONNÉES AVEC NUMPY, PANDAS ET SEABORN (GOOGLE COLAB)

**Documentation autorisée** (`numpy`, `pandas`, `matplotlib`, `seaborn`, documentation officielle, aide intégrée Colab)
**Travail individuel**
**Environnement obligatoire : Google Colab**
**Dataset imposé : Tips**

**Chaque réponse doit apparaître directement dans le notebook Colab** :

* le **code**
* le **résultat obtenu**
* une **interprétation claire et justifiée**

<br/>
<br/>

# CONSIGNES GÉNÉRALES

* Complétez toutes les parties dans l’ordre.
* Ne sautez **aucune étape**.
* **Respectez strictement les noms de variables demandés** lorsqu’ils sont imposés.
* Chaque graphique doit être **lisible**, **titré** et correctement **étiqueté**.
* Toute réponse purement théorique sans code lorsque le code est demandé sera considérée incomplète.
* Les réponses doivent être **propres**, **structurées** et **professionnelles**.
* Toutes les analyses doivent être faites à partir du dataset chargé dans Colab.
* Vous devez utiliser **NumPy**, **Pandas** et **Seaborn** au cours de l’examen.
* Ne remplacez pas le dataset par un autre.
* N’utilisez pas d’outil de machine learning dans cet examen.

<br/>
<br/>

# CELLULE DE DÉPART OBLIGATOIRE

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

pd.set_option("display.max_columns", None)

df = sns.load_dataset("tips")

df.head()
```

<br/>
<br/>

# PARTIE 1 – Préparation de l’environnement Colab et chargement du dataset

## Question 1 — Importez les bibliothèques `numpy`, `pandas`, `seaborn` et `matplotlib.pyplot`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 2 — Chargez le dataset `tips` dans un DataFrame nommé `df`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 3 — Affichez les 10 premières lignes du dataset.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 4 — Affichez les 10 dernières lignes du dataset.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 5 — Affichez le nombre de lignes et de colonnes.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 6 — Affichez la liste complète des colonnes.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 7 — Affichez les types de données de chaque colonne.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 8 — Affichez un résumé général du dataset.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 2 – Compréhension initiale du dataset

## Question 9 — Combien y a-t-il d’observations dans le dataset ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 10 — Combien y a-t-il de variables ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 11 — Quelle colonne semble représenter la variable la plus importante à analyser dans ce contexte ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 12 — Affichez les colonnes numériques.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 13 — Affichez les colonnes catégorielles.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 14 — Vérifiez s’il existe des colonnes booléennes.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 15 — Que représente une ligne du dataset ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 16 — Quelles colonnes semblent les plus utiles pour expliquer le montant du pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 17 — Affichez les statistiques descriptives des colonnes numériques.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 18 — Affichez un résumé descriptif des colonnes non numériques.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 3 – Qualité des données et nettoyage

## Question 19 — Affichez le nombre de valeurs manquantes par colonne.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 20 — Calculez le pourcentage de valeurs manquantes par colonne.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 21 — Classez les colonnes de la plus touchée à la moins touchée.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 22 — Indiquez s’il existe des colonnes problématiques.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 23 — Vérifiez s’il existe des doublons exacts.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 24 — Supprimez les doublons s’il y en a.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 25 — Indiquez combien de lignes ont été supprimées.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 26 — Vérifiez de nouveau les dimensions du DataFrame après nettoyage.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 27 — Vérifiez si certaines colonnes ont des valeurs incohérentes ou inhabituelles.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 28 — Repérez les valeurs extrêmes possibles dans `total_bill`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 29 — Repérez les valeurs extrêmes possibles dans `tip`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 30 — Expliquez brièvement pourquoi la détection des valeurs extrêmes peut être utile.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 4 – Analyse exploratoire avec Pandas

## Question 31 — Quel est le montant moyen de l’addition (`total_bill`) ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 32 — Quel est le montant moyen du pourboire (`tip`) ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 33 — Quelle est la taille moyenne des groupes (`size`) ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 34 — Quelle est la répartition des clients selon le sexe ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 35 — Quelle est la répartition selon le statut fumeur / non-fumeur ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 36 — Quelle est la répartition selon le jour ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 37 — Quelle est la répartition selon le moment de la journée (`time`) ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 38 — Quel sexe laisse en moyenne le plus de pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 39 — Les fumeurs laissent-ils en moyenne plus de pourboire que les non-fumeurs ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 40 — Quel jour présente le pourboire moyen le plus élevé ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 41 — Le midi ou le soir génère-t-il le pourboire moyen le plus élevé ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 42 — Quel jour présente l’addition moyenne la plus élevée ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 43 — Quelle catégorie semble la plus dépensière globalement ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 44 — Le nombre de personnes à table semble-t-il influencer le pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 45 — Justifiez votre réponse à l’aide de chiffres précis.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 5 – Création de nouvelles colonnes

## Question 46 — Créez une colonne `tip_pct` représentant le pourcentage du pourboire par rapport à l’addition.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 47 — Créez une colonne `bill_per_person` représentant le montant de l’addition par personne.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 48 — Créez une colonne `tip_per_person` représentant le pourboire par personne.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 49 — Créez une colonne `is_large_group` valant 1 si le groupe contient au moins 5 personnes, sinon 0.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 50 — Créez une colonne `bill_category` avec trois catégories : `small`, `medium`, `large`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 51 — Affichez les 15 premières lignes avec ces nouvelles colonnes.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 52 — Quel est le pourcentage moyen de pourboire (`tip_pct`) ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 53 — Les grands groupes laissent-ils en moyenne un pourcentage de pourboire plus élevé ou plus faible ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 54 — Quelle catégorie d’addition semble donner le meilleur pourcentage de pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 55 — Comparez le pourboire moyen par personne selon `time`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 56 — Comparez le montant moyen par personne selon `day`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 57 — Interprétez les résultats obtenus.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 6 – Sélection, filtrage et tri

## Question 58 — Affichez toutes les observations correspondant à des clientes (`Female`) ayant laissé un pourboire supérieur à 3.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 59 — Affichez toutes les observations correspondant à des clients (`Male`) fumeurs.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 60 — Affichez les repas dont l’addition dépasse 40.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 61 — Affichez les groupes de plus de 4 personnes.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 62 — Affichez les 10 additions les plus élevées.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 63 — Affichez les 10 pourboires les plus faibles.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 64 — Affichez les observations du dimanche soir.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 65 — Combien d’observations correspondent à des fumeurs le samedi ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 66 — Combien de groupes de 2 personnes ont laissé un pourboire supérieur à la moyenne ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 67 — Quel sous-groupe semble le plus généreux en pourcentage de pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 7 – GroupBy, agrégations et tableaux croisés

## Question 68 — Calculez l’addition moyenne par sexe.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 69 — Calculez le pourboire moyen par statut fumeur / non-fumeur.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 70 — Calculez le pourcentage moyen de pourboire par combinaison sexe / fumeur.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 71 — Calculez l’addition moyenne selon le jour et le moment.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 72 — Calculez la taille moyenne des groupes selon le jour.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 73 — Construisez un tableau croisé entre `sex` et `smoker`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 74 — Construisez un tableau croisé entre `day` et `time`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 75 — Construisez une version normalisée en proportions pour `sex` et `smoker`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 76 — Construisez une version normalisée en proportions pour `day` et `time`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 77 — Quelle combinaison de variables semble la plus explicative pour analyser le pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 78 — Rédigez une mini-conclusion analytique.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 8 – Utilisation de NumPy dans l’analyse

## Question 79 — Convertissez la colonne `total_bill` en tableau NumPy nommé `bill_array`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 80 — Affichez sa forme.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 81 — Calculez la moyenne avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 82 — Calculez la médiane avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 83 — Calculez l’écart-type avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 84 — Calculez le minimum avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 85 — Calculez le maximum avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 86 — Comparez ces résultats avec Pandas.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 87 — Construisez un tableau NumPy contenant `total_bill`, `tip`, `size`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 88 — Affichez la forme de ce tableau.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 89 — Extrayez avec NumPy uniquement les repas dont le pourboire est supérieur à 5.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 90 — Calculez l’addition moyenne des repas dont le pourboire est supérieur à 5 avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 91 — Calculez la taille moyenne des groupes dont l’addition dépasse la moyenne avec NumPy.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 92 — Utilisez `np.where` pour créer une catégorie : `high_tip` si `tip >= 4`, sinon `low_tip`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 93 — Expliquez dans quels cas NumPy peut être utile dans ce type d’analyse.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 9 – Visualisation avec Seaborn et Matplotlib

## Question 94 — Tracez un histogramme de `total_bill`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 95 — Tracez un boxplot de `tip`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 96 — Tracez un countplot du sexe.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 97 — Tracez un countplot du jour.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 98 — Tracez un countplot du moment de la journée (`time`).

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 99 — Tracez un barplot du pourboire moyen selon le sexe.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 100 — Tracez un barplot du pourboire moyen selon le jour.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 101 — Tracez un barplot du pourcentage moyen de pourboire selon le statut fumeur / non-fumeur.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 102 — Tracez un boxplot de `total_bill` selon `time`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 103 — Tracez un boxplot de `tip` selon `day`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 104 — Tracez un violinplot de `tip_pct` selon `sex`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 105 — Tracez un scatterplot entre `total_bill` et `tip`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 106 — Tracez un scatterplot entre `total_bill` et `tip` coloré par `smoker`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 107 — Tracez une heatmap de corrélation entre les colonnes numériques.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 108 — Tracez un pairplot sur un sous-ensemble pertinent du dataset.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 109 — Quel graphique vous semble le plus révélateur ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 110 — Quel graphique montre le mieux la relation entre addition et pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 111 — Quel graphique montre le mieux l’impact du jour ou du moment ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 112 — Voyez-vous une relation visuelle claire entre montant de l’addition et pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 113 — Justifiez vos réponses.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 10 – Analyse approfondie et interprétation

## Question 114 — Les clients qui paient une addition plus élevée laissent-ils généralement un pourboire plus élevé ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 115 — Les fumeurs semblent-ils laisser un pourboire différent des non-fumeurs ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 116 — Le moment de la journée influence-t-il le pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 117 — La taille du groupe semble-t-elle influencer le montant du pourboire ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 118 — Le pourcentage de pourboire varie-t-il selon le sexe ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 119 — Le pourcentage de pourboire varie-t-il selon le jour ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 120 — Les grands groupes sont-ils plus avantageux pour le restaurant ?

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 121 — Proposez trois hypothèses plausibles expliquant les tendances observées.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 122 — Proposez deux limites importantes de cette analyse.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 123 — Expliquez pourquoi une interprétation prudente reste nécessaire.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 11 – Transformations supplémentaires

## Question 124 — Triez le dataset par addition croissante.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 125 — Triez le dataset par pourboire décroissant.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 126 — Créez un nouveau DataFrame contenant `sex`, `total_bill`, `tip`, `size`, `day`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 127 — Renommez ces colonnes en français.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 128 — Créez une colonne textuelle indiquant si le groupe est `Petit groupe` ou `Grand groupe`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 129 — Créez une catégorie de pourboire : `faible`, `moyen`, `élevé`.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 130 — Analysez la répartition de cette catégorie de pourboire.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 131 — Exportez le DataFrame transformé en fichier CSV.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 132 — Téléchargez ce fichier depuis Colab.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

## Question 133 — Expliquez l’intérêt professionnel d’exporter un dataset transformé.

<details>
<summary>Réponse</summary>

```python
..................
```

</details>

<br/>
<br/>

# PARTIE 12 – Conclusion analytique rédigée

## Question 134 — Rédigez une conclusion complète de 10 à 15 lignes sur les tendances observées dans ce dataset.

<details>
<summary>Réponse</summary>

```markdown
..................
..................
..................
..................
..................
..................
..................
..................
..................
..................
```

</details>

<br/>
<br/>

# FICHIERS À REMETTRE

* Le notebook **Google Colab** complété
* Une version exportée en **`.ipynb`**
* Une version exportée en **`.pdf`**
* Le fichier **CSV transformé** exporté à la fin de l’examen
