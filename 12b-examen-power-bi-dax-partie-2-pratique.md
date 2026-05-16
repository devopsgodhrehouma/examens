# EXAMEN PRATIQUE — POWER BI ET DAX

## Analyse des ventes avec mesures DAX et tableau de bord interactif

---

## 1. Contexte de l’examen

Vous travaillez comme analyste de données junior pour une entreprise fictive qui vend du matériel informatique.

L’entreprise souhaite construire un tableau de bord Power BI permettant d’analyser ses ventes selon plusieurs axes :

* les produits ;
* les catégories ;
* les régions ;
* les canaux de vente ;
* les vendeurs ;
* les clients ;
* les dates ;
* les marges ;
* les remises ;
* les objectifs commerciaux.

Votre travail consiste à importer les données, créer les bonnes mesures DAX, construire un tableau de bord lisible et rédiger une courte analyse métier.

---

# 2. Objectifs de l’examen

À la fin de cet examen, vous devez démontrer que vous êtes capable de :

1. importer manuellement un jeu de données dans Power BI ;
2. vérifier les types de données ;
3. comprendre la différence entre une colonne brute et une mesure DAX ;
4. créer des mesures DAX adaptées à une analyse commerciale ;
5. utiliser des fonctions DAX de base et intermédiaires ;
6. créer des visuels pertinents ;
7. utiliser des segments de filtre ;
8. construire un tableau de bord clair ;
9. interpréter les résultats obtenus ;
10. expliquer vos choix de calculs et de visualisation.

---

# 3. Durée de l’examen

Durée suggérée : **2 h 30 à 3 h**

---

# 4. Documents autorisés

Sont autorisés :

* les notes de cours ;
* les exemples vus en classe ;
* la documentation officielle Power BI / DAX ;
* vos propres notes personnelles.

Ne sont pas autorisés :

* copier un tableau de bord complet déjà préparé ;
* remettre le travail d’un autre étudiant ;
* utiliser une solution complète générée automatiquement sans comprendre les mesures ;
* remettre un fichier sans explication.

---

# 5. Données à copier dans Power BI

Dans Power BI Desktop :

1. Ouvrir Power BI Desktop.
2. Cliquer sur **Accueil**.
3. Cliquer sur **Entrer des données**.
4. Copier les données ci-dessous.
5. Nommer la table : **Ventes**.
6. Cliquer sur **Charger**.

```text
Date	CommandeID	ClientID	Produit	Catégorie	Région	Canal	Vendeur	Quantité	PrixUnitaire	CoutUnitaire	RemisePct	ObjectifCA
2025-01-05	CMD001	CL001	PC	Informatique	Québec	Boutique	Samia	2	1000	700	0.05	1800
2025-01-08	CMD002	CL002	Souris	Accessoire	Québec	En ligne	Karim	10	25	10	0.00	250
2025-01-12	CMD003	CL003	Clavier	Accessoire	Ontario	Boutique	Nadia	5	60	30	0.10	300
2025-01-18	CMD004	CL004	Écran	Informatique	Ontario	En ligne	Samia	3	300	180	0.05	850
2025-01-25	CMD005	CL005	Casque	Accessoire	Québec	En ligne	Karim	4	80	35	0.00	320
2025-02-03	CMD006	CL001	PC	Informatique	Ontario	Boutique	Nadia	1	1000	700	0.00	1000
2025-02-09	CMD007	CL006	Portable	Informatique	Québec	Boutique	Samia	1	1500	1050	0.08	1400
2025-02-14	CMD008	CL007	Souris	Accessoire	Ontario	En ligne	Karim	8	25	10	0.00	200
2025-02-20	CMD009	CL008	Clavier	Accessoire	Québec	Boutique	Nadia	6	60	30	0.05	350
2025-02-27	CMD010	CL009	Écran	Informatique	Ontario	Boutique	Samia	2	300	180	0.00	600
2025-03-02	CMD011	CL010	Casque	Accessoire	Québec	En ligne	Karim	5	80	35	0.10	400
2025-03-08	CMD012	CL002	Portable	Informatique	Ontario	En ligne	Nadia	1	1500	1050	0.05	1450
2025-03-15	CMD013	CL003	PC	Informatique	Québec	Boutique	Samia	2	1000	700	0.00	2000
2025-03-19	CMD014	CL004	Souris	Accessoire	Ontario	Boutique	Karim	12	25	10	0.00	300
2025-03-25	CMD015	CL005	Clavier	Accessoire	Québec	En ligne	Nadia	7	60	30	0.10	420
2025-04-04	CMD016	CL006	Écran	Informatique	Québec	Boutique	Samia	2	300	180	0.05	600
2025-04-10	CMD017	CL007	Casque	Accessoire	Ontario	En ligne	Karim	6	80	35	0.00	480
2025-04-15	CMD018	CL008	Portable	Informatique	Québec	En ligne	Nadia	1	1500	1050	0.12	1500
2025-04-22	CMD019	CL009	PC	Informatique	Ontario	Boutique	Samia	2	1000	700	0.05	1900
2025-04-28	CMD020	CL010	Souris	Accessoire	Québec	Boutique	Karim	15	25	10	0.00	375
2025-05-03	CMD021	CL001	Clavier	Accessoire	Ontario	En ligne	Nadia	4	60	30	0.00	240
2025-05-09	CMD022	CL002	Écran	Informatique	Québec	En ligne	Samia	3	300	180	0.08	900
2025-05-16	CMD023	CL003	Casque	Accessoire	Ontario	Boutique	Karim	5	80	35	0.05	400
2025-05-21	CMD024	CL004	Portable	Informatique	Québec	Boutique	Nadia	1	1500	1050	0.00	1500
2025-05-27	CMD025	CL005	PC	Informatique	Ontario	En ligne	Samia	1	1000	700	0.10	1000
2025-06-02	CMD026	CL006	Souris	Accessoire	Québec	En ligne	Karim	20	25	10	0.00	500
2025-06-08	CMD027	CL007	Clavier	Accessoire	Ontario	Boutique	Nadia	8	60	30	0.05	480
2025-06-14	CMD028	CL008	Écran	Informatique	Québec	Boutique	Samia	4	300	180	0.00	1200
2025-06-20	CMD029	CL009	Casque	Accessoire	Ontario	En ligne	Karim	7	80	35	0.10	560
2025-06-26	CMD030	CL010	Portable	Informatique	Ontario	Boutique	Nadia	1	1500	1050	0.05	1500
```

---

# 6. Vérification obligatoire des types de données

Avant de créer les mesures, vous devez vérifier les types de colonnes.

| Colonne      | Type attendu                    |
| ------------ | ------------------------------- |
| Date         | Date                            |
| CommandeID   | Texte                           |
| ClientID     | Texte                           |
| Produit      | Texte                           |
| Catégorie    | Texte                           |
| Région       | Texte                           |
| Canal        | Texte                           |
| Vendeur      | Texte                           |
| Quantité     | Nombre entier                   |
| PrixUnitaire | Nombre décimal ou nombre entier |
| CoutUnitaire | Nombre décimal ou nombre entier |
| RemisePct    | Nombre décimal                  |
| ObjectifCA   | Nombre décimal ou nombre entier |

Vous devez corriger les types si Power BI les détecte mal.

---

# 7. Travail demandé — Mesures DAX à créer

Pour chaque mesure demandée, vous devez :

1. créer une **nouvelle mesure** dans Power BI ;
2. utiliser le nom exact demandé ;
3. écrire vous-même la formule DAX ;
4. tester la mesure dans un visuel ;
5. vérifier que le résultat réagit correctement aux filtres.

Les formules DAX complètes ne sont pas fournies.
Vous devez les écrire vous-même.

---

## 7.1 Mesure : CA brut

Créer une mesure nommée :

```text
CA brut
```

Cette mesure doit représenter le chiffre d’affaires avant remise.

Pour chaque ligne, le calcul logique est :

```text
Quantité × PrixUnitaire
```

La mesure doit additionner ce calcul pour toutes les lignes visibles selon le contexte du rapport.

---

## 7.2 Mesure : Montant remise

Créer une mesure nommée :

```text
Montant remise
```

Cette mesure doit calculer le montant total des remises accordées.

Pour chaque ligne, le calcul logique est :

```text
Quantité × PrixUnitaire × RemisePct
```

La mesure doit additionner les remises de toutes les ventes visibles selon les filtres appliqués.

---

## 7.3 Mesure : CA net

Créer une mesure nommée :

```text
CA net
```

Cette mesure doit représenter le chiffre d’affaires après remise.

Le calcul logique est :

```text
CA brut - Montant remise
```

Cette mesure doit être utilisée comme indicateur principal du tableau de bord.

---

## 7.4 Mesure : Coût total

Créer une mesure nommée :

```text
Coût total
```

Cette mesure doit représenter le coût total des produits vendus.

Pour chaque ligne, le calcul logique est :

```text
Quantité × CoutUnitaire
```

La mesure doit additionner le coût de toutes les ventes visibles selon le contexte.

---

## 7.5 Mesure : Marge

Créer une mesure nommée :

```text
Marge
```

Cette mesure doit représenter le gain réalisé après déduction des coûts.

Le calcul logique est :

```text
CA net - Coût total
```

---

## 7.6 Mesure : Taux de marge

Créer une mesure nommée :

```text
Taux de marge
```

Cette mesure doit représenter la proportion de la marge par rapport au chiffre d’affaires net.

Le calcul logique est :

```text
Marge / CA net
```

La mesure doit être formatée en pourcentage.

Vous devez utiliser une écriture DAX qui évite les erreurs en cas de division par zéro.

---

## 7.7 Mesure : Quantité vendue

Créer une mesure nommée :

```text
Quantité vendue
```

Cette mesure doit additionner toutes les quantités vendues.

Le calcul logique est :

```text
Somme de Quantité
```

---

## 7.8 Mesure : Nombre de ventes

Créer une mesure nommée :

```text
Nombre de ventes
```

Cette mesure doit compter le nombre de lignes de vente dans la table.

Chaque ligne représente une commande ou une transaction.

---

## 7.9 Mesure : Nombre de clients

Créer une mesure nommée :

```text
Nombre de clients
```

Cette mesure doit compter le nombre de clients différents.

Attention : un même client peut apparaître plusieurs fois dans les données.

---

## 7.10 Mesure : Nombre de produits

Créer une mesure nommée :

```text
Nombre de produits
```

Cette mesure doit compter le nombre de produits différents vendus.

---

## 7.11 Mesure : Prix moyen pondéré

Créer une mesure nommée :

```text
Prix moyen pondéré
```

Cette mesure doit calculer le prix moyen réel par unité vendue.

Le calcul logique est :

```text
CA net / Quantité vendue
```

Cette mesure est différente d’une simple moyenne des prix unitaires.

---

## 7.12 Mesure : Remise moyenne

Créer une mesure nommée :

```text
Remise moyenne
```

Cette mesure doit calculer le taux moyen de remise appliqué dans les ventes.

Le calcul logique est :

```text
Moyenne de RemisePct
```

La mesure doit être formatée en pourcentage.

---

## 7.13 Mesure : Objectif total

Créer une mesure nommée :

```text
Objectif total
```

Cette mesure doit additionner les objectifs de chiffre d’affaires.

Le calcul logique est :

```text
Somme de ObjectifCA
```

---

## 7.14 Mesure : Écart objectif

Créer une mesure nommée :

```text
Écart objectif
```

Cette mesure doit comparer le chiffre d’affaires net réalisé avec l’objectif prévu.

Le calcul logique est :

```text
CA net - Objectif total
```

Un résultat positif signifie que l’objectif est dépassé.
Un résultat négatif signifie que l’objectif n’est pas atteint.

---

## 7.15 Mesure : Taux atteinte objectif

Créer une mesure nommée :

```text
Taux atteinte objectif
```

Cette mesure doit calculer le pourcentage d’atteinte de l’objectif.

Le calcul logique est :

```text
CA net / Objectif total
```

La mesure doit être formatée en pourcentage.

Vous devez utiliser une écriture qui évite les erreurs de division.

---

## 7.16 Mesure : CA Québec

Créer une mesure nommée :

```text
CA Québec
```

Cette mesure doit calculer le chiffre d’affaires net uniquement pour la région Québec.

Le calcul logique est :

```text
CA net filtré sur Région = Québec
```

Cette mesure doit utiliser une logique DAX permettant de modifier le contexte de filtre.

---

## 7.17 Mesure : CA Ontario

Créer une mesure nommée :

```text
CA Ontario
```

Cette mesure doit calculer le chiffre d’affaires net uniquement pour la région Ontario.

Le calcul logique est :

```text
CA net filtré sur Région = Ontario
```

---

## 7.18 Mesure : CA en ligne

Créer une mesure nommée :

```text
CA en ligne
```

Cette mesure doit calculer le chiffre d’affaires net uniquement pour le canal **En ligne**.

Le calcul logique est :

```text
CA net filtré sur Canal = En ligne
```

---

## 7.19 Mesure : CA boutique

Créer une mesure nommée :

```text
CA boutique
```

Cette mesure doit calculer le chiffre d’affaires net uniquement pour le canal **Boutique**.

Le calcul logique est :

```text
CA net filtré sur Canal = Boutique
```

---

## 7.20 Mesure : Part du CA total

Créer une mesure nommée :

```text
Part du CA total
```

Cette mesure doit indiquer la contribution d’un élément au chiffre d’affaires total.

Exemple : si la mesure est utilisée dans un tableau par région, elle doit montrer la part de chaque région dans le chiffre d’affaires total.

Le calcul logique est :

```text
CA net du contexte actuel / CA net total sans filtre sur l’axe analysé
```

La mesure doit être formatée en pourcentage.

---

# 8. Table calendrier obligatoire

Vous devez créer une table calendrier dans Power BI.

La table calendrier doit permettre d’analyser les ventes par :

* année ;
* mois ;
* numéro du mois ;
* trimestre ;
* date.

Vous devez ensuite relier la table calendrier à la table **Ventes** avec la colonne **Date**.

---

## Colonnes attendues dans la table calendrier

Votre table calendrier doit contenir au minimum :

| Colonne    | Description          |
| ---------- | -------------------- |
| Date       | Date complète        |
| Année      | Année de la date     |
| Mois       | Nom du mois          |
| NuméroMois | Numéro du mois       |
| Trimestre  | Trimestre de l’année |

Vous devez vous assurer que le mois est trié correctement avec le numéro du mois.

---

# 9. Visuels obligatoires du tableau de bord

Votre rapport Power BI doit contenir au minimum les éléments suivants.

---

## 9.1 Cartes KPI

Créer des cartes pour afficher :

1. CA net ;
2. Marge ;
3. Taux de marge ;
4. Quantité vendue ;
5. Nombre de ventes ;
6. Nombre de clients ;
7. Taux atteinte objectif.

---

## 9.2 Tableau par région

Créer un tableau contenant :

* Région ;
* CA brut ;
* Montant remise ;
* CA net ;
* Coût total ;
* Marge ;
* Taux de marge ;
* Objectif total ;
* Écart objectif ;
* Taux atteinte objectif.

---

## 9.3 Tableau par produit

Créer un tableau contenant :

* Produit ;
* Catégorie ;
* Quantité vendue ;
* CA net ;
* Marge ;
* Taux de marge ;
* Part du CA total.

---

## 9.4 Graphique des ventes par mois

Créer un graphique permettant de visualiser le CA net par mois.

Le graphique doit utiliser la table calendrier.

---

## 9.5 Graphique par catégorie

Créer un graphique permettant de comparer le CA net par catégorie.

Catégories présentes :

```text
Informatique
Accessoire
```

---

## 9.6 Graphique par canal

Créer un graphique permettant de comparer le CA net selon le canal de vente.

Canaux présents :

```text
Boutique
En ligne
```

---

## 9.7 Graphique par vendeur

Créer un graphique permettant de comparer les performances des vendeurs.

Le graphique doit permettre de visualiser au moins :

* le CA net ;
* la marge ;
* ou le taux atteinte objectif.

---

## 9.8 Segments de filtre obligatoires

Ajouter des segments pour filtrer le tableau de bord par :

* Région ;
* Catégorie ;
* Produit ;
* Canal ;
* Vendeur ;
* Mois.

---

# 10. Mise en forme attendue

Votre tableau de bord doit être clair et professionnel.

Vous devez respecter les consignes suivantes :

* titre clair en haut de la page ;
* cartes KPI bien alignées ;
* graphiques lisibles ;
* noms des mesures compréhensibles ;
* formats monétaires appliqués aux montants ;
* formats en pourcentage pour les taux ;
* filtres visibles et faciles à utiliser ;
* aucune surcharge inutile ;
* couleurs cohérentes ;
* disposition propre.

---

# 11. Questions d’analyse à répondre

Répondez aux questions suivantes dans une page séparée du rapport Power BI ou dans un document Word/PDF.

Vous ne devez pas seulement donner une valeur.
Vous devez expliquer brièvement ce que vous observez.

---

## Question 1

Quelle région génère le plus de chiffre d’affaires net ?

Expliquez votre réponse à partir du tableau par région.

---

## Question 2

Quel produit génère le plus de chiffre d’affaires net ?

Expliquez si ce produit est aussi celui qui génère la meilleure marge.

---

## Question 3

Quelle catégorie est la plus performante ?

Comparez les catégories selon :

* le CA net ;
* la marge ;
* le taux de marge.

---

## Question 4

Quel canal de vente est le plus performant ?

Comparez :

* Boutique ;
* En ligne.

Vous devez expliquer si le meilleur canal est le même selon le CA net et selon la marge.

---

## Question 5

Quel vendeur obtient les meilleurs résultats ?

Analysez au moins deux indicateurs :

* CA net ;
* marge ;
* taux atteinte objectif ;
* nombre de ventes.

---

## Question 6

Les objectifs commerciaux sont-ils atteints globalement ?

Utilisez les mesures :

* Objectif total ;
* CA net ;
* Écart objectif ;
* Taux atteinte objectif.

---

## Question 7

Expliquez pourquoi le taux de marge peut changer lorsqu’on filtre par produit, région ou canal.

---

## Question 8

Expliquez la différence entre :

```text
CA brut
```

et

```text
CA net
```

---

## Question 9

Expliquez pourquoi une remise peut réduire le chiffre d’affaires net, mais ne réduit pas nécessairement le coût total.

---

## Question 10

Expliquez ce qu’est le contexte de filtre dans Power BI.

Donnez un exemple avec une région, un produit ou un canal.

---

## Question 11

Expliquez la différence entre une colonne calculée et une mesure.

Votre réponse doit préciser :

* où le calcul est stocké ;
* quand le calcul est évalué ;
* pourquoi les mesures sont importantes dans un tableau de bord.

---

## Question 12

Expliquez pourquoi il faut utiliser une fonction sécurisée pour les divisions dans les mesures comme :

```text
Taux de marge
Taux atteinte objectif
Part du CA total
```

---

# 12. Travail à remettre

Vous devez remettre :

1. le fichier Power BI au format `.pbix` ;
2. une capture d’écran du tableau de bord final ;
3. un document contenant les réponses aux questions d’analyse ;
4. la liste des mesures créées avec vos formules DAX ;
5. une courte conclusion de 5 à 10 lignes sur les résultats observés.

---

# 13. Barème d’évaluation

| Critère                                         |  Points |
| ----------------------------------------------- | ------: |
| Importation correcte des données                |       5 |
| Vérification et correction des types de données |       5 |
| Création de la table calendrier                 |      10 |
| Relation correcte entre Calendrier et Ventes    |       5 |
| Création correcte des mesures de base           |      20 |
| Création correcte des mesures avancées          |      20 |
| Utilisation correcte du contexte de filtre      |      10 |
| Qualité des visuels                             |      10 |
| Clarté du tableau de bord                       |       5 |
| Réponses d’analyse                              |      10 |
| **Total**                                       | **100** |

---

# 14. Détail du barème des mesures DAX

| Mesure                 | Points |
| ---------------------- | -----: |
| CA brut                |      2 |
| Montant remise         |      2 |
| CA net                 |      2 |
| Coût total             |      2 |
| Marge                  |      2 |
| Taux de marge          |      2 |
| Quantité vendue        |      1 |
| Nombre de ventes       |      1 |
| Nombre de clients      |      1 |
| Nombre de produits     |      1 |
| Prix moyen pondéré     |      2 |
| Remise moyenne         |      2 |
| Objectif total         |      1 |
| Écart objectif         |      2 |
| Taux atteinte objectif |      2 |
| CA Québec              |      2 |
| CA Ontario             |      2 |
| CA en ligne            |      2 |
| CA boutique            |      2 |
| Part du CA total       |      2 |

---

# 15. Consignes importantes

Les noms de colonnes doivent rester identiques à ceux fournis.

Les mesures doivent être créées manuellement.

Les formules DAX doivent être écrites par l’étudiant.

Le rapport doit être interactif.

Les segments doivent modifier les résultats affichés.

Les réponses doivent être rédigées avec des phrases complètes.

Les captures d’écran doivent être lisibles.

Aucun résultat attendu n’est fourni dans l’énoncé : vous devez utiliser vos mesures pour analyser les données.

---

# 16. Critères de qualité attendus

Un bon travail doit montrer que vous comprenez ce que vous faites.

Il ne suffit pas d’avoir beaucoup de graphiques.
Il faut que les graphiques répondent à des questions d’analyse.

Un tableau de bord réussi doit permettre de répondre rapidement aux questions suivantes :

```text
Combien l’entreprise a-t-elle vendu ?
Quelle marge a-t-elle générée ?
Quels produits performent le mieux ?
Quelle région est la plus rentable ?
Quel canal fonctionne le mieux ?
Les objectifs sont-ils atteints ?
Quels filtres permettent d’explorer les résultats ?
```

---

# 17. Conclusion attendue

À la fin du travail, ajoutez une courte conclusion.

Votre conclusion doit répondre à ces questions :

1. Quelle est la performance globale de l’entreprise ?
2. Quels sont les points forts observés ?
3. Quels sont les points faibles observés ?
4. Quelle recommandation donneriez-vous à l’entreprise ?

La conclusion doit contenir entre **5 et 10 lignes**.
