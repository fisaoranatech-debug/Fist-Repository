# PLAY & CHILL 🎮

Plateforme web complète pour salle de jeux vidéo avec réservations, tournois et boutique en ligne.

## Vue d'ensemble

PLAY & CHILL est une plateforme moderne permettant :
- ✅ **Réservations** de PC Gaming, consoles, Sim Racing
- ✅ **Tournois** avec brackets et classements
- ✅ **Boutique en ligne** avec livraison
- ✅ **Système de fidélité** partagé
- ✅ **Dashboard administrateur** complet
- ✅ **Authentification sécurisée** avec JWT

## Architecture

```
PLAY & CHILL
  ├── apps/web (Client public - Next.js)
  ├── apps/admin (Dashboard admin - Next.js)
  ├── apps/api (Backend API - Next.js API routes)
  ├── packages/database (Prisma + migrations)
  ├── packages/auth (JWT + authentification)
  └── packages/ui (Composants partagés)
```

## Stack technique

- **Frontend** : Next.js 14+, React 18+, TypeScript, Tailwind CSS
- **Backend** : Next.js API Routes, Node.js
- **Database** : PostgreSQL 16 + Prisma ORM
- **Auth** : JWT, bcrypt/argon2
- **DevOps** : Docker Compose, npm workspaces

## Installation (Windows)

### Prérequis

1. **Node.js** (v18+) : https://nodejs.org/
   - Installer Node.js LTS
   - Vérifier : `node --version` et `npm --version`

2. **Docker Desktop** (Windows) : https://www.docker.com/products/docker-desktop/
   - Installer et démarrer Docker Desktop
   - Vérifier : `docker --version` et `docker compose --version`

3. **Git** : https://git-scm.com/
   - Installer Git Bash ou utiliser la ligne de commande native

### Étapes d'installation

#### 1️⃣ Cloner le repository

```bash
git clone https://github.com/fisaoranatech-debug/Fist-Repository.git
cd Fist-Repository
```

#### 2️⃣ Installer les dépendances

```bash
npm install
```

#### 3️⃣ Créer le fichier `.env`

```bash
copy .env.example .env
```

Ou sur PowerShell :

```powershell
Copy-Item .env.example -Destination .env
```

Le `.env` utilise les paramètres par défaut Docker Compose.

#### 4️⃣ Démarrer PostgreSQL avec Docker

```bash
docker compose up -d
```

Vérifier que la base de données est prête :

```bash
docker compose logs postgres
```

Vous devriez voir : `database system is ready to accept connections`

#### 5️⃣ Créer les tables (Prisma)

```bash
npm run db:migrate
```

Cela créera automatiquement toutes les tables selon le schéma Prisma.

#### 6️⃣ Charger les données de démonstration

```bash
npm run db:seed
```

Cela va insérer :
- 1 `SUPER_ADMIN` et 1 `ADMIN`
- Équipements de démonstration
- Tarifs
- Produits et zones de livraison
- Utilisateurs de test

#### 7️⃣ Démarrer le serveur de développement

Terminal 1 - Site client (port 3000) :

```bash
cd apps/web
npm run dev
```

Terminal 2 - Dashboard admin (port 3001) :

```bash
cd apps/admin
npm run dev
```

Ou depuis la racine (avec Turbo) :

```bash
npm run dev
```

### Accéder au site

- **Site client** : http://localhost:3000
- **Dashboard admin** : http://localhost:3001
- **Prisma Studio** (consulter/modifier les données) : `npm run db:studio`

## Commandes utiles

```bash
# Consulter les données sans SQL
npm run db:studio

# Réinitialiser la base (attention : supprime tout)
npm run db:reset

# Créer une nouvelle migration après modification du schéma
npm run db:migrate

# Vérifier l'état de PostgreSQL
docker compose logs postgres

# Arrêter PostgreSQL
docker compose down

# Arrêter et supprimer les données
docker compose down -v
```

## Comptes de test

Après `npm run db:seed` :

### Admin
- **Email** : admin@playandchill.mg
- **Mot de passe** : admin123
- **Rôle** : ADMIN

### Super Admin
- **Email** : superadmin@playandchill.mg
- **Mot de passe** : superadmin123
- **Rôle** : SUPER_ADMIN

### Client
- **Email** : client@playandchill.mg
- **Mot de passe** : client123
- **Rôle** : CLIENT

## Structure des dossiers

```
play-and-chill/
├── apps/
│   ├── web/                 # Client public (Next.js)
│   ├── admin/               # Dashboard admin (Next.js)
│   └── api/                 # API Backend (Next.js API routes)
├── packages/
│   ├── database/            # Prisma schema & migrations
│   ├── auth/                # JWT + authentification
│   └── ui/                  # Composants Tailwind partagés
├── docs/
│   └── API.md               # Documentation API
├── docker-compose.yml
├── .env.example
├── package.json
├── turbo.json
└── README.md
```

## Documentation API

Voir [docs/API.md](./docs/API.md) pour les endpoints détaillés.

## Phases de développement

### Phase 1 ✅ MVP
- [x] Accueil + équipements + tarifs
- [x] Réservation
- [x] Compte client
- [x] Authentification
- [x] Dashboard admin
- [x] PostgreSQL + Prisma

### Phase 2 🔄 Tournois
- [ ] Tournois
- [ ] Inscriptions
- [ ] Matchs & brackets
- [ ] Classements

### Phase 3 🛒 Boutique
- [ ] Catalogue produits
- [ ] Panier
- [ ] Commande & livraison
- [ ] Gestion du stock
- [ ] Suivi de commande

### Phase 4 📢 Engagement
- [ ] Live
- [ ] Actualités
- [ ] Notifications
- [ ] Fidélité partagée
- [ ] Promotions

### Phase 5 💳 Avancé
- [ ] Paiements en ligne
- [ ] Mobile Money
- [ ] PWA
- [ ] Notifications temps réel
- [ ] Statistiques avancées

## Variables d'environnement

Voir `.env.example` pour la liste complète. Les principales :

```env
DATABASE_URL          # Connexion PostgreSQL
AUTH_SECRET           # Clé JWT secrète
NEXT_PUBLIC_APP_URL   # URL du site (client)
NEXT_PUBLIC_API_URL   # URL de l'API
```

## Sécurité

- ✅ Mots de passe hashés (bcrypt/argon2)
- ✅ JWT pour authentification
- ✅ Validation serveur de toutes les opérations
- ✅ Protection des routes admin
- ✅ Logs d'audit
- ✅ Variables sensibles dans `.env` (jamais commitées)

## Troubleshooting

### Erreur : `ECONNREFUSED` (base de données)

```bash
# Vérifier que Docker est en cours d'exécution
docker compose ps

# Redémarrer PostgreSQL
docker compose restart postgres

# Ou réinitialiser
docker compose down && docker compose up -d
```

### Erreur : `ENOMEM` sur Windows (Docker manque de ressources)

1. Ouvrir Docker Desktop
2. Aller dans **Settings > Resources**
3. Augmenter **Memory** à au moins 4 Go
4. Redémarrer Docker

### Erreur : `port 5432 already in use`

```bash
# Arrêter le conteneur existant
docker compose down

# Ou libérer le port (si PostgreSQL local l'utilise)
lsof -i :5432  # (sur WSL/Linux)
netstat -ano | findstr :5432  # (sur PowerShell Windows)
```

### Prisma/Migration échoue

```bash
# Vérifier la connexion à la base
npm run db:studio

# Réinitialiser (attention : perte de données)
npm run db:reset
```

## Contribution

1. Créer une branche pour votre feature : `git checkout -b feature/ma-feature`
2. Committer : `git commit -m "feat: description"`
3. Pousser : `git push origin feature/ma-feature`
4. Ouvrir une Pull Request

## Licence

Ce projet est sous licence propriétaire PLAY & CHILL.

---

**Besoin d'aide ?** Consultez la [documentation API](./docs/API.md) ou posez une question en issue.
