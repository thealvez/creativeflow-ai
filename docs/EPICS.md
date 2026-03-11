# 🎯 PRODUCT EPICS
## CreativeFlow AI — Roadmap por Épicos

**Data:** 11 de Março de 2026
**Preparado por:** Morgan (Product Manager)
**Status:** ✅ READY FOR @sm (Scrum Master) — Story Breakdown
**Objetivo:** Estruturar desenvolvimento em waves (fases paralelas)

---

## 📌 VISÃO GERAL DOS ÉPICOS

```
EPIC 1: Foundation & Setup (Parallel to other epics)
└─ Infrastructure, APIs, CI/CD
└─ Timeline: Weeks 1-4
└─ Stories: ~12
└─ Owner: @devops (Gage)

EPIC 2: MVP Core (Primary Path - Weeks 1-12)
├─ EPIC 2.1: User Authentication & Profiles
├─ EPIC 2.2: Create Creative Form & Validation
├─ EPIC 2.3: Agent Pipeline (6 agents orchestrated)
├─ EPIC 2.4: Real-time Status Dashboard
├─ EPIC 2.5: TikTok Publishing Integration
├─ EPIC 2.6: Creative Library & History
└─ EPIC 2.7: Error Handling & Recovery

EPIC 3: Production Ready (Weeks 13-24)
├─ EPIC 3.1: Multi-Platform Publishing
│  ├─ Instagram Reels
│  ├─ Facebook Videos
│  ├─ YouTube Shorts
│  └─ X/Twitter (Phase 2+)
├─ EPIC 3.2: Analytics Dashboard
├─ EPIC 3.3: Video Metadata Editor
├─ EPIC 3.4: Scheduling & Queue Management
├─ EPIC 3.5: Content Moderation System
└─ EPIC 3.6: Monetization (Billing & Subscriptions)

EPIC 4: Enterprise Features (Weeks 25-36)
├─ EPIC 4.1: Workspace & Team Management
├─ EPIC 4.2: Role-Based Access Control (RBAC)
├─ EPIC 4.3: Brand Kit Management
├─ EPIC 4.4: API Access & Integrations
├─ EPIC 4.5: White-Label Capabilities
└─ EPIC 4.6: Enterprise Analytics & Reporting

EPIC 5: Expansion & AI (Weeks 37+)
├─ EPIC 5.1: Creator Style Learning
├─ EPIC 5.2: Trend Prediction Engine
├─ EPIC 5.3: Multi-Language Support
├─ EPIC 5.4: Audio Generation (TTS + Music)
├─ EPIC 5.5: Mobile App (iOS + Android)
└─ EPIC 5.6: Advanced Performance Analytics
```

---

## 🏗️ EPIC 1: Foundation & Setup

### Epic Goal
Estabelecer infraestrutura, APIs, e CI/CD pipeline para suportar desenvolvimento de EPIC 2-5.

### Scope
- Infrastructure as Code (Terraform)
- API client setup (all platforms)
- Database schema design
- CI/CD pipeline (GitHub Actions)



### Stories (Estimated: 12)
```
EPIC 1.1: Project Setup
  Story 1.1.1: Initialize Git repository + GitHub setup
  Story 1.1.2: Setup Node.js project structure (monorepo)
  Story 1.1.3: Configure package.json (dependencies)
  Story 1.1.4: Setup development environment (.env, .vscode)

EPIC 1.2: Infrastructure
  Story 1.2.1: Create Terraform configs (Vercel + Railway)
  Story 1.2.2: Setup PostgreSQL (Neon)
  Story 1.2.3: Setup Redis (Redis Cloud)
  Story 1.2.4: Configure networking (HTTPS, domains)

EPIC 1.3: CI/CD
  Story 1.3.1: Create GitHub Actions workflow (lint + test)
  Story 1.3.2: Setup automated testing pipeline
  Story 1.3.3: Configure deployment pipeline (staging + prod)
  Story 1.3.4: Setup monitoring alerts (Datadog / NewRelic)
```

### Dependencies
- None (foundational)

### Success Criteria
- ✅ GitHub repo operational
- ✅ CI/CD pipeline runs on every push
- ✅ Staging environment accessible
- ✅ Database schema deployed
- ✅ Monitoring configured

### Owner
@devops (Gage)

### Timeline
Weeks 1-4 (parallel with EPIC 2.1)

---

## 🎬 EPIC 2: MVP Core (Phase 1)

**Epic Goal:** Validar core loop (ideia → vídeo em 5 min) com TikTok publishing

**Overall Timeline:** Weeks 1-12
**Resources:** 3 engineers (1 full-stack, 1 backend, 1 infra) + 1 PM + 1 designer
**Target Launch:** End of Week 12 (50-100 beta users)

---

### EPIC 2.1: User Authentication & Profiles

#### Goal
Implementar OAuth 2.0 login + user management básico

#### Scope
- OAuth (Google, GitHub)
- User registration + email verification
- JWT session management
- User profile (name, avatar, bio)
- Platform integrations (OAuth tokens storage)
- Password reset (email-based)

#### Stories (Estimated: 8)
```
Story 2.1.1: Design OAuth flow (Google + GitHub)
Story 2.1.2: Implement OAuth callback handler
Story 2.1.3: Create user model + database schema
Story 2.1.4: Implement JWT token management
Story 2.1.5: Build sign up form + validation
Story 2.1.6: Build login form + OAuth redirect
Story 2.1.7: Implement password reset flow
Story 2.1.8: Create user profile page + settings
```

#### Dependencies
- EPIC 1 (Infrastructure)

#### Success Criteria
- ✅ OAuth sign up works (Google, GitHub)
- ✅ Users can set profile (name, avatar, bio)
- ✅ JWT tokens refresh automatically
- ✅ Password reset via email
- ✅ Session persists across page reload
- ✅ User can disconnect OAuth integrations

#### Owner
@dev (Dex) + @devops (Gage)

#### Timeline
Weeks 2-4

---

### EPIC 2.2: Create Creative Form & Validation

#### Goal
Implementar form para submeter ideias + validação real-time

#### Scope
- Form design (simple, mobile-friendly)
- Text input (idea description)
- Platform selection (checkboxes)
- Optional fields (language, tone, audience)
- Client-side validation
- Server-side validation
- Error messaging (user-friendly)
- Submit → generate job ID
- Loading state + confirmation

#### Stories (Estimated: 6)
```
Story 2.2.1: Design form UI/UX (Figma)
Story 2.2.2: Build form component (React)
Story 2.2.3: Implement client-side validation
Story 2.2.4: Create API endpoint: POST /api/creatives
Story 2.2.5: Implement server-side validation
Story 2.2.6: Add success confirmation + job tracking
```

#### Dependencies
- EPIC 2.1 (Auth)
- EPIC 1 (Infrastructure)

#### Success Criteria
- ✅ Form loads < 1s
- ✅ Validation messages appear real-time
- ✅ Submit generates job ID < 2s
- ✅ User sees confirmation + can close
- ✅ Job persists in database
- ✅ API returns job status

#### Owner
@dev (Dex)

#### Timeline
Weeks 3-4

---

### EPIC 2.3: Agent Pipeline (6 Agents Orchestrated)

#### Goal
Implementar 6 agentes IA orquestrados (Agents 1-5, Publish é EPIC 2.5)

#### Scope
**Agent 1: Prompt Generator (Claude)**
- Input: User idea + context
- Output: Structured prompt (scene, elements, tone, pacing)
- Implementation: LangChain + Claude API
- Timeout: 30s
- Retry: 2x on failure

**Agent 2: Visual Prompt Converter (Claude)**
- Input: Creative prompt + platform specs
- Output: Visual prompt optimized (9:16, 30s TikTok)
- Implementation: LangChain + Claude API
- Timeout: 20s

**Agent 3: Image Generator (Gemini 2.0 Flash)**
- Input: Visual prompt
- Output: 1024x1024 image (PNG)
- Implementation: Google Generative AI SDK
- Timeout: 45s
- Retry: 3x with backoff
- Fallback: Nano Banana (Replicate)

**Agent 4: Video Generator (Grok Imagine)**
- Input: Image + motion prompt
- Output: MP4 (1080x1920, 30s, H.264)
- Implementation: Grok API
- Timeout: 120s (async job)
- Fallback: Stock footage + ffmpeg overlay

**Agent 5: Metadata Generator (Claude)**
- Input: Idea + generated assets
- Output: Caption, hashtags, description (per-platform)
- Implementation: LangChain + Claude API
- Timeout: 25s

#### Stories (Estimated: 18)
```
AGENT 1 - Prompt Generator:
Story 2.3.1: Design prompt engineering patterns
Story 2.3.2: Implement Claude API client
Story 2.3.3: Create prompt generator orchestrator
Story 2.3.4: Add retry + error handling
Story 2.3.5: Write unit tests

AGENT 2 - Visual Prompt Converter:
Story 2.3.6: Design visual prompt engineering
Story 2.3.7: Implement visual prompt agent
Story 2.3.8: Platform-specific optimizations (TikTok)
Story 2.3.9: Add retry logic
Story 2.3.10: Unit tests

AGENT 3 - Image Generator:
Story 2.3.11: Setup Gemini 2.0 API client
Story 2.3.12: Implement image generation
Story 2.3.13: Add Nano Banana fallback
Story 2.3.14: Implement retry with backoff
Story 2.3.15: Unit tests + quality checks

AGENT 4 - Video Generator:
Story 2.3.16: Setup Grok API client
Story 2.3.17: Implement video generation (async)
Story 2.3.18: Add stock footage fallback + ffmpeg

AGENT 5 - Metadata Generator:
Story 2.3.19: Design metadata prompt patterns
Story 2.3.20: Implement metadata agent
Story 2.3.21: Platform-specific metadata (TikTok)
Story 2.3.22: Unit tests
```

#### Dependencies
- EPIC 2.1 (Auth)
- EPIC 1 (Infrastructure)
- API credentials (Claude, Gemini, Grok)

#### Success Criteria
- ✅ All 5 agents execute sequentially
- ✅ Agent 3 + 4 can run in parallel (image + video)
- ✅ E2E pipeline completes < 5 min (P95)
- ✅ Each agent retries on failure
- ✅ Error messages are clear
- ✅ Job status persisted in database

#### Owner
@dev (Dex) + @architect (Aria)

#### Timeline
Weeks 5-10 (longest epic)

---

### EPIC 2.4: Real-time Status Dashboard

#### Goal
Mostrar progresso em tempo real (agente por agente) via WebSocket

#### Scope
- WebSocket server (Socket.io or native)
- Dashboard component (React)
- Agent progress tracking (✅/🔄/⏳)
- Expandable logs (input/output per agent)
- Error display + actionable next steps
- Mobile responsive
- Graceful fallback to polling

#### Stories (Estimated: 8)
```
Story 2.4.1: Design dashboard UI/UX
Story 2.4.2: Setup WebSocket server (Fastify)
Story 2.4.3: Implement dashboard component (React)
Story 2.4.4: Add job status tracking (database)
Story 2.4.5: Implement real-time updates via WS
Story 2.4.6: Add expandable logs + details
Story 2.4.7: Error display + recovery options
Story 2.4.8: Test mobile responsiveness
```

#### Dependencies
- EPIC 2.1 (Auth)
- EPIC 2.2 (Form)
- EPIC 2.3 (Pipeline)

#### Success Criteria
- ✅ WebSocket updates within 3s
- ✅ Shows agent-by-agent progress
- ✅ Auto-reconnect on disconnect
- ✅ Graceful polling fallback
- ✅ Mobile responsive
- ✅ No missing updates

#### Owner
@dev (Dex)

#### Timeline
Weeks 8-9 (parallel with Agent 4)

---

### EPIC 2.5: TikTok Publishing Integration

#### Goal
Publicar vídeo em TikTok via Business API com metadata

#### Scope
- TikTok Business API OAuth flow
- Video upload (resumable chunks)
- Publish with metadata (caption, hashtags)
- Status tracking (moderation pending → published)
- Token refresh (24h lifecycle)
- Error handling (429, 503, API-specific)
- Retry logic with exponential backoff
- Fallback: Generate download link

#### Stories (Estimated: 10)
```
Story 2.5.1: Design TikTok OAuth flow
Story 2.5.2: Setup TikTok API credentials + app
Story 2.5.3: Implement OAuth callback handler
Story 2.5.4: Create TikTok client (API wrapper)
Story 2.5.5: Implement video upload (resumable)
Story 2.5.6: Implement publish endpoint (metadata)
Story 2.5.7: Add token refresh scheduler
Story 2.5.8: Implement retry logic (429, 503)
Story 2.5.9: Add fallback (download link generation)
Story 2.5.10: Integration tests (sandbox account)
```

#### Dependencies
- EPIC 2.3 (Pipeline - needs video)
- EPIC 2.4 (Dashboard - shows status)
- TikTok API approval (CRITICAL)

#### Success Criteria
- ✅ OAuth sign in works
- ✅ Video uploads via chunked API
- ✅ Publish with metadata succeeds
- ✅ Token refreshes before expiry
- ✅ Retry on failure (max 3x)
- ✅ Share URL returned
- ✅ Status tracking (pending → published)
- ✅ Can generate download on API failure

#### Owner
@dev (Dex) + @devops (Gage)

#### Timeline
Weeks 8-11

**⚠️ CRITICAL:** Must apply for TikTok API access in Week 1 (approval takes 1-7 days)

---

### EPIC 2.6: Creative Library & History

#### Goal
Mostrar histórico de vídeos criados em grid view

#### Scope
- Grid layout (4 items per row)
- Thumbnail generation
- Sorting + filtering (platform, status, date)
- Search by title/description
- Actions per creative (view, edit, delete, archive)
- Pagination (50 per page)
- Lazy loading for performance

#### Stories (Estimated: 7)
```
Story 2.6.1: Design grid UI/UX
Story 2.6.2: Implement grid component (React)
Story 2.6.3: Create API endpoint: GET /api/creatives
Story 2.6.4: Implement filtering + sorting
Story 2.6.5: Implement search functionality
Story 2.6.6: Add action buttons (view, delete, archive)
Story 2.6.7: Implement pagination + lazy loading
```

#### Dependencies
- EPIC 2.1 (Auth)
- EPIC 2.5 (Publishing - needs creatives)

#### Success Criteria
- ✅ Grid loads < 2s
- ✅ Filter works in combinations
- ✅ Search works real-time
- ✅ Actions are responsive
- ✅ Pagination works
- ✅ Mobile responsive

#### Owner
@dev (Dex)

#### Timeline
Weeks 10-11

---

### EPIC 2.7: Error Handling & Recovery

#### Goal
Robust error recovery com retry automático + user notifications

#### Scope
- Retry logic (exponential backoff: 1m, 2m, 4m)
- Max 3 retries per operation
- User-friendly error messages
- Manual retry option
- Browser notifications
- Email notifications (daily summary)
- Fallback options (download, manual publish)
- Error logging + monitoring

#### Stories (Estimated: 6)
```
Story 2.7.1: Design error handling patterns
Story 2.7.2: Implement retry queue (Bull)
Story 2.7.3: Add exponential backoff logic
Story 2.7.4: Create error messaging system
Story 2.7.5: Implement browser notifications
Story 2.7.6: Add email notification system
```

#### Dependencies
- EPIC 2.3 (Pipeline)
- EPIC 2.5 (Publishing)

#### Success Criteria
- ✅ Retry on any failure
- ✅ Max 3 attempts
- ✅ Clear error messages
- ✅ User can manually retry
- ✅ Notifications work reliably
- ✅ Fallback options available

#### Owner
@dev (Dex) + @qa (Quinn)

#### Timeline
Weeks 11-12

---

## 🎯 EPIC 3: Production Ready (Phase 2)

**Epic Goal:** 5 plataformas, analytics, monetização

**Timeline:** Weeks 13-24
**Resources:** +1 QA engineer, +1 Infra engineer
**Stories:** ~40

---

### EPIC 3.1: Multi-Platform Publishing

#### Sub-Epics
- 3.1.1: Instagram Reels Publishing
- 3.1.2: Facebook Video Publishing
- 3.1.3: YouTube Shorts Publishing
- 3.1.4: X/Twitter API (Phase 2+)

#### Stories per Sub-Epic: ~8-10
#### Timeline: Weeks 13-20
#### Owner: @dev (Dex) + @devops (Gage)

---

### EPIC 3.2: Analytics Dashboard

#### Goal
Mostrar performance dos vídeos (views, likes, shares) por plataforma

#### Scope
- API integrations (TikTok, Instagram, YouTube, Facebook)
- Data aggregation (daily polling)
- Dashboard visualizations (line charts, comparisons)
- Per-video analytics
- Platform-specific metrics
- Export as CSV

#### Stories: ~8
#### Timeline: Weeks 19-21
#### Owner: @dev (Dex) + @analyst (Alex)

---

### EPIC 3.3: Video Metadata Editor

#### Goal
Permitir edição de captions, hashtags, descrição pós-geração

#### Scope
- Modal editor UI
- Caption editor (word counter)
- Hashtag suggestions (trending)
- Description editor (per-platform)
- Metadata validation
- Re-publish option

#### Stories: ~6
#### Timeline: Weeks 17-18
#### Owner: @dev (Dex)

---

### EPIC 3.4: Scheduling & Queue Management

#### Goal
Agendar publicação para data/hora específica

#### Scope
- Datepicker UI
- Queue visualization
- Priority queue (premium users first)
- Concurrency limits (5 jobs/user)
- Background scheduler (cron)

#### Stories: ~7
#### Timeline: Weeks 21-22
#### Owner: @dev (Dex) + @devops (Gage)

---

### EPIC 3.5: Content Moderation System

#### Goal
Detectar conteúdo violento, hateful, NSFW antes de publicar

#### Scope
- OpenAI Moderation API integration
- Pre-upload content check
- Auto-tagging (sensitivity levels)
- Manual review queue
- User override (logged)
- Compliance reporting

#### Stories: ~8
#### Timeline: Weeks 16-18
#### Owner: @dev (Dex) + @qa (Quinn)

---

### EPIC 3.6: Monetization (Billing & Subscriptions)

#### Goal
Implementar planos pagos (Free, Pro, Agency)

#### Scope
- Stripe integration
- Subscription plans (Free, Pro $49, Agency $199)
- Usage tracking (creatives/month)
- Billing portal
- Invoice generation
- Dunning (payment retry)

#### Stories: ~10
#### Timeline: Weeks 22-24
#### Owner: @dev (Dex) + @devops (Gage)

---

## 🏢 EPIC 4: Enterprise Features (Phase 3)

**Timeline:** Weeks 25-36
**Resources:** +2 engineers, +1 PM
**Stories:** ~35

### Sub-Epics
- 4.1: Workspace & Team Management
- 4.2: Role-Based Access Control (RBAC)
- 4.3: Brand Kit Management
- 4.4: API Access & Integrations
- 4.5: White-Label Capabilities
- 4.6: Enterprise Analytics & Reporting

---

## 🚀 EPIC 5: Expansion & AI (Phase 4+)

**Timeline:** Weeks 37+
**Resources:** +2 ML engineers
**Stories:** ~30+

### Sub-Epics
- 5.1: Creator Style Learning
- 5.2: Trend Prediction Engine
- 5.3: Multi-Language Support
- 5.4: Audio Generation (TTS + Music)
- 5.5: Mobile App (iOS + Android)
- 5.6: Advanced Performance Analytics

---

## 📊 DEPENDENCY GRAPH

```
EPIC 1 (Foundation)
├─ EPIC 2.1 (Auth)
│  ├─ EPIC 2.2 (Form)
│  │  ├─ EPIC 2.3 (Pipeline) ← CRITICAL PATH
│  │  │  ├─ EPIC 2.4 (Dashboard)
│  │  │  └─ EPIC 2.5 (Publishing) ← requires Agent 4 video
│  │  └─ EPIC 2.6 (Library)
│  └─ EPIC 2.7 (Error Handling)
│
EPIC 3 (Production)
├─ EPIC 3.1 (Multi-Platform) ← requires EPIC 2.5 working
├─ EPIC 3.2 (Analytics)
├─ EPIC 3.3 (Metadata Editor)
├─ EPIC 3.4 (Scheduling)
├─ EPIC 3.5 (Moderation)
└─ EPIC 3.6 (Monetization)

EPIC 4 (Enterprise) ← after EPIC 3 stable
EPIC 5 (Expansion) ← after EPIC 4 stable
```

---

## 🎬 WAVE-BASED DEVELOPMENT PLAN

### Wave 1 (Weeks 1-4): Foundation + Auth
```
EPIC 1: Foundation & Setup (parallel)
EPIC 2.1: User Authentication
EPIC 2.2: Creative Form
```

### Wave 2 (Weeks 5-8): Agent Pipeline
```
EPIC 2.3: Agent Pipeline (Agents 1-3)
EPIC 2.4: Dashboard (started)
Continued Agent development
```

### Wave 3 (Weeks 8-12): Publishing + Library
```
EPIC 2.3: Agent Pipeline (Agents 4-5 completion)
EPIC 2.4: Dashboard (completion)
EPIC 2.5: TikTok Publishing
EPIC 2.6: Creative Library
EPIC 2.7: Error Handling
```

### Wave 4+ (Weeks 13+): Multi-Platform + Enterprise
```
EPIC 3: Production features
EPIC 4: Enterprise features
EPIC 5: Expansion + AI
```

---

## ✅ MVP GATE CRITERIA

**Before proceeding to EPIC 3:**

```
□ EPIC 2.1: Auth working (50+ users)
□ EPIC 2.2: Form validated + tested
□ EPIC 2.3: 6-agent pipeline operational
□ EPIC 2.4: Dashboard showing real-time status
□ EPIC 2.5: TikTok publishing end-to-end
□ EPIC 2.6: Library with history
□ EPIC 2.7: Error recovery working

Quality Criteria:
□ 85%+ success rate (first attempt)
□ < 5 min E2E latency (P95)
□ NPS > 40
□ COGS < $0.25/video
□ 200+ signups
□ 50+ active beta users
```

---

## 📋 NEXT STEP: ASSIGN TO @sm

**Ready for:** @sm (River - Scrum Master)

**Action Items for @sm:**
1. [ ] Review epics for story breakdown
2. [ ] Estimate story points (Planning Poker)
3. [ ] Create stories for EPIC 1 + EPIC 2.1 + EPIC 2.2
4. [ ] Plan Sprint 1 (Weeks 1-4)
5. [ ] Assign stories to @dev team

---

**Document Status:** ✅ READY FOR SCRUM MASTER
**Prepared by:** Morgan (PM)
**Next Owner:** River (@sm - Scrum Master)
**Last Updated:** 11 de Março de 2026

*Épicos v1.0 — Wave-based development structure — Ready for Sprint Planning*
