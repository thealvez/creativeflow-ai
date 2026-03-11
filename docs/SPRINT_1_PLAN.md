# 🚀 SPRINT 1 PLAN
## CreativeFlow AI — MVP Foundation & User Authentication

**Sprint Number:** Sprint 1
**Duration:** 2 weeks (Weeks 1-2 of Phase 1)
**Start Date:** March 17, 2026
**End Date:** March 30, 2026
**Status:** 🟢 READY FOR KICKOFF

---

## 🎯 SPRINT GOAL

**Estabelecer infraestrutura, APIs, e autenticação de usuário para suportar desenvolvimento da pipeline de agentes (EPIC 2.3) a partir da semana 3.**

### Success Criteria
- ✅ GitHub repo operacional com CI/CD pipeline
- ✅ Development environment setup (local + staging)
- ✅ Database schema deployed (PostgreSQL)
- ✅ OAuth 2.0 (Google, GitHub) funcionando end-to-end
- ✅ User profile management working
- ✅ Monitoramento + logging configurado
- ✅ 0 blocking issues for Sprint 2

---

## 📋 SPRINT BACKLOG (26 Stories)

### EPIC 1: Foundation & Setup (12 stories)

#### Story 1.1.1: Initialize Git Repository + GitHub Setup
**Story Points:** 3
**Owner:** @devops (Gage)
**Description:**
- Create GitHub repository
- Setup GitHub Actions workflows
- Configure branch protection rules (main)
- Setup codeowners file
- Configure GitHub secrets

**Acceptance Criteria:**
- ✅ Repo accessible via GitHub
- ✅ Main branch protected (requires PR review)
- ✅ GitHub Actions ready (template)
- ✅ README with setup instructions
- ✅ Contributing guidelines documented

**Dependencies:** None
**Blocks:** All other stories

---

#### Story 1.1.2: Setup Node.js Project Structure (Monorepo)
**Story Points:** 5
**Owner:** @dev (Dex)
**Description:**
- Create monorepo structure (packages/frontend, packages/backend, packages/agents)
- Setup package.json (root + packages)
- Configure npm workspaces
- Setup TypeScript config (shared + per-package)
- Configure ESLint + Prettier

**Acceptance Criteria:**
- ✅ Monorepo runs `npm install` successfully
- ✅ TypeScript compilation works
- ✅ ESLint passes on all packages
- ✅ Prettier formatting enforced
- ✅ Scripts work: `npm run lint`, `npm run typecheck`

**Dependencies:** Story 1.1.1
**Blocks:** Story 1.1.3

---

#### Story 1.1.3: Configure package.json (Dependencies)
**Story Points:** 3
**Owner:** @dev (Dex)
**Description:**
- Add core dependencies:
  - Frontend: Next.js 15, React, TailwindCSS, ShadCN, Axios, React Query
  - Backend: Fastify, PostgreSQL (pg), Redis (redis), Bull (job queue)
  - Agents: LangChain, OpenAI SDK, Google Generative AI SDK
- Pin versions (no wildcards)
- Document why each dependency exists

**Acceptance Criteria:**
- ✅ All dependencies installed without errors
- ✅ No security vulnerabilities (npm audit)
- ✅ Versions pinned (exact, not ^)
- ✅ README documents major dependencies

**Dependencies:** Story 1.1.2
**Blocks:** Story 1.1.4, Story 1.2.x

---

#### Story 1.1.4: Setup Development Environment (.env, .vscode)
**Story Points:** 2
**Owner:** @dev (Dex)
**Description:**
- Create .env.example (no secrets)
- Create .vscode/settings.json (formatting, linting)
- Create .vscode/extensions.json (recommended)
- Document environment setup in README
- Create docker-compose.yml (local Postgres + Redis)

**Acceptance Criteria:**
- ✅ .env.example has all required vars (clearly labeled)
- ✅ VSCode extensions recommended
- ✅ Docker Compose brings up Postgres + Redis
- ✅ Local development works without errors
- ✅ README has setup steps

**Dependencies:** Story 1.1.3
**Blocks:** None (can proceed in parallel)

---

#### Story 1.2.1: Create Terraform Configs (Vercel + Railway)
**Story Points:** 5
**Owner:** @devops (Gage)
**Description:**
- Create Terraform state management (S3 backend)
- Configure Vercel project (frontend deployment)
- Configure Railway project (backend deployment)
- Setup environment variables per environment (dev, staging, prod)
- Create deployment workflow (GitHub Actions → Terraform)

**Acceptance Criteria:**
- ✅ Terraform deploys Vercel project
- ✅ Terraform deploys Railway project
- ✅ Environment variables set correctly
- ✅ GitHub Actions trigger on push (main branch)
- ✅ Manual deployment also works

**Dependencies:** Story 1.1.1
**Blocks:** Story 1.2.2, Story 1.2.3

---

#### Story 1.2.2: Setup PostgreSQL (Neon)
**Story Points:** 3
**Owner:** @devops (Gage)
**Description:**
- Create Neon database project
- Setup connection string (environment variable)
- Create schema migration system (Knex.js or similar)
- Create initial schema (users, creatives, videos tables)
- Document schema in SCHEMA.md

**Acceptance Criteria:**
- ✅ Connection string works (dev + staging + prod)
- ✅ Initial schema migrations run
- ✅ Database accessible from backend
- ✅ Backup strategy documented
- ✅ SCHEMA.md updated

**Dependencies:** Story 1.2.1
**Blocks:** Story 2.1.3 (user model)

---

#### Story 1.2.3: Setup Redis (Redis Cloud)
**Story Points:** 2
**Owner:** @devops (Gage)
**Description:**
- Create Redis Cloud project
- Setup connection string
- Test connection from backend
- Configure TTL policies (sessions, cache)
- Document usage patterns

**Acceptance Criteria:**
- ✅ Connection string works
- ✅ Can SET/GET keys from backend
- ✅ TTL policies configured
- ✅ Monitoring alerts setup (memory usage)

**Dependencies:** Story 1.2.1
**Blocks:** EPIC 2.7 (error handling with Bull)

---

#### Story 1.2.4: Configure Networking (HTTPS, Domains)
**Story Points:** 3
**Owner:** @devops (Gage)
**Description:**
- Register domain (creativeflow.app or similar)
- Setup SSL certificate (auto-renew)
- Configure DNS records (Vercel + Railway)
- Setup CORS policy (frontend domain)
- Configure environment-specific URLs

**Acceptance Criteria:**
- ✅ Domain resolves to Vercel
- ✅ HTTPS works (no warnings)
- ✅ SSL cert auto-renews
- ✅ CORS configured correctly
- ✅ API endpoints accessible

**Dependencies:** Story 1.2.1
**Blocks:** Story 2.1.2 (OAuth callbacks)

---

#### Story 1.3.1: Create GitHub Actions Workflow (Lint + Test)
**Story Points:** 4
**Owner:** @devops (Gage)
**Description:**
- Create CI workflow (.github/workflows/ci.yml)
- Run linting (ESLint) on all packages
- Run type checking (TypeScript)
- Run unit tests (Jest)
- Block merge if any step fails

**Acceptance Criteria:**
- ✅ Workflow runs on every push
- ✅ Lint passes on all files
- ✅ TypeScript compiles without errors
- ✅ Tests run and pass
- ✅ Build artifacts available

**Dependencies:** Story 1.1.1
**Blocks:** Story 1.3.2

---

#### Story 1.3.2: Setup Automated Testing Pipeline
**Story Points:** 3
**Owner:** @qa (Quinn)
**Description:**
- Configure Jest (unit tests)
- Setup test database (isolated)
- Create test utilities (factories, mocks)
- Configure coverage thresholds (>80%)
- Document testing standards

**Acceptance Criteria:**
- ✅ Jest runs with `npm test`
- ✅ Tests use isolated database
- ✅ Coverage reports generated
- ✅ Tests pass with 0 warnings
- ✅ CI fails if coverage < 80%

**Dependencies:** Story 1.3.1
**Blocks:** Developer work (must test all code)

---

#### Story 1.3.3: Configure Deployment Pipeline (Staging + Prod)
**Story Points:** 4
**Owner:** @devops (Gage)
**Description:**
- Create deployment workflow (.github/workflows/deploy.yml)
- Staging deploys on every merge to main
- Prod deploys on git tag (vX.Y.Z)
- Database migrations run automatically
- Rollback procedure documented

**Acceptance Criteria:**
- ✅ Staging auto-deploys on main merge
- ✅ Prod deploys on tag
- ✅ Database migrations run
- ✅ Previous version accessible (rollback)
- ✅ Deployment logs clear

**Dependencies:** Story 1.3.1, Story 1.2.1
**Blocks:** Testing in staging

---

#### Story 1.3.4: Setup Monitoring Alerts (Datadog/NewRelic)
**Story Points:** 3
**Owner:** @devops (Gage)
**Description:**
- Sign up for Datadog/NewRelic (free tier)
- Configure APM (Application Performance Monitoring)
- Setup error tracking
- Create dashboards (latency, errors, requests)
- Configure Slack notifications

**Acceptance Criteria:**
- ✅ Backend sends metrics to Datadog
- ✅ Dashboard shows latency, errors, requests
- ✅ Alerts on error rate > 5%
- ✅ Slack notifications work
- ✅ Documentation for on-call team

**Dependencies:** Story 1.2.1
**Blocks:** Production launch

---

### EPIC 2.1: User Authentication & Profiles (8 stories)

#### Story 2.1.1: Design OAuth Flow (Google + GitHub)
**Story Points:** 3
**Owner:** @architect (Aria)
**Description:**
- Document OAuth 2.0 flow (authorization code flow)
- Design database schema for OAuth integrations
- Define scopes needed (email, profile)
- Create sequence diagram
- Document error scenarios

**Acceptance Criteria:**
- ✅ OAuth flow documented (GitHub wiki)
- ✅ Sequence diagram created
- ✅ Scopes clearly defined
- ✅ Error handling strategies documented
- ✅ Security review passed

**Dependencies:** None
**Blocks:** Story 2.1.2

---

#### Story 2.1.2: Implement OAuth Callback Handler
**Story Points:** 5
**Owner:** @dev (Dex)
**Description:**
- Create OAuth endpoints:
  - GET /api/auth/google (redirect to Google)
  - GET /api/auth/google/callback (handle response)
  - GET /api/auth/github (redirect to GitHub)
  - GET /api/auth/github/callback (handle response)
- Exchange authorization code for tokens
- Verify token signature
- Create/update user in database
- Set JWT session cookie

**Acceptance Criteria:**
- ✅ Google sign in works end-to-end
- ✅ GitHub sign in works end-to-end
- ✅ User created in database
- ✅ JWT session cookie set
- ✅ Can access protected routes with token

**Dependencies:** Story 1.2.2, Story 2.1.1
**Blocks:** Story 2.1.6

---

#### Story 2.1.3: Create User Model + Database Schema
**Story Points:** 3
**Owner:** @dev (Dex)
**Description:**
- Create User table:
  - id (UUID)
  - email (unique)
  - name
  - avatar_url
  - bio
  - oauth_accounts (JSON: { google_id, github_id, etc })
  - subscription_tier (free, pro, agency)
  - created_at
  - updated_at
- Create indices (email, oauth_id)
- Create migration file
- Create Knex seeder (test user)

**Acceptance Criteria:**
- ✅ Migration runs successfully
- ✅ Indices created
- ✅ Can insert/query users
- ✅ Constraints enforced (unique email)
- ✅ Test user seeded

**Dependencies:** Story 1.2.2
**Blocks:** Story 2.1.2, Story 2.1.4

---

#### Story 2.1.4: Implement JWT Token Management
**Story Points:** 4
**Owner:** @dev (Dex)
**Description:**
- Create JWT utility (sign, verify, refresh)
- Implement token generation on login
- Implement token refresh logic (background job)
- Store refresh tokens in Redis (TTL: 7 days)
- Create middleware to verify tokens
- Handle token expiry gracefully

**Acceptance Criteria:**
- ✅ JWT tokens signed and verified
- ✅ Token refresh works
- ✅ Expired tokens rejected
- ✅ Middleware protects routes
- ✅ Can check token status

**Dependencies:** Story 1.2.3
**Blocks:** Story 2.1.5, Story 2.1.6

---

#### Story 2.1.5: Build Sign Up Form + Validation
**Story Points:** 4
**Owner:** @dev (Dex)
**Description:**
- Create sign up form (React component)
- Add OAuth buttons (Google, GitHub)
- Client-side validation (email format)
- Error messages (user-friendly)
- Loading state + feedback
- Responsive design (mobile-first)

**Acceptance Criteria:**
- ✅ Form renders correctly
- ✅ OAuth buttons functional
- ✅ Validation shows inline errors
- ✅ Form submits to API
- ✅ Mobile responsive
- ✅ Loading spinner appears

**Dependencies:** Story 2.1.2
**Blocks:** Story 2.1.6

---

#### Story 2.1.6: Build Login Form + OAuth Redirect
**Story Points:** 3
**Owner:** @dev (Dex)
**Description:**
- Create login page (Next.js page)
- Add OAuth sign in buttons
- Handle OAuth redirect (success + error)
- Create session from token
- Redirect to dashboard after login
- Handle already-logged-in users

**Acceptance Criteria:**
- ✅ Login page loads
- ✅ OAuth redirect works
- ✅ Session set after callback
- ✅ Redirects to dashboard
- ✅ Already logged-in users redirected

**Dependencies:** Story 2.1.4, Story 2.1.5
**Blocks:** Story 2.1.8

---

#### Story 2.1.7: Implement Password Reset Flow
**Story Points:** 4
**Owner:** @dev (Dex)
**Description:**
- Create "Forgot Password" form
- Generate reset tokens (secure, 1h TTL)
- Send reset email (SendGrid or similar)
- Create password reset page
- Validate token + set new password
- Invalidate reset token after use

**Acceptance Criteria:**
- ✅ Forgot password form works
- ✅ Email sent with reset link
- ✅ Reset link works (1h window)
- ✅ Password updated
- ✅ Token invalidated after use

**Dependencies:** Story 2.1.4
**Blocks:** None (nice-to-have for Sprint 1)

---

#### Story 2.1.8: Create User Profile Page + Settings
**Story Points:** 5
**Owner:** @dev (Dex)
**Description:**
- Create profile page (Next.js route: /profile)
- Display user info (name, email, avatar)
- Allow edit: name, bio, avatar upload
- Show connected platforms (TikTok, Instagram, etc.)
- Disconnect platform option
- Show subscription tier + usage stats
- Settings: timezone, notifications, privacy

**Acceptance Criteria:**
- ✅ Profile page loads
- ✅ Can edit name/bio
- ✅ Avatar upload works
- ✅ Connected platforms displayed
- ✅ Can disconnect platforms
- ✅ Settings saved to database

**Dependencies:** Story 2.1.6
**Blocks:** EPIC 2.2 (form submission uses authenticated user)

---

### EPIC 2.2: Create Creative Form & Validation (6 stories)

#### Story 2.2.1: Design Form UI/UX (Figma)
**Story Points:** 3
**Owner:** Designer
**Description:**
- Create Figma designs for:
  - Create Creative form (input fields, buttons)
  - Success confirmation modal
  - Error states
  - Mobile responsive variations
- Get feedback from PM
- Document design system (spacing, colors, fonts)

**Acceptance Criteria:**
- ✅ Form design in Figma
- ✅ Mobile variation designed
- ✅ Error states documented
- ✅ Approved by PM
- ✅ Design system documented

**Dependencies:** None
**Blocks:** Story 2.2.2

---

#### Story 2.2.2: Build Form Component (React)
**Story Points:** 4
**Owner:** @dev (Dex)
**Description:**
- Create form component (React Hook Form)
- Implement fields:
  - Idea description (textarea, max 500 chars)
  - Platform selection (checkboxes)
  - Optional: language, tone, audience
- Character counter on textarea
- Form validation (client-side)
- Submit button (disabled while loading)
- Error message display

**Acceptance Criteria:**
- ✅ Form renders correctly
- ✅ All fields functional
- ✅ Character counter works
- ✅ Validation real-time
- ✅ Mobile responsive
- ✅ Loading state clear

**Dependencies:** Story 2.2.1, Story 2.1.8
**Blocks:** Story 2.2.4

---

#### Story 2.2.3: Implement Client-Side Validation
**Story Points:** 2
**Owner:** @dev (Dex)
**Description:**
- Validate form on submit:
  - Idea: min 10 chars, max 500 chars
  - At least 1 platform selected
  - Language: enum validation
  - Tone: enum validation
- Show inline error messages
- Highlight error fields (red border)
- Clear errors on fix

**Acceptance Criteria:**
- ✅ Min/max validation enforced
- ✅ Platform required
- ✅ Error messages clear
- ✅ Errors clear on fix
- ✅ Form blocks submit if invalid

**Dependencies:** Story 2.2.2
**Blocks:** None (depends on server validation)

---

#### Story 2.2.4: Create API Endpoint: POST /api/creatives
**Story Points:** 5
**Owner:** @dev (Dex)
**Description:**
- Create POST /api/creatives endpoint
- Validate request body (server-side)
- Generate job UUID
- Store in database (creatives table):
  - id (UUID)
  - user_id (FK)
  - idea (text)
  - platforms (array)
  - status (pending, processing, completed, failed)
  - created_at
- Return job_id + status
- Handle authentication (must be logged in)

**Acceptance Criteria:**
- ✅ Endpoint accepts POST request
- ✅ Validates request body
- ✅ Job stored in database
- ✅ Returns job_id
- ✅ Non-authenticated requests rejected
- ✅ Unit tests pass

**Dependencies:** Story 2.1.4, Story 1.2.2
**Blocks:** Story 2.2.6

---

#### Story 2.2.5: Implement Server-Side Validation
**Story Points:** 3
**Owner:** @dev (Dex)
**Description:**
- Validate all form fields (server):
  - Idea: min 10 chars, max 500 chars
  - Platforms: non-empty array
  - Language: enum (EN, PT-BR, ES, FR)
  - Tone: enum (Professional, Casual, Playful, Educational)
- Return clear error messages
- Log validation errors (for analytics)
- Rate limit: max 10 creatives per user per day (MVP)

**Acceptance Criteria:**
- ✅ Invalid requests rejected (400)
- ✅ Error messages clear
- ✅ Rate limit enforced
- ✅ Validation logged
- ✅ Unit tests pass

**Dependencies:** Story 2.2.4
**Blocks:** None

---

#### Story 2.2.6: Add Success Confirmation + Job Tracking
**Story Points:** 3
**Owner:** @dev (Dex)
**Description:**
- Show success modal after submit
- Display job_id (for reference)
- "Processing started..." message
- Button: "Go to Dashboard" (redirect)
- Button: "Create Another" (reset form)
- Query job status from API (polling or WebSocket)
- Show "Processing..." state

**Acceptance Criteria:**
- ✅ Confirmation modal appears
- ✅ Job ID displayed
- ✅ Buttons functional
- ✅ Can redirect to dashboard
- ✅ Form resets properly

**Dependencies:** Story 2.2.4
**Blocks:** None

---

## 📊 SPRINT SUMMARY

### Backlog by Epic

```
EPIC 1: Foundation & Setup — 12 stories (32 points)
  ├─ 1.1: Project Setup (3+5+3+2 = 13 points)
  ├─ 1.2: Infrastructure (5+3+2+3 = 13 points)
  └─ 1.3: CI/CD (4+3+4+3 = 14 points)

EPIC 2.1: User Auth — 8 stories (31 points)
  ├─ Design & OAuth (3+5+3 = 11 points)
  ├─ JWT & Login (4+4+3 = 11 points)
  ├─ Password Reset (4 points)
  └─ Profile (5 points)

EPIC 2.2: Creative Form — 6 stories (21 points)
  ├─ Design & Component (3+4 = 7 points)
  ├─ Validation (2+3 = 5 points)
  ├─ API (5 points)
  └─ Confirmation (3 points)

TOTAL: 26 stories | 84 story points
```

### Velocity Estimation

```
Team size: 3 engineers (1 full-stack, 1 backend, 1 infra)
Sprint duration: 2 weeks
Estimated capacity: ~20-24 points/engineer
Sprint velocity target: 60-72 points

SPRINT 1: 84 points
└─ Distributed as:
   • @devops (Gage): Infrastructure stories (22 points)
   • @dev (Dex): Auth + Form stories (50 points)
   • @architect (Aria): Design review (3 points, support)
   • @designer: UI/UX (3 points, support)
   • @qa (Quinn): Testing setup (6 points, support)
```

---

## 🔄 DAILY STANDUP TEMPLATE

**When:** 10:00 AM UTC (15 min max)

**Questions:**
1. What did I complete since yesterday?
2. What am I working on today?
3. What blockers do I have?

**Escalation:**
- Blocker → immediately notify PM
- Design review → @architect
- Merge conflicts → @devops
- Testing questions → @qa

---

## ✅ DEFINITION OF DONE

**For each story:**
- [ ] Code written + peer reviewed (1 approval minimum)
- [ ] Unit tests written (>80% coverage)
- [ ] Tests pass (green CI pipeline)
- [ ] Lint passes (ESLint, Prettier)
- [ ] TypeScript compiles (no errors)
- [ ] Documentation updated (README, code comments)
- [ ] Merged to main branch
- [ ] Deployed to staging
- [ ] Verified working in staging

**For sprint:**
- [ ] All stories done or moved to next sprint
- [ ] No critical bugs in staging
- [ ] Backlog ready for Sprint 2

---

## 📦 DELIVERABLES

**End of Sprint 1:**
```
✅ GitHub repo with working CI/CD
✅ Development environment setup (local + staging)
✅ PostgreSQL + Redis configured
✅ OAuth 2.0 (Google, GitHub) working
✅ User profile management
✅ Create Creative form + validation
✅ API endpoint for job creation
✅ Database schema for users + creatives
✅ Monitoring + alerting setup
✅ All code merged to main
✅ Staging environment live
```

---

## 🎯 SPRINT 1 SUCCESS CRITERIA

**Must achieve:**
- ✅ 0 critical bugs in staging
- ✅ 100% CI/CD pipeline passing
- ✅ OAuth sign in working
- ✅ Create Creative form functional
- ✅ All stories completed or moved to Sprint 2

**Should achieve:**
- ✅ > 80% test coverage
- ✅ Staging fully functional (no regressions)
- ✅ Team confident in development process

**Nice to have:**
- ✅ Performance benchmarks documented
- ✅ Documentation polished

---

## 📅 SPRINT CALENDAR

```
Monday (Day 1):       Kickoff meeting, story refinement
Tuesday-Thursday:     Development, daily standups (10am)
Friday (Day 10):      Sprint review + retrospective

Week 2:
Monday-Thursday:      Continue development
Friday (Day 17):      Final push, sprint planning for Sprint 2
```

---

## 🚦 RISK ASSESSMENT

### High Risk Items

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|-----------|
| OAuth setup delays | Medium | High | Start Week 1, test sandbox |
| Database schema issues | Low | High | @architect reviews schema |
| Team unfamiliar with monorepo | Medium | Medium | Pair programming for setup |
| GitHub Actions complexity | Low | High | Use templates, document |

### Mitigation Strategy

```
Weekly check-ins on high-risk items
Pair programming for infrastructure setup
Clear escalation path to @architect/@devops
Reserve 20% buffer in velocity for unknowns
```

---

## 📋 HAND-OFF CHECKLIST

**From Morgan (PM) to @sm + @dev:**

- [x] EPICS.md created (story structure)
- [x] SPRINT_1_PLAN.md created (this document)
- [x] PRD.md completed (requirements)
- [x] API research completed (platform dependencies)
- [ ] @sm reviews stories + estimates
- [ ] @architect reviews technical design
- [ ] @dev ready to start development
- [ ] @devops ready to setup infrastructure

---

**Document Status:** ✅ READY FOR SPRINT KICKOFF
**Prepared by:** Morgan (Product Manager)
**For:** @sm (River - Scrum Master) + @dev (Dex) + @devops (Gage)
**Kickoff Date:** March 17, 2026
**Last Updated:** 11 de Março de 2026

*Sprint 1 Plan v1.0 — Foundation + Auth — Ready for execution*
