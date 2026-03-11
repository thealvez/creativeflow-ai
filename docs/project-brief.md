# 📊 PROJECT BRIEF — CreativeFlow AI
## SaaS de Criação e Publicação Automatizada de Vídeos Criativos

**Data de Criação:** 11 de Março de 2026
**Preparado por:** Atlas (Analyst)
**Status:** Briefing Executivo | Pronto para Validação
**Versão:** 1.0

---

## 🎯 BRIEFING EXECUTIVO

### Visão
Transformar criadores de conteúdo, pequenas agências e marcas em super-produtores de vídeo, eliminando a complexidade técnica e o tempo de edição manual através de orquestração inteligente de agentes IA.

### Missão
Automatizar 80% do ciclo de criação de conteúdo visual (da ideia à publicação multikanal) em menos de 5 minutos, mantendo qualidade e personalização por plataforma.

### Posicionamento
**CreativeFlow AI** é a plataforma de automação de conteúdo visual para criadores que pensam em múltiplas plataformas simultaneamente.

---

## 🔍 PROBLEMA & OPORTUNIDADE

### Problema Primário
**Criadores de conteúdo enfrentam:**
- ⏱️ Ciclo manual de 4-8 horas: ideação → criação visual → edição → adaptação multikanal → publicação
- 🎬 Necessidade de múltiplas skills: copywriting, design, videomaking, edição, social media strategy
- 💰 Custo elevado: ferramentas subscrito (Canva, Adobe, CapCut, etc.) + tempo humano
- 📱 Fricção multicanal: cada plataforma requer formatos, durações e proporções diferentes
- 🔄 Repetição manual: mesmo conteúdo precisa ser adaptado 4-5 vezes (TikTok, Reels, Shorts, feed, etc.)

### Oportunidade de Mercado
- **Mercado total:** ~50M criadores globais + ~5M pequenas agências
- **Segmento alvo:** 5-10M criadores profissionais/semi-profissionais que publicam 4-7 dias/semana
- **Valor econômico:** Economia de 15-20 horas/semana em operações repetitivas
- **Monetização:** $29-99/mês por criador (escalável para agências em $199-499/mês)

### Tese de Valor
Agentes IA orquestrados podem:
1. Entender intenção criativa com contexto
2. Gerar assets visuais nativos e otimizados por plataforma
3. Publicar atomicamente sem intervenção manual
4. Aprender preferências através de feedback loop

---

## 👥 PÚBLICO-ALVO

### Persona 1: Creator Profissional
- **Quem:** YouTubers, TikTokers, Instagrammers com 100K-10M seguidores
- **Dor:** Tempo de produção vs. volume de conteúdo necessário
- **Tamanho:** ~2M globais
- **Disposição de Pagar:** $49-99/mês

### Persona 2: Pequena Agência de Conteúdo
- **Quem:** Agências com 5-20 pessoas focadas em social media e produção
- **Dor:** Escalabilidade de produção para múltiplos clientes
- **Tamanho:** ~500K globais
- **Disposição de Pagar:** $199-499/mês

### Persona 3: Marketer In-House
- **Quem:** Coordenadores/especialistas de marketing em PMEs (50-500 funcionários)
- **Dor:** Ampliar frequência de publicação sem aumentar headcount
- **Tamanho:** ~3M globais
- **Disposição de Pagar:** $79-199/mês

### Persona 4: Creator Emergente
- **Quem:** Aspirantes e creators iniciantes (0-50K seguidores)
- **Dor:** Ferramentas profissionais com preço baixo
- **Tamanho:** ~40M globais (baixa conversão esperada)
- **Disposição de Pagar:** $9-29/mês

---

## 💎 PROPOSTA DE VALOR

| Benefício | CreativeFlow AI | Fluxo Manual | Economia |
|-----------|-----------------|-------------|----------|
| Tempo (ideia → 5 plataformas) | 5 min | 4-8 horas | 95% |
| Custo mensal (ferramentas) | $79-199 | $100-300 | 30-50% |
| Consistência visual | 95%+ | 60-70% | +25-35% |
| Volume de publicações | 7x/semana | 2-3x/semana | +200-250% |
| Adaptação multikanal | Automática | Manual | 6-8h/semana |

### Diferenciadores Competitivos
1. **Orquestração de agentes**: Não é "ferramenta de templates" — é sistema inteligente que adapta autonomamente
2. **Otimização por plataforma**: Trata TikTok ≠ Instagram ≠ YouTube (algoritmos, audiências, durações diferentes)
3. **Feedback loop**: Aprende com performance (likes, views, shares) e ajusta próximas criações
4. **Publicação atômica**: Publica em 5 plataformas simultaneamente com tratamento independente
5. **Zero config**: Usuário não precisa entender IA, prompts ou APIs

---

## 🔄 FLUXO PONTA A PONTA

### 1️⃣ ENTRADA (User Input)
```
User → Dashboard → Form: "Describe your creative idea"
Exemplo: "Dica rápida de produtividade: use Pomodoro com pausas de 2min"
```

### 2️⃣ ORQUESTRAÇÃO DE AGENTES (Backend)
```
┌─────────────────────────────────────────────────────────┐
│ INPUT PROCESSOR                                         │
│ └─ Parse ideia, detectar contexto (tutorial/tip/story) │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ AGENT 1: Creative Prompt Generator                      │
│ Input: Ideia bruta                                      │
│ Output: Prompt criativo estruturado (com elementos)    │
│ Tool: Claude 3.5 Sonnet                                │
│ Exemplos de output:                                    │
│  - Scene structure: [Opening hook] → [CTA]             │
│  - Visual elements: [Color palette, motion, style]     │
│  - Tone: [Energetic, educational, casual]              │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ AGENT 2: Visual Prompt Converter                        │
│ Input: Prompt criativo                                 │
│ Output: Prompts visuais por plataforma                 │
│ Tool: Claude (prompt engineering)                      │
│ Outputs:                                               │
│  - TikTok: [9:16, fast cuts, trending sounds]          │
│  - Reels: [9:16, 30-60s, hook in 1s]                  │
│  - Shorts: [9:16, 60s, text overlay]                  │
│  - Feed: [16:9, 60-120s, cinematic]                   │
│  - YouTube: [16:9, 120-300s, narrative]                │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ AGENT 3: Image Generator                               │
│ Input: Visual prompt para cada plataforma               │
│ Output: Imagem de alta qualidade (1024x1024)           │
│ Tool: Gemini 2.0 Flash (fast, quality)                │
│        OR Nano Banana (fallback, cheaper)              │
│ Retry logic: 3 tentativas com backoff exponencial      │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ AGENT 4: Video Generator (Grok Imagine)               │
│ Input: Imagem + Visual prompt (incluindo movimento)    │
│ Output: Vídeo 1080p por plataforma                    │
│ Processing:                                            │
│  - Grok Imagine (primary): Video gen com AI            │
│  - Fallback: Stock footage + motion overlay            │
│  - Duration: Auto-adaptado por plataforma              │
│  - Retry queue: Re-enqueue se falhar                   │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ AGENT 5: Metadata & Captions Generator                 │
│ Input: Ideia original + prompts criativos               │
│ Output: Captions, hashtags, descrições por plataforma  │
│ Tool: Claude (contextual generation)                   │
│ Outputs:                                               │
│  - Captions: [Platform-specific, length-optimized]     │
│  - Hashtags: [Trending, niche, reach-optimized]        │
│  - Descriptions: [SEO-optimized para cada plataforma]  │
│  - Timestamps: [Para YouTube chapters]                 │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ AGENT 6: Publisher & Scheduler                         │
│ Input: Vídeos finalizados + metadados                   │
│ Output: Status de publicação em 5 plataformas          │
│ Platform APIs:                                         │
│  - TikTok: TikTok Business API                         │
│  - Instagram: Meta Graph API (Reels)                   │
│  - YouTube: YouTube Data API v3                        │
│  - Facebook: Meta Graph API (Video)                    │
│  - Twitter/X: X API v2 (opcional Phase 2)              │
│ Handling:                                              │
│  - Atomicity: Tenta todas, registra falhas             │
│  - Retry: Fila de retry com backoff                    │
│  - Timing: Suporta scheduling futuro                   │
│  - Fallback: Gera link de download se API falhar       │
└──────────┬──────────────────────────────────────────────┘
           │
┌──────────▼──────────────────────────────────────────────┐
│ MONITORING & FEEDBACK                                   │
│ - Logs estruturados em cada etapa (JSON)               │
│ - Métricas: latência, taxa de sucesso, custos          │
│ - Webhooks: Notificações em tempo real                 │
│ - Dashboard: Status consolidado                        │
└──────────────────────────────────────────────────────────┘
```

### 3️⃣ SAÍDA (Dashboard)
```
User Dashboard mostra:
├─ Status em tempo real: [⏳ Processing...] ou [✅ Published]
├─ Vídeos gerados (5 versões):
│  ├─ TikTok (9:16, 30s) — View/Share count (se já publicado)
│  ├─ Reels (9:16, 45s) — Engagement metrics
│  ├─ Shorts (9:16, 60s) — Performance
│  ├─ Feed (16:9, 90s) — Stats
│  └─ YouTube (16:9, 180s) — Views, retention
├─ Logs e detalhes técnicos (expandible)
└─ Ações: Edit, Republish, Schedule, Archive
```

---

## 🤖 DEFINIÇÃO DOS AGENTES

### Agent 1: Creative Prompt Engineer (Dex)
| Atributo | Valor |
|----------|-------|
| **Responsabilidade** | Transformar ideia bruta em prompt criativo estruturado |
| **Inputs** | Texto da ideia + contexto (categoria, plataforma-alvo) |
| **Outputs** | JSON com scene structure, visual elements, tone, pacing |
| **Model** | Claude 3.5 Sonnet |
| **Error Handling** | Retry 2x com reformulação |
| **Timeout** | 30s |
| **Cost** | ~$0.002 por execução |

### Agent 2: Visual Prompt Converter (Aria)
| Atributo | Valor |
|----------|-------|
| **Responsabilidade** | Adaptar prompt criativo para specs visuais de cada plataforma |
| **Inputs** | Prompt criativo + plataforma target |
| **Outputs** | 5 prompts visuais otimizados (TikTok, Reels, Shorts, Feed, YouTube) |
| **Model** | Claude 3.5 Sonnet (prompt engineering) |
| **Rules** | Inclui aspectos técnicos (durações, resoluções, transitions) |
| **Timeout** | 20s |
| **Cost** | ~$0.003 por execução (5 variantes) |

### Agent 3: Image Generator (Dara)
| Atributo | Valor |
|----------|-------|
| **Responsabilidade** | Gerar imagem-base para cada plataforma |
| **Inputs** | Visual prompt para 1 plataforma |
| **Outputs** | Imagem otimizada (1024x1024 ou aspect ratio específico) |
| **Primary Tool** | Google Gemini 2.0 Flash (fast image gen) |
| **Fallback Tool** | Nano Banana (Replicate) — mais barato |
| **Retry Logic** | 3 tentativas com backoff (1s, 2s, 4s) |
| **Timeout** | 45s por imagem |
| **Cost** | $0.01-0.05 (Gemini) / $0.001-0.01 (Nano) |
| **Queue** | Pode ser processada em paralelo (5 imagens simultâneas) |

### Agent 4: Video Generator (Gage - DevOps/Orchestration)
| Atributo | Valor |
|----------|-------|
| **Responsabilidade** | Gerar vídeo animado a partir de imagem e áudio |
| **Inputs** | Imagem + Visual prompt com motion cues + (opcional) áudio |
| **Outputs** | Vídeo (MP4, H264, 1080p) com duração otimizada por plataforma |
| **Primary Tool** | Grok Imagine (Xai) — video generation com IA |
| **Fallback** | Stock footage library + motion overlay (ffmpeg) |
| **Retry Logic** | Fila de retry com prioridade |
| **Timeout** | 120s por vídeo (pode ser assíncrono) |
| **Cost** | $0.05-0.15 (Grok) / free (stock footage) |
| **Parallel Processing** | 2-3 vídeos simultâneos (limite de API) |

### Agent 5: Metadata Generator (Morgan/Alex)
| Atributo | Valor |
|----------|-------|
| **Responsabilidade** | Gerar captions, hashtags, descrições otimizadas por plataforma |
| **Inputs** | Ideia original + contexto + vídeo gerado |
| **Outputs** | JSON com captions, hashtags, descriptions (per-platform) |
| **Model** | Claude 3.5 Sonnet |
| **Platform-Specific Logic** | |
| | - **TikTok**: Captions curtos, trending hashtags, hook-first |
| | - **Instagram**: Emojis, lifestyle hashtags, CTA |
| | - **YouTube**: Descriptions SEO, timestamps, detailed hashtags |
| | - **Facebook**: Casual tone, community-focused, minimal hashtags |
| **Timeout** | 25s |
| **Cost** | ~$0.002 por execução |

### Agent 6: Publisher/Orchestrator (Gage - DevOps)
| Atributo | Valor |
|----------|-------|
| **Responsabilidade** | Coordenar publicação em 5 plataformas, gerenciar retries, logging |
| **Inputs** | Vídeos finalizados + metadados |
| **Outputs** | Status consolidado + URLs de publicação + error log |
| **Platform APIs** | TikTok, Instagram, YouTube, Facebook, Twitter/X (future) |
| **Atomicity** | Publica em todas as plataformas, registra falhas |
| **Retry Logic** | Exponential backoff: 1, 2, 4, 8 min (max 3 tentativas) |
| **Scheduling** | Suporta scheduling futuro (timestamps Unix) |
| **Webhooks** | Notificações em tempo real (Server-Sent Events) |
| **Timeout** | 60s por plataforma |
| **Cost** | API calls (negligenciável se cached) |

---

## 🏗️ MÓDULOS DO SISTEMA

### Camada 1: Frontend (Web Application)
```
creativeflow.app/
├─ Dashboard
│  ├─ Create new video form
│  ├─ Queue & status viewer
│  ├─ Video library (grid view)
│  ├─ Analytics & insights
│  └─ Settings & integrations
├─ Editor (optional, Phase 2)
│  ├─ Visual editor para ajustes pós-gen
│  ├─ Caption overlay editor
│  └─ Platform-specific preview
└─ API Client (WebSocket + REST)
```

**Tech Stack Recomendado:**
- Framework: Next.js 15 (App Router)
- UI: ShadCN + Tailwind CSS
- Real-time: WebSocket (Socket.io ou native WS)
- State: TanStack Query (react-query)
- Auth: NextAuth.js (SSO: Google, GitHub)

### Camada 2: Backend API (Core Service)
```
backend/
├─ REST API (Express/Fastify)
│  ├─ POST /api/creatives — Create new job
│  ├─ GET /api/creatives/:id — Get status
│  ├─ GET /api/creatives — List user creatives
│  ├─ PUT /api/creatives/:id — Edit & rerun
│  └─ DELETE /api/creatives/:id — Delete
├─ WebSocket Server
│  └─ Real-time status updates (jobs, failures)
├─ Auth & Users
│  ├─ JWT tokens
│  ├─ Platform OAuth (TikTok, Instagram, etc.)
│  └─ Subscription management
└─ Middleware
   ├─ Rate limiting
   ├─ Request validation
   └─ Error handling
```

**Tech Stack Recomendado:**
- Runtime: Node.js 20+ (ou Deno/Bun para future-proofing)
- Framework: Fastify (high-performance) ou Hono (lightweight)
- Job Queue: Bull (Redis) com workers em Node.js
- Database: PostgreSQL (relational data) + Redis (caching, sessions)
- Logging: Pino (structured JSON logging)
- Monitoring: OpenTelemetry + Datadog/NewRelic

### Camada 3: Agent Orchestration (Workflow Engine)
```
agents/
├─ CreativePromptAgent (Claude)
├─ VisualPromptAgent (Claude)
├─ ImageGeneratorAgent (Gemini/Nano)
├─ VideoGeneratorAgent (Grok)
├─ MetadataAgent (Claude)
└─ PublisherAgent (Multi-platform)

Orchestrator (Temporal.io ou custom):
├─ DAG execution
├─ Retry logic
├─ Error handling
└─ Distributed tracing
```

**Tech Stack Recomendado:**
- Orchestration: Temporal.io (workflow as code, retries, durability)
- Agent Framework: LangChain + custom adapters
- LLM Clients: OpenAI SDK para Claude, Google Generative AI SDK, Grok API
- Image Gen: Google Generative AI SDK + Replicate Python client
- Video Gen: Grok API + ffmpeg (fallback)
- API Clients: Axios + custom retry logic

### Camada 4: External Integrations (Platform APIs)
```
integrations/
├─ TikTok API (Business Account API)
│  └─ POST /v1/video/upload/init → /process → /publish
├─ Instagram API (Meta Graph)
│  └─ POST /me/media (Reels container)
├─ YouTube Data API v3
│  └─ POST /youtube/v3/videos
├─ Facebook Graph API
│  └─ POST /{page-id}/videos
└─ Twitter/X API (Phase 2)
   └─ POST /2/tweets
```

**Tech Stack:**
- HTTP Client: Axios + retry middleware
- Rate limiting: local per-platform config
- Token refresh: automatic with background jobs

### Camada 5: Data & Storage
```
Database (PostgreSQL):
├─ users
├─ creatives (ideas, status, metadata)
├─ videos (generated files, URLs, durations)
├─ platform_accounts (OAuth tokens, credentials)
├─ job_logs (execution history, errors)
├─ analytics (performance data from platforms)
└─ subscriptions & billing

File Storage (S3 / Cloudinary / R2):
├─ /originals (imagens geradas)
├─ /videos (vídeos finais)
├─ /temp (processamento, cleanup após 24h)
└─ /archive (histórico)

Cache Layer (Redis):
├─ Session tokens
├─ Job queue (Bull)
├─ Rate limit counters
└─ Platform token refresh (short-lived)
```

### Camada 6: Monitoring & Observability
```
Monitoring Stack:
├─ Logs
│  ├─ Structured JSON (Pino)
│  ├─ Aggregation: ELK / Loki
│  └─ Querying: Kibana / Grafana
├─ Metrics
│  ├─ Prometheus format
│  ├─ Key metrics: latency, success rate, cost per job
│  └─ Visualization: Grafana dashboards
├─ Tracing
│  ├─ OpenTelemetry (distributed tracing)
│  ├─ Backend: Jaeger / Tempo
│  └─ Trace visualization
├─ Alerting
│  ├─ PagerDuty / Alertmanager triggers
│  └─ Critical: API downtime, high error rates, quota limits
└─ Dashboards
   ├─ User-facing: Success rate, cost, publishing stats
   └─ Internal: System health, queue depth, latency percentiles
```

---

## 📋 REQUISITOS FUNCIONAIS

### RF-001: Create & Input Management
- [x] Usuário pode submeter ideia via form (texto livre, até 500 chars)
- [x] Sistema valida comprimento e detecta idioma
- [x] Suporte a múltiplos idiomas (EN, PT-BR, ES, FR inicialmente)
- [x] Opções de plataforma-alvo selecionáveis (checkboxes)
- [x] Campo opcional de contexto (URL, arquivo, descrição adicional)

### RF-002: Agent Orchestration
- [x] Agent 1 (Prompt) executa após submissão
- [x] Agent 2 (Visual) executa após Agent 1
- [x] Agents 3, 4 executam em paralelo (5 imagens + 5 vídeos simultâneos)
- [x] Agent 5 executa após vídeos prontos
- [x] Agent 6 (Publisher) executa com retry automático
- [x] Qualquer agente pode falhar sem bloquear pipeline (partial success)

### RF-003: Video Generation & Adaptation
- [x] 5 versões de vídeo geradas (TikTok, Reels, Shorts, Feed, YouTube)
- [x] Cada versão adaptada para durações, aspectos ratios e resoluções específicas
- [x] TikTok: 9:16, 15-60s (default 30s)
- [x] Reels: 9:16, 15-90s (default 45s)
- [x] Shorts: 9:16, até 60s (default 45s)
- [x] Feed: 16:9 ou 1:1, até 2min (default 90s)
- [x] YouTube: 16:9, até 10min (default 3min)

### RF-004: Metadata Generation
- [x] Captions gerados automaticamente (platform-specific)
- [x] Hashtags otimizados por plataforma (trending + niche)
- [x] Descrições SEO para YouTube
- [x] CTAs contextualizados (Follow, Like, Share, Subscribe)
- [x] Timestamps/chapters para YouTube

### RF-005: Multi-Platform Publishing
- [x] Publicar em TikTok via TikTok Business API
- [x] Publicar em Instagram Reels via Meta Graph API
- [x] Publicar em YouTube Shorts via YouTube Data API
- [x] Publicar em Facebook via Meta Graph API
- [x] Publicar em Feed (Instagram, Facebook, LinkedIn — Phase 2)

### RF-006: Status & Monitoring
- [x] Dashboard mostra status em tempo real (queued, processing, published, failed)
- [x] WebSocket push notifications para atualizações
- [x] Detalhe de cada etapa (Agent 1 done, Agent 2 done, etc.)
- [x] Erro detalhado com opção de retry
- [x] Link direto para post publicado

### RF-007: Library & History
- [x] Usuário visualiza histórico de vídeos criados (grid view)
- [x] Filter por plataforma, data, status
- [x] Ações: View detail, Edit, Republish, Download, Delete, Archive
- [x] Analytics básicas: views, likes, shares (se disponível via API)

### RF-008: User Management
- [x] Sign up / Sign in (OAuth: Google, GitHub)
- [x] Perfil e preferências
- [x] Integração de contas (TikTok, Instagram, YouTube, Facebook)
- [x] Platform account disconnect
- [x] Usage stats (creatives gerados, tokens gastos)

### RF-009: Retry & Error Recovery
- [x] Qualquer falha dispara retry automático (max 3 tentativas)
- [x] Exponential backoff: 1, 2, 4 minutos
- [x] Manual retry via UI para jobs falhados
- [x] Fallback para Agent 3 (Gemini → Nano Banana)
- [x] Fallback para Agent 4 (Grok → Stock footage)

### RF-010: Scheduling & Queuing
- [x] Usuário pode agendar publicação para data/hora específica
- [x] Queue visual mostra posição na fila
- [x] Priority queue (premium users first)
- [x] Concorrência controlada (max 5 jobs simultâneos por user)

---

## 🔐 REQUISITOS NÃO-FUNCIONAIS

### RNF-001: Performance
- **Latência end-to-end:** < 5 minutos (P95)
- **Agent Prompt (Agent 1):** < 30s
- **Visual Prompt (Agent 2):** < 20s
- **Image Generation (Agent 3):** < 45s (P95)
- **Video Generation (Agent 4):** < 120s (P95, pode ser assíncrono)
- **Metadata (Agent 5):** < 25s
- **Publishing (Agent 6):** < 60s por plataforma
- **API response:** < 500ms (p95) para endpoints não-blocking
- **Dashboard load:** < 2s (First Contentful Paint)

### RNF-002: Escalabilidade
- **Concorrência:** 100-1000 jobs simultâneos (horizontal scaling com Kubernetes)
- **Data:** PostgreSQL + sharding por user_id para tables grandes
- **Queue:** Bull (Redis) com múltiplos workers
- **API throughput:** 1000+ req/s
- **Storage:** S3/R2 com versioning, cleanup automático após 30 dias

### RNF-003: Disponibilidade & Reliability
- **Uptime target:** 99.5% (4 hours downtime/mês)
- **RTO (Recovery Time Objective):** < 15 min
- **RPO (Recovery Point Objective):** < 5 min
- **Backup:** Daily backups (PostgreSQL + S3) com retenção de 30 dias
- **Disaster recovery:** Multi-region failover (primary + standby)

### RNF-004: Security
- **Auth:** OAuth 2.0 (Google, GitHub) + JWT tokens
- **API keys:** Encrypted at rest (AES-256)
- **HTTPS only:** TLS 1.3+
- **Rate limiting:** 100 req/min per user, 1000 req/min global
- **Data privacy:** GDPR-compliant (data anonymization, deletion on request)
- **PCI DSS:** Se processar pagamentos (delegado a Stripe/Paddle)
- **Audit logs:** Todos os acessos a dados sensíveis registrados

### RNF-005: Monitorability & Observability
- **Logging:** 100% das requests + errores (JSON estruturado)
- **Metrics:** P50, P95, P99 latencies, success rates, costs
- **Distributed tracing:** Rastrear job end-to-end
- **Alerting:** Critical errors disparam PagerDuty
- **SLO:** 99.5% sucesso rate, < 30s P95 latency

### RNF-006: Cost Efficiency
- **Target COGS:** < $0.10 por vídeo gerado
- **LLM calls:** Claude $0.003-0.005 por execução
- **Image gen:** Gemini $0.01-0.05, Nano Banana $0.001-0.01
- **Video gen:** Grok $0.05-0.15 por vídeo
- **Storage:** S3 ~$0.023/GB/mês
- **Monetization:** Target 3-5x COGS (pricing $9-99/mês)

### RNF-007: Compliance & Legal
- **Terms of Service:** API usage, content ownership, liability limits
- **Content Policy:** No illegal, hateful, explicit content
- **Platform ToS:** Estar em compliance com TikTok, Instagram, YouTube, Facebook ToS
- **IP Rights:** User retém copyright, we retain rights to aggregate data for research
- **GDPR/CCPA:** Privacidade de dados, direito ao esquecimento

---

## ⚠️ RISCOS TÉCNICOS & OPERACIONAIS

### Risco T-001: API Rate Limits & Quotas
**Severidade:** 🔴 ALTA
**Descrição:** Grok Imagine, Gemini, Meta APIs têm rate limits agressivos (100-500 req/min)
**Impacto:** Jobs bloqueados em picos de tráfego
**Mitigação:**
- [ ] Queue com priorização e throttling local
- [ ] Fallback para múltiplos provedores (Gemini → Nano → Replicate)
- [ ] Caching agressivo de resultados
- [ ] Pre-warming de quota (dedicated accounts)

### Risco T-002: Video Generation Quality Inconsistency
**Severidade:** 🔴 ALTA
**Descrição:** Grok Imagine é nova (beta?), qualidade pode ser inconsistente
**Impacto:** Usuários insatisfeitos com qualidade de output
**Mitigação:**
- [ ] Human review para primeiros 100 outputs
- [ ] Feedback loop (usuário marca "good" ou "bad")
- [ ] A/B testing de prompts para otimizar resultados
- [ ] Fallback para stock footage + overlays (garantir qualidade mínima)

### Risco T-003: Platform API Changes & Deprecation
**Severidade:** 🟡 MÉDIA
**Descrição:** TikTok, Meta, YouTube mudam APIs frequentemente
**Impacto:** Publishing quebra, usuários não conseguem publicar
**Mitigação:**
- [ ] Versioning de API clients
- [ ] Webhook monitoring para deprecation notices
- [ ] Rapid response team para updates
- [ ] Fallback: generate link para download (usuário publica manualmente)

### Risco T-004: Token Expiration & Refresh Management
**Severidade:** 🟡 MÉDIA
**Descrição:** OAuth tokens expiram (TikTok: 24h, Meta: 60 dias)
**Impacto:** Publishing falha, usuário desconectado
**Mitigação:**
- [ ] Automatic token refresh (background jobs)
- [ ] Pre-emptive refresh antes de expiração
- [ ] Graceful degradation (prompt re-auth se falhar)
- [ ] Audit trail de token refreshes

### Risco T-005: LLM Cost Explosion
**Severidade:** 🟡 MÉDIA
**Descrição:** Claude calls podem custar muito em volume
**Impacto:** COGS > revenue, modelo inviável
**Mitigação:**
- [ ] Caching agressivo de prompts similares
- [ ] Model selection (Claude vs GPT-4 vs Gemini por use case)
- [ ] Prompt compression (fewer tokens)
- [ ] Budget limits per user (hard cap)

### Risco T-006: Storage & Bandwidth Costs
**Severidade:** 🟡 MÉDIA
**Descrição:** Vídeos são heavy (100-500MB cada)
**Impacto:** Storage + egress costs podem ser significativos
**Mitigação:**
- [ ] Compression (H.265, VP9, AV1)
- [ ] CDN caching (Cloudflare, CloudFront)
- [ ] Auto-cleanup (delete após 30 dias)
- [ ] Tiered storage (hot/cold)

### Risco O-001: Content Moderation at Scale
**Severidade:** 🔴 ALTA
**Descrição:** Usuários podem gerar conteúdo violento, hateful, ou de copyright
**Impacto:** Banimento de contas em plataformas, responsabilidade legal
**Mitigação:**
- [ ] Content filter antes de submit (OpenAI Moderation API)
- [ ] Automated scanning de output (NSFW detection)
- [ ] Manual review queue para borderline cases
- [ ] Clear ToS + takedown process
- [ ] Insurance/indemnity para partners

### Risco O-002: Platform Account Suspensions
**Severidade:** 🔴 ALTA
**Descrição:** TikTok, Instagram pode suspender contas que publicam via API
**Impacto:** Usuários perdem acesso a contas, churn
**Mitigação:**
- [ ] Respeitar rate limits de cada plataforma
- [ ] Authentic engagement (não spam/bulk content)
- [ ] User education (não publicar mesma ideia 50x)
- [ ] Monitoring de account health
- [ ] Escalation process com suporte da plataforma

### Risco O-003: Creator Dependency Risk
**Severidade:** 🟡 MÉDIA
**Descrição:** Criadores podem depender 100% de CreativeFlow, se cair perdem produção
**Impacto:** Reputação damage, churn
**Mitigação:**
- [ ] Alta confiabilidade (99.5% uptime SLA)
- [ ] Export de vídeos (usuário sempre pode fazer download)
- [ ] Redundancy (multi-region)
- [ ] Status page transparente

### Risco O-004: Market Education & Adoption
**Severidade:** 🟡 MÉDIA
**Descrição:** Criadores podem ser céticos de "IA gerada content"
**Impacto:** Slow adoption, difficulty raising capital
**Mitigação:**
- [ ] Narrative: "Co-creator tool", não "fully automated"
- [ ] Educational content (tutorials, case studies)
- [ ] Free tier / trial (lower barrier to entry)
- [ ] Community feedback loop (creator influencer partnerships)

---

## 🚀 MVP RECOMENDADO

### Escopo MVP (Phase 1 - 8-12 semanas)
**Goal:** Validar core loop (ideia → vídeo em 5 min) com qualidade aceitável

#### ✅ MVP Inclui:
1. **Input:** Form simples (text + plataforma seleção)
2. **Agents 1-2:** Prompt generation (Claude)
3. **Agent 3:** Image generation (Gemini ou Nano)
4. **Agent 4:** Video generation (Grok + fallback stock footage)
5. **Agent 5:** Metadata (captions, hashtags)
6. **Agent 6 (Partial):** Publicar em 2 plataformas (TikTok + Instagram)
7. **Dashboard:** Status viewer + library básico
8. **Quality:** Single platform publish (TikTok first, validar fluxo)

#### ❌ MVP Não Inclui:
- Editor visual (Phase 2)
- Feedback loop/analytics (Phase 2)
- Scheduling (Phase 2)
- All 5 platform publishing (Phase 2)
- Advanced prompting (Phase 2)
- Webhook integrations (Phase 3)
- Teams/collaboration (Phase 3)
- Enterprise billing (Phase 3)

### MVP Tech Stack (Simplified)
```
Frontend:
- Next.js 15 (App Router)
- TailwindCSS + basic UI components
- Axios + React Query

Backend:
- Node.js + Fastify
- PostgreSQL (basic schema)
- Bull queue (Redis)
- OpenAI SDK (Claude via OpenRouter)
- Gemini SDK

Agents:
- LangChain (basic integration)
- Custom orchestration (no Temporal yet)

Deployment:
- Vercel (frontend)
- Railway/Render (backend)
- Redis Cloud
- Neon (PostgreSQL)
```

### MVP Success Metrics
| Métrica | Target |
|---------|--------|
| End-to-end latency | < 5 min (P95) |
| Success rate | > 85% (first publish) |
| Video quality | Acceptable (human review) |
| Cost per job | < $0.25 |
| User satisfaction | > 7/10 (NPS) |

---

## 📊 ROADMAP POR FASES

### PHASE 1: MVP (Semanas 1-12)
**Goal:** Validar core loop, 1 plataforma, produção manual review
**Resources:** 3 eng (1 full-stack, 1 backend, 1 infra), 1 PM, 1 designer

**Deliverables:**
- [x] Landing page + sign up
- [x] Dashboard básico
- [x] Prompt generator agent
- [x] Image generator (Gemini)
- [x] Video generator (Grok + fallback)
- [x] TikTok publishing integration
- [x] Error handling & retry logic
- [x] Monitoring dashboard
- [x] Documentation
- [x] Beta user recruitment (50-100)

**KPIs:**
- Conversion: Sign up → first creative
- Retention: DAU/MAU
- Quality: % successful publishes
- NPS: Net Promoter Score

---

### PHASE 2: Production Grade (Semanas 13-24)
**Goal:** 5 platform publishing, quality assurance, scaling
**Resources:** +1 QA, +1 infra, +1 PM

**Deliverables:**
- [x] Multi-platform publishing (Instagram, YouTube, Facebook, Twitter)
- [x] Analytics dashboard (views, likes, shares integration)
- [x] Scheduling & queue UI
- [x] Video editor (basic adjustments)
- [x] Feedback loop system
- [x] Advanced prompt templates
- [x] A/B testing framework
- [x] Compliance (content moderation)
- [x] Performance optimization
- [x] Paid tier ($29-99/mth)

**Scaling:**
- Move to Kubernetes
- Database replication
- Multi-region deployment
- Caching layer (Redis → Memcached cluster)

**KPIs:**
- MRR (Monthly Recurring Revenue)
- Churn rate
- Platform distribution (which platforms most used)
- COGS per job

---

### PHASE 3: Enterprise & Features (Semanas 25-36)
**Goal:** Team collaboration, advanced branding, webhook integrations
**Resources:** +2 eng, +1 PM, +1 product manager

**Deliverables:**
- [x] Team management & roles
- [x] Brand kit (custom colors, fonts, logos)
- [x] Webhook integrations (Zapier, Make)
- [x] API access (for agencies)
- [x] Advanced analytics & reporting
- [x] Bulk operations (batch video generation)
- [x] Custom domain (white-label beta)
- [x] Enterprise pricing tier ($499-2K/mth)
- [x] SLA & support tiers

**New Integrations:**
- [ ] LinkedIn publishing
- [ ] Pinterest publishing
- [ ] Blog CMS integrations (WordPress, Webflow)

**KPIs:**
- ARR (Annual Recurring Revenue)
- Enterprise pipeline
- API usage metrics

---

### PHASE 4: AI Personalization & Expansion (Semanas 37+)
**Goal:** Advanced AI features, global expansion
**Resources:** +2 ML engineers, +1 PM

**Deliverables:**
- [x] Creator style learning (learns user aesthetic preferences)
- [x] Trend prediction (suggests trending topics)
- [x] Multi-language support (10+ languages)
- [x] Audio generation (text-to-speech, background music selection)
- [x] Performance prediction (ML model predicts view count)
- [x] Competitive benchmarking (compare against similar creators)
- [x] Mobile app (iOS + Android)

**Expansion:**
- [ ] International markets (Latin America, Asia)
- [ ] Local partnerships (agencies, creator networks)

---

## ❓ DÚVIDAS EM ABERTO PARA VALIDAÇÃO

### Questão #1: Qualidade de Vídeo & User Expectations
**Pergunta:** Qual é o padrão de qualidade aceitável? Full Pixar-quality ou "good enough"?
**Impacto:** Define escolha de providers (Grok vs stock footage), COGS, timeline
**Validação:** Teste com 20 criadores, recolha feedback
**Recomendação:** Começar com "good enough" (80/20 rule), iterar baseado em feedback

---

### Questão #2: Moat Competitivo
**Pergunta:** O que nos diferencia de competitors (Runway, Synthesia, etc.)?
**Dimensões:**
- Speed (5 min vs 30 min)?
- Multi-platform atomicity (5 plataformas 1x)?
- Cost ($9 vs $50/mth)?
- Ease of use (no technical knowledge)?

**Validação:** Competitive audit + user interviews
**Recomendação:** Foco em speed + multi-platform + ease, não em perfeição visual

---

### Questão #3: Monetização & Pricing
**Pergunta:** Que modelo de preço? Usage-based vs flat-rate vs hybrid?
**Opções:**
- Flat tier ($9/$29/$99): Simples, predictable
- Usage-based ($0.10/video): Fair, scales infinitely
- Hybrid (base + overage): Melhor conversão + retention

**Validação:** User surveys, pricing sensitivity analysis
**Recomendação:** Começar com flat tier ($9/$49), upsell para usage em Phase 2

---

### Questão #4: Platform Risk
**Pergunta:** Risco de TikTok, Meta mudar policies ou bloquear API calls?
**Impacto:** Negócio inteiro pode virar non-viable
**Mitigação:**
- Diversificar (não ser tudo TikTok)
- Fallback para download (usuário publica manualmente)
- Legal review de ToS com especialista

**Recomendação:** Validar com platform partners que API usage é permitido

---

### Questão #5: Content Moderation
**Pergunta:** Quem é responsável por conteúdo ilegal/hateful gerado?
**Legal:** Pode ser responsabilidade nossa se não moderarmos
**Impacto:** Liability, reputação
**Mitigação:**
- Conteúdo filter antes de submit
- ToS claro: usuário é responsável
- Insurance

**Recomendação:** Consultar advogado especialista antes de launch

---

### Questão #6: LLM Provider Lock-in
**Pergunta:** Usar só Claude ou multi-LLM?
**Trade-offs:**
- Single (Claude): Simpler, consistent quality
- Multi (Claude + GPT-4 + Gemini): Fallback, cost flexibility, no lock-in

**Recomendação:** Começar com Claude, abstrair em interface para multi-provider depois

---

### Questão #7: Video Hosting & CDN
**Pergunta:** Hospedar vídeos no S3 ou delegar aos platforms?
**Option A (S3):** Controle total, mais barato, complex
**Option B (Platform):** Simples, platform native, sem controle

**Recomendação:** Publica direto nas plataformas (elas hospedam), S3 apenas para backups

---

### Questão #8: Team Collaboration (Early)
**Pergunta:** Incluir team features no MVP ou Phase 2?
**MVP:** Pode ser limitation (single user) ou feature (privacy, simplicity)
**Phase 2:** Team tier ($99-199/mth) com collaboration

**Recomendação:** MVP = single user, Phase 2 = teams

---

### Questão #9: Creator Workflow Integration
**Pergunta:** Integrar com ferramentas populares (Buffer, Later, Meta Business Suite)?
**Benefício:** Frictionless publishing, competitor moat
**Custo:** Integração work, maintenance, API dependencies

**Recomendação:** Phase 2+, começar com Zapier/Make webhook

---

### Questão #10: Feedback Loop & Learning
**Pergunta:** Como coletar feedback de performance (views, likes) para melhorar prompts?
**Workflow:**
- User publica via CreativeFlow
- Coleta metrics (TikTok views, Instagram likes)
- ML model aprende padrões
- Próximo vídeo do user é mais otimizado

**Complexity:** Alta (requer LLM fine-tuning, feedback loop)
**Timeline:** Phase 3+

**Recomendação:** Começar com simples logging, machine learning em Phase 3

---

## 📍 PRÓXIMOS PASSOS

### Para PM (@pm):
1. [ ] Validar público-alvo (user interviews)
2. [ ] Competitive analysis detalhada
3. [ ] Pricing strategy & financial modeling
4. [ ] Go-to-market plan
5. [ ] Create PRD from this brief

### Para Architect (@architect):
1. [ ] Validar tech stack choices
2. [ ] API design (OpenAPI spec)
3. [ ] Database schema
4. [ ] Deployment architecture
5. [ ] Security review

### Para Analyst (@analyst):
1. [ ] Market research (TAM/SAM/SOM)
2. [ ] Competitor deep-dive (10+ companies)
3. [ ] User research with creators (20-30 interviews)
4. [ ] Feasibility assessment (cost, timeline)

### Para Equipe:
1. [ ] Setup GitHub repo + project structure
2. [ ] Configure CI/CD pipeline
3. [ ] Setup monitoring & logging
4. [ ] Begin infrastructure-as-code (Terraform)

---

## 📝 APÊNDICE: Definições & Glossário

| Termo | Definição |
|-------|-----------|
| **Atomic Publishing** | Publicar em múltiplas plataformas em 1 operação, com retry independente |
| **COGS** | Cost of Goods Sold (custo direto por vídeo gerado) |
| **DAG** | Directed Acyclic Graph (workflow com dependências) |
| **Greenfield** | Novo projeto do zero, sem código existente |
| **LLM** | Large Language Model (Claude, GPT-4, Gemini) |
| **MVP** | Minimum Viable Product (versão mínima para validação) |
| **NPS** | Net Promoter Score (métrica de satisfação) |
| **OAuth** | Open Authorization (login com Google, GitHub, etc.) |
| **P95** | 95th percentile (95% das requests são mais rápidas) |
| **RTO/RPO** | Recovery Time/Recovery Point Objectives (disaster recovery) |
| **SLA** | Service Level Agreement (uptime commitment) |
| **TAM/SAM/SOM** | Total/Serviceable/Serviceable Obtainable Market |
| **Temporal.io** | Workflow orchestration engine (como Step Functions mas open-source) |

---

**Document Status:** ✅ Completo — Pronto para Validação
**Autor:** Atlas (Analyst Agent)
**Data de Atualização:** 11 de Março de 2026
**Próxima Revisão:** Após validação com PM + Architect
