<div align="center">

# Kisan — Backend API

**Node.js + Express REST API powering the Kisan farmer assistance platform.**

[![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=flat-square&logo=node.js)](https://nodejs.org)
[![Supabase](https://img.shields.io/badge/Database-Supabase-3ECF8E?style=flat-square&logo=supabase)](https://supabase.com)
[![data.gov.in](https://img.shields.io/badge/Data-data.gov.in-FF6B35?style=flat-square)](https://data.gov.in)

</div>

---

## Overview

The backend handles live mandi price ingestion from [data.gov.in](https://data.gov.in), price trend prediction, crop stock inventory management, and residue pickup request tracking — all backed by a Supabase PostgreSQL database.

---

## Project Structure

```
app-backend/
├── src/
│   ├── config/
│   │   └── supabase.js          # Supabase public + admin clients
│   ├── cron/
│   │   └── priceFetcher.js      # Daily price sync job
│   ├── middleware/
│   │   └── auth.js              # Supabase JWT verification
│   ├── routes/
│   │   ├── mandiPrices.js       # GET mandi prices
│   │   ├── predictions.js       # GET price predictions
│   │   ├── stocks.js            # CRUD crop inventory
│   │   └── residue.js           # Residue pickup management
│   └── services/
│       ├── dataGovService.js    # data.gov.in API client
│       └── predictionService.js # Moving average prediction engine
├── supabase/
│   └── schema.sql               # Full DB schema with RLS policies
├── .env.example
└── server.js                    # App entry point
```

---

## API Reference

### Mandi Prices

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/mandi-prices` | List prices with optional filters (`commodity`, `state`, `market`, `search`) |
| `GET` | `/api/mandi-prices/commodities` | List all unique commodities in the database |
| `GET` | `/api/mandi-prices/:commodity` | Prices for a specific commodity across all markets |

### Price Predictions

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/predictions/:commodity` | Trend-based price forecast with risk level and sell/hold advice |

### Stocks

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/stocks` | Get all stocks for the authenticated user |
| `POST` | `/api/stocks` | Add a new stock entry |
| `PUT` | `/api/stocks/:id` | Update an existing stock |
| `DELETE` | `/api/stocks/:id` | Delete a stock entry |

### Residue Pickups

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/residue/requests` | List all pickup requests |
| `POST` | `/api/residue/pickup` | Book a new residue pickup |

### Utility

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Server health check |
| `POST` | `/api/cron/fetch-prices` | Manually trigger a mandi price sync |

---

## Database Schema

Three tables in Supabase PostgreSQL, all with Row Level Security (RLS) enabled:

| Table | Purpose |
|---|---|
| `mandi_prices` | Cached daily market prices from data.gov.in (unique on `commodity + market + arrival_date`) |
| `user_stocks` | Per-user crop inventory with quantity, unit and purchase price |
| `residue_pickups` | Eco-friendly crop residue pickup requests with status tracking |

Run [`supabase/schema.sql`](supabase/schema.sql) in your Supabase SQL Editor to initialise the schema.

---

## Setup

### 1. Configure environment variables

```bash
cp .env.example .env
```

```env
PORT=5000
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
DATA_GOV_API_KEY=your-data-gov-api-key
DATA_GOV_RESOURCE_ID=9ef84268-d588-465a-a308-a864a43d0070
```

### 2. Install dependencies and start

```bash
npm install
npm run dev       # Development (nodemon)
npm start         # Production
```

### 3. Seed initial market data

```bash
# Linux / macOS
curl -X POST http://localhost:5000/api/cron/fetch-prices

# Windows PowerShell
Invoke-RestMethod -Method Post -Uri http://localhost:5000/api/cron/fetch-prices
```

---

## Scheduled Jobs

The server runs a `node-cron` job every day at **8:00 AM IST** (02:30 UTC) to fetch and upsert up to 1,500 mandi price records from data.gov.in into Supabase.

---

## Prediction Engine

`predictionService.js` uses a weighted moving average over 90 days of historical price data:

- **Short-term trend** — last 7 entries vs. entries 8–30
- **Long-term trend** — last 30 entries vs. entries 31–90
- **Weighted forecast** — 70% short-term + 30% long-term
- **Risk level** — derived from price standard deviation (volatility)
- **Advice** — auto-generated sell/hold recommendation based on trend + risk
