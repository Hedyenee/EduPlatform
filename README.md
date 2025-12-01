📚 EduPlatform API - Cours MERN
🌟 Vue d'ensemble

Ce projet est une API REST pour une plateforme de cours en ligne, démontrant la maîtrise des relations de données dans MongoDB via Mongoose. L'API gère :

Utilisateurs et profils

Cours et inscriptions

Critiques et évaluations

C’est un projet éducatif réalisé par Hedyene Mili pour démontrer la conception d’une architecture RESTful complète et sécurisée.

🎯 Objectifs pédagogiques

Compétences acquises :

Implémentation complète d’un CRUD pour plusieurs ressources

Modélisation et gestion des relations 1:1, 1:N, N:M

Utilisation avancée de Mongoose (populate, références)

Conception d’une architecture RESTful logique

Mise en place d’un système d’authentification JWT

🛠️ Technologies utilisées
Backend

🟢 Node.js - Runtime JavaScript côté serveur

⚡ Express.js - Framework web minimaliste

🍃 MongoDB - Base de données NoSQL

🔗 Mongoose - ODM pour MongoDB

🔐 bcryptjs - Hashage sécurisé des mots de passe

🎫 jsonwebtoken (JWT) - Authentification par tokens

🌍 dotenv - Gestion des variables d’environnement

Outils de développement

📮 Postman / Thunder Client - Tests des API

🔧 Nodemon - Rechargement automatique du serveur

📦 npm - Gestionnaire de paquets

🐙 Git - Contrôle de version

🗂️ Structure du projet
EduPlatform/
├─ server.js
├─ .env
├─ config/
│ └─ db.js
├─ images/
├─ models/
│ ├─ User.js
│ ├─ Profile.js
│ ├─ Course.js
│ └─ Review.js
├─ controllers/
│ ├─ userController.js
│ ├─ profileController.js
│ ├─ courseController.js
│ └─ reviewController.js
├─ routes/
│ ├─ userRoutes.js
│ └─ courseRoutes.js
└─ middleware/
├─ authMiddleware.js
└─ errorMiddleware.js

🚀 Installation

Prérequis : Node.js (v14+), npm ou yarn, Postman

npm install
node server.js

Messages attendus :

✅ MongoDB connected
✅ Server running on port 3000

📊 Architecture des données
Schéma général des relations
USER ↔ PROFILE (1:1)
USER ↔ COURSE (N:M)
COURSE → REVIEW (1:N)

Relations expliquées :

1️⃣ One-to-One (User ↔ Profile)

Chaque utilisateur possède un seul profil.

Référence stockée dans Profile pour plus de flexibilité.

2️⃣ One-to-Many (Course → Reviews)

Un cours peut avoir plusieurs critiques, chaque critique appartient à un seul cours.

Référence stockée côté Review pour éviter les documents volumineux.

3️⃣ Many-to-Many (User ↔ Course)

Un utilisateur peut s’inscrire à plusieurs cours et un cours peut avoir plusieurs étudiants.

Références double : User.courses et Course.students.

Exemple d’inscription bidirectionnelle :

course.students.push(userId);
user.courses.push(courseId);
await course.save();
await user.save();

🔐 Authentification JWT

JWT = JSON Web Token, sécurisé pour transmettre des infos entre client et serveur.

Composé de : Header + Payload + Signature

Protège les routes via un middleware qui vérifie le token.

Exemple :

// Middleware protect
const protect = async (req, res, next) => {
const token = req.headers.authorization?.split(' ')[1];
if(!token) return res.status(401).json({ message: 'Accès refusé' });

const decoded = jwt.verify(token, process.env.JWT_SECRET);
req.userId = decoded.userId;
next();
}

🌐 Endpoints principaux
Auth (public)

POST /api/auth/register → Inscription

POST /api/auth/login → Connexion

Users

GET /api/users/ → Liste utilisateurs

GET /api/users/:id → Détails utilisateur

GET /api/users/:userId/profile → Profil utilisateur (🔒)

GET /api/users/:userId/courses → Cours utilisateur (🔒)

Courses

POST /api/courses → Créer cours (🔒)

GET /api/courses → Liste cours

POST /api/courses/:courseId/enroll → Inscription utilisateur (🔒)

Reviews

POST /api/courses/:courseId/reviews → Ajouter critique (🔒)

🔒 Routes protégées par JWT, ⚪ routes publiques.
