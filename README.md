# Al-Amanah Frontend

A modern web frontend for the Al-Amanah management system, built with Next.js, React, TypeScript, and Tailwind CSS.

## Overview

The Al-Amanah frontend provides the user interface for managing members, profiles, transactions, receipts, FDRs, notifications, reports, settings, roles, permissions, activity logs, and related administrative workflows.

The application communicates with the Laravel REST API backend deployed on Railway.

## Tech Stack

- Next.js
- React
- TypeScript
- Tailwind CSS
- Redux Toolkit / RTK Query
- ESLint

## Main Features

- User authentication and logout
- Role-based access and permission-aware UI
- User and member profile management
- Transactions and payment management
- Payment collection and receipt handling
- Receipt photo upload and verification workflows
- FDR management
- Meeting expense management
- Notifications
- Dashboard and transaction reports
- Application settings
- Profile sharing / linked accounts
- Activity logs
- Responsive interface

## Project Structure

```text
Al-Amanah_Frontend/
├── app/                 # Next.js application routes and pages
├── components/          # Reusable UI components
├── lib/                 # API client, utilities, navigation, roles, translations
├── public/              # Static assets
├── next.config.ts       # Next.js configuration
├── package.json         # Dependencies and scripts
├── package-lock.json    # npm lockfile
└── .env.example         # Environment variable example
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Sharar12/Al-Amanah_Frontend.git
cd Al-Amanah_Frontend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a local `.env.local` file based on `.env.example`:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api
```

For production, point the variable to the deployed Laravel API:

```env
NEXT_PUBLIC_API_URL=https://al-amanahbackend-backenddatabase.up.railway.app/api
```

Do not commit `.env.local` or other files containing secrets.

### 4. Run the development server

```bash
npm run dev
```

Then open:

```text
http://localhost:3000
```

## Production Deployment

The frontend is deployed on Vercel and connects to the Laravel backend hosted on Railway.

### Frontend

```text
https://al-amanah-frontend-mqgp8m5d6-sharar12s-projects.vercel.app
```

### Backend API

```text
https://al-amanahbackend-backenddatabase.up.railway.app/api
```

### Authentication API

```text
POST /api/login
```

## Environment Variables

| Variable | Purpose |
|---|---|
| `NEXT_PUBLIC_API_URL` | Base URL of the Laravel API |

Because `NEXT_PUBLIC_API_URL` is exposed to browser-side code by Next.js, it should contain only the public API base URL and never database credentials or server secrets.

## API Integration

API requests are centralized in `lib/api.ts` using Redux Toolkit Query. The client automatically attaches the stored Bearer token to authenticated requests when available.

Example production API base URL:

```text
https://al-amanahbackend-backenddatabase.up.railway.app/api
```

## Available Scripts

```bash
npm run dev       # Start development server
npm run build     # Create production build
npm run start     # Start production server
npm run lint      # Run ESLint
```

## Deployment Architecture

```text
                    Internet
                       │
                       ▼
              ┌──────────────────┐
              │ Next.js Frontend │
              │     Vercel       │
              └────────┬─────────┘
                       │ HTTPS
                       ▼
              ┌──────────────────┐
              │ Laravel Backend  │
              │     Railway      │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │  MySQL Database  │
              │     Railway      │
              └──────────────────┘
```

## Repository

```text
https://github.com/Sharar12/Al-Amanah_Frontend
```

## Notes

- Keep the frontend API URL environment-specific.
- Do not place Laravel `.env` contents in the frontend repository or Vercel environment variables.
- Keep backend/database credentials and other private secrets on the Laravel/Railway side.
- If the backend API URL changes, update `NEXT_PUBLIC_API_URL` in Vercel and redeploy the frontend.
