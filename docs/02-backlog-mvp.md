# Backlog Produit — EasySearch (MVP Sur-Mesure)

## Sprint 1 — Socle Backend + Interface de Suivi (Sync Excel)
*Objectif : Voir toutes tes candidatures actuelles dans une vraie interface web, modifier les statuts et ajouter des candidatures spontanées.*

### US-01 : Importer et synchroniser `Suivi_Stages_AMOA_Dimitri.xlsx`
**En tant que** Dimitri,
**je veux** retrouver toutes les lignes de mon fichier Excel actuel dans EasySearch (et pouvoir ré-exporter en Excel),
**afin de** ne rien perdre de mon suivi déjà commencé.
- **Priorité :** Must
- **Critères d'acceptation :**
  - Toutes les colonnes actuelles (`ID Offre`, `Entreprise`, `Secteur`, `Intitulé du Poste`, `Statut`, `Date`, `Notes`, etc.) sont affichées.
  - Les statuts exacts (`À postuler`, `Postulé en attente`, `Relancé`, `Entretien`, `Refusé`, `Ne me concerne pas`) sont conservés.

### US-02 : Vue Kanban & Tableau filtrable (Offres + Spontanées)
**En tant que** Dimitri,
**je veux** basculer entre une vue Kanban par statut et une vue Tableau, et filtrer par type (`Offre` / `Candidature spontanée`),
**afin de** piloter facilement mes deux stratégies (réponse à offres + prospection janvier).
- **Priorité :** Must
- **Critères d'acceptation :**
  - On peut changer le statut d'une candidature en 1 clic.
  - Un badge distingue clairement les `Offres` des `Candidatures spontanées`.

### US-03 : Ajout rapide (JobTeaser / Kompass / Spontanée)
**En tant que** Dimitri,
**je veux** un bouton « + Nouvelle candidature / cible » rapide,
**afin de** saisir en 15 secondes une offre vue sur JobTeaser Lyon 1 ou une entreprise repérée sur Kompass.
- **Priorité :** Must
- **Critères d'acceptation :**
  - Permet de choisir `Offre` ou `Spontanée`.
  - Champs : Entreprise, Secteur, Poste visé, Lien/Contact, Statut, Date, Notes.

---

## Sprint 2 — Bouton « Lancer la veille » + Relances + Stats
*Objectif : Piloter `pipeline.py` depuis l'interface, trier les nouvelles offres et gérer les relances.*

### US-04 : Lancer `pipeline.py` depuis l'interface Web
**En tant que** Dimitri,
**je veux** cliquer sur un bouton « Lancer la recherche » dans EasySearch pour exécuter mon script Python (et voir les logs/résultats),
**afin de** ne plus avoir à ouvrir le terminal.
- **Priorité :** Must
- **Critères d'acceptation :**
  - Le bouton déclenche le script sans bloquer l'interface.
  - Les nouvelles offres trouvées apparaissent dans un onglet « Boîte de tri » (statut `À trier` / `À postuler`).
  - En 1 clic sur chaque offre : **Garder (`À postuler`)** ou **Écarter (`Ne me concerne pas`)**.

### US-05 : Alertes de relance à J+7 & Modèles de mail
**En tant que** Dimitri,
**je veux** voir en haut du tableau toutes les candidatures en `Postulé en attente` depuis 7 jours ou plus, avec un bouton « Copier le mail de relance »,
**afin de** relancer systématiquement et augmenter mon taux de réponse.
- **Priorité :** Must
- **Critères d'acceptation :**
  - Calcul automatique du nombre de jours depuis `Date`.
  - Génération d'un texte de relance personnalisé + passage en statut `Relancé` en 1 clic.

### US-06 : Mini-Dashboard Stats & Raccourcis Annuaires
**En tant que** Dimitri,
**je veux** voir mes chiffres clés (taux de réponse, candidatures par semaine, par source) et avoir mes liens directs (JobTeaser Lyon 1, Kompass, Labos, Talent's Emploi, APEC),
**afin d'** avoir un vrai cockpit complet au quotidien.
- **Priorité :** Should

---

## Sprint 3 — Nouvelles sources & Déploiement Cloud gratuit
*Objectif : Ajouter France Travail / WTTJ dans `pipeline.py` et déployer l'interface en ligne.*

### US-07 : Enrichir `pipeline.py` (France Travail API, WTTJ, etc.)
**En tant que** Dimitri,
**je veux** ajouter de nouvelles sources fiables dans le pipeline,
**afin de** rater un minimum d'offres sur Lyon / Auvergne-Rhône-Alpes.
- **Priorité :** Should

### US-08 : Déploiement gratuit (Vercel + Supabase)
**En tant que** Dimitri,
**je veux** héberger l'interface en ligne gratuitement,
**afin de** consulter mon suivi depuis n'importe où et pouvoir montrer l'appli en entretien.
- **Priorité :** Could (Phase 2)

### US-09 : Détection automatique des réponses dans les e-mails (IMAP + Gemini)
**En tant que** Dimitri,
**je veux** un bouton / tâche qui scanne mes e-mails récents liés aux entreprises en statut `Postulé` ou `Relancé`, détecte les refus explicites ou les délais implicites (*« sans réponse sous 2 semaines… »*), et propose/applique la mise à jour vers `Refusé` ou `Entretien`,
**afin de** garder mon tableau propre sans trier mes mails à la main.
- **Priorité :** Should (Sprint 3)
