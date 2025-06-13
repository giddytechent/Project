Giddytech Enterprise – Project Blueprint & Base Concept

## 🚀 Overview

**Giddytech Enterprise** is a **hybrid Nigerian digital platform** that integrates:

1. **An e-commerce store** — selling authentic tech gadgets.
2. **A digital services agency** — offering web design, branding, and IT consulting.

**Goal:** To become the **go-to platform for Nigerian individuals and small businesses** seeking both quality tech products and reliable digital services.

---

## 🔧 MVP Core Functionality

### 1. **E-commerce Store (Frontend + Backend)**

* Browse and filter tech products
* View product details
* Add to cart and manage cart
* Secure user authentication
* Place orders via checkout
* View past orders in a user dashboard

### 2. **Digital Services Section**

* Static frontend pages describing:

  * Web Design
  * Branding
  * IT Consulting
* Admin-only backend to manage:

  * Clients
  * Projects (linked to clients)

---

## 🧱 System Architecture & Stack

### Frontend (Client-Facing)

* **Framework:** Next.js (React)
* **Hosted on:** Vercel
* **Interacts with:** Django backend via REST API only (headless)

### Backend (API & Admin)

* **Framework:** Django + Django REST Framework
* **Apps:**

  * `users` (auth)
  * `ecommerce` (products, orders)
  * `services` (clients, projects)
* **Search:** Elasticsearch (for product search)
* **Tasks/Queues:** Celery (async tasks)
* **Cache/Broker:** Redis
* **Database:** PostgreSQL
* **Admin Panel:** Django Admin (for managing all backend data)

### Infrastructure

* **Local Dev:** Docker + docker-compose
* **CI/CD:** GitHub Actions
* **Production:** AWS ECS (Fargate), RDS for DB, Vercel for frontend

---

## 🧹 App-Level Component Map

### Django Apps & Responsibilities

| App Name    | Purpose                             | API Features (DRF)                     |
| ----------- | ----------------------------------- | -------------------------------------- |
| `users`     | Custom user model, auth (JWT)       | Register, login, logout, profile       |
| `ecommerce` | Product catalog, cart, orders       | CRUD for products/categories, checkout |
| `services`  | Manage service clients and projects | Admin-only; no public APIs in MVP      |

---

## 🎯 MVP Features Breakdown

### 🔐 Authentication

* Custom user model (email as username)
* JWT-based authentication using `simplejwt`
* Auth endpoints: `/api/users/register/`, `/api/users/login/`, etc.

### 🛙 E-Commerce

#### Models

* `Product`: name, price, description, stock, image, category
* `Category`: name, slug
* `Order`: user, total, status
* `OrderItem`: product, quantity, subtotal

#### Features

* Search products (Elasticsearch)
* Cart management (in frontend state)
* Checkout (create order from cart)
* View order history

### 🧑‍💼 Digital Services

#### Models (Admin-Only)

* `Client`: name, contact info
* `Project`: name, status (ongoing/completed), description

#### Features

* Viewable/editable from Django Admin only (in MVP)

---

## 🗁 Suggested Project Structure (Backend)

```bash
giddytech_backend/
├── users/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── urls.py
├── ecommerce/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── urls.py
├── services/
│   ├── models.py
│   └── admin.py
├── config/
│   └── settings/
│       ├── base.py
│       ├── dev.py
│       └── prod.py
└── manage.py
```

---

## ⚙️ Dev Environment Guidelines

* Use **Docker** for full-stack local dev (`docker-compose` with containers for backend, frontend, Redis, Postgres).
* Environment variables for secure inter-container communication.
* Use **Celery + Redis** to handle background tasks (like sending emails).
* GitHub Actions automates testing, linting, and deployment.

---

## ✅ MVP Completion Checklist

| Feature                    | Status     |
| -------------------------- | ---------- |
| Dockerized environment     | 🟩 Planned |
| JWT Auth (DRF + SimpleJWT) | 🟩 Planned |
| Product/Category API       | 🟩 Planned |
| Cart + Checkout flow       | 🟩 Planned |
| Order history dashboard    | 🟩 Planned |
| Elasticsearch integration  | 🟩 Planned |
| Client/Project admin       | 🟩 Planned |
| CI/CD pipeline             | 🟩 Planned |

---

## 🗂️ Sample API Routes (REST)

* `POST /api/users/register/`
* `POST /api/users/login/`
* `GET /api/products/`
* `GET /api/products/:id/`
* `POST /api/orders/`
* `GET /api/orders/history/`

---

## 💡 Final Notes

* The MVP **must be modular, scalable, and cloud-ready**.
* The frontend should feel modern, mobile-friendly, and focused on **trust and usability**.
* The backend must be **secure**, easy to extend, and **ready for microservices** down the line.
* Admin interface should be clean and usable for non-technical staff.
