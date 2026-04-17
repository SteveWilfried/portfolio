# Portfolio JS — Stack 100% JavaScript

Conversion complète de PHP+MySQL vers **Node.js + Express + SQLite**.

## Structure du projet

```
portfolio-js/
├── server/
│   ├── index.js              ← Serveur Express (point d'entrée)
│   ├── config.js             ← Configuration (port, chemins, secret)
│   ├── db.js                 ← Base de données SQLite (auto-créée)
│   ├── middleware/
│   │   └── auth.js           ← Protection des routes admin
│   └── routes/
│       ├── api.js            ← API publique (profil, compétences, projets...)
│       └── admin.js          ← API admin (CRUD + upload fichiers)
└── public/
    ├── index.html            ← Page principale (statique + fetch)
    ├── js/
    │   ├── main.js           ← Animations, particules (inchangé)
    │   └── app.js            ← Chargement des données via fetch API
    ├── css/
    │   ├── style.css         ← Styles portfolio (inchangé)
    │   └── admin.css         ← Styles admin (inchangé)
    ├── uploads/              ← Photos, CV uploadés
    └── admin/
        ├── index.html        ← Page de connexion
        ├── dashboard.html    ← Tableau de bord avec stats
        ├── profil.html       ← Modifier profil + photo + CV
        ├── competences.html  ← CRUD compétences
        ├── projets.html      ← CRUD projets + upload image
        ├── parcours.html     ← CRUD parcours
        └── messages.html     ← Consultation des messages de contact
```

## Équivalences PHP → JavaScript

| PHP (ancien)              | JavaScript (nouveau)                  |
|---------------------------|---------------------------------------|
| `includes/config.php`     | `server/config.js`                    |
| `includes/db.php` (MySQL) | `server/db.js` (SQLite)               |
| `includes/functions.php`  | `server/routes/api.js`                |
| `admin/*.php`             | `server/routes/admin.js` + HTML fetch |
| `<?php echo $var; ?>`     | `fetch('/api/...').then(injectDOM)`   |
| `$_SESSION`               | `express-session`                     |
| `move_uploaded_file()`    | `multer`                              |
| `password_hash()`         | `bcryptjs`                            |

## Installation

```bash
# 1. Installer les dépendances
npm install

# 2. Lancer le serveur
npm start

# ou en mode développement (rechargement auto)
npm run dev
```

Le site sera disponible sur **http://localhost:3000**

## Première connexion

- **URL admin** : http://localhost:3000/admin/
- **Email** : votre email (configuré dans db.js)
- **Mot de passe par défaut** : `admin123`

⚠️ Changez le mot de passe dès la première connexion via la page Profil.

## API Routes

### Publiques
| Méthode | Route              | Description              |
|---------|--------------------|--------------------------|
| GET     | `/api/profil`      | Données du profil        |
| GET     | `/api/competences` | Compétences groupées     |
| GET     | `/api/projets`     | Liste des projets        |
| GET     | `/api/parcours`    | Parcours professionnel   |
| POST    | `/api/contact`     | Envoyer un message       |

### Admin (authentification requise)
| Méthode | Route                        | Description            |
|---------|------------------------------|------------------------|
| POST    | `/admin/api/login`           | Connexion              |
| POST    | `/admin/api/logout`          | Déconnexion            |
| GET/PUT | `/admin/api/profil`          | Profil + uploads       |
| GET/POST/PUT/DELETE | `/admin/api/competences/:id` | CRUD compétences |
| GET/POST/PUT/DELETE | `/admin/api/projets/:id`     | CRUD projets     |
| GET/POST/PUT/DELETE | `/admin/api/parcours/:id`    | CRUD parcours    |
| GET/PUT/DELETE | `/admin/api/messages/:id` | Messages contact    |
