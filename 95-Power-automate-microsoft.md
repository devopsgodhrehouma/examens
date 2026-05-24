# Sujet proposé

## **AgentFlow 365 — Application intelligente d’orchestration d’agents pour traiter les courriels, créer des tâches Planner et automatiser le suivi avec Power Automate**

L’idée : créer une application qui surveille une boîte Outlook, analyse les courriels entrants avec l’IA, décide automatiquement quoi faire, prépare une réponse, crée une tâche dans Microsoft Planner, notifie la bonne personne dans Teams, puis garde une trace dans SharePoint ou Dataverse.

Power Automate sert ici de moteur d’automatisation : Microsoft le présente comme un outil pour créer des flux cloud qui exécutent automatiquement des tâches après un déclencheur, par exemple lorsqu’un événement se produit. ([Microsoft Learn][1])
Copilot Studio peut jouer le rôle d’orchestrateur d’agents, car la documentation Microsoft indique que l’orchestration générative permet à un agent de choisir entre des outils, sujets, agents ou sources de connaissances, puis de les appeler en séquence si nécessaire. ([Microsoft Learn][2])

---

# Description générale du projet

L’application reçoit des courriels comme :

```text
Bonjour,

Je voudrais savoir si mon dossier de stage est complet.
Il manque peut-être une signature de mon superviseur.
Pouvez-vous me confirmer quoi faire ?

Merci.
```

Le système doit automatiquement :

```text
1. Lire le courriel entrant.
2. Identifier l’intention : demande de suivi de stage.
3. Classer le niveau d’urgence.
4. Chercher les informations nécessaires dans SharePoint ou Dataverse.
5. Générer une réponse proposée.
6. Créer une tâche Planner si une action humaine est nécessaire.
7. Assigner la tâche à la bonne personne.
8. Notifier l’équipe dans Teams.
9. Attendre validation humaine avant d’envoyer la réponse.
10. Archiver le traitement dans une liste SharePoint ou Dataverse.
```

---

# Architecture proposée

```text
Outlook / Boîte courriel partagée
        |
        | Déclencheur : nouveau courriel reçu
        v
Power Automate Cloud Flow
        |
        v
Agent orchestrateur Copilot Studio
        |
        +--> Agent Courriel
        |       - résume le message
        |       - détecte l’intention
        |       - classe l’urgence
        |
        +--> Agent Connaissance
        |       - cherche dans SharePoint / OneDrive / Dataverse
        |       - retrouve les règles internes
        |
        +--> Agent Réponse
        |       - génère une réponse professionnelle
        |       - propose le ton
        |       - prépare un brouillon Outlook
        |
        +--> Agent Planner
        |       - crée une tâche
        |       - assigne une personne
        |       - ajoute date limite et checklist
        |
        +--> Agent Teams
        |       - notifie le responsable
        |       - envoie un résumé dans un canal
        |
        +--> Agent Audit
                - conserve la trace
                - enregistre le statut
                - prépare un rapport
```

---

# Services Microsoft utilisés

| Outil                                      | Rôle                                                                   |
| ------------------------------------------ | ---------------------------------------------------------------------- |
| **Power Automate**                         | Automatiser les flux entre Outlook, Planner, Teams, SharePoint et l’IA |
| **Outlook / Office 365 Outlook connector** | Lire les courriels entrants et créer des brouillons                    |
| **Copilot Studio**                         | Créer l’orchestrateur d’agents                                         |
| **AI Builder / GPT prompt**                | Résumer, classifier, extraire les actions et générer une réponse       |
| **Planner**                                | Créer et assigner les tâches                                           |
| **Teams**                                  | Notifier les responsables                                              |
| **SharePoint List**                        | Journaliser les courriels et les décisions                             |
| **Dataverse**                              | Option plus professionnelle pour stocker les dossiers structurés       |
| **Power Apps**                             | Interface de validation humaine                                        |
| **Microsoft 365 / Entra ID**               | Authentification et permissions                                        |

Microsoft documente les connecteurs Power Automate, dont ceux utilisés avec Microsoft 365, et le connecteur Planner est bien prévu pour gérer des tâches, documents et conversations d’équipe. ([Microsoft Learn][3])
AI Builder peut être utilisé dans Power Automate pour créer du texte avec GPT à partir d’un prompt, et Microsoft indique que l’action “Create text with GPT using a prompt” est appelée “Run a prompt” depuis mai 2025. ([Microsoft Learn][4])

---

# Nom professionnel du projet

Tu peux l’appeler :

```text
AgentFlow 365
```

ou :

```text
AI MailOps Orchestrator
```

ou en français :

```text
Orchestrateur intelligent de courriels, tâches et suivis Microsoft 365
```

Titre long pour un projet final :

```text
Conception d’une application intelligente avec Power Automate, Copilot Studio et Microsoft 365 pour automatiser le traitement des courriels, la génération de réponses, la création de tâches Planner et le suivi collaboratif
```

---

# Rôles dans l’application

## 1. Agent orchestrateur principal

C’est le cerveau du système.

Il reçoit la demande et décide :

```text
- Est-ce un courriel simple ?
- Est-ce une demande urgente ?
- Est-ce une plainte ?
- Est-ce une demande administrative ?
- Faut-il créer une tâche Planner ?
- Faut-il répondre automatiquement ?
- Faut-il demander une validation humaine ?
- Faut-il escalader à un responsable ?
```

La documentation Microsoft précise que l’orchestration générative peut sélectionner des outils, agents ou sources de connaissances, remplir des entrées avec le contexte conversationnel et gérer des demandes multi-intentions. ([Microsoft Learn][5])

---

## 2. Agent Courriel

Il analyse le courriel entrant.

Il extrait :

```text
- expéditeur ;
- sujet ;
- résumé ;
- intention ;
- sentiment ;
- urgence ;
- informations manquantes ;
- action attendue ;
- personne responsable.
```

Exemple de sortie :

```json
{
  "type": "demande_stage",
  "urgence": "moyenne",
  "resume": "L’étudiant demande si son dossier de stage est complet.",
  "action_requise": true,
  "responsable": "coordonnateur_stage",
  "besoin_reponse": true
}
```

---

## 3. Agent Connaissance

Il consulte les sources internes.

Sources possibles :

```text
- documents SharePoint ;
- procédure de stage ;
- FAQ interne ;
- liste des superviseurs ;
- liste des étudiants ;
- règles de réponse ;
- historique du dossier.
```

Dans Copilot Studio, les sources de connaissances permettent à un agent d’utiliser des données d’entreprise, sites web ou systèmes externes pour produire des réponses plus pertinentes. ([Microsoft Learn][6])

---

## 4. Agent Réponse

Il prépare une réponse professionnelle.

Il ne doit pas envoyer directement le message dans la version pédagogique. Il doit créer un brouillon ou une proposition à valider.

Règles :

```text
- ne jamais envoyer une réponse sensible sans validation ;
- rester poli et professionnel ;
- ne pas inventer d’information ;
- indiquer clairement les documents manquants ;
- proposer une prochaine action ;
- utiliser le bon niveau de ton.
```

---

## 5. Agent Planner

Il crée automatiquement une tâche dans Planner si une action humaine est nécessaire.

Exemple :

```text
Titre : Vérifier le dossier de stage de l’étudiant
Description : Le courriel indique que le dossier pourrait être incomplet. Vérifier la signature du superviseur et répondre à l’étudiant.
Assigné à : Responsable des stages
Échéance : dans 48 heures
Priorité : Moyenne
Checklist :
- Vérifier le dossier
- Vérifier la signature
- Confirmer les documents manquants
- Valider la réponse proposée
```

---

## 6. Agent Teams

Il notifie l’équipe.

Exemple de notification :

```text
Nouveau courriel traité par l’agent IA.

Catégorie : dossier de stage
Urgence : moyenne
Action : tâche Planner créée
Responsable : coordonnateur de stage
Validation requise : oui
```

---

## 7. Agent Audit

Il conserve une trace.

Il enregistre :

```text
- courriel reçu ;
- résumé IA ;
- décision prise ;
- tâche créée ;
- responsable assigné ;
- statut ;
- date de traitement ;
- réponse proposée ;
- validation humaine ;
- date d’envoi final.
```

---

# Workflow complet

```text
1. Un courriel arrive dans une boîte Outlook partagée.
2. Power Automate déclenche le flux.
3. Le contenu du courriel est envoyé à l’agent orchestrateur.
4. L’orchestrateur appelle l’Agent Courriel.
5. L’Agent Courriel résume et classe le message.
6. L’orchestrateur appelle l’Agent Connaissance si une règle interne est nécessaire.
7. L’Agent Réponse génère une proposition de réponse.
8. L’Agent Planner crée une tâche si une action humaine est requise.
9. L’Agent Teams notifie le responsable.
10. L’Agent Audit enregistre la trace dans SharePoint ou Dataverse.
11. Un humain valide la réponse dans Power Apps.
12. Power Automate envoie le courriel final.
13. La tâche Planner est mise à jour automatiquement.
```

---

# Fonctionnalités de l’application

## Version minimale

```text
- Lire un courriel Outlook entrant
- Résumer le courriel avec IA
- Classer le courriel par catégorie
- Créer une tâche Planner
- Envoyer une notification Teams
- Enregistrer le suivi dans SharePoint
```

## Version intermédiaire

```text
- Générer une réponse proposée
- Créer un brouillon Outlook
- Ajouter une interface Power Apps pour validation
- Mettre à jour le statut dans SharePoint
- Assigner automatiquement la tâche selon la catégorie
```

## Version avancée

```text
- Orchestration multi-agents avec Copilot Studio
- Recherche dans une base de connaissances SharePoint
- Priorisation automatique des courriels
- Détection des courriels urgents
- Relance automatique si la tâche Planner n’est pas terminée
- Rapport hebdomadaire automatique
- Tableau de bord Power BI
```

---

# Exemple de catégories de courriels

```text
- Demande de stage
- Absence ou retard
- Problème technique
- Demande administrative
- Demande de document
- Plainte
- Question pédagogique
- Demande urgente
- Courriel non prioritaire
```

---

# Exemple de règles métier

```text
Si le courriel contient une plainte :
    créer une tâche Planner priorité haute
    notifier le responsable dans Teams
    demander validation humaine obligatoire

Si le courriel concerne un document manquant :
    créer une tâche Planner
    générer une réponse avec la liste des documents requis

Si le courriel est une simple question fréquente :
    proposer une réponse basée sur la FAQ
    créer un brouillon Outlook

Si le courriel contient une urgence :
    notifier immédiatement dans Teams
    assigner au responsable
    fixer une échéance courte

Si le courriel n’est pas clair :
    générer une réponse demandant des précisions
```

---

# Structure des flux Power Automate

## Flux 1 — Traitement d’un nouveau courriel

```text
Déclencheur :
- When a new email arrives

Étapes :
- Lire le courriel
- Envoyer le texte à l’IA
- Classer le courriel
- Créer un enregistrement SharePoint
- Créer une tâche Planner si nécessaire
- Générer une réponse proposée
- Notifier Teams
```

---

## Flux 2 — Validation humaine

```text
Déclencheur :
- Quand un responsable approuve la réponse dans Power Apps

Étapes :
- Récupérer la réponse validée
- Envoyer le courriel Outlook
- Mettre à jour la tâche Planner
- Mettre à jour SharePoint
```

---

## Flux 3 — Relance automatique

```text
Déclencheur :
- Tous les jours à 8 h

Étapes :
- Vérifier les tâches Planner non terminées
- Identifier les tâches en retard
- Envoyer une relance Teams
- Mettre à jour le statut
```

---

## Flux 4 — Rapport hebdomadaire

```text
Déclencheur :
- Chaque vendredi

Étapes :
- Compter les courriels traités
- Compter les tâches créées
- Identifier les retards
- Résumer les demandes fréquentes
- Envoyer un rapport Teams ou Outlook
```

---

# Modèle de données SharePoint ou Dataverse

## Table `EmailRequests`

```text
RequestId
EmailFrom
EmailSubject
EmailBody
ReceivedDate
Category
Urgency
Summary
DetectedIntent
RequiresHumanAction
PlannerTaskId
Status
AssignedTo
DraftReply
FinalReply
ValidationStatus
CreatedAt
UpdatedAt
```

## Table `AgentDecisions`

```text
DecisionId
RequestId
AgentName
Input
Output
Decision
Confidence
CreatedAt
```

## Table `ResponseApprovals`

```text
ApprovalId
RequestId
Reviewer
DraftReply
ApprovedReply
ApprovalStatus
ApprovalDate
Comments
```

---

# Interface Power Apps proposée

L’application Power Apps sert à superviser le système.

Écrans proposés :

```text
1. Tableau de bord
2. Courriels entrants traités
3. Détail d’un courriel
4. Réponse proposée par l’IA
5. Bouton Valider / Modifier / Refuser
6. Tâches Planner liées
7. Historique des décisions des agents
8. Statistiques
```

---

# Sécurité et gouvernance

Le projet doit appliquer des règles strictes :

```text
- l’IA ne doit pas envoyer seule des courriels sensibles ;
- les réponses doivent être validées par un humain ;
- les courriels confidentiels doivent être identifiés ;
- chaque décision doit être journalisée ;
- les tâches Planner doivent avoir un responsable ;
- les permissions Microsoft 365 doivent respecter le principe du moindre privilège ;
- les sources de connaissance doivent être contrôlées ;
- les réponses doivent être basées sur des informations disponibles, pas inventées.
```

---

# Livrables attendus

```text
1. Schéma d’architecture global
2. Description des agents
3. Flux Power Automate documentés
4. Application Power Apps de validation
5. Liste SharePoint ou tables Dataverse
6. Plan Planner utilisé
7. Démonstration du traitement d’un courriel
8. Démonstration de création automatique de tâche
9. Démonstration de notification Teams
10. Démonstration de validation humaine
11. Rapport final avec captures d’écran
```

---

# Critères d’évaluation possibles

| Critère                                    |  Points |
| ------------------------------------------ | ------: |
| Architecture Power Platform claire         |      15 |
| Utilisation pertinente de Power Automate   |      20 |
| Orchestration d’agents avec Copilot Studio |      20 |
| Analyse IA des courriels                   |      15 |
| Création automatique de tâches Planner     |      15 |
| Génération de réponses professionnelles    |      15 |
| Validation humaine avant envoi             |      10 |
| Notifications Teams                        |      10 |
| Journalisation SharePoint/Dataverse        |      15 |
| Sécurité et gouvernance                    |      15 |
| Documentation et démonstration             |      20 |
| **Total**                                  | **170** |

---

# Formulation finale du sujet

## **AgentFlow 365 — Orchestrateur intelligent de courriels et de tâches avec Power Automate, Copilot Studio, Outlook, Planner et Teams**

Ce projet consiste à concevoir une application intelligente basée sur Microsoft Power Platform permettant de traiter automatiquement des courriels entrants. Lorsqu’un courriel arrive dans une boîte Outlook, Power Automate déclenche un flux qui envoie le contenu à un orchestrateur d’agents construit avec Copilot Studio. L’orchestrateur analyse le courriel, identifie l’intention, résume la demande, consulte les sources de connaissance internes, génère une réponse proposée, crée une tâche dans Microsoft Planner, notifie l’équipe dans Teams et enregistre toutes les décisions dans SharePoint ou Dataverse.

L’objectif n’est pas seulement d’automatiser une réponse, mais de construire une vraie chaîne intelligente de traitement administratif avec validation humaine, traçabilité, priorisation et gouvernance. C’est un excellent sujet parce qu’il combine **Power Automate**, **Copilot Studio**, **IA générative**, **Outlook**, **Planner**, **Teams**, **SharePoint**, **Power Apps** et **automatisation métier réelle**.

[1]: https://learn.microsoft.com/en-us/power-automate/get-started-logic-flow?utm_source=chatgpt.com "Create a cloud flow in Power Automate"
[2]: https://learn.microsoft.com/en-us/microsoft-copilot-studio/advanced-generative-actions?utm_source=chatgpt.com "Orchestrate agent behavior with generative AI"
[3]: https://learn.microsoft.com/en-us/connectors/connector-reference/connector-reference-powerautomate-connectors?utm_source=chatgpt.com "List of all Power Automate connectors"
[4]: https://learn.microsoft.com/en-us/ai-builder/use-in-flow-overview?utm_source=chatgpt.com "AI Builder in Power Automate overview"
[5]: https://learn.microsoft.com/en-us/microsoft-copilot-studio/faqs-generative-orchestration?utm_source=chatgpt.com "FAQ for generative orchestration - Microsoft Copilot Studio"
[6]: https://learn.microsoft.com/en-us/microsoft-copilot-studio/knowledge-copilot-studio?utm_source=chatgpt.com "Knowledge sources summary - Microsoft Copilot Studio"
