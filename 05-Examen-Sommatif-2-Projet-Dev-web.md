# Projet — Application Web complète (Front Streamlit + Back Flask/FastAPI) + Docker

## Objectif
Réaliser une application complète en **2 parties** :

- **Front (obligatoire)** : une interface **Streamlit** (UI).
- **Back (obligatoire)** : une API **FastAPI** ou **Flask** (au choix de l’étudiant).
- **Déploiement (obligatoire)** : conteneurisation avec **Docker** (idéalement **Docker Compose**).

## Liberté de thème
Le sujet est au choix (ex. gestion d’inventaire, mini-CRM, suivi d’habitudes, bibliothèque, suivi de dépenses, suivi d’entraînement, gestion de tickets, catalogue de produits, etc.).  
**Important :** le projet doit s’inspirer du projet vu en classe (mêmes principes : UI séparée, API REST, échanges JSON, persistance, tests de base).

---

## 01 — Exigences minimales

### A) Architecture (2 services)
- **frontend** : Streamlit
- **backend** : Flask **ou** FastAPI

### B) API REST (obligatoire)
- au moins **4 endpoints** (ex. CRUD : Create / Read / Update / Delete)
- échanges en **JSON**
- validation minimale des entrées (champs requis, types, erreurs claires)
- réponses cohérentes (codes HTTP appropriés)

### C) Persistance (obligatoire)
- **SQLite (recommandé)**  
  ou fichier JSON/CSV (si très simple : moins de points)

### D) UI Streamlit (obligatoire)
- au moins **2 pages** (ex. liste + détail / dashboard + formulaire)
- au moins **1 formulaire** (création ou mise à jour)
- affichage clair des résultats + messages d’erreur compréhensibles

### E) Docker (obligatoire)
- un **Dockerfile** pour le front
- un **Dockerfile** pour le back
- un **docker-compose.yml** pour lancer les deux services

---

## 02 — Livrables

### À remettre
Un dépôt Git (ou un dossier compressé) contenant :
- `frontend/` (Streamlit)
- `backend/` (Flask ou FastAPI)
- `docker-compose.yml`
- `README.md` (installation, exécution, ports, endpoints, captures)

### Captures obligatoires
- preuve que Compose tourne : sortie de `docker compose ps`
- UI Streamlit fonctionnelle (page(s) + données affichées)
- au moins **2 appels API** (ex. navigateur / curl / Postman) avec résultat visible

---

## 03 — Contraintes techniques (qualité minimale)
- **Ports** : Streamlit sur `8501`, API sur `8000` (ou `5000` si Flask), clairement indiqués dans le README.
- **Connexion UI → API** : l’UI appelle l’API via HTTP (ex. `requests`).
- **Configuration** : l’URL du backend est configurable (ex. variable d’environnement `BACKEND_URL`).
- **Gestion d’erreurs** : si l’API est indisponible ou renvoie une erreur, l’UI affiche un message clair.

---

## Grille d’évaluation (100 points)

| Critère | Description | Points |
|---|---|---:|
| **A — Architecture & séparation Front/Back** | Deux services distincts (Streamlit + API), appels HTTP, structure de projet claire, configuration (URL backend). | **15** |
| **B — Backend (Flask ou FastAPI)** | API REST complète : au moins 4 endpoints, logique métier cohérente, validation des entrées, réponses JSON correctes (codes HTTP). | **25** |
| **C — Persistance des données** | Stockage fonctionnel (SQLite recommandé) : création, lecture, mise à jour, suppression. Données cohérentes et durables. | **15** |
| **D — Frontend Streamlit (UI)** | Au moins 2 pages, affichage des données, formulaire(s), UX claire, gestion des erreurs (messages utilisateurs). | **20** |
| **E — Docker & Docker Compose** | 2 Dockerfiles + Compose fonctionnel : build et run sans erreur, ports exposés, réseau entre services, variables d’environnement. | **15** |
| **F — Documentation & preuves** | README clair (prérequis, exécution, endpoints, exemples), captures demandées, instructions reproductibles. | **10** |
| **Total** |  | **100** |

---

## Bonus (jusqu’à +10 points)
- **+3** : tests simples (pytest) ou script de vérification des endpoints
- **+3** : pagination / filtrage / recherche côté API
- **+2** : authentification simple (token ou login basique) sans exposer de secrets
- **+2** : qualité UX Streamlit (navigation propre, mise en page claire, messages soignés)

---

## Pénalités (exemples)
- **-10** : pas de Docker Compose fonctionnel
- **-10** : UI Streamlit qui ne communique pas réellement avec l’API
- **-5** : absence de persistance (tout reste en mémoire)
- **-5** : README incomplet (reproduction impossible)
