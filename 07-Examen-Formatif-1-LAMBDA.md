<h2>Examen Formatif AWS Lambda — QCM (30 questions)</h2>

<p><strong>Note (aide autorisée) :</strong><br>
Vous pouvez consulter la documentation officielle AWS (Lambda, IAM, CloudWatch, API Gateway, SQS, SNS, EventBridge) pour valider les options, syntaxes et bonnes pratiques (triggers, permissions, timeout, mémoire, logs, variables d’environnement, VPC, etc.).</p>

<hr>

<h3>PARTIE 1 — Concepts & exécution (1–6)</h3>

<details> <summary> PARTIE 1 — Concepts &amp; exécution (1–6) </summary>

<p><strong>1) AWS Lambda est principalement…</strong><br>
A) Un serveur Linux à administrer manuellement<br>
B) Un service “serverless” qui exécute du code à la demande<br>
C) Une base de données NoSQL<br>
D) Un service de stockage d’objets</p>

<p><strong>2) Une “fonction Lambda” est…</strong><br>
A) Un conteneur Docker qui tourne en continu<br>
B) Du code + une configuration d’exécution (runtime, mémoire, timeout, rôle IAM)<br>
C) Un fichier texte stocké dans S3 uniquement<br>
D) Une règle de pare-feu</p>

<p><strong>3) Le paramètre <code>timeout</code> d’une Lambda contrôle…</strong><br>
A) La taille maximale des logs<br>
B) La durée maximale d’exécution de la fonction<br>
C) Le nombre maximal d’utilisateurs IAM<br>
D) La vitesse du réseau</p>

<p><strong>4) Que signifie “cold start” ?</strong><br>
A) La Lambda est chiffrée à froid<br>
B) Le premier démarrage d’un environnement d’exécution (latence initiale)<br>
C) La Lambda tourne uniquement la nuit<br>
D) Un redémarrage de votre ordinateur</p>

<p><strong>5) Quel élément décide des permissions d’accès AWS de la Lambda (S3, DynamoDB, etc.) ?</strong><br>
A) Le Security Group<br>
B) Le rôle IAM associé à la fonction (Execution Role)<br>
C) Le nom de la fonction<br>
D) Le runtime (Python/Node)</p>

<p><strong>6) En général, augmenter la mémoire d’une Lambda peut…</strong><br>
A) Toujours réduire les permissions IAM<br>
B) Augmenter aussi les ressources CPU allouées (donc parfois accélérer l’exécution)<br>
C) Désactiver CloudWatch Logs<br>
D) Supprimer le besoin de timeout</p>

</details>

<hr>

<h3>PARTIE 2 — Triggers & événements (7–12)</h3>

<details> <summary> PARTIE 2 — Triggers &amp; événements (7–12) </summary>

<p><strong>7) Un “trigger” Lambda sert à…</strong><br>
A) Changer la langue de l’interface AWS<br>
B) Déclencher l’exécution de la fonction à partir d’un événement (S3, API, cron, etc.)<br>
C) Installer Python automatiquement<br>
D) Créer un VPC</p>

<p><strong>8) Quel service est souvent utilisé pour exposer une Lambda comme API HTTP ?</strong><br>
A) AWS CloudTrail<br>
B) Amazon API Gateway (ou Lambda Function URL)<br>
C) Amazon EBS<br>
D) Amazon Route 53 Resolver uniquement</p>

<p><strong>9) Quel événement peut déclencher une Lambda via un “cron” AWS ?</strong><br>
A) CloudWatch Logs uniquement<br>
B) EventBridge (règle schedule / cron)<br>
C) S3 Glacier<br>
D) IAM Access Analyzer</p>

<p><strong>10) Quel trigger est typique pour traiter des messages en file d’attente ?</strong><br>
A) Amazon SQS<br>
B) Amazon ECR<br>
C) Amazon CloudFront<br>
D) Amazon KMS</p>

<p><strong>11) Si une Lambda est déclenchée par S3 (ObjectCreated), le “payload” contient souvent…</strong><br>
A) Le mot de passe du bucket<br>
B) Le nom du bucket et la clé (key) de l’objet créé<br>
C) Le code source de la Lambda<br>
D) L’IP privée de l’utilisateur</p>

<p><strong>12) Quel service publie des notifications “pub/sub” pouvant déclencher Lambda ?</strong><br>
A) Amazon SNS<br>
B) Amazon EBS<br>
C) Amazon EMR<br>
D) Amazon Inspector</p>

</details>

<hr>

<h3>PARTIE 3 — Logs, monitoring & erreurs (13–18)</h3>

<details> <summary> PARTIE 3 — Logs, monitoring &amp; erreurs (13–18) </summary>

<p><strong>13) Où vont les logs <code>print()</code> / <code>console.log()</code> d’une Lambda par défaut ?</strong><br>
A) Dans S3 automatiquement<br>
B) Dans CloudWatch Logs (si permissions IAM OK)<br>
C) Dans DynamoDB<br>
D) Dans Route 53</p>

<p><strong>14) Quelle métrique indique le nombre d’exécutions Lambda qui ont échoué ?</strong><br>
A) <code>Invocations</code> uniquement<br>
B) <code>Errors</code><br>
C) <code>Throttles</code> uniquement<br>
D) <code>NetworkPackets</code></p>

<p><strong>15) Une erreur “Task timed out after X seconds” indique…</strong><br>
A) Un problème de DNS uniquement<br>
B) Que la fonction a dépassé son timeout configuré<br>
C) Que le rôle IAM est trop permissif<br>
D) Que l’image Docker est corrompue</p>

<p><strong>16) Si CloudWatch Logs ne reçoit aucun log, une cause fréquente est…</strong><br>
A) La Lambda n’a pas de nom<br>
B) Le rôle IAM n’a pas les permissions de logs (CreateLogGroup/Stream/PutLogEvents)<br>
C) Le VPC est trop grand<br>
D) Le runtime est “trop récent”</p>

<p><strong>17) Quel mécanisme aide à recevoir les erreurs asynchrones (ex: EventBridge → Lambda) ?</strong><br>
A) Dead-Letter Queue (DLQ) ou Destination (onFailure)<br>
B) Un Security Group<br>
C) Un bucket S3 public<br>
D) Une AMI EC2</p>

<p><strong>18) Le champ “Billed Duration” dans le rapport Lambda correspond…</strong><br>
A) Au temps exact CPU utilisé uniquement<br>
B) Au temps facturé (arrondi selon les règles AWS) pour l’exécution<br>
C) Au temps de téléchargement internet<br>
D) Au temps d’affichage dans la console</p>

</details>

<hr>

<h3>PARTIE 4 — IAM, sécurité & configuration (19–24)</h3>

<details> <summary> PARTIE 4 — IAM, sécurité &amp; configuration (19–24) </summary>

<p><strong>19) Le principe de sécurité recommandé pour IAM est…</strong><br>
A) Donner <code>AdministratorAccess</code> à tout le monde<br>
B) Least privilege (moindre privilège) : donner uniquement ce qui est nécessaire<br>
C) Désactiver CloudWatch<br>
D) Mettre les secrets dans le code</p>

<p><strong>20) Quelle bonne pratique pour les secrets (API keys) dans Lambda ?</strong><br>
A) Les écrire en dur dans le code<br>
B) Les stocker dans S3 en public<br>
C) Utiliser AWS Secrets Manager ou SSM Parameter Store (et variables d’environnement si adapté)<br>
D) Les mettre dans les logs</p>

<p><strong>21) Pourquoi éviter de mettre une Lambda dans un VPC “sans besoin” ?</strong><br>
A) Parce que ça supprime IAM<br>
B) Parce que ça peut augmenter la latence (cold start) et complexifier l’accès réseau (NAT, endpoints)<br>
C) Parce que Lambda ne supporte pas VPC<br>
D) Parce que VPC rend la Lambda gratuite</p>

<p><strong>22) Une variable d’environnement Lambda sert à…</strong><br>
A) Installer automatiquement Python<br>
B) Fournir de la configuration (ex: <code>ENV=prod</code>, <code>TABLE_NAME</code>) sans modifier le code<br>
C) Remplacer CloudWatch Logs<br>
D) Créer des buckets S3</p>

<p><strong>23) Le “Resource-based policy” d’une Lambda sert à…</strong><br>
A) Définir la RAM<br>
B) Autoriser un service/compte à invoquer la fonction (ex: API Gateway, S3, cross-account)<br>
C) Compresser le code<br>
D) Créer un VPC</p>

<p><strong>24) Le paramètre “Concurrency” est lié à…</strong><br>
A) La taille du zip<br>
B) Le nombre d’exécutions en parallèle possibles<br>
C) Le nombre de buckets S3<br>
D) Le type de CPU de votre PC</p>

</details>

<hr>

<h3>PARTIE 5 — Intégrations & bonnes pratiques (25–30)</h3>

<details> <summary> PARTIE 5 — Intégrations &amp; bonnes pratiques (25–30) </summary>

<p><strong>25) Pour exécuter une Lambda toutes les 5 minutes, on utilise souvent…</strong><br>
A) Un crontab Linux sur votre PC<br>
B) EventBridge Schedule (rate/cron)<br>
C) Un fichier <code>.env</code><br>
D) Un bucket S3</p>

<p><strong>26) Une Lambda “stateless” signifie…</strong><br>
A) Qu’elle stocke automatiquement en base de données<br>
B) Qu’elle ne doit pas dépendre d’un état local permanent (le conteneur peut disparaître)<br>
C) Qu’elle ne peut pas lire de fichiers<br>
D) Qu’elle ne peut pas utiliser internet</p>

<p><strong>27) Quel service est typique pour stocker un état clé/valeur de façon simple avec Lambda ?</strong><br>
A) DynamoDB<br>
B) CloudFront<br>
C) ECR<br>
D) IAM</p>

<p><strong>28) Pour traiter beaucoup d’événements SQS, un bon réglage à connaître est…</strong><br>
A) La résolution d’écran<br>
B) La taille de batch (batch size) et la visibilité (visibility timeout) côté queue<br>
C) Le nom du bucket<br>
D) Le thème de la console AWS</p>

<p><strong>29) Une bonne pratique pour réduire le temps de démarrage est…</strong><br>
A) Mettre toutes les dépendances possibles même inutiles<br>
B) Garder le package léger et éviter les initialisations lourdes à chaque invocation<br>
C) Désactiver les logs<br>
D) Exécuter <code>sudo apt upgrade</code> dans la Lambda</p>

<p><strong>30) Pour un workflow “API + Lambda”, le flux le plus courant est…</strong><br>
A) Lambda appelle API Gateway pour créer l’URL<br>
B) API Gateway reçoit HTTP → invoque Lambda → renvoie une réponse HTTP<br>
C) S3 reçoit HTTP → appelle IAM → renvoie la page<br>
D) EC2 reçoit HTTP → envoie à CloudTrail</p>

</details>

<hr>

<h3>PARTIE 6 — Questions de développement (31–40) (optionnel)</h3>

<details> <summary> PARTIE 6 — Questions de développement (31–40) (optionnel) </summary>

<p><strong>Consignes :</strong> Répondez en <strong>5 lignes maximum</strong> par question. Réponses courtes, claires, structurées.</p>

<p><strong>31) Expliquez “cold start” et donnez une action simple pour réduire son impact.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>32) Donnez un exemple de variable d’environnement utile dans Lambda et expliquez son rôle.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>33) Expliquez la différence entre invocation synchrone et asynchrone (un exemple de service pour chaque).</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>34) Vous devez déclencher une Lambda chaque jour à 10:00 (heure de Montréal). Quel service utilisez-vous et quel point important devez-vous vérifier sur le fuseau horaire ?</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>35) Expliquez ce que fait <code>journalctl -u</code> n’existe pas sur Lambda, et comment on lit les logs à la place.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>36) Donnez 2 raisons possibles d’une erreur “Task timed out” et une action corrective pour chacune.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>37) Expliquez ce que permet une DLQ (Dead-Letter Queue) et dans quel scénario elle est utile.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>38) Donnez une règle simple de “least privilege” pour une Lambda qui lit un seul bucket S3.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>39) Expliquez comment une Lambda peut accéder à Internet lorsqu’elle est dans un VPC (idée générale).</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

<p><strong>40) Donnez une architecture simple “Streamlit UI + API + Lambda” et le rôle de chaque composant.</strong><br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................<br>
..............................................................................................................</p>

</details>

