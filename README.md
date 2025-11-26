# Dream-scrapper

# 🧠 Dramed Scrapper — Agent Web Intelligent

Dramed Scrapper est un **agent web intelligent** qui visite des sites web, comprend leur contenu et en extrait automatiquement des informations utiles (nom d’école, contacts, programmes, etc.) sous forme de **fiche structurée**.

---

## 🚀 TL;DR

- 🧭 Va automatiquement sur les sites (navigation headless avec Playwright)  
- 👁️ Comprend la page avec un LLM (type GPT)  
- 🧾 Extrait les infos utiles (mails, adresses, programmes, etc.)  
- 📇 Génère une **fiche synthèse** standardisée (ex : école / organisation)  
- 🌐 Expose tout ça via une **API FastAPI** (`/scrape` et `/results/{id}`)

---

## 🎯 Objectif du projet

Automatiser la recherche d’informations sur des écoles, organisations ou programmes :

- Qui ? → Nom, type, pays, ville  
- Où ? → Site web, adresses  
- Comment contacter ? → Emails, téléphones, pages de contact  
- Que fait l’école ? → Description, domaines  
- Quels programmes ? → Programmes principaux, domaines d’enseignement  
- Comment candidater ? → Liens et résumé des conditions si détectés  

---

## 🧩 Fonctionnement global

1. **Navigation** : un navigateur headless ouvre l’URL, clique sur les liens, scrolle, gère la pagination.
2. **Perception** : un LLM analyse le HTML et détecte le type de page + zones importantes.
3. **Extraction** : le LLM extrait les données demandées selon des instructions (nom, emails, etc.).
4. **Synthèse** : les données sont transformées en **fiche profil** (ex : profil d’école).
5. **Validation** : vérification de la cohérence (structure, champs essentiels).
6. **Stockage / API** : les résultats sont sauvegardés et accessibles via l’API.

---

## 🧱 Architecture (modules)

Le projet est organisé en plusieurs modules indépendants :

- `navigator.py` : navigation web (Playwright)
- `perception_agent.py` : analyse de page (LLM)
- `extractor.py` : extraction des données ciblées
- `strategy_agent.py` : agent stratégique (exploration multi-pages)
- `profile_synthesis.py` : génération de la fiche synthèse (profil école / organisation)
- `validation.py` : vérification des résultats
- `storage.py` : sauvegarde en JSON/CSV
- `server.py` : API FastAPI

---

## 🛠️ Stack technique

- **Langage** : Python 3.11
- **Backend / API** : FastAPI + Uvicorn
- **Navigation web** : Playwright (mode headless)
- **LLM** : modèle accessible via API (OpenAI ou équivalent)
- **Stockage** : fichiers JSON (MVP), extension possible en PostgreSQL/MongoDB

---

## 📁 Structure du projet

```bash
dramed_scrapper/
├── app/
│   ├── __init__.py
│   ├── config.py
│   ├── navigator.py
│   ├── perception_agent.py
│   ├── extractor.py
│   ├── strategy_agent.py
│   ├── profile_synthesis.py
│   ├── validation.py
│   ├── storage.py
│   └── server.py
├── tests/
│   ├── test_navigator.py
│   ├── test_perception.py
│   ├── test_extractor.py
│   └── test_end_to_end.py
├── scripts/
│   ├── run_local_scrape.py
│   └── demo_notebook.ipynb   # (optionnel)
├── data/                     # résultats des runs (créé à l’exécution)
├── requirements.txt
├── README.md
└── .env.example
