# Deploy Guide

Deploy the backend API on **Render** and the React dashboard on **Vercel** (or deploy both together on Render).

## Option 1: Vercel (Frontend) + Render (API)

### 1. Deploy the API on Render

1. Go to [dashboard.render.com](https://dashboard.render.com) → **New** → **Blueprint**
2. Connect your GitHub account and select `varsha-kotegar/NEXORA`
3. Render reads `render.yaml` automatically — click **Apply**
4. Optional: add `DATABASE_URL` with a [Neon](https://neon.tech) Postgres connection string (if omitted, the build uses the CSV fallback)
5. Copy your Render service URL (e.g. `https://nexora-api.onrender.com`)

### 2. Deploy the Dashboard on Vercel

1. Go to [vercel.com/new](https://vercel.com/new) and import `varsha-kotegar/NEXORA`
2. Set **Root Directory** to `web`
3. Add environment variable:
   - `VITE_API_URL` = `https://nexora-api.onrender.com`
4. Click **Deploy** and copy your Vercel URL (e.g. `https://nexora.vercel.app`)

### 3. Configure CORS

In your Render service **Environment** settings, set `CORS_ORIGINS` to your Vercel URL (e.g. `https://nexora.vercel.app`) and redeploy.

## Option 2: Single-Service Deploy on Render

`render.yaml` also builds `web/` and serves the static frontend from FastAPI at `/`, with API docs at `/docs` and health check at `/health`.

> **Note:** Render free tier sleeps after ~15 min of inactivity. First request may take ~30s.

## Verify after deploy

```powershell
curl https://YOUR-API-URL/health
curl https://YOUR-API-URL/api/metrics/summary
```
