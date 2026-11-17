# EasySearch - Cockpit Personnel de Pilotage de Candidatures (CRM & Veille)

> **Note :** EasySearch est un outil interne développé pour un usage personnel (suivi de recherche de stage M1 MIAGE). Ce dépôt présente la démarche produit, le cadrage fonctionnel, le backlog Agile et l'architecture technique du projet.

---

## 1. Contexte & Problème initial
Lors d'une recherche de stage ou d'alternance, le suivi manuel dans un tableur Excel montre vite ses limites :
- Dispersion des offres sur plusieurs plateformes (*LinkedIn, Indeed, HelloWork, Welcome to the Jungle, France Travail, JobTeaser*) ;
- Saisie répétitive et risque d'oubli sur les relances de candidatures spontanées ;
- Difficulté à suivre les retours par e-mail (refus, entretiens, délais de réponse).

**Objectif :** Concevoir un mini-CRM local sur-mesure pour centraliser le suivi, automatiser les tâches répétitives et consacrer plus de temps au ciblage des entreprises et à la préparation des candidatures.

---

## 2. Démarche Product Owner & Sprints réalisés

Le projet a été cadré et découpé en **5 sprints itératifs** (voir [docs/01-product-brief.md](docs/01-product-brief.md) et [docs/02-backlog-mvp.md](docs/02-backlog-mvp.md)) :

### Ce qui a été réalisé (Sprints 1 à 5)
- **Sprint 1 - Socle & Suivi Kanban :**
  - API REST locale (FastAPI) synchronisée en lecture/écriture avec le fichier Excel de suivi existant ;
  - Interface web React/TypeScript avec vue **Kanban** (sans scroll horizontal, masquage des colonnes vides), vue **Tableau**, filtres et fiche détaillée.
- **Sprint 2 - Veille automatisée & Lettres de motivation :**
  - Lancement du pipeline Python multi-sources depuis l'interface avec **barre de progression en direct** (*Indeed, LinkedIn, HelloWork, Welcome to the Jungle, France Travail*) ;
  - Hub de raccourcis vers les portails universitaires et annuaires (JobTeaser, Kompass, APEC, Auvergne-Rhône-Alpes) ;
  - Générateur de **Lettres de Motivation** éditables avec export **PDF A4** (modèle strict basé sur le profil réel, sans invention).
- **Sprint 3 - Suivi Gmail & Règles métier :**
  - Scanner **Gmail** en lecture seule (IMAP par lots de 100 mails sur les 7 derniers jours, Tous les messages + Spams) avec classification IA et secours local Python ;
  - Règles métier différenciées : alertes de relance à `J+7` sur les **candidatures spontanées**, et délai d'expiration (`60 jours` par défaut ou délai extrait par e-mail) sur les **offres classiques**.
- **Sprint 4 - Chasseur de candidatures spontanées :**
  - Ciblage géographique strict (*Lyon & Métropole*), exclusion automatique des entreprises déjà suivies ;
  - Enrichissement via `BeautifulSoup` (vérification du site, page Carrières, e-mail public si disponible) et génération de messages d'approche (e-mail + LinkedIn) copiables en 1 clic.
- **Sprint 5 - Productivité & Mini-BI :**
  - Tri rapide en 1 clic sur la colonne `En attente` (*Postulé* / *Écarter*) et archivage des offres expirées ;
  - Onglet **Stats** (répartition par statut et performance par canal).

### Ce qui a été volontairement écarté / gardé pour plus tard
- **Déploiement cloud public & comptes multi-utilisateurs :** écarté pour garder l'outil 100 % local, maîtriser les coûts d'API et protéger les données personnelles.
- **Scraping des portails authentifiés (JobTeaser / Kompass) :** remplacé par des raccourcis directs en 1 clic et un formulaire d'ajout rapide, par respect des accès authentifiés.

---

## 3. Architecture & Technologies
- **Frontend :** React 18, TypeScript, Vite, Lucide Icons
- **Backend :** Python, FastAPI, Uvicorn, OpenPyXL
- **Automatisation & IA :** `google-genai` (cascade de modèles Gemini avec gestion de quotas), `BeautifulSoup4`, `requests`, `imaplib` (IMAP SSL), Microsoft Edge Headless (export PDF)
- **Gestion de projet :** Product Brief, User Stories (format *En tant que / Je veux / Afin de* + critères d'acceptation), priorisation MoSCoW.
