# 🏛️ Lakuplete — System Architecture & Implementation Documentation

**Lakuplete** is an enterprise-grade private register of capacity, built as a full-stack, modular API/service marketplace. This document serves as the comprehensive technical specification, file directory guide, data contract reference, and setup manual.

---

## 📐 System Architecture Overview

* **Frontend Layer**: Built using React & TypeScript with zero hardcoded visual styles. Powered by unified Design Tokens (`tokens.ts`), persisted theme context (`ThemeProvider.tsx`), and custom state stores (`Zustand/React`).
* **Backend Layer**: Node.js & Express API server operating as a single-port architecture serving static public assets alongside RESTful API endpoints. Fully configured for HTTPS production environments and secure session handling.
* **Authentication**: Google OAuth 2.0 Authorization Code flow delivering stateless `httpOnly` JWT session cookies for secure cross-platform authentication across Web and Mobile (Expo).
* **Database & Persistence**: SQLite storage engine using `better-sqlite3` providing low-latency atomic operations and custom seed automation capabilities.

---

## 📁 Repository Directory Structure

```text
lakuplete/
├── public/                             ← Static Frontend Assets (Web Client)
│   ├── index.html
│   ├── styles.css
│   ├── app.js
│   └── assets/
│       └── icon.png
│
├── server/                             ← Express API Server Backend
│   ├── server.js                       ← Main HTTPS/HTTP Server Entry Point
│   ├── auth.js                         ← JWT Cookie Signer & Session Middleware
│   ├── .env.example
│   ├── package.json
│   ├── db/
│   │   ├── index.js                    ← SQLite Connection Handler
│   │   ├── schema.sql                  ← SQL DDL Definitions
│   │   ├── seed.js                     ← 12-Service Core Seed Script
│   │   └── seed_250.js                 ← 250+ Multi-Catalog Service Generator
│   └── routes/
│       ├── auth.js                     ← Google OAuth Flow Endpoints
│       ├── entries.js                  ← Public & Filtered Registry Service Routes
│       ├── inquiries.js                ← User Inquiry Management (Protected)
│       └── stats.js                    ← Dashboard Aggregations Endpoint
│
└── lakuplete-frontend/                 ← Shared Component Library & State Engine
    ├── package.json
    ├── tsconfig.json
    ├── README.md
    └── src/
        ├── index.ts
        ├── types.ts                    ← System TypeScript Interfaces
        ├── config.ts
        ├── theme/                      ← Design System Tokens & Context
        │   ├── tokens.ts
        │   ├── ThemeProvider.tsx
        │   └── index.ts
        ├── lib/                        ← Formatting, Helper Functions & Keyframe Injections
        │   ├── format.ts
        │   ├── entries.ts
        │   ├── css.ts
        │   ├── apiClient.ts
        │   └── storage.ts
        ├── store/                      ← Shared State Management Stores
        │   ├── authStore.ts
        │   ├── browseStore.ts
        │   ├── inquiriesStore.ts
        │   └── index.ts
        ├── hooks/                      ← React Data Hooks & Server Caching Logic
        │   ├── useServerCache.ts
        │   ├── useAuth.ts
        │   ├── useEntries.ts
        │   ├── useEntry.ts
        │   ├── useStats.ts
        │   ├── useInquiries.ts
        │   ├── useCreateInquiry.ts
        │   └── index.ts
        └── components/                 ← Enterprise UI Component System
            ├── index.ts
            ├── Text.tsx
            ├── Button.tsx
            ├── Input.tsx
            ├── Card.tsx
            ├── Badge.tsx
            ├── Feedback.tsx
            ├── Layout.tsx
            ├── Modal.tsx
            ├── Toast.tsx
            └── domain/                 ← Business Logic & Feature Components
                ├── EntryCard.tsx
                ├── EntryList.tsx
                ├── StatsRow.tsx
                ├── CategoryChips.tsx
                ├── InquiryList.tsx
                └── SignInGate.tsx
