# Système Dynamique d'Intermédiation Académique - Application Full-Stack de Gestion de Stages



##  Description du Projet
Ce projet consiste en la conception et le développement d'une application web Full-Stack dédiée à l'automatisation et à la centralisation de la gestion des stages au sein d'un établissement d'enseignement supérieur (INPT). 

L'application remplace les processus traditionnels manuels (échanges d'e-mails disparates, documents papier) par une plateforme unifiée et sécurisée où interagissent trois profils principaux : les **Étudiants**, les **Entreprises** et l'**Administration**.

---

##  Fonctionnalités Clés par Profil

###  Espace Étudiant
* **Exploration des offres :** Consultation en temps réel des opportunités de stage (1A, 2A, PFE) publiées par les entreprises partenaires.
* **Formulaire de postulation :** Envoi instantané des candidatures avec liens vers le CV (Google Drive/Dropbox) et lettre de motivation.
* **Phase finale :** Dépôt asynchrone du rapport de stage au format PDF pour évaluation.

###  Espace Entreprise
* **Gestion des offres :** Publication et suppression dynamique des opportunités de stage avec ciblage par filière (ex: ASEDS).
* **Suivi du recrutement :** Interface de traitement des candidatures permettant d'accepter ou de refuser un profil en un clic.

###  Espace Administration (Pilotage & Évaluation)
* **Tableau de bord :** Statistiques globales de la promotion en temps réel (nombre d'étudiants inscrits, stages trouvés, conventions en attente).
* **Suivi académique :** Gestion du parcours des étudiants et attribution des notes de soutenance.
* **Gestion contractuelle :** Validation et suivi des signatures des conventions de stage.

---

##  Architecture Technique & Base de Données

L'application repose sur un modèle architectural **Client-Serveur** strict, assurant une séparation nette entre l'interface utilisateur et la logique métier.

### Technologies utilisées
* **Frontend :** HTML5, CSS3 (Flexbox & Grid pour une interface responsive), JavaScript Vanille (ES6+, communication asynchrone via l'API `fetch` pour une expérience de type SPA).
* **Backend :** Node.js avec le framework Express.js pour la construction d'une API RESTful robuste.
* **SGBD :** MySQL (géré localement via la suite XAMPP).

### Modèle Logique de Données (MLD)
La persistance est assurée par un schéma relationnel normalisé comprenant 4 tables principales :
* `USERS` (id, full_name, email, password, role, filiere)
* `OFFERS` (id, title, type, filiere, description, company_name, #company_id)
* `APPLICATIONS` (id, #student_id, #offer_id, status, applied_at)
* `CONVENTIONS` (id, #student_id, company_name, file_path, status, note, signed_at)

---

##  Sécurité et Robustesse Technique

* **Protection contre les Injections SQL :** Utilisation systématique de requêtes préparées (requêtes paramétrées avec le caractère `?` via le pilote MySQL de Node.js).
* **Intégrité Référentielle :** Implémentation de la clause `ON DELETE CASCADE`. La suppression d'une offre par une entreprise nettoie automatiquement toutes les candidatures associées dans la table `applications`.
* **Gestion des Sessions & Contrôles d'Accès :** Utilisation de `sessionStorage` pour maintenir temporairement l'état (ID, Rôle) et adapter dynamiquement l'interface selon les privilèges de l'utilisateur.

---

##  Structure du Dépôt

```text
├── database/
│   └── script.sql          # Script de création des tables et contraintes MySQL
├── backend/
│   ├── server.js           # Serveur Node.js / Express, configuration des routes de l'API REST
│   └── package.json        # Dépendances du projet Backend
└── frontend/
    ├── index.html          # Page d'accès et interface de connexion unique
    ├── style.css           # Feuilles de style responsives (Flexbox/Grid)
    └── script.js           # Logique applicative et requêtes asynchrones (Fetch/AJAX)
