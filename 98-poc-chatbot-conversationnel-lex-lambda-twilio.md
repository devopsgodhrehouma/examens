# Travail pratique — POC Chatbot conversationnel avec Amazon Lex, AWS Lambda, CSV, Amazon Connect ou Twilio

## 1. Contexte du travail

Dans ce travail, vous devez réaliser un **POC**, c’est-à-dire une preuve de concept, d’un chatbot conversationnel capable de répondre à des questions simples à partir d’un fichier CSV.

Le chatbot sera construit avec **Amazon Lex V2**. Amazon Lex permet de créer des assistants conversationnels capables de comprendre des phrases écrites ou parlées. Le chatbot devra ensuite utiliser une fonction **AWS Lambda** pour chercher une réponse dans un fichier CSV généré avec l’aide de ChatGPT.

Votre POC doit démontrer qu’un utilisateur peut interagir avec le chatbot à travers un vrai canal de communication. Vous devez donc tester votre chatbot dans Amazon Lex, puis le connecter à au moins un des deux canaux suivants :

```text
Option A : Amazon Connect pour une interaction vocale.
Option B : Twilio pour une interaction par SMS ou messagerie.
```

Le but du travail est de comprendre l’architecture complète d’un chatbot moderne :

```text
canal utilisateur → Amazon Lex → AWS Lambda → fichier CSV → réponse utilisateur
```

---

## 2. Objectif général

Vous devez créer un chatbot capable de répondre à des questions simples en utilisant les données d’un fichier CSV.

Votre chatbot doit être capable de :

```text
1. Recevoir une question d’un utilisateur.
2. Comprendre l’intention de la question avec Amazon Lex.
3. Extraire un mot-clé ou une information importante.
4. Appeler une fonction AWS Lambda.
5. Chercher une réponse dans un fichier CSV.
6. Retourner une réponse claire à l’utilisateur.
7. Fonctionner dans Amazon Lex et dans au moins un canal externe : Amazon Connect ou Twilio.
```

---

## 3. Architecture générale du POC

L’architecture complète du projet est la suivante :

```text
                              UTILISATEUR
                                  │
              ┌───────────────────┼───────────────────┐
              │                                       │
              ▼                                       ▼
   ┌──────────────────────┐              ┌──────────────────────┐
   │  Amazon Connect      │              │  Twilio              │
   │  Canal vocal         │              │  SMS / Messagerie    │
   │  Appel téléphonique  │              │  Message texte       │
   └──────────┬───────────┘              └──────────┬───────────┘
              │                                       │
              └───────────────────┬───────────────────┘
                                  ▼
                         ┌─────────────────┐
                         │  Amazon Lex V2  │
                         │  Chatbot        │
                         │  Intents        │
                         │  Slots          │
                         └────────┬────────┘
                                  ▼
                         ┌─────────────────┐
                         │  AWS Lambda     │
                         │  Logique métier │
                         │  Recherche CSV  │
                         └────────┬────────┘
                                  ▼
                         ┌─────────────────┐
                         │  Fichier CSV    │
                         │  FAQ / prix     │
                         │  services       │
                         │  horaires       │
                         └────────┬────────┘
                                  ▼
                         ┌─────────────────┐
                         │  Réponse        │
                         │  générée        │
                         └────────┬────────┘
                                  ▼
              ┌───────────────────┼───────────────────┐
              │                                       │
              ▼                                       ▼
   ┌──────────────────────┐              ┌──────────────────────┐
   │ Réponse vocale       │              │ Réponse SMS          │
   │ via Amazon Connect   │              │ via Twilio           │
   └──────────────────────┘              └──────────────────────┘
```

Vous devez aussi tester le chatbot directement dans Amazon Lex avant de le connecter à Amazon Connect ou Twilio.

Le test direct dans Amazon Lex permet de vérifier que votre bot fonctionne correctement avant l’intégration externe.

---

## 4. Architecture minimale obligatoire

Votre projet doit respecter l’architecture suivante :

```text
Utilisateur
   ↓
Amazon Connect ou Twilio
   ↓
Amazon Lex V2
   ↓
AWS Lambda
   ↓
Fichier CSV
   ↓
Réponse retournée à l’utilisateur
```

Vous devez choisir au minimum **une intégration externe** :

```text
Amazon Connect pour le vocal
ou
Twilio pour SMS / messagerie
```

Vous pouvez faire les deux si vous voulez obtenir une meilleure démonstration.

---

## 5. Exemple de fonctionnement attendu

### Exemple avec Amazon Connect

```text
Utilisateur au téléphone :
Bonjour, je veux connaître le prix du cours AWS.

Amazon Connect transmet la demande à Amazon Lex.

Amazon Lex comprend l’intention : ConsulterPrixIntent.

AWS Lambda cherche le mot-clé "aws" dans le fichier CSV.

Le fichier CSV contient :
aws → Le cours AWS coûte 400 $.

Le chatbot répond vocalement :
Le cours AWS coûte 400 $.
```

---

### Exemple avec Twilio

```text
Utilisateur par SMS :
prix aws

Twilio transmet le message à Amazon Lex.

Amazon Lex comprend la demande.

AWS Lambda cherche la réponse dans le fichier CSV.

Le chatbot retourne par SMS :
Le cours AWS coûte 400 $.
```

---

## 6. Création ou utilisation du compte AWS

Vous devez créer ou utiliser un compte AWS pour réaliser ce travail.

AWS demande généralement une méthode de paiement valide lors de la création du compte. Vous pouvez utiliser une carte acceptée par AWS. Si vous utilisez une carte prépayée, comme Koho, vous devez vérifier vous-même qu’elle est acceptée par AWS.

Vous devez travailler avec prudence. Ce travail ne demande pas de dépenses importantes. Vous devez éviter de créer des ressources inutiles ou de laisser des services actifs après le travail.

Avant de commencer, vous devez configurer une alerte de coût ou un budget AWS.

Budget recommandé :

```text
Budget maximum : 5 $
Alerte à : 1 $
Alerte à : 3 $
Alerte à : 5 $
```

Vous devez remettre une capture d’écran montrant que votre budget ou votre alerte de coût a été configuré.

---

## 7. Règles de sécurité AWS

Vous devez respecter les règles suivantes :

```text
1. Ne partagez jamais votre mot de passe AWS.
2. Ne partagez jamais vos clés d’accès AWS.
3. Ne placez jamais vos clés AWS dans GitHub.
4. Ne créez pas de ressources inutiles.
5. Ne laissez pas Amazon Connect, Lambda, Lex ou d’autres services actifs inutilement.
6. Supprimez les ressources non nécessaires à la fin du travail.
7. Vérifiez régulièrement la section Billing / Facturation.
8. Travaillez uniquement avec des données fictives.
```

Aucune donnée personnelle réelle ne doit être utilisée dans ce projet.

---

## 8. Choix du scénario

Vous devez choisir un scénario simple et réaliste.

Vous pouvez choisir l’un des scénarios suivants :

```text
1. Chatbot pour un centre de formation.
2. Chatbot pour une école.
3. Chatbot pour un service de support informatique.
4. Chatbot pour une boutique en ligne fictive.
5. Chatbot pour une clinique fictive.
6. Chatbot pour une compagnie de livraison fictive.
7. Chatbot pour une banque fictive.
8. Chatbot pour une agence de voyage fictive.
9. Chatbot pour un service RH fictif.
10. Chatbot pour un service de réservation fictif.
```

Votre scénario doit rester simple. Vous ne devez pas créer un système trop complexe.

Exemples de bons scénarios :

```text
Un chatbot qui donne les prix de cours.
Un chatbot qui donne les horaires d’ouverture.
Un chatbot qui répond à une FAQ.
Un chatbot qui indique le statut fictif d’une commande.
Un chatbot qui donne les informations d’un service.
```

Exemples de scénarios à éviter :

```text
Un chatbot qui effectue de vrais paiements.
Un chatbot qui utilise de vraies données clients.
Un chatbot qui traite de vraies données médicales.
Un chatbot qui demande des informations confidentielles.
```

---

## 9. Génération du fichier CSV avec ChatGPT

Vous devez utiliser ChatGPT pour générer un fichier CSV fictif.

Votre fichier CSV servira de petite base de connaissances pour votre chatbot.

Le fichier CSV doit contenir au minimum **20 lignes**.

Les données doivent être :

```text
fictives ;
réalistes ;
claires ;
faciles à rechercher ;
cohérentes avec votre scénario.
```

Votre fichier CSV doit contenir au minimum les colonnes suivantes :

```csv
id,categorie,question,mot_cle,reponse
```

Explication des colonnes :

| Colonne   | Description                                                                      |
| --------- | -------------------------------------------------------------------------------- |
| id        | Identifiant unique de la ligne                                                   |
| categorie | Type d’information : prix, horaire, durée, support, inscription, livraison, etc. |
| question  | Exemple de question possible                                                     |
| mot_cle   | Mot-clé utilisé par Lambda pour chercher la bonne réponse                        |
| reponse   | Réponse retournée par le chatbot                                                 |

---

## 10. Prompt suggéré pour générer le CSV

Vous pouvez utiliser le prompt suivant dans ChatGPT :

```text
Génère-moi un fichier CSV fictif pour un chatbot de service client.

Le fichier doit contenir 20 lignes.

Colonnes :
id, categorie, question, mot_cle, reponse

Le scénario est : un centre de formation qui offre des cours en Python, AWS, Machine Learning, cybersécurité et développement web.

Les réponses doivent être courtes, claires, réalistes et faciles à utiliser dans un chatbot.

Les données doivent être entièrement fictives.

Donne-moi uniquement le contenu CSV, sans explication.
```

---

## 11. Exemple de fichier CSV attendu

Votre fichier CSV pourrait ressembler à ceci :

```csv
id,categorie,question,mot_cle,reponse
1,horaire,Quels sont vos horaires?,horaires,Nous sommes ouverts du lundi au vendredi de 9h à 17h.
2,prix,Combien coûte le cours Python?,python,Le cours Python coûte 250 $.
3,prix,Combien coûte le cours AWS?,aws,Le cours AWS coûte 400 $.
4,duree,Quelle est la durée du cours Python?,python,Le cours Python dure 30 heures.
5,duree,Quelle est la durée du cours AWS?,aws,Le cours AWS dure 45 heures.
6,support,Comment contacter le support?,support,Vous pouvez contacter le support par courriel à support@exemple.com.
7,inscription,Comment s’inscrire à un cours?,inscription,L’inscription se fait en ligne à partir du formulaire d’inscription.
8,recommandation,Quel cours recommandez-vous pour débuter?,debutant,Nous recommandons le cours Python débutant.
```

Vous devez enregistrer votre fichier sous le nom suivant :

```text
faq_chatbot.csv
```

---

## 12. Création du chatbot Amazon Lex V2

Vous devez créer un chatbot avec Amazon Lex V2.

Nom recommandé :

```text
BotPOCServiceClient
```

Vous pouvez choisir un autre nom, mais il doit être clair et professionnel.

Exemples acceptables :

```text
BotFormationPOC
BotSupportClient
BotFAQService
BotReservationPOC
```

Exemples à éviter :

```text
test
bot1
abc
chatbotfinal
chatbotfinalfinal
```

---

## 13. Configuration minimale du bot Lex

Votre bot doit contenir au minimum :

```text
1 bot Amazon Lex V2
1 langue
3 intentions minimum
5 phrases d’entraînement minimum par intention
1 slot minimum
1 fonction Lambda connectée
1 test direct dans Amazon Lex
1 intégration externe avec Amazon Connect ou Twilio
```

---

## 14. Intentions obligatoires

Vous devez créer au minimum trois intentions.

Exemple :

```text
ConsulterPrixIntent
ConsulterInformationIntent
ContacterSupportIntent
```

Vous pouvez ajouter d’autres intentions selon votre scénario.

Exemples supplémentaires :

```text
ConsulterHoraireIntent
ConsulterDureeIntent
ConsulterProduitIntent
ConsulterCommandeIntent
ConsulterServiceIntent
RecommanderCoursIntent
```

---

## 15. Exemples de phrases d’entraînement

Pour chaque intention, vous devez fournir au minimum **5 phrases d’entraînement**.

### ConsulterPrixIntent

```text
Combien coûte le cours AWS ?
Quel est le prix du cours Python ?
Je veux connaître le tarif de la formation Machine Learning.
Combien dois-je payer pour le cours cybersécurité ?
Quel est le coût du cours développement web ?
```

### ConsulterHoraireIntent

```text
Quels sont vos horaires ?
À quelle heure êtes-vous ouverts ?
Quand puis-je vous contacter ?
Quels sont les jours d’ouverture ?
Êtes-vous ouverts le samedi ?
```

### ContacterSupportIntent

```text
Comment contacter le support ?
J’ai besoin d’aide.
Comment parler au service client ?
Où puis-je demander de l’aide ?
Quel est le courriel du support ?
```

---

## 16. Slots

Vous devez créer au moins un slot pour récupérer une information importante dans la phrase de l’utilisateur.

Exemple :

```text
Nom du slot : motCle
Type : AMAZON.AlphaNumeric ou type personnalisé
Question posée par le bot : Quel cours ou service voulez-vous consulter ?
```

Exemple de conversation :

```text
Utilisateur : Combien coûte le cours ?
Bot : Quel cours voulez-vous consulter ?
Utilisateur : AWS
Bot : Le cours AWS coûte 400 $.
```

---

## 17. Création de la fonction AWS Lambda

Vous devez créer une fonction AWS Lambda en Python.

Lambda doit recevoir la demande envoyée par Amazon Lex, chercher l’information dans le fichier CSV, puis retourner une réponse.

La fonction Lambda doit faire les étapes suivantes :

```text
1. Recevoir l’événement envoyé par Amazon Lex.
2. Récupérer le texte saisi ou prononcé par l’utilisateur.
3. Récupérer l’intention détectée.
4. Chercher un mot-clé dans le fichier CSV.
5. Retourner la réponse correspondante.
6. Retourner une réponse par défaut si aucune information n’est trouvée.
```

---

## 18. Version simple acceptée pour le CSV

Pour simplifier le POC, vous pouvez intégrer le contenu du CSV directement dans le code Lambda.

Architecture de la version simple :

```text
Amazon Lex
   ↓
AWS Lambda
   ↓
CSV intégré dans le code Lambda
   ↓
Réponse
```

Cette version est acceptée pour le travail.

---

## 19. Version avancée acceptée

Vous pouvez aussi placer votre fichier CSV dans Amazon S3.

Architecture de la version avancée :

```text
Amazon Lex
   ↓
AWS Lambda
   ↓
Amazon S3
   ↓
faq_chatbot.csv
   ↓
Réponse
```

Cette version est plus professionnelle, mais elle demande plus de configuration.

---

## 20. Exemple de code Lambda en Python

Vous pouvez utiliser ce code comme point de départ et l’adapter à votre propre CSV.

```python
import csv
import io
import unicodedata

CSV_DATA = """id,categorie,question,mot_cle,reponse
1,horaire,Quels sont vos horaires?,horaires,Nous sommes ouverts du lundi au vendredi de 9h à 17h.
2,prix,Combien coûte le cours Python?,python,Le cours Python coûte 250 $.
3,prix,Combien coûte le cours AWS?,aws,Le cours AWS coûte 400 $.
4,duree,Quelle est la durée du cours Python?,python,Le cours Python dure 30 heures.
5,duree,Quelle est la durée du cours AWS?,aws,Le cours AWS dure 45 heures.
6,support,Comment contacter le support?,support,Vous pouvez contacter le support par courriel à support@exemple.com.
7,inscription,Comment s’inscrire à un cours?,inscription,L’inscription se fait en ligne à partir du formulaire d’inscription.
8,recommandation,Quel cours recommandez-vous pour débuter?,debutant,Nous recommandons le cours Python débutant.
"""

def normalize(text):
    if not text:
        return ""

    text = text.lower()
    text = unicodedata.normalize("NFD", text)
    text = "".join(c for c in text if unicodedata.category(c) != "Mn")
    return text


def load_csv_data():
    rows = []
    file_like_object = io.StringIO(CSV_DATA)
    reader = csv.DictReader(file_like_object)

    for row in reader:
        rows.append(row)

    return rows


def find_answer(user_text):
    user_text_normalized = normalize(user_text)
    rows = load_csv_data()

    for row in rows:
        keyword = normalize(row.get("mot_cle", ""))
        question = normalize(row.get("question", ""))

        if keyword and keyword in user_text_normalized:
            return row.get("reponse", "")

        question_words = question.split()
        for word in question_words:
            if len(word) > 3 and word in user_text_normalized:
                return row.get("reponse", "")

    return "Je n’ai pas trouvé de réponse précise dans ma base de connaissances. Pouvez-vous reformuler votre question ?"


def build_response(intent_name, message):
    return {
        "sessionState": {
            "dialogAction": {
                "type": "Close"
            },
            "intent": {
                "name": intent_name,
                "state": "Fulfilled"
            }
        },
        "messages": [
            {
                "contentType": "PlainText",
                "content": message
            }
        ]
    }


def lambda_handler(event, context):
    intent_name = event.get("sessionState", {}).get("intent", {}).get("name", "UnknownIntent")
    user_text = event.get("inputTranscript", "")

    answer = find_answer(user_text)

    return build_response(intent_name, answer)
```

---

## 21. Connexion entre Amazon Lex et AWS Lambda

Vous devez connecter votre fonction Lambda à votre bot Amazon Lex.

Vous devez vérifier que :

```text
1. La fonction Lambda existe.
2. La fonction Lambda est dans une région compatible avec Amazon Lex.
3. Amazon Lex a le droit d’appeler la fonction Lambda.
4. L’intention utilise Lambda pour générer la réponse.
5. Le bot a été reconstruit après modification.
6. L’alias du bot pointe vers la bonne version.
```

Après chaque modification importante, vous devez reconstruire le bot avant de le tester.

---

## 22. Test direct dans Amazon Lex

Avant de connecter Amazon Connect ou Twilio, vous devez tester le chatbot directement dans Amazon Lex.

Vous devez poser au minimum **5 questions différentes**.

Exemples :

```text
Quels sont vos horaires ?
Combien coûte le cours AWS ?
Quelle est la durée du cours Python ?
Comment contacter le support ?
Quel cours recommandez-vous pour débuter ?
```

Vous devez fournir des captures d’écran montrant :

```text
1. La question posée.
2. L’intention détectée.
3. La réponse retournée par le chatbot.
4. Le bon fonctionnement de Lambda.
```

---

# 23. Intégration externe obligatoire : Amazon Connect ou Twilio

Après avoir testé votre chatbot dans Amazon Lex, vous devez le connecter à au moins un canal externe.

Vous devez choisir une des deux options suivantes :

```text
Option A : Amazon Connect pour le vocal.
Option B : Twilio pour SMS ou messagerie.
```

Vous pouvez réaliser les deux options si vous voulez obtenir une démonstration plus complète.

---

# 24. Option A — Intégration avec Amazon Connect

## 24.1 Objectif

Avec Amazon Connect, vous devez permettre à un utilisateur de parler au chatbot par téléphone ou à travers un flux de contact vocal.

L’objectif est de démontrer que votre chatbot peut être utilisé dans un scénario de type centre d’appel.

Architecture attendue :

```text
Utilisateur au téléphone
        ↓
Amazon Connect
        ↓
Flux de contact
        ↓
Amazon Lex V2
        ↓
AWS Lambda
        ↓
Fichier CSV
        ↓
Réponse vocale retournée à l’utilisateur
```

---

## 24.2 Exemple de conversation vocale

```text
Utilisateur :
Bonjour, je veux connaître le prix du cours AWS.

Bot vocal :
Le cours AWS coûte 400 $.

Utilisateur :
Quels sont vos horaires ?

Bot vocal :
Nous sommes ouverts du lundi au vendredi de 9h à 17h.
```

---

## 24.3 Travail demandé avec Amazon Connect

Si vous choisissez Amazon Connect, vous devez :

```text
1. Créer ou utiliser une instance Amazon Connect.
2. Créer un flux de contact simple.
3. Ajouter votre bot Amazon Lex dans le flux.
4. Configurer l’appel vers le bot.
5. Tester une interaction vocale.
6. Montrer que la réponse vient du fichier CSV.
```

---

## 24.4 Captures d’écran à fournir

Vous devez fournir :

```text
1. Capture d’écran de l’instance Amazon Connect.
2. Capture d’écran du flux de contact.
3. Capture d’écran montrant l’intégration du bot Lex.
4. Capture d’écran ou courte vidéo du test vocal.
5. Capture d’écran des logs Lambda ou du test Lex si nécessaire.
```

---

# 25. Option B — Intégration avec Twilio

## 25.1 Objectif

Avec Twilio, vous devez permettre à un utilisateur d’envoyer un message texte au chatbot et de recevoir une réponse.

L’objectif est de démontrer que votre bot Amazon Lex peut être utilisé dans un canal de messagerie.

Architecture attendue :

```text
Utilisateur
        ↓
Message SMS ou messagerie Twilio
        ↓
Twilio
        ↓
Canal Twilio relié à Amazon Lex
        ↓
Amazon Lex V2
        ↓
AWS Lambda
        ↓
Fichier CSV
        ↓
Réponse retournée à Twilio
        ↓
Message reçu par l’utilisateur
```

---

## 25.2 Exemple de conversation par SMS

```text
Utilisateur :
prix aws

Bot par SMS :
Le cours AWS coûte 400 $.

Utilisateur :
horaires

Bot par SMS :
Nous sommes ouverts du lundi au vendredi de 9h à 17h.
```

---

## 25.3 Travail demandé avec Twilio

Si vous choisissez Twilio, vous devez :

```text
1. Créer ou utiliser un compte Twilio.
2. Configurer un numéro ou un canal de test.
3. Relier Twilio à Amazon Lex.
4. Envoyer au moins trois messages de test.
5. Recevoir les réponses du chatbot.
6. Montrer que les réponses proviennent du fichier CSV.
```

---

## 25.4 Captures d’écran à fournir

Vous devez fournir :

```text
1. Capture d’écran de votre configuration Twilio.
2. Capture d’écran de l’intégration avec Amazon Lex.
3. Capture d’écran d’un message envoyé.
4. Capture d’écran de la réponse reçue.
5. Capture d’écran montrant que Lambda est appelée.
```

---

# 26. Tests obligatoires

Vous devez effectuer au minimum les tests suivants :

```text
1. Test direct dans Amazon Lex avec au moins 5 questions.
2. Test avec Amazon Connect ou Twilio avec au moins 3 questions.
3. Test d’une question connue présente dans le CSV.
4. Test d’une question reformulée.
5. Test d’une question inconnue pour vérifier la réponse par défaut.
```

---

## 27. Exemple de tests attendus

| Test   | Question utilisateur                  | Résultat attendu                                           |
| ------ | ------------------------------------- | ---------------------------------------------------------- |
| Test 1 | Combien coûte le cours AWS ?          | Le chatbot retourne le prix du cours AWS                   |
| Test 2 | Quelle est la durée du cours Python ? | Le chatbot retourne la durée du cours Python               |
| Test 3 | Quels sont vos horaires ?             | Le chatbot retourne les horaires                           |
| Test 4 | Comment contacter le support ?        | Le chatbot retourne les informations de support            |
| Test 5 | Avez-vous un cours en astronomie ?    | Le chatbot indique qu’il n’a pas trouvé de réponse précise |

---

# 28. Rapport à remettre

Vous devez remettre un court rapport professionnel de 2 à 4 pages.

Votre rapport doit contenir les sections suivantes :

```text
1. Présentation du scénario choisi.
2. Architecture du POC.
3. Explication du fichier CSV.
4. Prompt utilisé pour générer le CSV avec ChatGPT.
5. Description des intentions Amazon Lex.
6. Description des slots utilisés.
7. Explication du rôle de Lambda.
8. Description de l’intégration Amazon Connect ou Twilio.
9. Résultats des tests.
10. Limites du POC.
11. Améliorations possibles.
12. Conclusion.
```

---

## 29. Livrables à remettre

Vous devez remettre :

```text
1. Le fichier CSV généré avec ChatGPT.
2. Le prompt utilisé pour générer le CSV.
3. Le code complet de la fonction Lambda.
4. Des captures d’écran du bot Amazon Lex.
5. Des captures d’écran des intentions et des slots.
6. Des captures d’écran du test direct dans Amazon Lex.
7. Des captures d’écran de l’intégration Amazon Connect ou Twilio.
8. Une courte vidéo ou démonstration si vous utilisez le vocal avec Amazon Connect.
9. Le rapport final en PDF ou Word.
10. Une capture d’écran du budget ou de l’alerte de coût AWS.
```

---

# 30. Critères d’évaluation

| Critère                                                                      | Points |
| ---------------------------------------------------------------------------- | -----: |
| Création ou utilisation correcte du compte AWS avec budget ou alerte de coût |     10 |
| Scénario clair, simple et réaliste                                           |      5 |
| Fichier CSV généré avec ChatGPT, propre et exploitable                       |     10 |
| Bot Amazon Lex V2 correctement créé                                          |     15 |
| Intentions pertinentes et bien nommées                                       |     10 |
| Phrases d’entraînement suffisantes et variées                                |     10 |
| Utilisation correcte d’au moins un slot                                      |      5 |
| Fonction AWS Lambda fonctionnelle                                            |     15 |
| Recherche correcte des réponses dans le CSV                                  |     10 |
| Test direct réussi dans Amazon Lex                                           |     10 |
| Intégration réussie avec Amazon Connect ou Twilio                            |     15 |
| Rapport clair, structuré et professionnel                                    |     10 |
| Captures d’écran et preuves de fonctionnement                                |     10 |
| Nettoyage des ressources AWS ou explication des ressources conservées        |      5 |

Total : **130 points**

---

## 31. Bonus

Vous pouvez obtenir un bonus si vous réalisez des éléments supplémentaires.

| Bonus                                                             | Points |
| ----------------------------------------------------------------- | -----: |
| Intégration Amazon Connect et Twilio dans le même projet          |    +10 |
| Utilisation d’Amazon S3 pour stocker le fichier CSV               |     +5 |
| Réponses plus intelligentes avec meilleure recherche de mots-clés |     +5 |
| Interface ou démonstration particulièrement claire                |     +5 |
| Gestion propre des erreurs et des questions inconnues             |     +5 |

---

# 32. Contraintes importantes

Vous devez respecter les contraintes suivantes :

```text
1. Toutes les données doivent être fictives.
2. Le CSV doit contenir au minimum 20 lignes.
3. Le bot doit contenir au minimum 3 intentions.
4. Chaque intention doit contenir au minimum 5 phrases d’entraînement.
5. Le bot doit utiliser AWS Lambda.
6. La réponse doit provenir du fichier CSV.
7. Le chatbot doit être testé directement dans Amazon Lex.
8. Le chatbot doit être connecté à Amazon Connect ou Twilio.
9. Vous devez fournir des preuves de fonctionnement.
10. Vous devez configurer une alerte de coût ou un budget AWS.
```

---

# 33. Nettoyage final des ressources

À la fin du travail, vous devez vérifier vos ressources AWS.

Vous devez supprimer ou désactiver les ressources qui ne sont plus nécessaires.

Vous devez vérifier notamment :

```text
1. Amazon Lex
2. AWS Lambda
3. Amazon Connect
4. Amazon S3 si utilisé
5. CloudWatch Logs si nécessaire
6. Numéros ou configurations Twilio si utilisés
```

Dans votre rapport, vous devez indiquer ce que vous avez supprimé ou conservé.

---

# 34. Résultat attendu

À la fin du travail, vous devez être capable de démontrer un POC complet.

Votre démonstration doit montrer clairement :

```text
1. Un utilisateur pose une question.
2. La question arrive dans Amazon Lex.
3. Amazon Lex détecte une intention.
4. AWS Lambda est appelée.
5. Lambda cherche la réponse dans le fichier CSV.
6. Le chatbot retourne une réponse claire.
7. La réponse est reçue dans Amazon Connect ou Twilio.
```

Le projet doit être simple, mais fonctionnel. L’objectif est de démontrer votre compréhension de l’intégration entre un chatbot, une fonction serverless et une source de données externe simple.
