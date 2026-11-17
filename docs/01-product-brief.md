# Product Brief — EasySearch (Cockpit de Recherche de Stage)

> **Rôle du document :** Poser la vision du produit avant de développer. Ce document reflète l'architecture sur-mesure connectée à ton pipeline Python existant.

---

## 1. Le problème
Aujourd'hui, le suivi se fait dans un fichier Excel (`Suivi_Stages_AMOA_Dimitri.xlsx`) alimenté par un script Python (`pipeline.py`). Ça fonctionne, mais :
- un fichier Excel n'est pas pratique pour trier vite, gérer les relances et suivre les candidatures spontanées ;
- il faut lancer le script à la main dans un terminal ;
- il manque une vue claire sur *qui a répondu*, *qui relancer* et *les statistiques* ;
- certaines sources clés (JobTeaser Lyon 1, Kompass, annuaires de labos/entreprises santé, France Travail, WTTJ) ne sont pas encore centralisées au même endroit.

## 2. La cible
**Outil interne sur-mesure** pour Dimitri (MIAGE Polytech Lyon — recherche de stage M1 mai–août en AMOA / Chef de projet SI / Consultant fonctionnel, puis alternance/stage M2).
*Note CV/GitHub : le code reste générique et propre pour être présentable sur GitHub (avec `.env` et données personnelles ignorés via `.gitignore`).*

## 3. Les statuts métier (alignés avec ton Excel)
- `À postuler` *(offres validées ou entreprises ciblées en attente d'envoi)*
- `Postulé en attente` *(candidature envoyée, en attente de retour)*
- `Relancé` *(relance effectuée à J+7)*
- `Entretien` *(processus de recrutement en cours)*
- `Offre / Accepté` *(proposition reçue)*
- `Refusé` *(retour négatif)*
- `Ne me concerne pas` *(offres écartées lors du tri)*

---

## 4. Périmètre : MVP vs Évolutions

### Inclus dans le MVP (Phase 1 — Local sur ton PC)
1. **Import / Sync Excel** : Lecture et écriture compatibles avec `Suivi_Stages_AMOA_Dimitri.xlsx` (tu ne perds aucune donnée existante).
2. **Tableau de bord unifié (Kanban + Tableau)** :
   - Gestion des **Offres classiques** (LinkedIn, Indeed, HelloWork, etc.) **ET** des **Candidatures spontanées** (type `Offre` vs `Spontanée`).
   - Changement de statut en 1 clic.
3. **Lanceur du Pipeline Python depuis l'interface** :
   - Un bouton « Lancer la veille » exécute `pipeline.py` (avec ta clé Gemini 3.5 Lite et ta déduplication existante).
   - Boîte de tri rapide des nouvelles offres trouvées (*À postuler* / *Ne me concerne pas*).
4. **Moteur de relances & Stats** :
   - Alerte automatique sur les candidatures `Postulé en attente` depuis ≥ 7 jours.
   - Modèle de mail de relance pré-rempli en 1 clic.
   - KPIs : total envoyées, taux de réponse, répartition par canal / type.
5. **Hub de raccourcis & Annuaires** :
   - Liens pré-filtrés en 1 clic : JobTeaser Lyon 1, Kompass, annuaires labos/santé, Talent's Emploi, APEC, WTTJ.
   - Formulaire « Ajout rapide » (pour coller une offre JobTeaser ou une entreprise Kompass en 10 secondes).

### Phase 2 — Élargissement des sources & Mise en ligne (Serveur gratuit)
- **Nouvelles sources automatisées** dans `pipeline.py` : API officielle **France Travail**, **Welcome to the Jungle**, test de **APEC / Meteojob / Talent's Emploi**.
- **Hébergement gratuit** : Base de données **Supabase** (PostgreSQL gratuit) + Interface web sur **Vercel** ou **Render** pour y accéder depuis n'importe où.
- **Automatisation GitHub Actions** *(à tester prudemment)* : Utile pour les APIs officielles (France Travail), mais les IPs cloud sont souvent bloquées par LinkedIn/Indeed (d'où l'intérêt de garder aussi le lancement local).

---

## 5. Architecture technique
- **Backend / API locale (Phase 1)** : FastAPI (Python) — communique directement avec `pipeline.py`, l'Excel et une base SQLite locale.
- **Frontend** : React + Vite (ou Next.js) — interface moderne, rapide, facile à déployer ensuite sur Vercel.
