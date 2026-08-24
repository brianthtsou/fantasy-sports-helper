# fantasy-sports-helper

A personal tool for managing a Yahoo Fantasy Sports league. Django + Django REST Framework backend (using [yfpy](https://github.com/uberfastman/yfpy) to talk to Yahoo's Fantasy Sports API), React frontend.

## Project layout

```
backend/    Django project (uv-managed)
  config/       settings, urls, wsgi/asgi
  apps/
    accounts/   custom User model
    leagues/    Yahoo league data (WIP)
frontend/   React + TypeScript app (Vite)
```

## Backend setup

Requires [uv](https://docs.astral.sh/uv/).

```
cd backend
cp .env.example .env      # fill in a real DJANGO_SECRET_KEY, and Yahoo creds once you have them
uv sync
uv run python manage.py migrate
uv run python manage.py createsuperuser
uv run python manage.py runserver
```

Run tests with `uv run pytest`.

### Yahoo API access

To call the Yahoo Fantasy Sports API you need your own app registered at the [Yahoo Developer Network](https://developer.yahoo.com/apps/). Create an app, request Fantasy Sports read access, and set its redirect URI to match whatever OAuth callback route you build in `apps/accounts`. Put the resulting client ID/secret in `backend/.env` as `YAHOO_CLIENT_ID` / `YAHOO_CLIENT_SECRET`.

## Frontend setup

Requires Node.

```
cd frontend
npm install
npm run dev
```

Runs at `http://localhost:5173` by default, which is what the backend's CORS/CSRF settings (`FRONTEND_URL` in `backend/.env`) are configured to allow.
