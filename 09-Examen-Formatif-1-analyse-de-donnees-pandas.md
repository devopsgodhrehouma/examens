<a id="top"></a>

# EXAMEN PRATIQUE — ANALYSE DE DONNÉES AVEC NUMPY, PANDAS ET SEABORN (GOOGLE COLAB)

**Documentation autorisée** (`numpy`, `pandas`, `matplotlib`, `seaborn`, documentation officielle, aide intégrée Colab)  
**Travail individuel**  
**Environnement obligatoire : Google Colab**  
**Dataset imposé : Titanic**

**Chaque réponse doit apparaître directement dans le notebook Colab** :
- le **code**
- le **résultat obtenu**
- une **interprétation claire et justifiée**

<br/>
<br/>

# CONSIGNES GÉNÉRALES

- Complétez toutes les parties dans l’ordre.
- Ne sautez **aucune étape**.
- **Respectez strictement les noms de variables demandés** lorsqu’ils sont imposés.
- Chaque graphique doit être **lisible**, **titré** et correctement **étiqueté**.
- Toute réponse purement théorique sans code lorsque le code est demandé sera considérée incomplète.
- Les réponses doivent être **propres**, **structurées** et **professionnelles**.
- Toutes les analyses doivent être faites à partir du dataset chargé dans Colab.
- Vous devez utiliser **NumPy**, **Pandas** et **Seaborn** au cours de l’examen.
- Ne remplacez pas le dataset par un autre.
- N’utilisez pas d’outil de machine learning dans cet examen.

<br/>
<br/>

# CELLULE DE DÉPART OBLIGATOIRE

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

pd.set_option("display.max_columns", None)

url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)

df.head()
````

<br/>
<br/>

# PARTIE 1 – Préparation de l’environnement Colab et chargement du dataset

## Question 1 — Importez les bibliothèques `numpy`, `pandas`, `seaborn` et `matplotlib.pyplot`.

<details>
<summary>Réponse</summary>

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

</details>

## Question 2 — Chargez le dataset Titanic dans un DataFrame nommé `df`.

<details>
<summary>Réponse</summary>

```python
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)
```

</details>

## Question 3 — Affichez les 10 premières lignes du dataset.

<details>
<summary>Réponse</summary>

```python
df.head(10)
```

</details>

## Question 4 — Affichez les 10 dernières lignes du dataset.

<details>
<summary>Réponse</summary>

```python
df.tail(10)
```

</details>

## Question 5 — Affichez le nombre de lignes et de colonnes.

<details>
<summary>Réponse</summary>

```python
df.shape
```

</details>

## Question 6 — Affichez la liste complète des colonnes.

<details>
<summary>Réponse</summary>

```python
df.columns.tolist()
```

</details>

## Question 7 — Affichez les types de données de chaque colonne.

<details>
<summary>Réponse</summary>

```python
df.dtypes
```

</details>

## Question 8 — Affichez un résumé général du dataset.

<details>
<summary>Réponse</summary>

```python
df.info()
df.describe(include="all")
```

</details>

<br/>
<br/>

# PARTIE 2 – Compréhension initiale du dataset

## Question 9 — Combien y a-t-il de passagers dans le dataset ?

<details>
<summary>Réponse</summary>

```python
df.shape[0]
```

</details>

## Question 10 — Combien y a-t-il de variables ?

<details>
<summary>Réponse</summary>

```python
df.shape[1]
```

</details>

## Question 11 — Quelle colonne semble représenter la variable cible la plus importante ?

<details>
<summary>Réponse</summary>

```python
print("La variable cible la plus importante est : survived")
```

</details>

## Question 12 — Affichez les colonnes numériques.

<details>
<summary>Réponse</summary>

```python
df.select_dtypes(include=np.number).columns.tolist()
```

</details>

## Question 13 — Affichez les colonnes catégorielles.

<details>
<summary>Réponse</summary>

```python
df.select_dtypes(include=["object", "category"]).columns.tolist()
```

</details>

## Question 14 — Affichez les colonnes booléennes.

<details>
<summary>Réponse</summary>

```python
df.select_dtypes(include=["bool"]).columns.tolist()
```

</details>

## Question 15 — Que représente une ligne du dataset ?

<details>
<summary>Réponse</summary>

```python
print("Chaque ligne représente un passager du Titanic.")
```

</details>

## Question 16 — Quelles colonnes semblent les plus utiles pour expliquer la survie ?

<details>
<summary>Réponse</summary>

```python
print(["sex", "pclass", "age", "fare", "embarked", "alone"])
```

</details>

## Question 17 — Affichez les statistiques descriptives des colonnes numériques.

<details>
<summary>Réponse</summary>

```python
df.describe()
```

</details>

## Question 18 — Affichez un résumé descriptif des colonnes non numériques.

<details>
<summary>Réponse</summary>

```python
df.describe(include=["object", "category", "bool"])
```

</details>

<br/>
<br/>

# PARTIE 3 – Qualité des données et nettoyage

## Question 19 — Affichez le nombre de valeurs manquantes par colonne.

<details>
<summary>Réponse</summary>

```python
df.isnull().sum()
```

</details>

## Question 20 — Calculez le pourcentage de valeurs manquantes par colonne.

<details>
<summary>Réponse</summary>

```python
(df.isnull().sum() / len(df)) * 100
```

</details>

## Question 21 — Classez les colonnes de la plus touchée à la moins touchée.

<details>
<summary>Réponse</summary>

```python
((df.isnull().sum() / len(df)) * 100).sort_values(ascending=False)
```

</details>

## Question 22 — Identifiez les colonnes particulièrement problématiques.

<details>
<summary>Réponse</summary>

```python
missing_pct = ((df.isnull().sum() / len(df)) * 100).sort_values(ascending=False)
missing_pct[missing_pct > 20]
```

</details>

## Question 23 — Expliquez brièvement pourquoi certaines colonnes peuvent poser problème.

<details>
<summary>Réponse</summary>

```python
print("Une colonne avec beaucoup de valeurs manquantes peut fausser l’analyse ou nécessiter un traitement important.")
```

</details>

## Question 24 — Traitez les valeurs manquantes de `age`.

<details>
<summary>Réponse</summary>

```python
df["age"] = df["age"].fillna(df["age"].median())
```

</details>

## Question 25 — Traitez les valeurs manquantes de `embarked`.

<details>
<summary>Réponse</summary>

```python
df["embarked"] = df["embarked"].fillna(df["embarked"].mode()[0])
```

</details>

## Question 26 — Décidez quoi faire de `deck`.

<details>
<summary>Réponse</summary>

```python
df = df.drop(columns=["deck"])
```

</details>

## Question 27 — Vérifiez les valeurs manquantes après traitement.

<details>
<summary>Réponse</summary>

```python
df.isnull().sum()
```

</details>

## Question 28 — Vérifiez s’il existe des doublons exacts.

<details>
<summary>Réponse</summary>

```python
df.duplicated().sum()
```

</details>

## Question 29 — Supprimez les doublons s’il y en a.

<details>
<summary>Réponse</summary>

```python
df = df.drop_duplicates()
```

</details>

## Question 30 — Indiquez combien de lignes ont été supprimées.

<details>
<summary>Réponse</summary>

```python
# version simple
print("Comparer le nombre de lignes avant et après suppression.")
```

</details>

<br/>
<br/>

# PARTIE 4 – Analyse exploratoire avec Pandas

## Question 31 — Quel est le taux global de survie ?

<details>
<summary>Réponse</summary>

```python
df["survived"].mean()
```

</details>

## Question 32 — Combien de passagers ont survécu ?

<details>
<summary>Réponse</summary>

```python
df["survived"].value_counts().get(1, 0)
```

</details>

## Question 33 — Combien de passagers sont décédés ?

<details>
<summary>Réponse</summary>

```python
df["survived"].value_counts().get(0, 0)
```

</details>

## Question 34 — Quelle est la répartition des passagers par sexe ?

<details>
<summary>Réponse</summary>

```python
df["sex"].value_counts()
```

</details>

## Question 35 — Quelle est la répartition des passagers par classe ?

<details>
<summary>Réponse</summary>

```python
df["pclass"].value_counts().sort_index()
```

</details>

## Question 36 — Quel est le taux de survie par sexe ?

<details>
<summary>Réponse</summary>

```python
df.groupby("sex")["survived"].mean()
```

</details>

## Question 37 — Quel est le taux de survie par classe ?

<details>
<summary>Réponse</summary>

```python
df.groupby("pclass")["survived"].mean()
```

</details>

## Question 38 — Quel est le taux de survie par port d’embarquement ?

<details>
<summary>Réponse</summary>

```python
df.groupby("embarked")["survived"].mean()
```

</details>

## Question 39 — Quel est l’âge moyen des passagers ?

<details>
<summary>Réponse</summary>

```python
df["age"].mean()
```

</details>

## Question 40 — Quel est l’âge moyen des survivants ?

<details>
<summary>Réponse</summary>

```python
df[df["survived"] == 1]["age"].mean()
```

</details>

## Question 41 — Quel est l’âge moyen des non-survivants ?

<details>
<summary>Réponse</summary>

```python
df[df["survived"] == 0]["age"].mean()
```

</details>

## Question 42 — Quel est le tarif moyen payé par les passagers ?

<details>
<summary>Réponse</summary>

```python
df["fare"].mean()
```

</details>

## Question 43 — Quel est le tarif moyen payé par classe ?

<details>
<summary>Réponse</summary>

```python
df.groupby("pclass")["fare"].mean()
```

</details>

## Question 44 — Quel groupe semble avoir la plus forte probabilité de survie ?

<details>
<summary>Réponse</summary>

```python
df.groupby(["sex", "pclass"])["survived"].mean().sort_values(ascending=False)
```

</details>

## Question 45 — Justifiez votre réponse à l’aide de chiffres précis.

<details>
<summary>Réponse</summary>

```python
df.groupby(["sex", "pclass"])["survived"].mean().sort_values(ascending=False)
```

</details>

<br/>
<br/>

# PARTIE 5 – Création de nouvelles colonnes

## Question 46 — Créez la colonne `is_child`.

<details>
<summary>Réponse</summary>

```python
df["is_child"] = np.where(df["age"] < 18, 1, 0)
```

</details>

## Question 47 — Créez la colonne `family_size`.

<details>
<summary>Réponse</summary>

```python
df["family_size"] = df["sibsp"] + df["parch"] + 1
```

</details>

## Question 48 — Créez la colonne `is_alone`.

<details>
<summary>Réponse</summary>

```python
df["is_alone"] = np.where(df["family_size"] == 1, 1, 0)
```

</details>

## Question 49 — Créez la colonne `fare_per_person`.

<details>
<summary>Réponse</summary>

```python
df["fare_per_person"] = df["fare"] / df["family_size"]
```

</details>

## Question 50 — Créez la colonne `age_group`.

<details>
<summary>Réponse</summary>

```python
def age_group(age):
    if age < 18:
        return "child"
    elif age < 60:
        return "adult"
    else:
        return "senior"

df["age_group"] = df["age"].apply(age_group)
```

</details>

## Question 51 — Affichez les 15 premières lignes avec ces nouvelles colonnes.

<details>
<summary>Réponse</summary>

```python
df.head(15)
```

</details>

## Question 52 — Quel est le taux de survie des enfants ?

<details>
<summary>Réponse</summary>

```python
df[df["age_group"] == "child"]["survived"].mean()
```

</details>

## Question 53 — Quel est le taux de survie des adultes ?

<details>
<summary>Réponse</summary>

```python
df[df["age_group"] == "adult"]["survived"].mean()
```

</details>

## Question 54 — Quel est le taux de survie des seniors ?

<details>
<summary>Réponse</summary>

```python
df[df["age_group"] == "senior"]["survived"].mean()
```

</details>

## Question 55 — Les passagers seuls survivent-ils moins que les autres ?

<details>
<summary>Réponse</summary>

```python
df.groupby("is_alone")["survived"].mean()
```

</details>

## Question 56 — Les familles nombreuses semblent-elles avantagées ou désavantagées ?

<details>
<summary>Réponse</summary>

```python
df.groupby("family_size")["survived"].mean()
```

</details>

## Question 57 — Interprétez les résultats.

<details>
<summary>Réponse</summary>

```python
print("Comparer les taux de survie selon age_group, is_alone et family_size.")
```

</details>

<br/>
<br/>

# PARTIE 6 – Sélection, filtrage et tri

## Question 58 — Affichez tous les passagers de sexe féminin ayant survécu.

<details>
<summary>Réponse</summary>

```python
df[(df["sex"] == "female") & (df["survived"] == 1)]
```

</details>

## Question 59 — Affichez tous les passagers masculins de troisième classe n’ayant pas survécu.

<details>
<summary>Réponse</summary>

```python
df[(df["sex"] == "male") & (df["pclass"] == 3) & (df["survived"] == 0)]
```

</details>

## Question 60 — Affichez les passagers âgés de plus de 60 ans.

<details>
<summary>Réponse</summary>

```python
df[df["age"] > 60]
```

</details>

## Question 61 — Affichez les passagers dont le tarif est supérieur à la moyenne.

<details>
<summary>Réponse</summary>

```python
df[df["fare"] > df["fare"].mean()]
```

</details>

## Question 62 — Affichez les 10 passagers ayant payé les billets les plus chers.

<details>
<summary>Réponse</summary>

```python
df.sort_values(by="fare", ascending=False).head(10)
```

</details>

## Question 63 — Affichez les 10 plus jeunes passagers.

<details>
<summary>Réponse</summary>

```python
df.sort_values(by="age", ascending=True).head(10)
```

</details>

## Question 64 — Affichez les passagers embarqués à Southampton.

<details>
<summary>Réponse</summary>

```python
df[df["embark_town"] == "Southampton"]
```

</details>

## Question 65 — Combien de femmes de première classe ont survécu ?

<details>
<summary>Réponse</summary>

```python
df[(df["sex"] == "female") & (df["pclass"] == 1) & (df["survived"] == 1)].shape[0]
```

</details>

## Question 66 — Combien d’enfants voyageaient seuls ?

<details>
<summary>Réponse</summary>

```python
df[(df["is_child"] == 1) & (df["is_alone"] == 1)].shape[0]
```

</details>

## Question 67 — Quel sous-groupe semble le plus vulnérable ?

<details>
<summary>Réponse</summary>

```python
df.groupby(["sex", "pclass"])["survived"].mean().sort_values()
```

</details>

<br/>
<br/>

# PARTIE 7 – GroupBy, agrégations et tableaux croisés

## Question 68 — Calculez l’âge moyen par sexe.

<details>
<summary>Réponse</summary>

```python
df.groupby("sex")["age"].mean()
```

</details>

## Question 69 — Calculez le tarif moyen par classe.

<details>
<summary>Réponse</summary>

```python
df.groupby("pclass")["fare"].mean()
```

</details>

## Question 70 — Calculez le taux de survie par combinaison sexe / classe.

<details>
<summary>Réponse</summary>

```python
df.groupby(["sex", "pclass"])["survived"].mean()
```

</details>

## Question 71 — Calculez l’âge moyen selon le sexe et le statut de survie.

<details>
<summary>Réponse</summary>

```python
df.groupby(["sex", "survived"])["age"].mean()
```

</details>

## Question 72 — Calculez la taille moyenne de famille selon la classe.

<details>
<summary>Réponse</summary>

```python
df.groupby("pclass")["family_size"].mean()
```

</details>

## Question 73 — Construisez un tableau croisé entre `sex` et `survived`.

<details>
<summary>Réponse</summary>

```python
pd.crosstab(df["sex"], df["survived"])
```

</details>

## Question 74 — Construisez un tableau croisé entre `pclass` et `survived`.

<details>
<summary>Réponse</summary>

```python
pd.crosstab(df["pclass"], df["survived"])
```

</details>

## Question 75 — Construisez une version normalisée en proportions pour `sex` et `survived`.

<details>
<summary>Réponse</summary>

```python
pd.crosstab(df["sex"], df["survived"], normalize="index")
```

</details>

## Question 76 — Construisez une version normalisée en proportions pour `pclass` et `survived`.

<details>
<summary>Réponse</summary>

```python
pd.crosstab(df["pclass"], df["survived"], normalize="index")
```

</details>

## Question 77 — Quelle combinaison de variables semble la plus explicative ?

<details>
<summary>Réponse</summary>

```python
print("sex et pclass semblent très explicatives.")
```

</details>

## Question 78 — Rédigez une mini-conclusion analytique.

<details>
<summary>Réponse</summary>

```python
print("Les résultats montrent que le sexe et la classe influencent fortement la survie.")
```

</details>

<br/>
<br/>

# PARTIE 8 – Utilisation de NumPy dans l’analyse

## Question 79 — Convertissez la colonne `age` en tableau NumPy.

<details>
<summary>Réponse</summary>

```python
age_array = df["age"].to_numpy()
age_array
```

</details>

## Question 80 — Affichez sa forme.

<details>
<summary>Réponse</summary>

```python
age_array.shape
```

</details>

## Question 81 — Calculez la moyenne avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.mean(age_array)
```

</details>

## Question 82 — Calculez la médiane avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.median(age_array)
```

</details>

## Question 83 — Calculez l’écart-type avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.std(age_array)
```

</details>

## Question 84 — Calculez le minimum avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.min(age_array)
```

</details>

## Question 85 — Calculez le maximum avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.max(age_array)
```

</details>

## Question 86 — Comparez ces résultats avec Pandas.

<details>
<summary>Réponse</summary>

```python
df["age"].describe()
```

</details>

## Question 87 — Construisez un tableau NumPy contenant `age`, `fare`, `survived`.

<details>
<summary>Réponse</summary>

```python
subset_array = df[["age", "fare", "survived"]].to_numpy()
subset_array
```

</details>

## Question 88 — Affichez la forme de ce tableau.

<details>
<summary>Réponse</summary>

```python
subset_array.shape
```

</details>

## Question 89 — Extrayez avec NumPy uniquement les passagers survivants.

<details>
<summary>Réponse</summary>

```python
subset_array[subset_array[:, 2] == 1]
```

</details>

## Question 90 — Calculez le tarif moyen des survivants avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.mean(subset_array[subset_array[:, 2] == 1][:, 1])
```

</details>

## Question 91 — Calculez le tarif moyen des non-survivants avec NumPy.

<details>
<summary>Réponse</summary>

```python
np.mean(subset_array[subset_array[:, 2] == 0][:, 1])
```

</details>

## Question 92 — Utilisez `np.where` pour créer une catégorie tarifaire.

<details>
<summary>Réponse</summary>

```python
np.where(df["fare"] > 50, "Expensive", "Affordable")
```

</details>

## Question 93 — Expliquez dans quels cas NumPy peut être utile.

<details>
<summary>Réponse</summary>

```python
print("NumPy est utile pour les calculs numériques rapides sur des tableaux.")
```

</details>

<br/>
<br/>

# PARTIE 9 – Visualisation avec Seaborn et Matplotlib

## Question 94 — Histogramme des âges.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.histplot(df["age"], kde=True)
plt.title("Distribution des âges")
plt.xlabel("Âge")
plt.ylabel("Fréquence")
plt.show()
```

</details>

## Question 95 — Boxplot des âges.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.boxplot(x=df["age"])
plt.title("Boxplot des âges")
plt.xlabel("Âge")
plt.show()
```

</details>

## Question 96 — Countplot du sexe.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.countplot(data=df, x="sex")
plt.title("Répartition par sexe")
plt.xlabel("Sexe")
plt.ylabel("Nombre")
plt.show()
```

</details>

## Question 97 — Countplot de la classe.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.countplot(data=df, x="pclass")
plt.title("Répartition par classe")
plt.xlabel("Classe")
plt.ylabel("Nombre")
plt.show()
```

</details>

## Question 98 — Countplot de la survie.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.countplot(data=df, x="survived")
plt.title("Répartition de la survie")
plt.xlabel("Survie")
plt.ylabel("Nombre")
plt.show()
```

</details>

## Question 99 — Barplot de la survie selon le sexe.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.barplot(data=df, x="sex", y="survived")
plt.title("Taux de survie par sexe")
plt.xlabel("Sexe")
plt.ylabel("Taux de survie")
plt.show()
```

</details>

## Question 100 — Barplot de la survie selon la classe.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.barplot(data=df, x="pclass", y="survived")
plt.title("Taux de survie par classe")
plt.xlabel("Classe")
plt.ylabel("Taux de survie")
plt.show()
```

</details>

## Question 101 — Barplot de la survie selon le port d’embarquement.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.barplot(data=df, x="embarked", y="survived")
plt.title("Taux de survie par port d’embarquement")
plt.xlabel("Port")
plt.ylabel("Taux de survie")
plt.show()
```

</details>

## Question 102 — Boxplot de l’âge selon la survie.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.boxplot(data=df, x="survived", y="age")
plt.title("Âge selon la survie")
plt.xlabel("Survie")
plt.ylabel("Âge")
plt.show()
```

</details>

## Question 103 — Boxplot du tarif selon la classe.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.boxplot(data=df, x="pclass", y="fare")
plt.title("Tarif selon la classe")
plt.xlabel("Classe")
plt.ylabel("Tarif")
plt.show()
```

</details>

## Question 104 — Violinplot de l’âge selon le sexe.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.violinplot(data=df, x="sex", y="age")
plt.title("Âge selon le sexe")
plt.xlabel("Sexe")
plt.ylabel("Âge")
plt.show()
```

</details>

## Question 105 — Scatterplot entre `age` et `fare`.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.scatterplot(data=df, x="age", y="fare")
plt.title("Relation entre âge et tarif")
plt.xlabel("Âge")
plt.ylabel("Tarif")
plt.show()
```

</details>

## Question 106 — Scatterplot entre `age` et `fare` coloré par `survived`.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(8,5))
sns.scatterplot(data=df, x="age", y="fare", hue="survived")
plt.title("Relation entre âge, tarif et survie")
plt.xlabel("Âge")
plt.ylabel("Tarif")
plt.show()
```

</details>

## Question 107 — Heatmap de corrélation.

<details>
<summary>Réponse</summary>

```python
plt.figure(figsize=(10,6))
corr = df.select_dtypes(include=np.number).corr()
sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("Matrice de corrélation")
plt.show()
```

</details>

## Question 108 — Pairplot sur un sous-ensemble pertinent.

<details>
<summary>Réponse</summary>

```python
sns.pairplot(df[["age", "fare", "pclass", "survived"]].dropna(), hue="survived")
plt.show()
```

</details>

## Question 109 — Quel graphique vous semble le plus révélateur ?

<details>
<summary>Réponse</summary>

```python
print("Le barplot de survie par sexe et par classe est très révélateur.")
```

</details>

## Question 110 — Quel graphique montre le mieux l’impact du sexe ?

<details>
<summary>Réponse</summary>

```python
print("Le barplot de la survie selon le sexe.")
```

</details>

## Question 111 — Quel graphique montre le mieux l’impact de la classe sociale ?

<details>
<summary>Réponse</summary>

```python
print("Le barplot de la survie selon la classe.")
```

</details>

## Question 112 — Voyez-vous une relation évidente entre âge et survie ?

<details>
<summary>Réponse</summary>

```python
print("La relation semble moins forte que pour le sexe ou la classe.")
```

</details>

## Question 113 — Justifiez vos réponses.

<details>
<summary>Réponse</summary>

```python
print("Les différences visuelles de hauteur entre les catégories montrent des écarts de survie importants.")
```

</details>

<br/>
<br/>

# PARTIE 10 – Analyse approfondie et interprétation

## Question 114 — Les femmes survivent-elles davantage que les hommes ?

<details>
<summary>Réponse</summary>

```python
df.groupby("sex")["survived"].mean()
```

</details>

## Question 115 — Les passagers de première classe semblent-ils avantagés ?

<details>
<summary>Réponse</summary>

```python
df.groupby("pclass")["survived"].mean()
```

</details>

## Question 116 — Les enfants semblent-ils mieux protégés ?

<details>
<summary>Réponse</summary>

```python
df.groupby("is_child")["survived"].mean()
```

</details>

## Question 117 — Les passagers voyageant seuls sont-ils désavantagés ?

<details>
<summary>Réponse</summary>

```python
df.groupby("is_alone")["survived"].mean()
```

</details>

## Question 118 — Le tarif payé peut-il être un indice indirect du statut social ?

<details>
<summary>Réponse</summary>

```python
df.groupby("pclass")["fare"].mean()
```

</details>

## Question 119 — Existe-t-il un lien apparent entre âge et survie ?

<details>
<summary>Réponse</summary>

```python
df.groupby("survived")["age"].mean()
```

</details>

## Question 120 — Existe-t-il un lien apparent entre taille de famille et survie ?

<details>
<summary>Réponse</summary>

```python
df.groupby("family_size")["survived"].mean()
```

</details>

## Question 121 — Proposez trois hypothèses plausibles expliquant les tendances observées.

<details>
<summary>Réponse</summary>

```python
print("1. Les femmes ont été prioritaires lors de l’évacuation.")
print("2. Les passagers de première classe avaient un meilleur accès aux secours.")
print("3. Le statut social a pu influencer les chances de survie.")
```

</details>

## Question 122 — Proposez deux limites importantes de cette analyse.

<details>
<summary>Réponse</summary>

```python
print("1. Certaines données sont manquantes ou imputées.")
print("2. L’analyse est descriptive et ne démontre pas la causalité.")
```

</details>

## Question 123 — Expliquez pourquoi une interprétation prudente reste nécessaire.

<details>
<summary>Réponse</summary>

```python
print("Une corrélation observée ne prouve pas une relation de cause à effet.")
```

</details>

<br/>
<br/>

# PARTIE 11 – Transformations supplémentaires

## Question 124 — Triez le dataset par âge croissant.

<details>
<summary>Réponse</summary>

```python
df.sort_values(by="age", ascending=True)
```

</details>

## Question 125 — Triez le dataset par tarif décroissant.

<details>
<summary>Réponse</summary>

```python
df.sort_values(by="fare", ascending=False)
```

</details>

## Question 126 — Créez un nouveau DataFrame contenant `sex`, `age`, `fare`, `survived`, `pclass`.

<details>
<summary>Réponse</summary>

```python
df_small = df[["sex", "age", "fare", "survived", "pclass"]].copy()
df_small.head()
```

</details>

## Question 127 — Renommez ces colonnes en français.

<details>
<summary>Réponse</summary>

```python
df_small.columns = ["sexe", "age", "tarif", "survie", "classe"]
df_small.head()
```

</details>

## Question 128 — Remplacez les valeurs de survie par `Décédé` et `Survécu`.

<details>
<summary>Réponse</summary>

```python
df_small["survie"] = df_small["survie"].replace({0: "Décédé", 1: "Survécu"})
df_small.head()
```

</details>

## Question 129 — Créez une catégorie de tarif : faible, moyen, élevé.

<details>
<summary>Réponse</summary>

```python
df_small["categorie_tarif"] = pd.cut(
    df_small["tarif"],
    bins=[-1, 10, 50, df_small["tarif"].max()],
    labels=["faible", "moyen", "élevé"]
)
df_small.head()
```

</details>

## Question 130 — Analysez la survie selon cette catégorie tarifaire.

<details>
<summary>Réponse</summary>

```python
df_small.groupby("categorie_tarif")["survie"].value_counts(normalize=True)
```

</details>

## Question 131 — Exportez le DataFrame nettoyé en fichier CSV.

<details>
<summary>Réponse</summary>

```python
df_small.to_csv("titanic_transforme.csv", index=False)
```

</details>

## Question 132 — Téléchargez ce fichier depuis Colab.

<details>
<summary>Réponse</summary>

```python
from google.colab import files
files.download("titanic_transforme.csv")
```

</details>

## Question 133 — Expliquez l’intérêt professionnel d’exporter un dataset transformé.

<details>
<summary>Réponse</summary>

```python
print("Cela permet de réutiliser les données nettoyées dans d’autres analyses, rapports ou applications.")
```

</details>

<br/>
<br/>

# PARTIE 12 – Conclusion analytique rédigée

## Question 134 — Rédigez une conclusion complète de 10 à 15 lignes.

<details>
<summary>Réponse</summary>

```markdown
L’analyse du dataset Titanic met en évidence plusieurs facteurs fortement liés à la survie des passagers. Le sexe apparaît comme l’une des variables les plus influentes, avec un taux de survie nettement plus élevé chez les femmes. La classe sociale joue également un rôle important, puisque les passagers de première classe semblent avoir été avantagés par rapport à ceux de troisième classe. L’âge montre certaines différences, mais son effet paraît moins marqué que celui du sexe et de la classe. Le tarif payé peut aussi servir d’indicateur indirect du niveau social et des conditions de voyage. Les variables construites, comme la taille de la famille et le fait de voyager seul, enrichissent l’analyse et permettent d’observer d’autres tendances intéressantes. Les visualisations réalisées avec Seaborn confirment les écarts observés dans les tableaux statistiques. Toutefois, cette étude reste descriptive et ne permet pas d’établir une causalité. Certaines données ont dû être imputées ou supprimées, ce qui peut influencer les résultats. Si un modèle prédictif devait être construit plus tard, les variables `sex`, `pclass`, `age`, `fare`, `family_size` et `is_alone` seraient particulièrement pertinentes.
```

</details>

<br/>
<br/>

# FICHIERS À REMETTRE

* Le notebook **Google Colab** complété
* Une version exportée en **`.ipynb`**
* Une version exportée en **`.pdf`**
* Le fichier **CSV transformé** exporté à la fin de l’examen

