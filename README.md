# 🚌 BusWise — Smart Bus Travel App

Apple-inspired minimal & premium UI for smart bus booking with real-time price comparison and trip expense tracking.

---

## 📁 Project Structure

```
buswise/
├── index.html                     # HTML entry point
├── package.json                   # Dependencies
├── vite.config.js                 # Vite config
└── src/
    ├── main.jsx                   # React root mount
    ├── App.jsx                    # Root router (auth → portal → bus → expense)
    ├── styles.css                 # Global Apple-style CSS (all animations, tokens)
    │
    ├── icons/
    │   └── Icons.jsx              # All SVG icons used in the app
    │
    ├── constants/
    │   └── data.js                # Cities, bus sites, categories, budget
    │
    ├── utils/
    │   └── helpers.js             # generateBusResults(), addRipple(), inr(), today()
    │
    └── components/
        ├── Rpl.jsx                # Ripple-effect button wrapper
        ├── NavBar.jsx             # Sticky top nav with logo + user badge
        ├── AuthScreen.jsx         # Login / Signup + Google & Apple OAuth
        ├── PortalScreen.jsx       # Home dashboard with 2 feature cards
        ├── BusSearchScreen.jsx    # Search form + results with sort
        ├── BusCard.jsx            # Individual bus result card
        ├── BookingPopup.jsx       # Post-booking popup: "Track expenses?"
        └── ExpenseScreen.jsx      # Full trip expense tracker in ₹
```

---

## 🚀 Features

| Feature | Details |
|---|---|
| **Apple UI/UX** | SF Pro-inspired spacing, `#f5f5f7` bg, glass nav, spring animations |
| **Bus Recommender** | Compare redBus · AbhiBus · MakeMyTrip · Goibibo simultaneously |
| **Lowest Price Badge** | AI sorts & highlights cheapest option with green "Lowest 🎉" badge |
| **Booking Popup** | After booking: "Want to track your trip expenses?" with Yes/No |
| **Expense Tracker** | All amounts in ₹ · 7 categories · Budget bar · Smart AI insight |
| **Animations** | fadeUp · popIn · ripple · float · shimmer · barGrow · dotDance |
| **Responsive** | Works on mobile, tablet and desktop |

---

## ⚙️ Setup & Run

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build
```

Then open: [http://localhost:5173](http://localhost:5173)

---

## 🎨 Design Tokens (CSS Variables)

| Variable | Value | Usage |
|---|---|---|
| `--accent` | `#0071e3` | Primary blue (Apple blue) |
| `--green`  | `#30d158` | Success / expense green |
| `--bg`     | `#f5f5f7` | Apple page background |
| `--surface`| `#ffffff`  | Card background |
| `--f`      | Plus Jakarta Sans | Body font |
| `--spring` | cubic-bezier(0.34,1.56,0.64,1) | Spring bounce easing |
| `--out`    | cubic-bezier(0.22,1,0.36,1) | Smooth out easing |

---

## 📦 To Connect Real APIs

In `src/utils/helpers.js`, replace `generateBusResults()` with actual parallel API calls:

```js
// Example: fetch from all 4 platforms in parallel
const [redbus, abhibus, mmt, goibibo] = await Promise.all([
  fetch(`/api/redbus?from=${from}&to=${to}&date=${date}`).then(r => r.json()),
  fetch(`/api/abhibus?from=${from}&to=${to}&date=${date}`).then(r => r.json()),
  fetch(`/api/mmt?from=${from}&to=${to}&date=${date}`).then(r => r.json()),
  fetch(`/api/goibibo?from=${from}&to=${to}&date=${date}`).then(r => r.json()),
]);
return [...redbus, ...abhibus, ...mmt, ...goibibo].sort((a,b) => a.price - b.price);
```
