# 🛡️ Secure & Observable RESTful Articles API  
### Advanced Web Service Engineering • Praktikum #8 — 20251

<p align="left">
  <img src="https://img.shields.io/badge/Node.js-18%2B-3c873a?logo=node.js&logoColor=white" />
  <img src="https://img.shields.io/badge/Express-4.x-black?logo=express&logoColor=white" />
  <img src="https://img.shields.io/badge/MongoDB-Atlas-4aa73c?logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/Auth-JWT-orange?logo=jsonwebtokens" />
  <img src="https://img.shields.io/badge/Observability-Pino-00b4d8?logo=logstash&logoColor=white" />
  <img src="https://img.shields.io/badge/Documentation-OpenAPI%203-blue?logo=swagger" />
</p>

> **Nama:** Muhammad Raihan Azmi  
> **NIM:** 230104040079  
> **Dosen Pengampu:** Muhayat, M.IT  
> **Topik Praktikum:** Secure & Observable RESTful CRUD API (JWT • Hardening • Observability)

---

# 📘 Overview

Project ini adalah implementasi resmi **Praktikum #8 Web Service Engineering (20251)**:  
membangun **RESTful CRUD API tingkat lanjut** untuk resource **Articles** dengan fokus pada:

- **Keamanan (Hardening + JWT + RBAC)**
- **Observability modern (Structured Logging + Correlation-ID + Healthcheck)**
- **Kepatuhan RESTful Principles**
- **Design-first OpenAPI**
- **Arsitektur Layered (Controller → Service → Repository)**

Project ini siap digunakan sebagai **API production-ready**, lengkap dari **design → implementasi → testing → dokumentasi**.

---

# 🚀 Key Features

## 🔐 1. Authentication & Authorization
- Register, Login, Refresh Token, Logout
- JWT Access Token (15m) & Refresh Token (7d)
- Password hashing (bcrypt)
- **RBAC**:
  - `admin` → full control
  - `user` → manage own articles
  - `owner` → only update/delete own article

---

## 📰 2. Articles CRUD (RESTful)
- Create, Read, Update, Delete
- Pagination (`page`, `limit`)
- Filtering (`status`, `tag`)
- Searching (`q`)
- Sorting (`sortBy=createdAt&order=desc`)
- Ownership validation
- Public + protected endpoint mix

---

## 🛡️ 3. Hardening
- Input validation (Joi)
- Rate limiting (anti-bruteforce)
- Security headers (Helmet)
- Strict CORS
- Sanitasi input dasar
- Error hygiene (no sensitive error leak)
- Environment secrets menggunakan `.env`

---

## 🔎 4. Observability (Production Level)
- **Pino structured JSON logging**
- **Correlation-ID (x-correlation-id)** otomatis
- Request timing & metadata logging
- Health endpoint: `/health`
- Metrics (opsional): `/metrics`

---

## 📑 5. OpenAPI 3.1 Documentation
- Live Swagger UI via: `/docs`
- Mendukung:
  - BearerAuth
  - Article schemas
  - Auth schemas
  - Examples untuk request/response

---

# 🧰 Tech Stack

| Layer | Tools |
|------|-------|
| Runtime | Node.js 18+ |
| Framework | Express.js |
| Database | MongoDB Atlas (Mongoose) |
| Auth | JWT, bcrypt |
| Validation | Joi |
| Hardening | Helmet, CORS, Rate Limit |
| Observability | Pino, UUID |
| Docs | OpenAPI + Swagger UI |
| Testing | Jest + Supertest (optional) |
| CI/CD | GitHub Actions (lint → test → build) |

---

# ⚙️ Installation

## 1. Clone Project
```bash
git clone https://github.com/<your-repo>
cd P8_SecureArticles_230104040079
```

## 2. Install Dependencies
```bash
npm install
```

## 3. Create Environment Variables
File `.env`:

```env
NODE_ENV=development
PORT=3000

DB_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/wse_p8_secure_articles

LOG_LEVEL=debug

JWT_ACCESS_SECRET=supersecret_access_123
JWT_REFRESH_SECRET=supersecret_refresh_123
JWT_ACCESS_EXPIRES=15m
JWT_REFRESH_EXPIRES=7d
```

## 4. Run Development Server
```bash
npm run dev
```

## 5. Access API
- Base API → http://localhost:3000  
- Swagger Docs → http://localhost:3000/docs  
- Healthcheck → http://localhost:3000/health

---

# 📚 API Endpoints

## 🔐 Auth Endpoints
| Method | Endpoint | Auth | Deskripsi |
|--------|----------|------|-----------|
| POST | `/api/auth/register` | Public | Daftar user (role: user/admin) |
| POST | `/api/auth/login` | Public | Login → access + refresh token |
| POST | `/api/auth/refresh` | Public | Ambil access token baru |
| POST | `/api/auth/logout` | Access Token | Logout & invalidate refresh token |
| GET | `/api/auth/me` | Access Token | Profile user |

---

## 📰 Articles Endpoints
| Method | Endpoint | Auth | Role | Deskripsi |
|--------|----------|------|------|-----------|
| GET | `/api/articles` | Public | - | List + pagination + query |
| GET | `/api/articles/:id` | Public | - | Detail artikel |
| POST | `/api/articles` | Token | user/admin | Create article |
| PUT | `/api/articles/:id` | Token | owner/admin | Update |
| DELETE | `/api/articles/:id` | Token | admin | Delete |

---

# 📂 Project Architecture

```
src/
├── app.js               # Express app wiring
├── server.js            # Server bootstrap
├── config/
│   ├── env.js
│   └── db.js
├── controllers/
├── services/
├── repositories/
├── middlewares/
│   ├── auth.middleware.js
│   ├── role.middleware.js
│   ├── correlationId.middleware.js
│   ├── rateLimit.middleware.js
│   └── error.middleware.js
├── utils/
│   ├── jwt.js
│   ├── logger.js
│   ├── response.js
│   └── dto/
├── routes/
├── docs/                # OpenAPI spec
└── ...
```

---

# 🧪 Evidence (Screenshot Checklist)

Sertakan minimal **6 bukti** sesuai modul praktikum:

### 🔹 1. Register User (Postman)  
### 🔹 2. Login (success → JWT token)  
### 🔹 3. Create Article (author otomatis)  
### 🔹 4. List Article + pagination  
### 🔹 5. Update / Delete Article (RBAC)  
### 🔹 6. Structured Logging + Correlation-ID  

Tambahan (rekomendasi dosen):  
- Screenshot `/health`  
- Screenshot `/docs` Swagger  

---

# 🏆 RESTful Compliance

Project mengikuti **7 REST Principles** dari modul:

- Resource-oriented (`/api/articles`)
- Method semantics (GET/POST/PUT/DELETE)
- Stateless (JWT)
- Proper status codes
- Layered architecture
- Cache-ready (ETag optional)
- Uniform interface + lightweight HATEOAS

---

# 🔐 Hardening Summary

- Security headers → Helmet  
- Rate limiting  
- CORS whitelist  
- Input validation + sanitasi  
- Environment secret isolation  
- No sensitive error leakage  

---

# 🔎 Observability Summary

- Pino structured JSON
- Correlation-ID otomatis
- Request latency logging
- Healthcheck `/health`
- Metrics (opsional)

---

# ✨ Author
**Muhammad Raihan Azmi**  
Praktikum Web Service Engineering — 2025  
Created with modern backend architecture.

