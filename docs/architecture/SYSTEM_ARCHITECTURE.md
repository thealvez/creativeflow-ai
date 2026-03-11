# CreativeFlow AI — System Architecture

**Status:** ✅ Approved for Development
**Version:** 1.0.0
**Architecture Level:** C2 (Containers + Components)
**Design Pattern:** Microservices-lite (Logical separation, single deployments)

---

## 1. System Overview (C1 Diagram)

```
┌─────────────────────────────────────────────────────────────┐
│                      CreativeFlow AI                         │
│            Automated Video Creation & Publishing              │
└─────────────────────────────────────────────────────────────┘

   ┌──────────────────┐          ┌──────────────────┐
   │    Frontend      │          │  Agent Pipeline  │
   │  (Next.js 15)    │◄────────►│  (LangChain)     │
   │  - React + TW    │          │  - Claude        │
   │  - WebSocket     │          │  - Gemini        │
   │  - Real-time UI  │          │  - Grok          │
   └────────┬─────────┘          └────────┬─────────┘
            │                             │
            │                             │
            └──────────────┬──────────────┘
                           │
                    ┌──────▼──────┐
                    │   Backend   │
                    │  (Fastify)  │
                    │  - API      │
                    │  - Jobs     │
                    │  - Auth     │
                    └──────┬──────┘
                           │
            ┌──────────────┼──────────────┐
            │              │              │
      ┌─────▼────┐   ┌─────▼────┐   ┌────▼─────┐
      │PostgreSQL│   │  Redis   │   │ Platforms│
      │  (Neon)  │   │ (Cloud)  │   │ APIs     │
      │  - Data  │   │ - Queue  │   │(TikTok...|
      │  - Auth  │   │ - Cache  │   │         │
      └──────────┘   └──────────┘   └─────────┘
```

---

## 2. Container Architecture (C2 Diagram)

### **Frontend Container** (Vercel)
```yaml
Container: NextJS Application
  Components:
    - Pages (App Router)
      * /dashboard — Creative library
      * /create — New creative form
      * /status/:id — Job progress
      * /publish/:id — Review & publish
      * /analytics — Performance metrics

    - Components
      * CreateForm (user input)
      * ProgressTracker (WebSocket updates)
      * VideoPreview (full-screen player)
      * MetadataEditor (inline editing)
      * LibraryGrid (pagination + filters)

    - Services
      * apiClient (fetch + error handling)
      * websocketClient (real-time updates)
      * authService (OAuth + JWT)

    - State Management
      * React Context (global UI state)
      * React Query (server state + caching)

  Technologies:
    - Framework: Next.js 15 + React 19
    - Styling: Tailwind CSS 3
    - Real-time: WebSocket (native)
    - HTTP: Fetch API
    - Auth: NextAuth.js v5
```

### **Backend Container** (Railway)
```yaml
Container: Fastify Application
  Layers:
    - HTTP Layer
      * Express-like routing
      * Middleware (auth, logging, rate-limit)
      * Error handling (global handler)
      * Request/response compression

    - Business Logic Layer
      * AuthService (OAuth token mgmt)
      * CreativeService (CRUD + job creation)
      * JobOrchestrator (agent coordination)
      * PublishingService (platform APIs)

    - Data Layer
      * Repository pattern (Knex.js queries)
      * PostgreSQL ORM (no Prisma, raw Knex)
      * Redis cache layer

    - External Integrations
      * LangChain agents (orchestration)
      * TikTok API (publishing)
      * Meta Graph API (Instagram/FB)
      * YouTube API (Shorts)
      * Gemini API (image generation)
      * Grok API (video generation)

  Technologies:
    - Framework: Fastify 4.25+
    - Database: PostgreSQL 16 (Neon)
    - Cache: Redis 7 (Redis Cloud)
    - ORM: Knex.js (query builder)
    - Job Queue: Bull 4
    - Logging: Pino + structured logs
    - APM: OpenTelemetry + Datadog
```

### **Agent Pipeline** (Node.js Workers)
```yaml
Container: LangChain Orchestrator
  Agents:
    1. Prompt Generator
       - Input: User idea
       - LLM: Claude 3.5 Sonnet
       - Output: Structured creative prompt
       - Latency: 30s max

    2. Visual Converter
       - Input: Prompt + platform specs
       - LLM: Claude 3.5 Sonnet
       - Output: Visual prompt (TikTok optimized)
       - Latency: 20s max

    3. Image Generator
       - Input: Visual prompt
       - LLM: Gemini 2.0 Flash
       - Output: 1024x1024 PNG
       - Latency: 45s max
       - Retry: 3x on failure

    4. Video Generator
       - Input: Image + motion prompt
       - API: Grok Imagine
       - Output: MP4 (1080x1920, 30s)
       - Latency: 120s max
       - Async processing

    5. Metadata Generator
       - Input: Idea + assets
       - LLM: Claude 3.5 Haiku
       - Output: Caption, hashtags, description
       - Latency: 25s max

    6. Publisher
       - Input: Video + metadata
       - API: TikTok Business API
       - Output: Published URL + status
       - Latency: 60s max
       - Retry: 3x on rate-limit

  Orchestration:
    - Sequential with parallel image/video generation
    - Job queue: Bull (Redis-backed)
    - Status tracking: Real-time WebSocket to frontend
    - Error handling: Exponential backoff + user notification
```

---

## 3. Data Architecture

### **Database Schema (PostgreSQL)**
```sql
-- Users & Authentication
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR UNIQUE NOT NULL,
  name VARCHAR,
  avatar_url VARCHAR,
  bio TEXT,
  subscription_tier VARCHAR DEFAULT 'free',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  INDEX (email)
);

-- OAuth Integrations
CREATE TABLE oauth_integrations (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  platform VARCHAR, -- 'google', 'github', 'tiktok'
  oauth_id VARCHAR,
  access_token TEXT, -- encrypted
  refresh_token TEXT, -- encrypted
  expires_at TIMESTAMP,
  created_at TIMESTAMP,
  INDEX (user_id, platform)
);

-- Creatives (Job Records)
CREATE TABLE creatives (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  idea TEXT NOT NULL,
  platforms JSONB, -- ['tiktok', 'instagram', ...]
  status VARCHAR DEFAULT 'pending', -- pending, processing, completed, failed
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP,
  INDEX (user_id, status, created_at DESC)
);

-- Videos (Generated Assets)
CREATE TABLE videos (
  id UUID PRIMARY KEY,
  creative_id UUID REFERENCES creatives(id),
  platform VARCHAR, -- 'tiktok', 'instagram', ...
  video_url VARCHAR,
  duration_seconds INT,
  aspect_ratio VARCHAR, -- '9:16', '1:1', etc
  created_at TIMESTAMP,
  INDEX (creative_id, platform)
);

-- Platform Posts (Published)
CREATE TABLE platform_posts (
  id UUID PRIMARY KEY,
  creative_id UUID REFERENCES creatives(id),
  platform VARCHAR,
  post_url VARCHAR,
  post_id VARCHAR, -- platform's post ID
  publish_status VARCHAR, -- 'pending_moderation', 'published', 'failed'
  published_at TIMESTAMP,
  INDEX (creative_id, platform)
);

-- Analytics (Aggregated)
CREATE TABLE analytics (
  id UUID PRIMARY KEY,
  creative_id UUID REFERENCES creatives(id),
  platform VARCHAR,
  views INT DEFAULT 0,
  likes INT DEFAULT 0,
  shares INT DEFAULT 0,
  collected_at TIMESTAMP,
  INDEX (creative_id, platform, collected_at DESC)
);

-- Job Queue (Bull persisted)
-- Stored in Redis, synced to DB on completion
```

### **Caching Strategy (Redis)**
```yaml
Cache Layers:
  1. User Sessions
     - Key: session:{sessionId}
     - TTL: 24 hours
     - Content: JWT payload + metadata

  2. OAuth Tokens
     - Key: oauth_token:{userId}:{platform}
     - TTL: 50 minutes (before refresh)
     - Content: access_token, refresh_token

  3. Job Queue
     - Type: Bull queue
     - Key: bull:creativeflow:job_queue
     - Content: Job metadata, status, progress

  4. API Response Cache
     - Key: api:{endpoint}:{userId}
     - TTL: 5 minutes
     - Content: Paginated creative list, analytics
```

---

## 4. API Design (OpenAPI 3.0)

### **Authentication Endpoints**
```yaml
POST /api/auth/google
  Summary: Initiate Google OAuth flow
  Parameters:
    - redirect_uri (query) — Callback URL
  Response: { authorization_url, state }

GET /api/auth/google/callback
  Summary: OAuth callback handler
  Parameters:
    - code (query)
    - state (query)
  Response: { user, token, refresh_token }

POST /api/auth/github
  Summary: Initiate GitHub OAuth
  Parameters:
    - redirect_uri (query)
  Response: { authorization_url, state }

GET /api/auth/github/callback
  Summary: GitHub OAuth callback
  Parameters:
    - code (query)
    - state (query)
  Response: { user, token, refresh_token }
```

### **Creative Management Endpoints**
```yaml
POST /api/creatives
  Summary: Create new creative job
  Authentication: Bearer {JWT}
  Request:
    {
      "idea": "productivity tips with pomodoro",
      "platforms": ["tiktok", "instagram"],
      "language": "pt-BR",
      "tone": "educational"
    }
  Response:
    {
      "id": "creative_123",
      "status": "pending",
      "job_id": "job_456",
      "created_at": "2026-03-11T..."
    }
  Status Codes: 201 (created), 400 (validation), 401 (unauthorized)

GET /api/creatives/:id
  Summary: Get creative job status
  Authentication: Bearer {JWT}
  Response:
    {
      "id": "creative_123",
      "status": "processing",
      "progress": {
        "prompt_generated": true,
        "visual_prompt": true,
        "image_generated": true,
        "video_generating": true,
        "metadata": false,
        "publishing": false
      },
      "videos": [...]
    }

GET /api/creatives
  Summary: List user's creatives
  Authentication: Bearer {JWT}
  Query Params:
    - page (default: 1)
    - limit (default: 20, max: 100)
    - status (filter)
  Response:
    {
      "data": [...],
      "pagination": { "page": 1, "limit": 20, "total": 50 }
    }

DELETE /api/creatives/:id
  Summary: Delete creative
  Authentication: Bearer {JWT}
  Status: 204 No Content
```

### **Publishing Endpoints**
```yaml
POST /api/creatives/:id/publish
  Summary: Publish generated videos
  Authentication: Bearer {JWT}
  Request:
    {
      "platforms": ["tiktok"],
      "schedule_at": null, -- null for now, ISO string for later
      "metadata_overrides": { "caption": "..." }
    }
  Response:
    {
      "platform_posts": [
        {
          "platform": "tiktok",
          "post_url": "https://vm.tiktok.com/...",
          "status": "published"
        }
      ]
    }
```

### **User Profile Endpoints**
```yaml
GET /api/users/profile
  Summary: Get authenticated user profile
  Authentication: Bearer {JWT}
  Response:
    {
      "id": "user_123",
      "email": "creator@example.com",
      "name": "Sofia",
      "avatar_url": "...",
      "subscription_tier": "pro",
      "platforms_connected": ["tiktok", "instagram"]
    }

PUT /api/users/profile
  Summary: Update user profile
  Authentication: Bearer {JWT}
  Request: { "name": "...", "bio": "..." }
  Response: { updated user object }

POST /api/users/connect-platform/:platform
  Summary: Connect platform OAuth (TikTok, Instagram, etc)
  Authentication: Bearer {JWT}
  Response: { oauth_authorization_url }
```

---

## 5. API Error Handling

```yaml
Standard Error Response:
  {
    "error": {
      "code": "INVALID_REQUEST",
      "message": "Validation failed: idea must be 10-500 characters",
      "details": {
        "field": "idea",
        "constraint": "length",
        "expected": "10-500",
        "received": 3
      }
    }
  }

HTTP Status Codes:
  400: Bad Request (validation, missing fields)
  401: Unauthorized (invalid/expired token)
  403: Forbidden (user doesn't own resource)
  404: Not Found (resource doesn't exist)
  429: Too Many Requests (rate limit exceeded)
  500: Internal Server Error (unexpected)
  502: Bad Gateway (external API failure)
  503: Service Unavailable (maintenance)

Rate Limiting:
  - 100 requests/minute per user (authenticated)
  - 10 requests/minute per IP (unauthenticated)
  - Response headers: X-RateLimit-{Limit,Remaining,Reset}
```

---

## 6. Security Architecture

### **Authentication**
- **Strategy:** OAuth 2.0 (Google, GitHub, TikTok)
- **Token Management:** JWT (RS256 signing)
- **Refresh Token:** Redis-backed, 7-day rotation
- **Token Storage (Frontend):** httpOnly cookie (no localStorage)
- **Token Validation:** Backend signature + expiration check

### **Authorization**
- **Model:** Resource-based (users can only access own creatives)
- **Enforcement:** Middleware (userId from JWT vs resource.userId)
- **Admin Operations:** Role-based (future: admin dashboard)

### **Encryption**
- **In Transit:** HTTPS/TLS 1.3 (enforced)
- **At Rest:** OAuth tokens encrypted (AES-256-GCM)
- **Database:** No sensitive data in plaintext
- **Secrets Management:** Environment variables (GitHub Actions secrets)

### **API Security**
- **CORS:** Strict (only frontend domain)
- **CSRF:** State parameter (OAuth) + SameSite cookies
- **Input Validation:** All endpoints (max length, type checking)
- **SQL Injection Prevention:** Parameterized queries (Knex.js)
- **XSS Prevention:** Content-Security-Policy headers

### **OAuth Security**
- **PKCE Flow:** For server-side apps (prevent auth code interception)
- **State Parameter:** Random, session-specific
- **Redirect URI:** Whitelist (prevent open redirects)
- **Scope Limiting:** Only request necessary permissions

---

## 7. Performance Architecture

### **Frontend Performance**
- **Code Splitting:** Per-route lazy loading (Next.js)
- **Image Optimization:** Next/Image (auto-resize, format conversion)
- **Caching:** React Query (stale-while-revalidate)
- **Compression:** gzip + Brotli (Vercel automatic)
- **CDN:** Vercel global edge network
- **Target:** <3s FCP (First Contentful Paint), <5s LCP

### **Backend Performance**
- **API Response Time:** <200ms P95 (excluding external APIs)
- **Database Query Optimization:**
  - Indexes on foreign keys (user_id, creative_id)
  - Indexes on frequently filtered columns (status, created_at)
  - Connection pooling (Knex.js with max 20 connections)
- **Caching:** Redis for sessions, tokens, frequently-accessed data
- **Async Processing:** Bull queues for long-running jobs

### **Agent Pipeline Performance**
- **Sequential Processing:** Optimized for latency
  - Prompt generation: 30s
  - Visual conversion: 20s
  - Image generation: 45s (Gemini)
  - Video generation: 120s (Grok, async)
  - Metadata: 25s
  - Publishing: 60s
  - **Total E2E:** ~5 minutes (target <5min)

### **Database Performance**
- **Query Optimization:** EXPLAIN ANALYZE for slow queries
- **Batch Operations:** Bulk inserts where applicable
- **Archival:** Soft deletes (is_deleted column) for GDPR
- **Monitoring:** Slow query logs (<100ms threshold)

---

## 8. Deployment Architecture

### **Frontend Deployment (Vercel)**
```
GitHub (master branch)
  ↓
Vercel CI/CD
  - Install dependencies (npm ci)
  - Build (next build)
  - Run tests (npm test)
  - Deploy to edge network
  ↓
https://creativeflow.vercel.app
  - Global CDN
  - Auto-scaling
  - SSL/TLS managed
```

### **Backend Deployment (Railway)**
```
GitHub (master branch)
  ↓
Railway CI/CD
  - Build Docker image (Dockerfile)
  - Run tests (npm test)
  - Push to Railway registry
  - Rolling deployment
  ↓
https://api.creativeflow.railway.app
  - Docker container (production-grade)
  - Auto-scaling (horizontal)
  - Health checks (readiness/liveness probes)
  - Managed PostgreSQL (Neon)
  - Redis Cloud connection
```

### **Environment Variables**
```yaml
Development (.env.local):
  - DATABASE_URL=postgresql://dev:pwd@localhost:5432/creativeflow_dev
  - REDIS_URL=redis://localhost:6379
  - NEXT_PUBLIC_API_URL=http://localhost:3001
  - OPENAI_API_KEY=sk-...
  - GEMINI_API_KEY=...

Staging (.env.staging):
  - DATABASE_URL=postgresql://... (Neon staging)
  - REDIS_URL=... (Redis Cloud staging)
  - NEXT_PUBLIC_API_URL=https://api-staging.creativeflow.rail...
  - OAuth credentials (TikTok staging sandbox)

Production (.env.production):
  - DATABASE_URL=postgresql://... (Neon production)
  - REDIS_URL=... (Redis Cloud production)
  - NEXT_PUBLIC_API_URL=https://api.creativeflow.railway.app
  - OAuth credentials (TikTok production)
  - Datadog API key
```

---

## 9. Monitoring & Observability

### **Logging (Pino + Datadog)**
```yaml
Log Levels:
  error: Critical issues (requires action)
  warn: Warnings (may need attention)
  info: General info (important events)
  debug: Debugging (developer use only)

Log Format:
  {
    "timestamp": "2026-03-11T10:30:45Z",
    "level": "error",
    "message": "Video generation failed",
    "service": "backend",
    "job_id": "job_456",
    "error": "Grok API timeout",
    "user_id": "user_123"
  }

Centralization: Datadog (automatic log ingestion from Railway)
```

### **Metrics (OpenTelemetry + Datadog)**
```yaml
Application Metrics:
  - Request latency (by endpoint)
  - Error rate (by status code)
  - Job success rate (by agent)
  - Agent latency (Prompt, Image, Video, etc)
  - Database query time
  - Cache hit ratio

Infrastructure Metrics:
  - CPU usage (Railway)
  - Memory usage
  - Disk I/O
  - Network bandwidth
  - Database connections
  - Redis memory

Dashboards:
  - Real-time service health
  - Job success/failure trends
  - Performance trends (weekly)
  - Error tracking by agent
```

### **Alerting (Datadog)**
```yaml
Critical Alerts:
  - API error rate > 1% for 5min
  - Job success rate < 85% for 10min
  - Database connection pool exhausted
  - Redis connection lost
  - Agent timeout (30min+)

Warning Alerts:
  - API latency P95 > 500ms
  - Job success rate < 95%
  - Memory usage > 80%

Notification: Slack #creativeflow-alerts channel
```

---

## 10. Technology Stack Rationale

| Layer | Technology | Why |
|-------|-----------|-----|
| **Frontend** | Next.js 15 | Full-stack React, server components, auto-deploy to Vercel |
| **Styling** | Tailwind CSS | Utility-first, performant, zero-runtime |
| **Real-time** | WebSocket (native) | Built-in Next.js, low latency for job progress |
| **Backend** | Fastify | Lightweight, fast, excellent JSON serialization |
| **ORM** | Knex.js | Query builder, flexible, avoids ORM overhead |
| **Database** | PostgreSQL | ACID, relational, Neon (serverless option) |
| **Cache** | Redis | High-speed, Bull queue integration, session storage |
| **Jobs** | Bull 4 | Redis-backed, reliable, retry logic |
| **AI Orchestration** | LangChain | Unified interface for Claude, Gemini, Grok |
| **AI Models** | Claude, Gemini, Grok | Best-in-class for text, image, video generation |
| **Deploy Frontend** | Vercel | Optimal Next.js support, edge functions, auto-scaling |
| **Deploy Backend** | Railway | Docker-native, PostgreSQL included, generous free tier |
| **Logging** | Pino | Ultra-fast JSON logging, low memory |
| **APM** | OpenTelemetry + Datadog | Industry standard, vendor-agnostic, comprehensive |

---

## 11. Architectural Constraints & Decisions

### **Constraints**
1. **E2E Latency:** <5 minutes (idea → published video)
2. **Scalability:** Support 10K concurrent users (Phase 2+)
3. **Cost:** <$0.25 per video processed (COGS)
4. **Security:** OAuth 2.0 mandatory, encrypted tokens, HTTPS only
5. **Availability:** 99.5% uptime SLA (Phase 2+)

### **Key Decisions (ADR Format)**

**ADR-1: Monolith vs Microservices**
- **Decision:** Microservices-lite (logical separation, single deployments)
- **Rationale:** Complexity of microservices premature for MVP; logical separation enables future splitting
- **Trade-off:** Simpler deployment/debugging vs harder to split later

**ADR-2: Database (Monolithic vs Per-Service)**
- **Decision:** Single PostgreSQL (Neon) for all services
- **Rationale:** MVP needs single source of truth; distributed data complexity not yet needed
- **Trade-off:** Simpler queries vs harder to scale individual services

**ADR-3: Queue System**
- **Decision:** Bull (Redis-backed, in-process)
- **Rationale:** Simplicity, Redis already required, adequate for MVP throughput
- **Trade-off:** Not distributed vs simpler mental model

**ADR-4: Real-time Updates**
- **Decision:** WebSocket (native) + polling fallback
- **Rationale:** Low latency, native browser support, no external dependencies
- **Trade-off:** Stateful connections vs simplicity of implementation

**ADR-5: ORM Choice**
- **Decision:** Knex.js (query builder, not full ORM)
- **Rationale:** Flexibility, performance, explicit SQL understanding
- **Trade-off:** More boilerplate vs better control

---

## 12. Future Scaling (Phase 2+)

### **Horizontal Scaling**
- Multiple API instances (Railway auto-scaling)
- Read replicas for PostgreSQL (Neon Pro)
- Distributed job queue (RabbitMQ if Bull insufficient)
- Edge functions for API (Vercel Edge Middleware)

### **Vertical Scaling**
- Larger database instance (Neon managed)
- Larger Redis instance (Redis Cloud enterprise)
- More agent worker processes

### **Service Separation** (if needed)
- Extract agent pipeline to separate service
- Separate analytics service (read-only DB replica)
- API gateway for multi-backend orchestration

---

**Architecture Approved:** ✅ Ready for development
**Next Step:** @data-engineer to design detailed database schema
**Timeline:** Week 1 (March 17-23) — Architecture locked

