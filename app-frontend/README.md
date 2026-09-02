<div align="center">

# Kisan — Mobile App (Frontend)

**Expo React Native app for the Kisan farmer assistance platform.**

[![Expo](https://img.shields.io/badge/Expo-54-000020?style=flat-square&logo=expo)](https://expo.dev)
[![React Native](https://img.shields.io/badge/React_Native-0.81-61DAFB?style=flat-square&logo=react)](https://reactnative.dev)
[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20iOS-lightgrey?style=flat-square)](https://expo.dev)

</div>

---

## Overview

The Kisan mobile app gives farmers access to live mandi prices, AI-assisted crop disease detection, stock inventory management, and residue pickup booking — all through a clean, intuitive interface built with Expo and React Navigation.

---

## Project Structure

```
app-frontend/
├── App.js                          # Root component, DB initialisation
├── app.json                        # Expo config
├── src/
│   ├── navigation/
│   │   ├── AppNavigator.js         # Root stack (Splash → Onboarding → Login → Tabs)
│   │   ├── TabNavigator.js         # Bottom tab bar
│   │   ├── DiseaseNavigator.js     # Disease detection stack
│   │   ├── MarketNavigator.js      # Market & stocks stack
│   │   └── ResidueNavigator.js     # Residue management stack
│   ├── screens/
│   │   ├── SplashScreen.js
│   │   ├── OnboardingScreen.js
│   │   ├── LoginScreen.js
│   │   ├── HomeScreen.js
│   │   ├── disease/
│   │   │   ├── CaptureScreen.js    # Camera / gallery image capture
│   │   │   ├── FormScreen.js       # Crop details form
│   │   │   └── ResultScreen.js     # AI diagnosis result
│   │   ├── market/
│   │   │   ├── MarketScreen.js     # Live mandi prices
│   │   │   ├── PricePredictionScreen.js
│   │   │   └── MyStocksScreen.js
│   │   └── residue/
│   │       ├── BookPickupScreen.js
│   │       └── ViewRequestsScreen.js
│   ├── services/
│   │   ├── api.js                  # Axios client for backend API
│   │   └── db.js                   # Expo SQLite service
│   └── styles/
│       ├── colors.js               # App-wide color palette
│       └── commonStyles.js         # Reusable StyleSheet definitions
```

---

## Navigation Flow

```
Splash
  └── Onboarding
        └── Login
              └── Tab Navigator
                    ├── Home
                    ├── Disease  →  Capture → Form → Result
                    ├── Market   →  Prices / Prediction / My Stocks
                    └── Residue  →  Book Pickup / View Requests
```

---

## Setup

### Prerequisites
- Node.js ≥ 18
- Expo Go app on your Android or iOS device (or an emulator)

### Install and run

```bash
cd app-frontend
npm install
npm start
```

Then scan the QR code with **Expo Go**, or press:
- `a` — Android emulator
- `i` — iOS simulator
- `w` — Web browser

### Connect to the backend

Update the base URL in `src/services/api.js` to point to your running backend:

```js
const BASE_URL = 'http://<your-local-ip>:5000/api';
```

> Use your machine's local network IP (not `localhost`) when testing on a physical device.

---

## Key Implementation Details

### Local Database (SQLite)
- Disease detection history is stored locally via Expo SQLite
- Persists across app sessions without requiring a network connection

### API Integration
- `src/services/api.js` wraps all backend calls (mandi prices, predictions, stocks, residue)
- Falls back gracefully when the backend is unreachable

### Styling
- Green-themed UI (`src/styles/colors.js`) designed for outdoor readability
- Shared `commonStyles.js` keeps component styles consistent across screens

---

## Roadmap

- [ ] Real OTP authentication with Supabase Auth
- [ ] Live weather API on the home dashboard
- [ ] Push notifications for price alerts
- [ ] Multilingual support (Hindi, Punjabi, Marathi)
- [ ] Real ML model for disease detection
- [ ] Farmer community feed

---

<div align="center">
  Made with ❤️ for Indian Farmers
</div>
