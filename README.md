# SwiftShip Global — Transport & Logistics Website

A full-featured logistics and transport website with Firebase Authentication and Firestore backend integration.

## 🔥 Firebase Project

- **Project:** swiftship-d8b13
- **Auth domain:** swiftship-d8b13.firebaseapp.com
- **Firebase mode:** **LIVE** (real Firebase Auth + Firestore enabled)

---

## 🚀 Pages & Entry Points

| URL | Description |
|-----|-------------|
| `index.html` | Public-facing logistics landing page |
| `admin/login.html` | Admin login (Firebase Auth) |
| `admin/index.html` | Protected admin dashboard (redirect to login if unauthenticated) |

---

## ✅ Implemented Features

### Public Website (`index.html`)
- Sticky navbar with mobile hamburger menu
- Hero section with animated counters
- Features strip (Worldwide / Certified / 24/7 / Insured)
- About section with experience badge
- Services grid (Sea, Air, Road, Rail, Warehousing, Customs)
- Why Choose Us with animated progress bars
- Stats/counters (animated on scroll)
- Projects portfolio with hover overlays
- **Shipment Tracking** — enter tracking ID for step-by-step status
- **Request a Quote form** — validated, anti-spam, saves to Firestore
- **Contact Us form** — validated, anti-spam, saves to Firestore
- Team section
- Partners strip
- Footer with newsletter

### Admin Login (`admin/login.html`)
- Firebase Email/Password authentication
- Password show/hide toggle
- Remember email (localStorage)
- Forgot password → sends Firebase reset email
- Anti-spam: honeypot + timing check
- Auto-redirect if already signed in

### Admin Dashboard (`admin/index.html`)
- 🔒 **Protected by Firebase Auth guard** (redirects to login if not authenticated)
- Dashboard overview: KPI cards + status chart + mode chart + recent shipments
- **Shipment CRUD** — create, view, edit, delete with auto-generated tracking IDs
- Quote requests management (view details, update status, delete)
- Contact messages management (mark read/unread, view, delete)
- Tracking lookup with step-by-step timeline
- Settings: account info, change password, Firebase project info
- Responsive sidebar with mobile overlay
- Pagination on all tables

---

## 🔑 Getting Started

### 1. Enable Email/Password Auth
In Firebase Console:
`Authentication → Sign-in method → Email/Password → Enable`

### 2. Create Admin User
In Firebase Console:
`Authentication → Users → Add user`

Then use those credentials to sign in at `admin/login.html`.

### 3. Create Firestore Collections
The app will auto-create these collections when data is first submitted:
- `shipments`
- `quotes`
- `contacts`

### 4. Firestore Security Rules (Recommended)
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /shipments/{docId} {
      allow read: if true;           // public tracking
      allow write: if request.auth != null; // admin only
    }
    match /quotes/{docId} {
      allow create: if true;         // public form submission
      allow read, update, delete: if request.auth != null;
    }
    match /contacts/{docId} {
      allow create: if true;         // public form submission
      allow read, update, delete: if request.auth != null;
    }
  }
}
```

---

## 📂 File Structure

```
index.html               ← Public logistics website
css/
  style.css              ← Full responsive stylesheet
js/
  firebase-config.js     ← Firebase config + data layer (LIVE mode ON)
  main.js                ← Navbar, counters, scroll animations, tracking form
  forms.js               ← Quote & contact form logic + validation
  tracking.js            ← Shipment tracking module
admin/
  login.html             ← Firebase Auth login page
  login.css              ← Login page styles
  index.html             ← Protected admin dashboard
  admin.css              ← Dashboard stylesheet
  admin.js               ← Dashboard logic (CRUD, charts, modals)
README.md
```

---

## 🧪 Demo Tracking IDs (pre-seeded)

| Tracking ID | Status |
|-------------|--------|
| SWG-DEMO001ABC | In Transit (Sea Freight, NY → London) |
| SWG-DEMO002XYZ | Customs Clearance (Air Freight, Shanghai → Frankfurt) |
| SWG-DEMO003DEL | Delivered (Sea Freight, Dubai → Toronto) |

---

## 🌐 To Go Live

Use the **Publish tab** to deploy your website. All Firebase functionality will work immediately as the project is connected to real Firebase.
