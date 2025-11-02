# Technical Overview of the “Portal for Small Business” Startup

## Introduction
Portal for Small Business (hereafter referred to as the Portal) is a SaaS PWA that serves as a **corporate portal tailored to the scale of small organizations** — enabling managers to control payroll and shift schedules within a single, ready-to-use IT solution, while employees can track all information about their earnings and work shifts in their personal accounts.

A short (3 min) YouTube video with overview is [available](https://www.youtube.com/watch?v=Jp4zi1htoVI).  

## Architecture

**High-level system diagram:**

<br/>
<img width="550" height="500" alt="Arch" src="https://github.com/user-attachments/assets/0b81ec2b-b3e3-4bae-8091-413112e349d7" />
<br/>

The frontend runs on **Next.js (React)** inside a **Docker Swarm cluster**.  
The backend is a **PHP REST API** with **MySQL** and **Redis**.  
All traffic passes through **Cloudflare (HTTPS, CDN, DDoS protection)**, and internal communication between services is strictly isolated within a private Docker network.

<br />

---

<br />


## Technology Stack

### Languages
- TypeScript  
- PHP  
- SQL  
- HTML / CSS (SCSS Modules)

### Frontend
- React  
- Next.js  
- Framer Motion (animations)  
- MDX (mixed Markdown + JSX)  
- Fully responsive design + **Progressive Web App (PWA)**  

### Backend
- **Layered Architecture:** Controllers, Services, Repositories  
- PHP PDO for database layer  
- PHP JWT for authentication  
- Redis (Predis) for caching and anti-spam  
- MySQL transactions for consistency  
- Payment SDK integration  

### Infrastructure & DevOps
- Docker & Docker Swarm  
- Apache  
- Node.js  
- phpMyAdmin (2FA-protected)  
- Ubuntu VM  
- Cloudflare (HTTPS, DNS, CDN, Rate Limiting)  
- Secret Vault & Docker Swarm Secrets  
- Web Metrics for monitoring

<br />

---

<br />

## Key Engineering Decisions
- Optimized rendering of large React trees (e.g., shift schedules) via **memoization** and **timestamp-based updates**.  
- Efficient lazy loading and caching using **React Suspense**.  
- Full **Excel/CSV export** for complete data extraction.  
- Anti-spam and rate-limiting via **Redis counters**.  
- **UUID-based entity IDs** for enhanced integrity and security.  
- Strict **container isolation** for PHP API, MySQL, and Redis within the Docker network.



## Security and Access Control
- **JWT-based authentication** (Access + Refresh tokens).  
- **RBAC** (Admin / Employee roles).  
- No external database access — all queries go through the API.  
- **Cloudflare HTTPS** enforcement and DDoS / brute-force protection.  
- **Two-factor authentication (2FA)** via email.  
- Secure environment variables via **Docker Secrets**.  



## Performance Optimization
- Strict **React memoization** policies and timestamp-based fetching.  
- Server-side caching with **Redis**.  
- **PHP OPcache** for backend execution speed.  
- **Horizontal scaling** using Docker Swarm replicas.  
- **Next.js SSR and streaming** for fast initial page loads.  



## Why This Architecture Works
- **Isolation-first design:** Each service runs in its own Docker container.  
- **Predictable scalability:** Docker Swarm provides zero-downtime scaling.  
- **Balanced stack:** Combining PHP and Next.js ensures modern UX with stable backend.  
- **Security-driven approach:** Cloudflare, HTTPS, RBAC, and Redis protection layers.  

<br />

---

<br />

## Final Note
This project was **fully designed and implemented from scratch** by @mtansk  — including backend architecture, frontend, and deployment. A short video of the UI and User Pathway is [here](https://www.youtube.com/watch?v=Jp4zi1htoVI).

