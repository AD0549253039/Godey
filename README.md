# Verdant

Farm-to-door grocery storefront.

```
frontend/   static site (index.html, styles.css, script.js, assets/)
backend/    Express + TypeScript + Prisma (PostgreSQL) API
```

Express serves the `frontend/` folder and the API from the same origin
(`http://localhost:3000`), so there is no CORS setup in development.

## Run it locally

```bash
# 1. Start Postgres (or point DATABASE_URL at a hosted one such as Neon)
docker compose up -d

# 2. Install and configure the backend
cd backend
npm install
cp .env.example .env

# 3. Create tables and load starter data
npx prisma migrate dev --name init
npx prisma db seed

# 4. Start the server
npm run dev
# open http://localhost:3000
```

## API (so far)

| Method | Path | Purpose |
|---|---|---|
| GET | `/api/health` | Liveness check |
| GET | `/api/categories` | Aisles with live item counts |
| GET | `/api/products?category=&q=&featured=` | List / filter / search products |
| GET | `/api/products/:slug` | One product |
| GET | `/api/delivery/check?zip=11215` | Is this ZIP in a delivery zone? |

Prices are returned in cents (`priceCents`); the frontend formats them.

## Roadmap

1. Auth (register / login / `me`) with httpOnly cookies
2. Basket (guest cart that merges on login), wired to the "Add" buttons and "Basket · N"
3. Delivery slots (2pm cutoff, 2-hour windows), orders and payments
4. Admin area and image uploads
