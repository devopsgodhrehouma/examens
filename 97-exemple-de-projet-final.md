# Sujet de projet final

## **InternTask AI Cloud — Application Flutter intelligente pour l’assignation, le suivi et la notification des tâches de stage avec AWS Cognito, Terraform et IA**

---

## 1. Contexte général du projet

Dans une organisation, un collège ou une entreprise, les stagiaires reçoivent souvent des tâches par courriel, par message Teams, par document partagé ou verbalement. Cette méthode devient rapidement difficile à suivre : certaines tâches sont oubliées, les échéances ne sont pas visibles, l’instructeur ne sait pas toujours si le stagiaire avance, et les preuves de réalisation sont dispersées.

Le projet **InternTask AI Cloud** propose de créer une application mobile Flutter permettant à un instructeur de créer, générer avec l’IA, assigner et suivre des tâches destinées aux stagiaires. Les stagiaires reçoivent une notification lorsqu’une tâche leur est assignée, peuvent consulter les détails, changer le statut, ajouter un commentaire et déposer une preuve de travail.

L’application repose sur une architecture cloud moderne avec **AWS Cognito** pour l’authentification, **API Gateway** pour exposer une API sécurisée, **Lambda** pour la logique backend, **DynamoDB** pour les données, **S3** pour les fichiers, **SNS** pour les notifications, **Amazon Bedrock** pour la génération de tâches avec l’IA, et **Terraform** pour déployer l’infrastructure automatiquement.

Amazon Cognito User Pools est adapté ici parce qu’il fournit un répertoire d’utilisateurs pour l’authentification et l’autorisation d’applications web et mobiles. Cognito peut aussi fonctionner comme fournisseur d’identité OIDC pour l’application. ([Documentation AWS][1])

---

# 2. Titre officiel du projet

## **Développement d’une application mobile Flutter intelligente pour la gestion des tâches de stage avec AWS Cognito, Amazon Bedrock, API Gateway, Lambda, DynamoDB, S3, SNS et Terraform**

Nom court du projet :

```text
InternTask AI Cloud
```

---

# 3. Problématique

Les instructeurs et superviseurs ont besoin d’un outil centralisé pour :

```text
- créer des tâches de stage ;
- assigner les tâches aux stagiaires ;
- suivre l’état d’avancement ;
- vérifier les preuves de réalisation ;
- communiquer avec les stagiaires ;
- relancer les stagiaires en retard ;
- générer rapidement des tâches pédagogiques pertinentes avec l’IA ;
- sécuriser l’accès selon les rôles.
```

Sans outil structuré, la gestion devient manuelle, dispersée et difficile à auditer.

Le projet vise donc à répondre à la question suivante :

> Comment concevoir une application mobile sécurisée permettant à un instructeur d’assigner, générer avec l’IA, suivre et valider les tâches de stage, tout en authentifiant les utilisateurs avec AWS Cognito et en déployant l’infrastructure avec Terraform ?

---

# 4. Objectif général

L’objectif général du projet est de développer une application mobile Flutter connectée à un backend serverless AWS permettant de gérer les tâches des stagiaires de façon sécurisée, intelligente et automatisée.

L’application devra permettre :

```text
- l’authentification des utilisateurs avec AWS Cognito ;
- la séparation des rôles : administrateur, instructeur, stagiaire ;
- la création manuelle de tâches ;
- la génération de tâches avec IA ;
- l’assignation des tâches aux stagiaires ;
- l’envoi de notifications ;
- le suivi des statuts ;
- le dépôt de preuves dans S3 ;
- le stockage des données dans DynamoDB ;
- le déploiement complet de l’infrastructure avec Terraform.
```

---

# 5. Objectifs pédagogiques

À la fin du projet, l’étudiant doit être capable de :

```text
- créer une application mobile Flutter connectée à AWS ;
- intégrer une authentification sécurisée avec Amazon Cognito ;
- comprendre le rôle d’un User Pool Cognito ;
- configurer des groupes Cognito pour gérer les rôles ;
- utiliser un token JWT pour appeler une API sécurisée ;
- protéger une API avec API Gateway et Cognito ;
- créer des fonctions Lambda pour la logique backend ;
- stocker les tâches dans DynamoDB ;
- stocker les pièces jointes dans S3 ;
- envoyer des notifications aux stagiaires ;
- appeler un modèle d’IA avec Amazon Bedrock ;
- automatiser l’infrastructure avec Terraform ;
- appliquer les principes de sécurité IAM ;
- documenter une architecture cloud complète.
```

---

# 6. Rôle central de Cognito dans le projet

Dans ce projet, **Cognito n’est pas seulement un écran de connexion**. Il joue un rôle central dans la sécurité de l’application.

Cognito sera utilisé pour :

```text
- gérer les comptes utilisateurs ;
- permettre l’inscription et la connexion ;
- gérer les groupes d’utilisateurs ;
- séparer les rôles ;
- produire des tokens JWT ;
- sécuriser les appels API ;
- permettre au backend de savoir qui appelle l’API ;
- empêcher un stagiaire d’accéder aux tâches d’un autre stagiaire.
```

Les groupes Cognito permettent de représenter différents types d’utilisateurs et peuvent servir à gérer les permissions. AWS indique que les groupes dans un User Pool peuvent être utilisés pour organiser les utilisateurs, représenter des types d’utilisateurs et associer des permissions. ([Documentation AWS][2])

---

# 7. Groupes Cognito à créer

Le projet doit créer trois groupes principaux dans Cognito.

## 7.1 Groupe `admin`

L’administrateur possède le niveau d’accès le plus élevé.

Il peut :

```text
- créer des utilisateurs ;
- désactiver des comptes ;
- voir tous les stagiaires ;
- voir tous les instructeurs ;
- consulter toutes les tâches ;
- modifier ou supprimer une tâche ;
- consulter les statistiques globales ;
- gérer les paramètres de l’application.
```

---

## 7.2 Groupe `instructor`

L’instructeur est la personne qui encadre les stagiaires.

Il peut :

```text
- voir la liste de ses stagiaires ;
- créer une tâche manuellement ;
- générer une tâche avec l’IA ;
- modifier une tâche proposée par l’IA ;
- assigner une tâche à un stagiaire ;
- définir une date limite ;
- ajouter une priorité ;
- suivre l’avancement ;
- commenter le travail du stagiaire ;
- valider ou refuser une tâche terminée ;
- relancer un stagiaire.
```

---

## 7.3 Groupe `intern`

Le stagiaire utilise l’application pour consulter et réaliser ses tâches.

Il peut :

```text
- voir uniquement ses propres tâches ;
- consulter les consignes ;
- changer le statut d’une tâche ;
- ajouter un commentaire ;
- déposer une preuve de travail ;
- recevoir une notification ;
- voir les commentaires de l’instructeur ;
- voir l’historique de ses tâches.
```

---

# 8. Fonctionnement des tokens Cognito

Après connexion, Cognito retourne des tokens à l’application Flutter.

Les tokens importants sont :

```text
- ID token ;
- Access token ;
- Refresh token.
```

L’**access token** contient des informations sur l’utilisateur authentifié, ses groupes et ses scopes. AWS précise que le but de l’access token est d’autoriser des opérations API. ([Documentation AWS][3])

Dans ce projet, Flutter devra envoyer le token dans l’appel API :

```text
Authorization: Bearer <access_token>
```

API Gateway utilisera ensuite un authorizer Cognito pour vérifier que le token est valide. AWS indique qu’une API REST peut utiliser un authorizer de type `COGNITO_USER_POOLS`, et que le client doit d’abord se connecter au User Pool, obtenir un token, puis appeler l’API avec ce token dans le header `Authorization`. ([Documentation AWS][4])

---

# 9. Règles de sécurité attendues

Le projet doit respecter les règles suivantes :

```text
- un utilisateur non connecté ne peut pas appeler l’API ;
- un stagiaire ne peut voir que ses propres tâches ;
- un stagiaire ne peut pas créer une tâche pour quelqu’un d’autre ;
- un instructeur peut créer et assigner des tâches ;
- un instructeur ne peut voir que les stagiaires qui lui sont associés ;
- un administrateur peut tout consulter ;
- une tâche générée par l’IA doit être validée par l’instructeur avant d’être assignée ;
- les fichiers déposés doivent être reliés à une tâche existante ;
- les permissions IAM doivent être minimales.
```

---

# 10. Architecture globale

```text
Application Flutter
        |
        | Authentification
        v
Amazon Cognito User Pool
        |
        | JWT : ID token / Access token
        v
API Gateway sécurisé par Cognito Authorizer
        |
        v
AWS Lambda
        |
        +--> DynamoDB
        |       - utilisateurs
        |       - tâches
        |       - commentaires
        |       - notifications
        |
        +--> Amazon Bedrock
        |       - génération intelligente de tâches
        |
        +--> Amazon S3
        |       - preuves
        |       - rapports
        |       - fichiers joints
        |
        +--> Amazon SNS
        |       - notifications aux stagiaires
        |
        +--> CloudWatch
        |       - logs
        |       - erreurs
        |       - surveillance
        |
        +--> Terraform
                - infrastructure as code
```

---

# 11. Services AWS utilisés

| Service        | Rôle dans le projet                                         |
| -------------- | ----------------------------------------------------------- |
| Amazon Cognito | Authentification, groupes, tokens JWT, sécurité utilisateur |
| API Gateway    | API REST sécurisée                                          |
| Lambda         | Logique backend                                             |
| DynamoDB       | Stockage des tâches, utilisateurs, statuts et commentaires  |
| S3             | Stockage des fichiers, preuves, rapports                    |
| SNS            | Notifications aux stagiaires                                |
| Amazon Bedrock | Génération de tâches avec IA                                |
| CloudWatch     | Logs et surveillance                                        |
| IAM            | Permissions entre services AWS                              |
| Terraform      | Déploiement automatisé de l’infrastructure                  |

Amazon Bedrock est pertinent pour la partie IA, car c’est un service entièrement géré donnant accès à des modèles de fondation pour construire des applications d’IA générative. ([Documentation AWS][5])

---

# 12. Fonctionnalités principales de l’application Flutter

## 12.1 Écran de connexion

L’utilisateur doit pouvoir se connecter avec :

```text
- courriel ;
- mot de passe ;
- compte Cognito.
```

Après connexion, l’application récupère le token Cognito.

---

## 12.2 Écran d’accueil selon le rôle

L’écran affiché dépend du groupe Cognito.

Exemple :

```text
admin       -> tableau de bord administrateur
instructor  -> tableau de bord instructeur
intern      -> tableau de bord stagiaire
```

Les tokens Cognito peuvent contenir l’appartenance aux groupes dans la claim `cognito:groups`, ce qui permet au backend ou à l’application de prendre des décisions d’accès. ([Documentation AWS][6])

---

## 12.3 Tableau de bord instructeur

L’instructeur doit voir :

```text
- nombre de stagiaires ;
- nombre de tâches assignées ;
- tâches en retard ;
- tâches terminées ;
- tâches en attente de validation ;
- bouton “Créer une tâche” ;
- bouton “Générer avec IA”.
```

---

## 12.4 Création manuelle d’une tâche

L’instructeur peut remplir un formulaire :

```text
Titre de la tâche
Description
Stagiaire assigné
Priorité
Date limite
Catégorie
Livrable attendu
Critères de validation
```

Exemple :

```text
Titre : Préparer un rapport sur AWS S3
Description : Expliquer le rôle de S3, créer un bucket de test et ajouter une capture d’écran.
Stagiaire : Aissata Kaba
Priorité : Moyenne
Date limite : 2026-06-20
Livrable : PDF + capture d’écran
```

---

## 12.5 Génération de tâches avec IA

L’instructeur peut demander à l’IA de générer des tâches.

Formulaire IA :

```text
Nom du stagiaire
Domaine du stage
Niveau technique
Semaine du stage
Objectif pédagogique
Compétences ciblées
Durée estimée
Type de livrable attendu
```

Exemple de demande :

```text
Domaine : Cloud Computing
Niveau : Débutant
Semaine : 2
Objectif : pratiquer Terraform, S3 et IAM
Durée : 3 heures
Livrable : fichier Terraform + capture d’écran + court rapport
```

L’IA peut retourner une réponse structurée :

```json
{
  "tasks": [
    {
      "title": "Créer un bucket S3 avec Terraform",
      "description": "Le stagiaire doit créer un bucket S3 en utilisant Terraform.",
      "difficulty": "Débutant",
      "estimatedDuration": "45 minutes",
      "deliverable": "Fichier main.tf et capture d’écran",
      "validationCriteria": [
        "Le bucket est créé avec Terraform",
        "Le nom du bucket est unique",
        "Le code est documenté"
      ]
    },
    {
      "title": "Ajouter une politique IAM minimale",
      "description": "Le stagiaire doit expliquer pourquoi les permissions minimales sont importantes.",
      "difficulty": "Débutant",
      "estimatedDuration": "45 minutes",
      "deliverable": "Court rapport explicatif",
      "validationCriteria": [
        "Le principe du moindre privilège est expliqué",
        "La politique IAM est cohérente",
        "Les permissions inutiles sont évitées"
      ]
    }
  ]
}
```

Amazon Bedrock peut être appelé via l’opération `InvokeModel`, qui permet d’exécuter une inférence avec un prompt et des paramètres fournis dans la requête. ([Documentation AWS][7])

---

# 13. Règle importante sur l’IA

L’IA ne doit pas assigner automatiquement une tâche finale.

Le workflow attendu est :

```text
1. L’instructeur décrit le besoin.
2. L’IA génère des propositions de tâches.
3. L’instructeur relit les propositions.
4. L’instructeur modifie si nécessaire.
5. L’instructeur valide.
6. La tâche est enregistrée dans DynamoDB.
7. Le stagiaire reçoit une notification.
```

Cette règle est importante pour éviter que l’IA produise des tâches imprécises, trop difficiles ou mal adaptées au niveau du stagiaire.

---

# 14. Fonctionnalités côté stagiaire

Le stagiaire doit pouvoir :

```text
- se connecter ;
- voir uniquement ses propres tâches ;
- filtrer les tâches par statut ;
- ouvrir le détail d’une tâche ;
- lire la description ;
- consulter la date limite ;
- changer le statut ;
- ajouter un commentaire ;
- joindre un fichier ;
- indiquer qu’il est bloqué ;
- soumettre la tâche pour validation.
```

Statuts proposés :

```text
À faire
En cours
Bloqué
Soumis
À corriger
Validé
En retard
```

---

# 15. Notifications

Lorsqu’une tâche est assignée, le stagiaire doit recevoir une notification.

Deux versions sont possibles.

## Version simple

Notification par courriel ou notification interne dans l’application.

## Version avancée

Notification push mobile.

Amazon SNS peut envoyer des notifications push à des applications mobiles via des services comme FCM pour Android et APNs pour iOS. ([Documentation AWS][8])

Exemple de notification :

```text
Nouvelle tâche assignée

Titre : Créer un bucket S3 avec Terraform
Date limite : 20 juin 2026
Priorité : Moyenne
```

---

# 16. Modèle de données DynamoDB

## Table `Users`

```text
userId
email
fullName
role
cognitoSub
department
createdAt
updatedAt
```

## Table `Tasks`

```text
taskId
title
description
assignedTo
createdBy
status
priority
category
deadline
source
createdAt
updatedAt
```

Valeurs possibles pour `source` :

```text
manual
ai_generated
```

## Table `TaskComments`

```text
commentId
taskId
authorId
message
createdAt
```

## Table `Attachments`

```text
attachmentId
taskId
fileName
s3Key
uploadedBy
createdAt
```

## Table `Notifications`

```text
notificationId
userId
taskId
title
message
status
createdAt
```

---

# 17. Endpoints API attendus

```text
POST   /auth/profile
GET    /users/me
GET    /users/interns

POST   /ai/generate-tasks

POST   /tasks
GET    /tasks
GET    /tasks/{taskId}
PUT    /tasks/{taskId}
PUT    /tasks/{taskId}/status
DELETE /tasks/{taskId}

POST   /tasks/{taskId}/comments
GET    /tasks/{taskId}/comments

POST   /tasks/{taskId}/attachments
GET    /tasks/{taskId}/attachments

POST   /notifications/send
GET    /notifications
PUT    /notifications/{notificationId}/read
```

---

# 18. Contrôle d’accès par rôle

## Stagiaire

```text
GET /tasks
GET /tasks/{taskId}
PUT /tasks/{taskId}/status
POST /tasks/{taskId}/comments
POST /tasks/{taskId}/attachments
GET /notifications
```

Le stagiaire ne doit voir que les tâches où :

```text
assignedTo = userId connecté
```

---

## Instructeur

```text
GET /users/interns
POST /ai/generate-tasks
POST /tasks
GET /tasks
GET /tasks/{taskId}
PUT /tasks/{taskId}
PUT /tasks/{taskId}/status
POST /tasks/{taskId}/comments
POST /notifications/send
```

L’instructeur peut voir les tâches qu’il a créées ou les tâches de ses stagiaires.

---

## Administrateur

```text
Accès complet à toutes les ressources applicatives.
```

---

# 19. Infrastructure Terraform attendue

L’étudiant doit créer une infrastructure organisée.

Structure recommandée :

```text
terraform/
├── main.tf
├── provider.tf
├── variables.tf
├── outputs.tf
├── cognito.tf
├── api_gateway.tf
├── lambda.tf
├── dynamodb.tf
├── s3.tf
├── sns.tf
├── bedrock.tf
├── iam.tf
└── cloudwatch.tf
```

Terraform doit créer au minimum :

```text
- Cognito User Pool
- Cognito User Pool Client
- Cognito Groups : admin, instructor, intern
- API Gateway
- Cognito Authorizer
- Lambda functions
- DynamoDB tables
- S3 bucket
- SNS topic ou configuration notification
- IAM roles et policies
- CloudWatch log groups
```

Le fournisseur Terraform AWS fournit notamment la ressource `aws_cognito_user_pool`, utilisée pour créer un User Pool Cognito dans l’infrastructure as code. ([Terraform Registry][9])

---

# 20. Sorties Terraform attendues

Le fichier `outputs.tf` doit afficher :

```text
cognito_user_pool_id
cognito_user_pool_client_id
api_gateway_url
tasks_table_name
attachments_bucket_name
sns_topic_arn
```

Ces valeurs seront utilisées par l’application Flutter.

---

# 21. Exemple de configuration Cognito attendue

Le projet doit prévoir :

```text
- User Pool : interntask-user-pool
- App Client : interntask-flutter-client
- Groupes :
  - admin
  - instructor
  - intern
- Attributs utilisateurs :
  - email
  - name
  - custom:role si nécessaire
- Politique de mot de passe :
  - longueur minimale
  - majuscule
  - minuscule
  - chiffre
  - caractère spécial
- Vérification du courriel
- MFA optionnel
```

---

# 22. Scénario complet d’utilisation

## Étape 1 — Connexion

L’instructeur ouvre l’application Flutter et se connecte avec son compte Cognito.

## Étape 2 — Choix du stagiaire

Il consulte la liste des stagiaires associés à son compte.

## Étape 3 — Génération IA

Il clique sur :

```text
Générer avec l’IA
```

Il remplit :

```text
Domaine : AWS / Terraform
Niveau : Débutant
Semaine : 2
Objectif : apprendre S3 et IAM
Durée estimée : 3 heures
```

## Étape 4 — Appel à Bedrock

Flutter appelle l’API :

```text
POST /ai/generate-tasks
```

API Gateway vérifie le token Cognito.

Lambda appelle Amazon Bedrock.

Bedrock retourne des tâches proposées.

## Étape 5 — Validation humaine

L’instructeur relit les tâches générées.

Il peut :

```text
- accepter ;
- modifier ;
- supprimer ;
- ajouter une date limite ;
- changer la priorité.
```

## Étape 6 — Assignation

L’instructeur assigne la tâche au stagiaire.

La tâche est enregistrée dans DynamoDB.

## Étape 7 — Notification

Le stagiaire reçoit une notification.

## Étape 8 — Réalisation

Le stagiaire consulte la tâche, travaille dessus, ajoute un commentaire et dépose une preuve.

## Étape 9 — Validation

L’instructeur consulte le travail et change le statut :

```text
Validé
```

ou :

```text
À corriger
```

---

# 23. Livrables attendus

Les étudiants doivent remettre :

```text
1. Code Flutter de l’application mobile
2. Code Terraform complet
3. Code des fonctions Lambda
4. Schéma d’architecture cloud
5. Modèle de données DynamoDB
6. Documentation d’installation
7. Captures d’écran de l’application
8. Captures d’écran AWS
9. Démonstration de connexion Cognito
10. Démonstration de génération IA
11. Démonstration d’assignation de tâche
12. Démonstration de notification
13. Rapport final
```

---

# 24. Critères d’évaluation proposés

| Critère                              |  Points |
| ------------------------------------ | ------: |
| Architecture AWS claire et cohérente |      15 |
| Configuration Cognito complète       |      20 |
| Sécurité des routes API avec Cognito |      15 |
| Application Flutter fonctionnelle    |      20 |
| Backend Lambda fonctionnel           |      15 |
| DynamoDB bien modélisé               |      10 |
| Intégration IA avec Bedrock          |      15 |
| Notifications                        |      10 |
| Terraform propre et réutilisable     |      20 |
| Documentation et démonstration       |      20 |
| **Total**                            | **160** |

---

# 25. Niveaux de difficulté possibles

## Version minimale

```text
- Connexion Cognito
- Groupes admin, instructor, intern
- Création manuelle de tâches
- Consultation des tâches
- Modification du statut
- Stockage DynamoDB
```

## Version intermédiaire

```text
- Génération IA avec Bedrock
- Validation des tâches générées
- Notifications internes
- Dépôt de fichiers dans S3
- API sécurisée avec Cognito Authorizer
```

## Version avancée

```text
- Notifications push mobile avec SNS
- Tableau de bord statistique
- Historique des modifications
- Gestion des retards
- Recherche et filtres
- Règles avancées selon les groupes Cognito
```

---

# 26. Formulation courte du sujet pour un plan de cours

```text
Ce projet consiste à développer une application mobile Flutter permettant à un instructeur d’assigner et de suivre des tâches de stage. L’application utilisera AWS Cognito pour l’authentification et la gestion des rôles, API Gateway et Lambda pour le backend serverless, DynamoDB pour le stockage des tâches, S3 pour les pièces jointes, SNS pour les notifications et Amazon Bedrock pour générer automatiquement des propositions de tâches avec l’IA. Toute l’infrastructure devra être déployée avec Terraform.
```

---

# 27. Formulation professionnelle finale

## **InternTask AI Cloud**

Le projet **InternTask AI Cloud** vise à concevoir et déployer une application mobile Flutter sécurisée permettant la gestion intelligente des tâches de stage. Les instructeurs peuvent créer des tâches manuellement ou utiliser une IA générative pour produire des tâches adaptées au niveau, au domaine et aux objectifs pédagogiques du stagiaire. Les stagiaires reçoivent les tâches, consultent les consignes, mettent à jour leur progression, déposent des preuves et reçoivent des notifications.

L’architecture repose sur AWS Cognito pour l’authentification et la séparation des rôles, API Gateway pour exposer une API REST sécurisée, AWS Lambda pour la logique métier, DynamoDB pour le stockage des données, S3 pour les fichiers, SNS pour les notifications, Amazon Bedrock pour la génération intelligente de tâches, et Terraform pour l’automatisation complète de l’infrastructure cloud.

Ce projet permet aux étudiants de comprendre une architecture cloud moderne combinant mobile, sécurité, backend serverless, infrastructure as code et intelligence artificielle générative.

[1]: https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools.html?utm_source=chatgpt.com "Amazon Cognito user pools"
[2]: https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-user-groups.html?utm_source=chatgpt.com "Adding groups to a user pool - Amazon Cognito"
[3]: https://docs.aws.amazon.com/cognito/latest/developerguide/amazon-cognito-user-pools-using-the-access-token.html?utm_source=chatgpt.com "Understanding the access token - Amazon Cognito"
[4]: https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-integrate-with-cognito.html?utm_source=chatgpt.com "Control access to REST APIs using Amazon Cognito user ..."
[5]: https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html?utm_source=chatgpt.com "Overview - Amazon Bedrock"
[6]: https://docs.aws.amazon.com/cognito/latest/developerguide/amazon-cognito-user-pools-using-tokens-with-identity-providers.html?utm_source=chatgpt.com "Understanding user pool JSON web tokens (JWTs)"
[7]: https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModel.html?utm_source=chatgpt.com "InvokeModel - Amazon Bedrock"
[8]: https://docs.aws.amazon.com/sns/latest/dg/sns-mobile-application-as-subscriber.html?utm_source=chatgpt.com "Sending mobile push notifications with Amazon SNS"
[9]: https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cognito_user_pool?utm_source=chatgpt.com "aws_cognito_user_pool | Resources | hashicorp/aws | Terraform"
