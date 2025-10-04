# GoCart – PERN E-commerce Platform

[![Built with Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)](https://nextjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon-336791?logo=postgresql)](https://neon.tech/)
[![Stripe Enabled](https://img.shields.io/badge/Payments-Stripe-635BFF?logo=stripe)](https://stripe.com/)
[![Deploys on Vercel](https://img.shields.io/badge/Deploy-Vercel-000000?logo=vercel)](https://vercel.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license)

---

## Overview

GoCart is a production-grade, multi-role e-commerce platform powered by the PERN stack. It delivers a seamless experience for customers, sellers, and administrators with secure authentication, scalable architecture, real-time dashboards, and integrated payments. The project emphasizes enterprise-ready coding practices, modular design, and modern DevOps workflows suitable for showcasing on professional portfolios.

### Project Summary

- Full-stack E-commerce solution engineered with PostgreSQL, Express.js, React/Next.js, and Node.js (PERN).
- Implements production best practices including SSR-first rendering, modular APIs, and resilient middleware for a seamless shopping experience.
- Demonstrates mastery in secure authentication, relational data modeling, payment integrations, asynchronous workflows, and performance-focused UI engineering.

### Key Concepts & Building Blocks

1. **RESTful API Design:** Modular endpoints for products, users, stores, orders, ratings, coupons, and cart flows under `app/api`.
2. **Authentication & Authorization:** Clerk session management paired with custom middleware (`middlewares/authAdmin.js`, `middlewares/authSeller.js`) to enforce role-based access.
3. **Relational Database Modeling:** Prisma schema defining users, stores, products, orders, order items, ratings, addresses, and coupons, optimized for referential integrity.
4. **State Management:** Redux Toolkit slices (`lib/features/**`) managing cart, product, rating, and address workflows in tandem with Next.js components.
5. **Server-Side Rendering & Routing:** Next.js App Router delivering SEO-friendly pages with client hydration for dynamic interactions.
6. **Image & Asset Management:** ImageKit integration for uploads, transformations, and CDN delivery plus curated assets in `assets/`.
7. **Payment Integration:** Stripe checkout sessions, webhooks, and refunds to power secure transactions end to end.
8. **Event Scheduling:** Inngest functions automating coupon expiry, inventory sync, and order notifications.
9. **Responsive UI & UX:** TailwindCSS-driven design ensuring accessibility and responsiveness across devices.
10. **Security Practices:** Environment-based secrets, input validation, error handling, audit logging, and RBAC enforcement throughout the stack.
11. **Scalable Architecture:** Modular folder structure, reusable components, and clearly separated concerns to support future expansion.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Testing](#testing)
- [CI/CD](#cicd)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [Troubleshooting & FAQ](#troubleshooting--faq)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Features

- 🔐 **Clerk-powered authentication** with role-based access control for Admin, Seller, and Customer personas.
- 🛒 **End-to-end commerce**: product catalog, inventory controls, cart, checkout, and order tracking.
- 💳 **Stripe integration** for secure payments, refunds, and webhook-driven order state changes.
- 🧾 **Coupon management** including automated expiry handled via Inngest scheduled functions.
- 🏪 **Store onboarding workflow**: seller applications, admin approvals, and store dashboards.
- 🖼️ **ImageKit integration** for image uploads, optimization, and responsive delivery.
- 📈 **Analytics dashboards** for admin/store roles with charts and KPIs.
- 🔄 **Redux Toolkit** state slices for cart, product, rating, and address management.
- ⚙️ **Prisma ORM** with Neon PostgreSQL for relational data, indexes, and cascading relations.
- 🚀 **Next.js App Router** leveraging SSR-first rendering with client hydration optimizations.
- 🧠 **OpenAI-enhanced experiences** (e.g., store assistant / smart suggestions).
- 📬 **In-app notifications & modals** (address modal, rating modal) for improved UX.
- 🔒 **Audit logging & monitoring hooks** for admin insight and compliance readiness.

---

## Tech Stack

| Layer | Technologies |
| ----- | ------------ |
| Frontend | Next.js 15, React 18, TypeScript-ready setup, TailwindCSS, Redux Toolkit, Clerk, Stripe.js, ImageKit SDK |
| Backend | Node.js 20, Express-style Next.js route handlers, Prisma ORM |
| Database | PostgreSQL (Neon with connection pooling) |
| Async / Jobs | Inngest (coupon expiry, inventory sync, order notifications) |
| Auth & Security | Clerk, RBAC middleware, Prisma guards, environment-based secrets |
| Payments & Media | Stripe, ImageKit |
| AI | OpenAI SDK |
| Tooling | ESLint, Prettier, Git, Vercel, Postman |

---

## Architecture

![photo_2025-10-04_23-08-09](https://github.com/user-attachments/assets/0e89789f-66d2-4724-807b-1fc70212ef36)


## Project Structure

```
GoCart/
├── app/                      # Next.js app router pages (public, admin, store)
│   ├── (public)/             # Customer-facing flows
│   ├── admin/                # Admin dashboards
│   ├── store/                # Seller dashboards
│   └── api/                  # Route handlers (REST-style endpoints)
├── components/               # Reusable UI components (client/server)
│   ├── admin/                # Admin dashboard components
│   └── store/                # Seller dashboard components
├── lib/                      # Prisma client, Redux slices, store setup
├── configs/                  # Third-party client configs (ImageKit, OpenAI)
├── middlewares/              # Auth guards (admin, seller)
├── inngest/                  # Inngest client + scheduled functions
├── prisma/                   # Prisma schema and migrations
├── assets/                   # Static images & asset registry
├── .env.example              # (Recommended) environment template
└── package.json
```

---

## Getting Started

### Prerequisites
- Node.js ≥ 18
- pnpm / npm / yarn
- PostgreSQL database (Neon recommended)
- Stripe, Clerk, ImageKit, OpenAI accounts

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/<your-user>/GoCart.git
cd GoCart

# 2. Install dependencies
npm install
# or
pnpm install

# 3. Generate Prisma client
npm run postinstall

# 4. Create environment file
cp .env.example .env
# fill in secrets (see Configuration)
```

### Database Setup

```bash
# Push Prisma schema to database
npx prisma db push

# Optional: seed data script (if available)
# npx prisma db seed
```

### Run Locally

```bash
npm run dev
# Visit http://localhost:3000
```

---

## Usage

### 1. Customer Journey
- Browse `/` landing page, view categories, add products to cart.
- Checkout via Stripe, manage addresses via AddressModal component.
- Track orders under `/orders`.

### 2. Seller Journey
- Apply for store at `/create-store`.
- Manage products `/store/manage-product`, add new inventory `/store/add-product`.
- Monitor store analytics `/store`.

### 3. Admin Journey
- Review store applications `/admin/approve`.
- Manage coupons `/admin/coupons`.
- View platform analytics `/admin`.

### Example: Creating a Product (Seller)

````http
POST /api/store/product
Content-Type: application/json
Authorization: Bearer <Clerk JWT>

{
	"name": "Wireless Headphones",
	"description": "Noise-cancelling, 30h battery life",
	"price": 129.99,
	"stock": 50,
	"images": ["https://ik.imagekit.io/.../headphones.webp"],
	"categories": ["Headphones"]
}
````

Response:

````json
{
	"product": {
		"id": "prod_123",
		"status": "active",
		"storeId": "store_abc",
		"createdAt": "2025-05-01T10:00:00.000Z"
	}
}
````

---

## API Documentation

| Endpoint | Method | Description | Auth |
| -------- | ------ | ----------- | ---- |
| `/api/products` | GET | List products with filters | Public |
| `/api/products` | POST | Create product (seller) | Seller |
| `/api/store/create` | POST | Submit store application | Authenticated |
| `/api/admin/stores` | GET | List all stores | Admin |
| `/api/admin/approve-store` | POST | Approve/reject store | Admin |
| `/api/admin/coupon` | POST | Create coupon | Admin |
| `/api/coupon` | POST | Apply coupon during checkout | Authenticated |
| `/api/orders` | POST | Create order via Stripe session | Authenticated |
| `/api/orders` | GET | List customer orders | Authenticated |
| `/api/store/orders` | GET | Seller order dashboard | Seller |
| `/api/rating` | POST | Submit product rating | Authenticated |
| `/api/store/ai` | POST | OpenAI-powered store assistant | Authenticated |

> Use Clerk-issued JWT in `Authorization: Bearer <token>` header for protected routes.

---

## Configuration

Create [`.env`](.env ) with the following keys (never commit secrets):

```
# Public configuration
NEXT_PUBLIC_CURRENCY_SYMBOL=$
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=<clerk_publishable_key>

# Server-only secrets
DATABASE_URL=<postgres_connection_string>
DIRECT_URL=<postgres_direct_connection>
CLERK_SECRET_KEY=<clerk_secret_key>
STRIPE_SECRET_KEY=<stripe_secret_key>
STRIPE_WEBHOOK_SECRET=<stripe_webhook_secret>
IMAGEKIT_PUBLIC_KEY=<imagekit_public>
IMAGEKIT_PRIVATE_KEY=<imagekit_private>
IMAGEKIT_ENDPOINT=<imagekit_endpoint>
OPENAI_API_KEY=<openai_api_key>
OPENAI_BASE_URL=<optional_custom_endpoint>
ADMIN_EMAIL=<admin_contact_email>
```

> Use `dotenv` or Vercel Environment Variables for secure secret management.

---

## Deployment

1. **Vercel Setup**
	 - Import repository into Vercel dashboard.
	 - Select Next.js framework preset.
	 - Configure environment variables in Vercel project settings.
	 - Enable `Postinstall Command: prisma generate`.

2. **Database**
	 - Provision Neon PostgreSQL instance.
	 - Set `DATABASE_URL` & `DIRECT_URL` in Vercel.

3. **Stripe Webhooks**
	 - Use Vercel Edge Functions or Vercel CLI to forward webhooks:
		 ```bash
		 stripe listen --forward-to https://<vercel-domain>/api/stripe
		 ```

4. **Inngest**
	 - Deploy Inngest functions using `inngest-cli` or managed runtime linking to Vercel deployment.

5. **Domain & SSL**
	 - Configure custom domain at Vercel if required.

---

## Testing

```bash
# Unit & integration tests (add when test suite available)
npm test

# Linting
npm run lint

# Type checking (if TypeScript configured)
npm run typecheck
```

> Add Jest/Playwright suites for comprehensive coverage as future enhancement.

---

## CI/CD

- Integrate **GitHub Actions** (recommended):
	- Workflow: install, lint, test, Prisma migrations check, Vercel deployment.
	- Example jobs: `ci.yml` with matrix Node versions, caching.

- Suggested pipeline stages:
	1. `build`: `npm ci && npm run lint`
	2. `test`: `npm test -- --coverage`
	3. `deploy`: Trigger Vercel deployment on main branch merges.

---

## Contributing

1. Fork the repository & create feature branch.
2. Ensure code conforms to ESLint/Prettier configuration.
3. Write/update Prisma schema migrations if database changes.
4. Include documentation updates for new features.
5. Open a pull request with clear summary and screenshots where relevant.

```
git checkout -b feature/amazing-update
git commit -m "feat: add amazing update"
git push origin feature/amazing-update
```

---

## Roadmap

- [ ] Comprehensive Jest/Playwright test coverage.
- [ ] GraphQL gateway for mobile clients.
- [ ] Real-time order status via WebSockets.
- [ ] Multi-language support & localization.
- [ ] Automated email notifications using Inngest + third-party provider.
- [ ] Enhanced AI assistant for personalized recommendations.
- [ ] Advanced analytics using data warehouse (BigQuery/Redshift).

---

## Troubleshooting & FAQ

| Issue | Fix |
| ----- | --- |
| Prisma `P2003` foreign key errors | Ensure Clerk user exists before creating store; validate `userId`. |
| Images not displaying | Confirm ImageKit credentials and verify upload folder permissions. |
| Stripe webhook failing | Reconfigure webhook secret and ensure endpoint path matches `/api/stripe`. |
| Admin routes returning 401 | Verify `ADMIN_EMAIL` matches Clerk user email and auth middleware returns correct role. |
| Build errors about assets | Check [`assets/assets.js`](assets/assets.js ) for duplicate imports; ensure each asset exported once. |

---

## License

Distributed under the MIT License.

All rights reserved by **Koushik Biswas © 2025**.

---

## Acknowledgements

- [Next.js](https://nextjs.org/) for the application framework.
- [Prisma](https://www.prisma.io/) ORM.
- [Clerk](https://clerk.com/) for authentication.
- [Stripe](https://stripe.com/) for payments.
- [ImageKit](https://imagekit.io/), [Inngest](https://www.inngest.com/), and [OpenAI](https://openai.com/) for integrations.
- UI inspiration from modern commerce platforms and Tailwind community designs.

---

> For questions or demo requests, feel free to reach out via issues or discussions.
