# AGENTS.md

## Project Overview
Express.js + EJS + MongoDB learning app. Renders server-side views, demonstrates sessions, cookies, and basic CRUD with Mongoose.

## Architecture
- **Entry point**: `bin/www` (standard Express generator server bootstrap, listens on `PORT` env or 3000)
- **App config**: `app.js` — Express setup, view engine (EJS), session middleware, static files, route mounting
- **Routes**: `routes/index.js` (home, cookie/session demos, CRUD endpoints), `routes/users.js` (Mongoose model + DB connection)
- **Views**: `views/index.ejs`, `views/error.ejs`
- **Static assets**: `public/stylesheets/style.css`

## Running in Base44
```
docker compose -f docker-compose.base44.yml up -d --build
```
- **Mongo** runs as a compose service (`mongo:7`); the app connects via `MONGODB_URI` env var.
- **Web** runs `node:22` with the source bind-mounted; uses `nodemon` for live reload on file changes.
- Preview is served on host port 3000.

## Key Notes
- `bin/www` was deleted in the original repo's git history and had to be recreated — `package.json`'s `start` script references it.
- MongoDB connection string is configurable via `MONGODB_URI` env var (defaults to `mongodb://127.0.0.1:27017/amazonDB` for local dev).
- No external secrets or credentials required — MongoDB runs locally in compose.
- No test suite configured.

## Useful Routes
- `/` — home page (renders EJS view)
- `/checkCookie`, `/deleteCookie` — cookie demo
- `/checkSession`, `/removeSession` — session demo
- `/create`, `/allUser`, `/delete` — MongoDB CRUD demo endpoints
