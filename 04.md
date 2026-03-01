<h2>Examen Docker + Flask + FastAPI + Streamlit — QCM (30 questions)</h2>

<p><strong>Note (aide autorisée) :</strong><br>
Vous pouvez consulter la documentation officielle (<code>docs.docker.com</code>, <code>flask.palletsprojects.com</code>, <code>fastapi.tiangolo.com</code>, <code>docs.streamlit.io</code>) pour valider des options, syntaxes et bonnes pratiques (Dockerfile, Compose, ports, variables d’environnement, serveurs ASGI/WSGI, etc.).</p>

<h3>PARTIE 1 — Docker : fondamentaux (1–6)</h3>

<p><strong>1) Dans Docker, qu’est-ce qu’une image ?</strong><br>
A) Un conteneur en cours d’exécution<br>
B) Un modèle immuable pour créer des conteneurs<br>
C) Un volume de stockage persistant<br>
D) Un réseau virtuel</p>

<p><strong>2) Quelle commande affiche la liste des conteneurs en cours d’exécution ?</strong><br>
A) <code>docker images</code><br>
B) <code>docker ps</code><br>
C) <code>docker logs</code><br>
D) <code>docker exec</code></p>

<p><strong>3) Quelle commande construit une image à partir d’un Dockerfile dans le répertoire courant ?</strong><br>
A) <code>docker pull .</code><br>
B) <code>docker build -t monimage .</code><br>
C) <code>docker run -t monimage .</code><br>
D) <code>docker push -t monimage .</code></p>

<p><strong>4) Quel est l’effet de <code>docker run</code> (le plus souvent) ?</strong><br>
A) Il supprime l’image après exécution<br>
B) Il crée (si nécessaire) puis démarre un conteneur à partir d’une image<br>
C) Il compile automatiquement le code Python<br>
D) Il installe Docker Compose</p>

<p><strong>5) À quoi sert l’option <code>-p 8080:5000</code> ?</strong><br>
A) Port 8080 du conteneur → port 5000 de l’hôte<br>
B) Port 8080 de l’hôte → port 5000 du conteneur<br>
C) Désactive le réseau du conteneur<br>
D) Active uniquement IPv6</p>

<p><strong>6) Pourquoi utilise-t-on un volume Docker en pratique ?</strong><br>
A) Pour accélérer la RAM du conteneur<br>
B) Pour rendre les données persistantes malgré la suppression du conteneur<br>
C) Pour obliger l’application à redémarrer<br>
D) Pour remplacer Dockerfile</p>

<hr>

<h3>PARTIE 2 — Dockerfile & Compose (7–12)</h3>

<p><strong>7) Quelle instruction Dockerfile définit l’image de base ?</strong><br>
A) <code>RUN</code><br>
B) <code>FROM</code><br>
C) <code>COPY</code><br>
D) <code>CMD</code></p>

<p><strong>8) Quel fichier sert à exclure des fichiers du contexte de build ?</strong><br>
A) <code>.dockerignore</code><br>
B) <code>.gitignore</code><br>
C) <code>ignore.compose</code><br>
D) <code>exclude.txt</code></p>

<p><strong>9) Quel ordre est généralement recommandé dans un Dockerfile Python pour profiter du cache ?</strong><br>
A) Copier tout le code puis installer les dépendances<br>
B) Installer les dépendances après avoir lancé l’app<br>
C) Copier <code>requirements.txt</code>, installer, puis copier le reste du code<br>
D) Ne jamais utiliser de cache</p>

<p><strong>10) Quelle commande démarre des services via Compose (v2) ?</strong><br>
A) <code>docker start</code><br>
B) <code>docker compose up</code><br>
C) <code>docker build compose</code><br>
D) <code>docker run compose</code></p>

<p><strong>11) Dans Compose, la section <code>services:</code> sert à…</strong><br>
A) Définir les conteneurs/applications à exécuter (web, db, etc.)<br>
B) Définir des permissions Linux sur l’hôte<br>
C) Définir les commits Git<br>
D) Définir le pare-feu de Windows</p>

<p><strong>12) Quel est l’avantage principal d’un réseau Compose (par défaut) entre services ?</strong><br>
A) Les services peuvent se joindre par nom (ex. <code>db</code>) via DNS interne<br>
B) Les services sont obligés d’utiliser IPv6<br>
C) Les services partagent automatiquement le disque dur<br>
D) Les services deviennent publics sur Internet automatiquement</p>

<hr>

<h3>PARTIE 3 — Flask : c’est quoi et pourquoi (13–18)</h3>

<p><strong>13) Flask est principalement…</strong><br>
A) Un framework Java pour microservices<br>
B) Un micro-framework web Python basé sur WSGI<br>
C) Un serveur de base de données<br>
D) Un outil de conteneurisation</p>

<p><strong>14) Dans quel cas Flask est souvent un bon choix ?</strong><br>
A) Un petit site web, une API simple, un prototype rapide<br>
B) Un GPU driver<br>
C) Un système d’exploitation<br>
D) Une application mobile native Android</p>

<p><strong>15) Dans Flask, à quoi sert un “route” (ex. <code>@app.route("/ping")</code>) ?</strong><br>
A) À compresser les réponses HTTP<br>
B) À associer une URL à une fonction Python (endpoint)<br>
C) À créer un conteneur Docker<br>
D) À lancer un notebook</p>

<p><strong>16) Pourquoi une application Flask dans Docker doit écouter sur <code>0.0.0.0</code> ?</strong><br>
A) Pour ne répondre qu’aux requêtes internes<br>
B) Pour être accessible depuis l’extérieur du conteneur (via port publié)<br>
C) Pour activer TLS automatiquement<br>
D) Pour installer pip</p>

<p><strong>17) Flask “en production” est généralement servi par…</strong><br>
A) Un serveur WSGI (ex. gunicorn) derrière un reverse proxy<br>
B) Un compilateur C++<br>
C) Un navigateur web<br>
D) Un driver audio</p>

<p><strong>18) Quel risque est le plus associé au mode debug en production ?</strong><br>
A) L’app devient plus jolie<br>
B) Exposition d’informations sensibles et comportements dangereux<br>
C) L’app devient plus rapide<br>
D) Les routes disparaissent</p>

<hr>

<h3>PARTIE 4 — FastAPI : c’est quoi et pourquoi (19–24)</h3>

<p><strong>19) FastAPI est principalement…</strong><br>
A) Un framework web Python moderne orienté API, basé sur ASGI<br>
B) Un plugin Docker officiel<br>
C) Une base de données relationnelle<br>
D) Un outil de monitoring</p>

<p><strong>20) Quel avantage typique de FastAPI (par rapport à Flask) est souvent cité ?</strong><br>
A) Documentation automatique (OpenAPI/Swagger) et validation via types (Pydantic)<br>
B) Nécessite Java<br>
C) Fonctionne uniquement sur Windows XP<br>
D) N’a pas besoin de routes</p>

<p><strong>21) Pour exécuter FastAPI en production, on utilise souvent…</strong><br>
A) Un serveur ASGI (ex. uvicorn) éventuellement derrière un reverse proxy<br>
B) Un serveur FTP<br>
C) Un compilateur Rust<br>
D) Un lecteur PDF</p>

<p><strong>22) Dans FastAPI, à quoi sert un “model” Pydantic ?</strong><br>
A) À rendre les pages HTML plus jolies<br>
B) À valider/structurer les données d’entrée/sortie (schemas)<br>
C) À créer un volume Docker<br>
D) À chiffrer le disque dur</p>

<p><strong>23) Dans quel cas FastAPI est particulièrement adapté ?</strong><br>
A) API REST/JSON, microservices, besoin de validation stricte, docs automatiques<br>
B) Montage vidéo After Effects<br>
C) Jeux 3D AAA<br>
D) Système BIOS</p>

<p><strong>24) Pourquoi dit-on que FastAPI est “ASGI” ?</strong><br>
A) Parce qu’il n’utilise jamais HTTP<br>
B) Parce qu’il est conçu pour un serveur ASGI et supporte des patterns modernes (async)<br>
C) Parce qu’il remplace Dockerfile<br>
D) Parce qu’il supprime les dépendances</p>

<hr>

<h3>PARTIE 5 — Streamlit : c’est quoi et pourquoi (25–30)</h3>

<p><strong>25) Streamlit sert principalement à…</strong><br>
A) Déployer des VM sur AWS<br>
B) Construire rapidement des applications web de data/ML (dashboards) en Python<br>
C) Compiler du C<br>
D) Administrer des comptes Linux</p>

<p><strong>26) Un cas d’usage typique de Streamlit est…</strong><br>
A) Un tableau de bord de KPI, démo ML, interface d’analyse de données<br>
B) Un serveur DNS<br>
C) Une base de données<br>
D) Un pare-feu matériel</p>

<p><strong>27) Dans un conteneur, quel réglage est souvent nécessaire pour rendre Streamlit accessible ?</strong><br>
A) <code>--server.address=0.0.0.0</code><br>
B) <code>--server.address=127.0.0.1</code><br>
C) <code>--server.address=localhost-only</code><br>
D) <code>--server.address=none</code></p>

<p><strong>28) Quel port Streamlit utilise le plus souvent par défaut ?</strong><br>
A) 80<br>
B) 443<br>
C) 8501<br>
D) 22</p>

<p><strong>29) Dans une architecture “API + UI”, quel montage est le plus courant ?</strong><br>
A) Streamlit (UI) appelle une API (Flask/FastAPI) via HTTP<br>
B) Flask appelle Streamlit pour créer des conteneurs<br>
C) Docker remplace Python<br>
D) L’UI n’a pas besoin d’API</p>

<p><strong>30) Quelle bonne pratique est la plus correcte pour les secrets (API keys) en conteneur ?</strong><br>
A) Les écrire en dur dans le code Python<br>
B) Les mettre dans l’image Docker au build<br>
C) Les passer via variables d’environnement / secrets (sans les committer)<br>
D) Les publier dans les logs pour déboguer</p>
