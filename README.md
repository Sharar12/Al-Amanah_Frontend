# Al-Amanah — Frontend

A modern, role-based financial management frontend for the **Al-Amanah** application. The frontend is built with **Next.js, React, TypeScript, Tailwind CSS, Redux Toolkit, and RTK Query**, and communicates with the Al-Amanah Laravel API.

## Overview

The application provides separate workflows for administrators, accounts staff, and members. It includes authentication, role-based navigation, financial transaction management, receipts, reports, expenses, notifications, settings, and member profile features.

### Main Areas

- **Admin** — dashboard, users & members, billing & demands, receipts, reports, expenses, settings, activity logs, and FDR management.
- **Accounts** — accounts dashboard, receipts, billing & demands, financial reports, expenses, FDRs, and notifications.
- **Member** — personal dashboard, subscriptions & receipts, financial reports, profile, and notifications.
- **Public** — public-facing pages and shared UI.

The navigation and authorization logic are implemented on the frontend with role-aware guards and helpers for roles such as `super_admin`, `admin`, and `accountant`.

## Tech Stack

| Technology | Purpose |
| --- | --- |
| [Next.js](https://nextjs.org/) 16 | React framework and application routing |
| [React](https://react.dev/) 19 | UI development |
| [TypeScript](https://www.typescriptlang.org/) | Static typing |
| [Tailwind CSS](https://tailwindcss.com/) 4 | Styling and responsive UI |
| [Redux Toolkit](https://redux-toolkit.js.org/) | Global application state |
| [RTK Query](https://redux-toolkit.js.org/rtk-query/overview) | API communication and server-state caching |
| [React Hook Form](https://react-hook-form.com/) | Form handling |
| [Zod](https://zod.dev/) | Schema validation |
| [Lucide React](https://lucide.dev/) | Icons |

## Key Features

### Authentication & Authorization

- Login, logout, and current-user (`me`) handling.
- Bearer-token authentication through the API layer.
- Protected application areas with authentication guards.
- Role-based navigation and access control.
- Permission-aware transaction management.

### Financial Management

- Transaction listing with filters and pagination.
- Create, update, and delete transactions.
- Generate recurring or one-time payment demands.
- Collect full or partial payments.
- Receipt photo upload and rejection workflows.
- Batch receipt processing.
- Receipt management.
- Transaction reports and dashboard statistics.
- Meeting expense management.
- FDR investment section.

### Administration

- User/member management.
- Role and permission management.
- Admin payment permissions.
- Application settings.
- Activity log viewing.
- Profile sharing / linked-account management.

### Member & Accounts Experience

- Dedicated dashboards for different user roles.
- Member financial history and subscription information.
- Financial reports and receipts.
- Notifications and read/unread state.
- Member profile management.

### Internationalization & UI

- Translation/localization support through dedicated translation files and language context.
- Reusable layouts and shared UI components.
- Responsive dashboard and data-management interfaces.
- Printable report, receipt, and expense views.

## Project Structure

```text
Al-Amanah_Frontend/
├── app/
│   ├── (public)/          # Public-facing pages
│   ├── admin/             # Admin routes
│   ├── accounts/          # Accounts routes
│   ├── dashboard/         # Dashboard-related routes
│   ├── login/             # Authentication entry point
│   ├── member/            # Member routes
│   ├── globals.css
│   └── layout.tsx
│
├── components/
│   ├── public/            # Public UI components
│   ├── *-layout.tsx       # Role/application layouts
│   ├── auth-guard.tsx     # Authentication protection
│   ├── role-gate.tsx      # Role-based rendering/access
│   ├── pagination.tsx     # Shared pagination
│   ├── providers.tsx      # Application providers
│   ├── receipt-*.tsx      # Receipt viewing/printing utilities
│   ├── report-print.tsx   # Report printing
│   └── expense-print.tsx  # Expense printing
│
├── lib/
│   ├── api.ts             # RTK Query API endpoints
│   ├── nav.ts             # Role-aware navigation configuration
│   ├── roles.ts           # Role and permission helpers
│   ├── schemas.ts         # Validation schemas
│   ├── translations.ts    # Application translations
│   ├── member-translations.ts
│   ├── site-data.ts       # Public/site data
│   └── utils.ts            # Shared utilities
│
├── store/
│   ├── index.ts           # Redux store configuration
│   └── authSlice.ts       # Authentication state
│
├── types/                 # Shared TypeScript types
├── public/                # Static assets
├── .env.example           # Environment variable template
├── next.config.ts
├── postcss.config.mjs
├── eslint.config.mjs
├── package.json
└── README.md
```

## API Integration

The frontend uses **Redux Toolkit Query** for backend communication. The API base URL is read from:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api
```

When a token is available, the API layer automatically sends it as a Bearer token:

```http
Authorization: Bearer <token>
```

The current API module covers authentication, users, roles, permissions, transactions, receipts, reports, expenses, FDRs, notifications, settings, payment permissions, profile shares, and activity logs.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Sharar12/Al-Amanah_Frontend.git
cd Al-Amanah_Frontend
```

### 2. Install dependencies

Using npm:

```bash
npm install
```

Or using pnpm:

```bash
pnpm install
```

### 3. Configure environment variables

Create a local environment file:

```bash
cp .env.example .env.local
```

On Windows PowerShell, you can create/copy the file manually if `cp` is unavailable.

Set the API URL in `.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api
```

Use the URL of your deployed Laravel backend when running against a production API.

### 4. Start the development server

```bash
npm run dev
```

Then open:

```text
http://localhost:3000
```

## Available Scripts

```bash
npm run dev      # Start the development server
npm run build    # Create a production build
npm run start    # Start the production server
npm run lint     # Run ESLint
```

## Production Build

Create a production build with:

```bash
npm run build
```

Then start the production server with:

```bash
npm run start
```

For deployment, the project can be hosted on platforms that support Next.js, including Vercel. Make sure the production environment contains the correct `NEXT_PUBLIC_API_URL` value for the Laravel backend.

## Backend

The frontend is designed to work with the Al-Amanah Laravel backend:

**Backend repository:** https://github.com/Sharar12/Al-Amanah_Backend

The backend is responsible for the API, authentication, business logic, persistence, and database operations. This repository contains the **frontend only**.

## Development Notes

- Keep secrets and environment-specific values out of Git; use `.env.local` for local configuration.
- The frontend expects the backend API to expose the routes consumed by `lib/api.ts`.
- Authentication and role checks are handled in the frontend for UX and route protection; backend authorization should remain the final security boundary.
- Reusable shared logic should generally live in `components/`, `lib/`, `store/`, or `types/` rather than being duplicated inside route files.

## License

This project is distributed under the license included in the repository.

<!-- README refresh: documentation-only change. -->
