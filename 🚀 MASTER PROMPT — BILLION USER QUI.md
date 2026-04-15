🚀 MASTER PROMPT — BILLION USER QUIZ SYSTEM (CLEAN ENTERPRISE BUILD)
🎯 GOAL

Build a high-scale quiz platform (login, register, quiz, leaderboard) that is:

scalable to millions → billions of users
containerized (Docker)
Kubernetes-ready
cache-optimized
production-safe
single database system (no fragmentation)
❌ REMOVE COMPLETELY (IMPORTANT CLEANUP)
1. Remove multiple databases
❌ SQLite3 (delete fully)
❌ MongoDB (delete fully)
❌ any dual DB logic

👉 ONLY USE:
👉 PostgreSQL

2. Remove database confusion in code
No mixed ORM usage
No dual models
No Mongo schemas
No SQLite fallback logic

👉 ONE DATABASE LAYER ONLY

3. Remove local storage logic for users
No user data in frontend storage
No insecure session handling
4. Remove direct DB calls in frontend
Frontend MUST NOT talk to DB
Only backend APIs allowed
✅ KEEP / IMPLEMENT (FINAL ARCHITECTURE)
🧱 CORE STACK
Frontend: Next.js
Backend: Express.js (stateless)
DB: PostgreSQL only
Cache: Redis
Proxy: Nginx or Kong (later upgrade)
Orchestration: Kubernetes
Containers: Docker
🗄️ DATABASE RULE (STRICT)

Use ONLY PostgreSQL for ALL:

Tables:
users (login/register)
sessions / refresh tokens
cantos
chapters
questions
options
answers
user_attempts
leaderboard
⚡ PERFORMANCE LAYER (CRITICAL)
1. Cache layer

👉 Redis

Use for:

quiz questions
leaderboard top results
session tokens
API caching
2. Auth system (IMPORTANT FIX)

Login flow:

user login request
PostgreSQL verify user
bcrypt password check
JWT generate
store refresh token in Redis

👉 After login:

NO DB calls per request
JWT-only auth
3. Quiz flow (CRITICAL OPTIMIZATION)
quiz questions → Redis first
fallback → PostgreSQL
submissions → queue system
4. Async system (MANDATORY)

Use queue worker:

answer processing
leaderboard update
analytics

👉 NEVER block API response

🌐 API STRUCTURE (MICROSERVICES)

Split services:

auth-service (login/register)
quiz-service (questions)
result-service (history)
leaderboard-service
realtime-service (WebSocket)
🔁 REALTIME SYSTEM

Use:
👉 Socket.IO

ONLY for:

live leaderboard
timer sync
instant score updates

NOT for:

database operations
authentication
🧠 TRAFFIC FLOW (FINAL DESIGN)
User
 ↓
Nginx / Gateway
 ↓
API Services (Express cluster)
 ↓
Redis (cache + session)
 ↓
PostgreSQL (source of truth)
 ↓
Worker Queue (async processing)
☸️ KUBERNETES REQUIREMENTS

Deploy:

Stateless services:
Next.js
Express APIs
Workers
Stateful services:
PostgreSQL (primary + replicas)
Redis cluster
MUST ADD:
Horizontal Pod Autoscaler (HPA)
health checks
auto restart policies
🗄️ DATABASE SCALING RULES
PostgreSQL setup:
1 primary (writes)
multiple replicas (reads)
Add:
connection pooling (PgBouncer)
indexing on all FK columns
query optimization mandatory
🔐 SECURITY RULES
JWT authentication only
rate limiting via gateway
input validation everywhere
HTTPS mandatory
no direct DB exposure
📊 OBSERVABILITY (MANDATORY FOR SCALE)

Add:

logs (centralized)
metrics (Prometheus)
dashboards (Grafana)
tracing (OpenTelemetry)
🚀 SCALING STRATEGY
Phase 1 (now)
Docker + single Kubernetes cluster
Phase 2
Redis caching fully enabled
PostgreSQL replication
Phase 3
API gateway upgrade (Kong/Envoy)
multi-node scaling
Phase 4 (billion scale)
multi-region deployment
CDN integration
global load balancing
⚠️ NON-NEGOTIABLE RULES
❌ No MongoDB
❌ No SQLite
❌ No direct frontend DB access
❌ No synchronous heavy processing
❌ No DB calls during quiz play loop
🧠 FINAL RESULT TARGET

If implemented correctly:

⚡ <50ms API response
🚀 millions of concurrent users
📈 horizontally scalable system
🔥 enterprise-grade reliability
🌍 future billion-user readiness
✔️ FINAL SUMMARY

👉 Use ONE database: PostgreSQL
👉 Use Redis for speed
👉 Use queues for heavy tasks
👉 Use microservices + Kubernetes
👉 Remove all extra databases immediately