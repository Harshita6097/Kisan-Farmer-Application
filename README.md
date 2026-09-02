<div align="center">

# 🌾 Kisan — Farmer Assistance App

**Empowering Indian farmers with real-time market intelligence, AI-assisted crop disease detection, and smart inventory management.**

[![React Native](https://img.shields.io/badge/React_Native-0.81-61DAFB?style=flat-square&logo=react)](https://reactnative.dev)
[![Expo](https://img.shields.io/badge/Expo-54-000020?style=flat-square&logo=expo)](https://expo.dev)
[![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=flat-square&logo=node.js)](https://nodejs.org)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=flat-square&logo=supabase)](https://supabase.com)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

</div>

---

## Overview

Kisan is a full-stack mobile application designed to bridge the information gap for Indian farmers. It provides live mandi (market) prices sourced from [data.gov.in](https://data.gov.in), AI-driven price predictions, crop disease diagnosis, stock inventory tracking, and eco-friendly residue pickup management — all in one place.

---

## Repository Structure

```
Kisan-Farmer-Application/
├── app-backend/        # Node.js + Express REST API
│   ├── src/
│   │   ├── config/     # Supabase client setup
│   │   ├── cron/       # Scheduled price sync job
│   │   ├── middleware/ # JWT authentication
│   │   ├── routes/     # API route handlers
│   │   └── services/   # Business logic (data.gov.in, predictions)
│   ├── supabase/       # Database schema (SQL)
│   └── server.js       # App entry point
│
└── app-frontend/       # Expo React Native mobile app
    ├── src/
    │   ├── navigation/ # Stack & tab navigators
    │   ├── screens/    # All app screens
    │   ├── services/   # API client & SQLite
    │   └── styles/     # Colors & shared styles
    └── App.js          # App entry point
```

---

## Features

| Module | Highlights |
|---|---|
| 🔐 **Auth & Onboarding** | Splash screen, onboarding carousel, phone + OTP login |
| 🏠 **Home Dashboard** | Personalized greeting, weather widget, farming tips, quick actions |
| 🔬 **Disease Detection** | Camera/gallery capture, crop form, AI diagnosis, treatment cost estimates |
| 📊 **Market Analysis** | Live mandi prices, search & filter, best-price highlighting |
| 📈 **Price Prediction** | Moving average trend engine, risk assessment, expert sell/hold advice |
| 💼 **Stock Management** | Crop inventory CRUD, total value calculation, multi-crop support |
| ♻️ **Residue Management** | Eco-pickup booking, request history, status tracking |

---

## Tech Stack

### Frontend
| Technology | Purpose |
|---|---|
| Expo (React Native) | Cross-platform mobile framework |
| React Navigation | Stack & bottom tab navigation |
| Expo SQLite | Local persistent storage |
| Expo Image Picker | Camera & gallery access |
| AsyncStorage | Lightweight key-value storage |
| @expo/vector-icons | MaterialIcons icon set |

### Backend
| Technology | Purpose |
|---|---|
| Node.js + Express | REST API server |
| Supabase (PostgreSQL) | Cloud database with RLS |
| data.gov.in API | Live mandi price data source |
| node-cron | Scheduled daily price sync |
| Supabase Auth | JWT-based authentication |

---

## Getting Started

### Prerequisites
- Node.js ≥ 18
- Expo CLI (`npm install -g expo-cli`)
- A [Supabase](https://supabase.com) project
- A [data.gov.in](https://data.gov.in) API key

### 1. Clone the repository
```bash
git clone https://github.com/Harshita6097/Kisan-Farmer-Application.git
cd Kisan-Farmer-Application
```

### 2. Set up the backend
```bash
cd app-backend
cp .env.example .env        # Fill in your credentials
npm install
npm run dev
```

### 3. Set up the frontend
```bash
cd app-frontend
npm install
npm start                   # Scan QR with Expo Go
```

> See [`app-backend/README.md`](app-backend/README.md) and [`app-frontend/README.md`](app-frontend/README.md) for detailed setup instructions.

---

## Architecture

```
Mobile App (Expo)
      │
      ▼
Express REST API  ──────►  Supabase (PostgreSQL)
      │                          ▲
      ▼                          │
data.gov.in API  ──── cron ──────┘
(daily price sync)
```

---

## Roadmap

- [ ] Real ML model for crop disease detection
- [ ] Live weather API integration
- [ ] Push notifications for price alerts
- [ ] Multilingual support (Hindi, Punjabi, Marathi)
- [ ] Farmer community & social features
- [ ] Real OTP authentication backend

---

## License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">
  Made with ❤️ for Indian Farmers
</div>
