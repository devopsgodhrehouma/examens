# Travail pratique — POC d’agent vocal IA avec Twilio, CSV et agent conversationnel

## 1. Contexte

Dans ce travail, il faut créer un **POC d’agent vocal IA** capable de parler avec un utilisateur de manière naturelle.

L’objectif est de simuler un assistant vocal de service client. L’utilisateur appelle un numéro ou interagit avec un canal vocal. L’agent écoute la question, comprend la demande, cherche une réponse dans une petite base de connaissances, puis répond oralement comme un assistant réel.

Le but n’est pas de créer un chatbot à boutons ou un simple menu vocal. Le but est de créer une expérience conversationnelle simple, naturelle et fonctionnelle.

---

## 2. Objectif général

Créer un agent vocal IA capable de :

```text
1. Recevoir un appel vocal.
2. Comprendre la question posée oralement.
3. Chercher une réponse dans un fichier CSV ou Google Sheet.
4. Générer une réponse claire avec une IA conversationnelle.
5. Répondre oralement à l’utilisateur.
6. Gérer une question inconnue avec une réponse professionnelle.
7. Fournir une preuve de fonctionnement.
```

---

## 3. Architecture attendue

```text
                         ┌─────────────────────────────┐
                         │        Utilisateur           │
                         │  Appelle ou parle à l’agent  │
                         └──────────────┬──────────────┘
                                        │
                                        ▼
                         ┌─────────────────────────────┐
                         │        Twilio Voice          │
                         │  Canal vocal / téléphone     │
                         └──────────────┬──────────────┘
                                        │
                                        ▼
                         ┌─────────────────────────────┐
                         │   Twilio ConversationRelay   │
                         │   Voix → Texte               │
                         │   Texte → Voix               │
                         │   Session vocale             │
                         └──────────────┬──────────────┘
                                        │
                                        ▼
                         ┌─────────────────────────────┐
                         │   Serveur Agent IA           │
                         │   FastAPI ou Node.js         │
                         │   WebSocket / logique agent  │
                         └──────────────┬──────────────┘
                                        │
                         ┌──────────────┼──────────────┐
                         │                             │
                         ▼                             ▼
              ┌───────────────────┐        ┌─────────────────────┐
              │  Modèle IA / LLM   │        │ CSV ou Google Sheet │
              │  Réponse naturelle │        │ FAQ / prix / infos  │
              └─────────┬─────────┘        └──────────┬──────────┘
                        │                             │
                        └──────────────┬──────────────┘
                                       ▼
                         ┌─────────────────────────────┐
                         │   Réponse finale             │
                         │   retournée à Twilio         │
                         └──────────────┬──────────────┘
                                        ▼
                         ┌─────────────────────────────┐
                         │   Réponse vocale             │
                         │   entendue par l’utilisateur │
                         └─────────────────────────────┘
```

---

## 4. Fonctionnement attendu

Exemple de conversation :

```text
Utilisateur :
Bonjour, je veux connaître le prix du cours AWS.

Agent vocal :
Le cours AWS coûte 400 $. Il dure 45 heures et il est recommandé aux personnes qui veulent découvrir les services cloud.

Utilisateur :
Est-ce que vous avez un cours pour débuter ?

Agent vocal :
Oui. Pour débuter, je recommande le cours Python débutant, car il permet d’apprendre les bases de la programmation avant d’aller vers le cloud ou l’intelligence artificielle.

Utilisateur :
Comment contacter le support ?

Agent vocal :
Vous pouvez contacter le support par courriel à support@exemple.com. Un membre de l’équipe vous répondra pendant les heures d’ouverture.
```

---

## 5. Technologies utilisées

La solution recommandée utilise :

```text
Twilio Voice
Twilio ConversationRelay
Un serveur FastAPI ou Node.js
Un modèle IA conversationnel
Un fichier CSV ou Google Sheet
Optionnel : n8n pour enregistrer les conversations ou envoyer une notification
```

Whisper n’est pas obligatoire dans cette architecture. ConversationRelay gère déjà la transcription voix-vers-texte et la synthèse texte-vers-voix. Une architecture personnalisée avec Whisper est acceptée comme option avancée, mais elle est plus difficile à mettre en place. OpenAI propose aussi des architectures temps réel pour agents vocaux capables de garder une session ouverte et de gérer la conversation en direct. ([OpenAI Développeurs][2])

---

## 6. Données à préparer

Il faut créer une petite base de connaissances fictive.

Le fichier peut être :

```text
Option 1 : fichier CSV
Option 2 : Google Sheet
```

La version la plus simple est le fichier CSV.

Nom recommandé :

```text
base_connaissances_agent.csv
```

Le fichier doit contenir au minimum **20 lignes**.

Colonnes obligatoires :

```csv
id,categorie,mot_cle,question,reponse
```

Exemple :

```csv
id,categorie,mot_cle,question,reponse
1,horaire,horaires,Quels sont vos horaires?,Nous sommes ouverts du lundi au vendredi de 9h à 17h.
2,prix,python,Combien coûte le cours Python?,Le cours Python coûte 250 $ et dure 30 heures.
3,prix,aws,Combien coûte le cours AWS?,Le cours AWS coûte 400 $ et dure 45 heures.
4,duree,machine learning,Quelle est la durée du cours Machine Learning?,Le cours Machine Learning dure 60 heures.
5,support,support,Comment contacter le support?,Vous pouvez contacter le support par courriel à support@exemple.com.
```

---

## 7. Génération du CSV avec ChatGPT

Utiliser le prompt suivant pour générer la base de connaissances :

```text
Génère-moi un fichier CSV fictif pour un agent vocal IA de service client.

Le fichier doit contenir 20 lignes.

Colonnes :
id,categorie,mot_cle,question,reponse

Scénario :
Un centre de formation fictif propose des cours en Python, AWS, Machine Learning, cybersécurité, développement web et intelligence artificielle.

Contraintes :
- Les données doivent être entièrement fictives.
- Les réponses doivent être courtes, naturelles et adaptées à une réponse vocale.
- Les réponses doivent être faciles à comprendre à l’oral.
- Le champ mot_cle doit contenir le mot principal à détecter dans la question.
- Ne mets aucune vraie donnée personnelle.
- Donne uniquement le contenu CSV, sans explication.
```

---

## 8. Comportement de l’agent

L’agent vocal doit respecter les règles suivantes :

```text
1. Répondre poliment.
2. Donner des réponses courtes.
3. Utiliser les informations du CSV ou du Google Sheet.
4. Ne pas inventer une réponse si l’information n’existe pas.
5. Demander une reformulation si la question est vague.
6. Dire clairement qu’il ne trouve pas l’information si elle est absente.
7. Garder un ton professionnel et naturel.
```

Exemple de réponse si l’information existe :

```text
Le cours AWS coûte 400 $ et dure 45 heures.
```

Exemple de réponse si l’information n’existe pas :

```text
Je n’ai pas trouvé cette information dans ma base actuelle. Pouvez-vous reformuler votre question ou demander un autre service ?
```

---

## 9. Prompt système de l’agent IA

Le serveur de l’agent doit utiliser un prompt système clair.

Prompt recommandé :

```text
Tu es un agent vocal professionnel pour un centre de formation fictif.

Ton rôle est de répondre aux questions des utilisateurs à partir d’une base de connaissances fournie sous forme de CSV ou Google Sheet.

Règles :
1. Réponds de façon courte, claire et naturelle.
2. Utilise uniquement les informations disponibles dans la base de connaissances.
3. Si l’information n’est pas trouvée, dis que tu ne trouves pas l’information.
4. Ne donne jamais de fausses informations.
5. Ne demande jamais de données personnelles sensibles.
6. Garde un ton professionnel, calme et serviable.
7. Les réponses doivent être adaptées à une conversation vocale.
8. Évite les réponses trop longues.
```

---

## 10. Étapes de réalisation

### Étape 1 — Créer la base de connaissances

Créer un fichier CSV avec ChatGPT.

Le fichier doit contenir :

```text
20 lignes minimum
5 catégories minimum
des mots-clés simples
des réponses adaptées à l’oral
des données fictives
```

Catégories possibles :

```text
prix
horaire
durée
inscription
support
recommandation
certificat
modalité
paiement fictif
annulation fictive
```

---

### Étape 2 — Créer le compte Twilio

Créer ou utiliser un compte Twilio.

Configurer un numéro vocal Twilio ou un environnement de test selon les possibilités du compte.

Ne pas utiliser de données personnelles inutiles. Ne pas partager les identifiants Twilio.

---

### Étape 3 — Créer le serveur de l’agent IA

Créer une petite application serveur.

Deux choix sont acceptés :

```text
Option A : FastAPI avec Python
Option B : Node.js avec Express
```

Le serveur doit faire quatre choses :

```text
1. Recevoir les messages de ConversationRelay.
2. Comprendre le texte reçu.
3. Chercher une réponse dans le CSV ou Google Sheet.
4. Retourner une réponse textuelle à Twilio.
```

Twilio transformera ensuite cette réponse textuelle en réponse vocale.

---

### Étape 4 — Connecter Twilio ConversationRelay

Configurer Twilio pour que l’appel vocal soit envoyé vers le serveur de l’agent.

L’appel doit passer par ConversationRelay.

ConversationRelay est utilisé pour gérer la conversation vocale en temps réel. Il permet au serveur de recevoir ce que l’utilisateur dit et de renvoyer ce que l’agent doit répondre. ([Twilio][3])

---

### Étape 5 — Tester l’agent

Faire au minimum **5 tests vocaux**.

Tests obligatoires :

```text
1. Une question sur un prix.
2. Une question sur les horaires.
3. Une question sur une durée.
4. Une question sur le support.
5. Une question inconnue.
```

Exemples :

```text
Combien coûte le cours AWS ?
Quels sont vos horaires ?
Combien de temps dure le cours Python ?
Comment contacter le support ?
Avez-vous un cours sur la robotique spatiale ?
```

---

## 11. Version simple acceptée

La version simple acceptée est :

```text
Twilio Voice
   ↓
ConversationRelay
   ↓
Serveur Agent IA
   ↓
CSV local
   ↓
Réponse vocale
```

Dans cette version, le CSV peut être placé directement dans le dossier du projet.

---

## 12. Version avancée acceptée

La version avancée est :

```text
Twilio Voice
   ↓
ConversationRelay
   ↓
Serveur Agent IA
   ↓
Google Sheet ou base externe
   ↓
n8n pour journalisation ou notification
   ↓
Réponse vocale
```

n8n peut être utilisé pour automatiser des actions après la conversation, par exemple enregistrer une trace dans Google Sheets ou envoyer un courriel de suivi. n8n dispose d’intégrations avec Twilio et Google Sheets. ([n8n][4])

---

## 13. Code logique attendu

Le code exact peut varier, mais la logique doit respecter ce modèle :

```text
1. Recevoir le texte prononcé par l’utilisateur.
2. Nettoyer le texte.
3. Comparer le texte avec les mots-clés du CSV.
4. Trouver la meilleure réponse.
5. Envoyer la réponse à l’agent vocal.
```

Pseudo-code :

```text
charger le fichier CSV

quand un message arrive :
    récupérer la phrase de l’utilisateur
    convertir la phrase en minuscules
    chercher si un mot-clé du CSV existe dans la phrase

    si un mot-clé est trouvé :
        retourner la réponse correspondante

    sinon :
        demander à l’utilisateur de reformuler
```

---

## 14. Exemple de fonction de recherche en Python

```python
import csv
import unicodedata

def normalize(text):
    if not text:
        return ""
    text = text.lower()
    text = unicodedata.normalize("NFD", text)
    text = "".join(c for c in text if unicodedata.category(c) != "Mn")
    return text

def load_knowledge_base(csv_path):
    rows = []
    with open(csv_path, mode="r", encoding="utf-8") as file:
        reader = csv.DictReader(file)
        for row in reader:
            rows.append(row)
    return rows

def find_answer(user_text, rows):
    user_text = normalize(user_text)

    for row in rows:
        keyword = normalize(row.get("mot_cle", ""))
        question = normalize(row.get("question", ""))

        if keyword and keyword in user_text:
            return row.get("reponse", "")

        if question:
            important_words = [w for w in question.split() if len(w) > 4]
            for word in important_words:
                if normalize(word) in user_text:
                    return row.get("reponse", "")

    return "Je n’ai pas trouvé cette information dans ma base actuelle. Pouvez-vous reformuler votre question ?"
```

---

## 15. Qualité minimale attendue

L’agent doit être capable de répondre correctement à au moins **4 questions sur 5** si les réponses existent dans le CSV.

L’agent doit aussi bien gérer une question inconnue.

Exemple :

```text
Question :
Est-ce que vous donnez un cours sur la cuisine italienne ?

Réponse attendue :
Je n’ai pas trouvé cette information dans ma base actuelle. Pouvez-vous poser une question sur nos cours ou nos services ?
```

---

## 16. Captures et preuves à fournir

Fournir les éléments suivants :

```text
1. Capture du fichier CSV ou du Google Sheet.
2. Capture du compte ou de la configuration Twilio.
3. Capture de la configuration ConversationRelay.
4. Capture du code du serveur.
5. Capture du test vocal.
6. Capture des logs montrant la question reçue.
7. Capture des logs montrant la réponse générée.
8. Vidéo courte ou démonstration de l’appel vocal.
```

---

## 17. Rapport à remettre

Remettre un rapport court, clair et professionnel.

Le rapport doit contenir :

```text
1. Titre du projet.
2. Scénario choisi.
3. Architecture utilisée.
4. Explication du CSV ou Google Sheet.
5. Prompt utilisé pour générer les données.
6. Fonctionnement de l’agent vocal.
7. Description du rôle de Twilio.
8. Description du rôle de ConversationRelay.
9. Description du rôle du modèle IA.
10. Résultats des tests.
11. Limites du POC.
12. Améliorations possibles.
13. Conclusion.
```

---

## 18. Tests à documenter

| Test | Question orale                                  | Résultat attendu                                  |
| ---- | ----------------------------------------------- | ------------------------------------------------- |
| 1    | Combien coûte le cours AWS ?                    | L’agent donne le prix du cours AWS                |
| 2    | Quels sont vos horaires ?                       | L’agent donne les horaires                        |
| 3    | Quelle est la durée du cours Python ?           | L’agent donne la durée du cours Python            |
| 4    | Comment contacter le support ?                  | L’agent donne le contact du support               |
| 5    | Avez-vous un cours sur un sujet absent du CSV ? | L’agent indique qu’il ne trouve pas l’information |

---

## 19. Livrables

Remettre :

```text
1. Le fichier CSV ou le lien vers le Google Sheet.
2. Le prompt utilisé pour générer les données.
3. Le code du serveur agent IA.
4. Les captures d’écran de configuration.
5. Les captures ou logs des tests.
6. Une courte vidéo ou preuve de l’appel vocal.
7. Le rapport final en PDF ou Word.
```

---

## 20. Grille d’évaluation

| Critère                                        | Points |
| ---------------------------------------------- | -----: |
| Scénario clair et réaliste                     |     10 |
| CSV ou Google Sheet bien structuré             |     15 |
| Données fictives, cohérentes et exploitables   |     10 |
| Agent vocal fonctionnel                        |     20 |
| Connexion correcte avec Twilio Voice           |     15 |
| Utilisation correcte de ConversationRelay      |     15 |
| Recherche correcte dans le CSV ou Google Sheet |     15 |
| Réponses naturelles et adaptées à l’oral       |     15 |
| Gestion des questions inconnues                |     10 |
| Tests vocaux documentés                        |     15 |
| Rapport clair et professionnel                 |     15 |
| Captures, logs ou vidéo de démonstration       |     15 |

Total : **170 points**

---

## 21. Bonus

| Bonus                                                       | Points |
| ----------------------------------------------------------- | -----: |
| Utilisation de Google Sheet au lieu d’un CSV local          |     +5 |
| Utilisation de n8n pour enregistrer l’historique des appels |     +5 |
| Envoi automatique d’un courriel après l’appel               |     +5 |
| Meilleure recherche de réponse avec similarité sémantique   |    +10 |
| Architecture personnalisée avec Whisper + Text-to-Speech    |    +10 |
| Interface de suivi des conversations                        |    +10 |

---

## 22. Contraintes importantes

```text
1. Toutes les données doivent être fictives.
2. Aucune donnée personnelle réelle ne doit être utilisée.
3. Le CSV doit contenir au minimum 20 lignes.
4. L’agent doit répondre oralement.
5. L’agent doit utiliser la base de connaissances.
6. L’agent ne doit pas inventer une réponse absente du CSV.
7. Une question inconnue doit être gérée proprement.
8. Les clés API ne doivent jamais être publiées.
9. Les identifiants Twilio ne doivent jamais être partagés.
10. Le projet doit rester simple et démontrable.
```

---

## 23. Résultat final attendu

À la fin du travail, la démonstration doit montrer clairement :

```text
1. Un utilisateur parle à l’agent.
2. Twilio reçoit l’appel vocal.
3. ConversationRelay transmet le contenu de la conversation.
4. Le serveur agent IA analyse la demande.
5. L’agent cherche une réponse dans le CSV ou Google Sheet.
6. L’agent prépare une réponse naturelle.
7. Twilio retourne la réponse oralement à l’utilisateur.
```

Le résultat attendu est un **agent vocal IA simple, fonctionnel et démontrable**, capable de répondre comme un assistant de service client à partir d’une petite base de connaissances fictive.

[1]: https://www.twilio.com/docs/voice/conversationrelay?utm_source=chatgpt.com "Conversation Relay"
[2]: https://developers.openai.com/api/docs/guides/realtime?utm_source=chatgpt.com "Realtime and audio | OpenAI API"
[3]: https://www.twilio.com/docs/voice/twiml/connect/conversationrelay?utm_source=chatgpt.com "TwiML™ Voice: <ConversationRelay>"
[4]: https://n8n.io/integrations/google-sheets/and/twilio/?utm_source=chatgpt.com "Google Sheets and Twilio integration"
