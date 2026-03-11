# 📋 PRODUCT REQUIREMENTS DOCUMENT (PRD)
## CreativeFlow AI — SaaS de Criação e Publicação Automatizada de Vídeos

**Status:** ✅ APPROVED FOR DEVELOPMENT
**Versão:** 2.0 (Executive Edition)
**Data:** 11 de Março de 2026
**Proprietário:** Morgan (Product Manager)
**Preparado por:** Atlas (Analyst) + Morgan (PM)
**Aprovação:** Product Manager ✅

---

## 📌 EXECUTIVE SUMMARY

**CreativeFlow AI** é uma plataforma SaaS que transforma criadores de conteúdo em super-produtores de vídeo, automatizando 80% do ciclo de criação — desde ideação até publicação multikanal — em menos de 5 minutos.

### O Problema
Criadores profissionais gastam **4-8 horas por semana** em tarefas repetitivas:
- Adaptar um vídeo para 5 plataformas diferentes
- Gerar captions, hashtags, descrições otimizadas
- Lidar com formatos, durações e proporções distintas
- Gerenciar múltiplas ferramentas (Canva, Adobe, CapCut, Buffer, etc.)

**Impacto:** Publica apenas 2-3 vídeos/semana quando poderia publicar 5-7x mais.

### A Solução
Agentes IA orquestrados que:
1. Entendem a intenção criativa do usuário
2. Geram prompts criativos estruturados
3. Criam imagens otimizadas por plataforma
4. Produzem vídeos com movimento e narrativa
5. Geram metadados contextualizados
6. Publicam atomicamente em 5 plataformas

### O Valor
| Métrica | Antes | Depois | Ganho |
|---------|-------|--------|-------|
| Tempo (ideia → publish) | 4-8h | 5 min | **95% redução** |
| Volume semanal | 2-3 vídeos | 5-7 vídeos | **+200-250%** |
| Adaptação multikanal | Manual (6-8h) | Automática | **Elimina fricção** |
| Custo mensal | $100-300 | $29-99 | **-70%** |

### Mercado Alvo
- **50M criadores globais**
- **5-10M criadores profissionais/semi-profissionais**
- **TAM:** $1.5B+ (mercado de criadores + agências)

---

## 🎯 DEFINIÇÃO DO PRODUTO

### Visão
CreativeFlow AI é a camada de automação inteligente para criadores que pensam em múltiplas plataformas simultaneamente.

### Missão
Eliminar atrito entre ideação criativa e execução multikanal, permitindo que criadores focquem em estratégia enquanto agentes IA lidam com tática.

### Posicionamento
**Para:** Criadores profissionais e pequenas agências
**Que:** Publicam em múltiplas plataformas (4-7x/semana)
**CreativeFlow AI é:** A plataforma de automação de conteúdo visual end-to-end
**Diferente de:** Canva, Adobe, CapCut, Runway
**Porque:** Publica em 5 plataformas simultaneamente com otimizações específicas de cada uma

---

## 👥 DEFINIÇÃO DO PÚBLICO-ALVO

### Persona Primária: Sofia (Creator Profissional)
- **Perfil:** YouTuber/TikToker, 500K-10M seguidores, 25-40 anos
- **Dor:** Não consegue publicar mais frequentemente (falta de tempo)
- **Comportamento:** Publica 4-7x/semana, usa 5+ ferramentas
- **Budget:** $49-99/mês (já gasta ~$300/mth em ferramentas)
- **Success:** Reduz 1h para 5-10 min por vídeo, publica 2-3x mais

### Persona Secundária: Marina (Agência)
- **Perfil:** Diretora de conteúdo, agência 5-20 pessoas, 28-45 anos
- **Dor:** Escalabilidade sem contratar mais people
- **Comportamento:** Gerencia 10-50 clientes, precisa de 3-5 vídeos/semana por cliente
- **Budget:** $199-499/mês (rateado entre clientes)
- **Success:** Produz 2-3x mais, reduz custo por projeto

### Persona Terciária: Carlos (Marketer In-House)
- **Perfil:** Especialista marketing, PME 50-500 pessoas, 28-45 anos
- **Dor:** Ampliar frequência sem expandir team
- **Comportamento:** Marketing team 2-5 pessoas, publica 1-2x/semana
- **Budget:** $79-199/mês
- **Success:** Aumenta frequência, reduz custo operacional

---

## 💎 PROPOSTA DE VALOR

### Value Proposition Canvas

**Jobs to be Done:**
1. Gerar ideias visuais rapidamente
2. Adaptar conteúdo para múltiplas plataformas
3. Publicar consistentemente sem estresse
4. Maximizar alcance com otimizações específicas

**Pains (Dores):**
- Tempo (4-8h por conteúdo)
- Complexidade técnica (formatos, durações)
- Custo de ferramentas ($100-300/mês)
- Repetição manual (mesma ideia 5 plataformas)
- Risco de contas suspensas (publicação em massa)

**Gains (Ganhos Desejados):**
- Publicar 3-5x mais conteúdo
- Economizar 15-20h por semana
- Focar em ideação, não execução
- Consistência visual garantida
- Aprender o que funciona (feedback loop)

**Our Solution:**
- ✅ Orquestração de agentes IA (Prompt → Visual → Imagem → Vídeo → Metadata → Publish)
- ✅ Otimização automática por plataforma (5 versões diferentes)
- ✅ Publicação atômica (tudo ou nada, com retry automático)
- ✅ Dashboard consolidado (status + analytics + biblioteca)
- ✅ Feedback loop (aprende com performance)

---

## 🔄 FLUXO DO USUÁRIO (USER JOURNEY)

### Journey Map: Sofia (Creator Profissional)

```
09:00 - ENTRADA
└─ Sofia abre CreativeFlow
└─ Dashboard mostra: histórico (últimos 5 vídeos) + status (1 agendado em 2h)

09:05 - CRIAR NOVO VÍDEO
└─ Clica "New Creative"
└─ Form simples: "Dica de produtividade com Pomodoro"
└─ Seleciona plataformas: TikTok, Reels, Shorts
└─ Clica "Generate" → Job iniciado

09:06 - PROCESSAMENTO EM TEMPO REAL
└─ WebSocket mostra progresso:
   ✅ Agent 1 (Prompt) — 30s
   ✅ Agent 2 (Visual) — 20s
   🔄 Agent 3 (Imagem) — 45s
   🔄 Agent 4 (Vídeo) — 2min
   ⏳ Agent 5 (Metadata) — 25s
   ⏳ Agent 6 (Publish) — 60s
└─ Sofia pode fechar página (job continua em background)

09:11 - REVISÃO & PUBLICAÇÃO
└─ 3 vídeos prontos (TikTok 30s, Reels 45s, Shorts 45s)
└─ Cada um em tab separada, pode assistir full-screen
└─ Metadados aparecem automaticamente
└─ Opções: [Publish Now] [Edit Metadata] [Schedule] [Download]
└─ Clica "Publish Now"

09:12 - CONFIRMAÇÃO
└─ Dashboard atualiza em tempo real:
   ✅ TikTok — Published 1 min ago — https://vt.tiktok.com/...
   ✅ Reels — Published 1 min ago — https://instagram.com/...
   ✅ Shorts — Published 1 min ago — https://youtube.com/...
└─ Pode compartilhar URLs imediatamente
└─ Browser notification: "Videos published successfully!"

14:00 - ANALYTICS
└─ Sofia volta ao app
└─ Vê vídeo das 09:12:
   • TikTok: 5.2K views | 340 likes | 12 shares
   • Reels: 1.8K views | 95 likes | 3 shares
   • Shorts: 890 views | 48 likes | 2 shares
└─ Insight: "TikTok performs best for this format"

17:00 - BATCH CRIAÇÃO
└─ 2 novas ideias → 2 creatives
└─ Um publica agora, outro agenda para amanhã 08:00
└─ Total do dia: 3 vídeos (vs. 1 manual)
```

**Tempo Total:** 15 minutos (vs. 4 horas manual) — **95% redução**

---

## 📊 FUNCIONALIDADES DO MVP (FASE 1)

### MVP Escopo: 8-12 semanas | 1 plataforma (TikTok) | Production ready

#### RF-001: Create New Creative
```
User submits idea → System generates job

Features:
□ Form com 3 campos:
  • "Describe your idea" (texto, 10-500 chars)
  • Platform selection (checkboxes)
  • Optional: language, tone, audience context
□ Real-time validation (min chars, max chars)
□ Submit → generates UUID job ID
□ Instant confirmation: "Processing started..."
```

#### RF-002: Agent Orchestration Pipeline
```
Sequential execution with parallel processing:

Agent 1 (Prompt Generator) — Claude
  Input: User idea
  Output: Structured prompt
  Timeout: 30s | Cost: ~$0.002

Agent 2 (Visual Prompt Converter) — Claude
  Input: Prompt + TikTok specs
  Output: Visual prompt optimized
  Timeout: 20s | Cost: ~$0.002

Agent 3 (Image Generator) — Gemini 2.0 Flash
  Input: Visual prompt
  Output: 1024x1024 image
  Timeout: 45s | Retry: 3x | Cost: $0.01-0.05

Agent 4 (Video Generator) — Grok Imagine
  Input: Image + motion prompt
  Output: MP4 (1080x1920, 30s)
  Timeout: 120s | Async | Cost: $0.05-0.15

Agent 5 (Metadata Generator) — Claude
  Input: Idea + assets
  Output: Caption, hashtags, description
  Timeout: 25s | Cost: ~$0.002

Agent 6 (Publisher) — TikTok Business API
  Input: Video + metadata
  Output: Published URL + status
  Timeout: 60s | Retry: 3x | Cost: FREE
```

#### RF-003: Real-time Status Dashboard
```
WebSocket live updates showing progress:

□ Agent-by-agent status (✅/🔄/⏳)
□ Overall progress percentage
□ Estimated time remaining
□ Expandable logs (input/output per agent)
□ Error handling with retry options
```

#### RF-004: Video Preview & Publishing
```
Review before publishing:

□ Full-screen video player
□ Edit captions/hashtags inline
□ Schedule for later (date picker)
□ Download button (MP4)
□ Copy link to clipboard
□ Publish confirmation dialog
```

#### RF-005: TikTok Publishing
```
Integration with TikTok Business API:

□ OAuth token management (24h refresh)
□ Chunked upload (resumable)
□ Publish with metadata
□ Status tracking (moderation pending → published)
□ Error handling (429, 503, etc.)
□ Fallback: Generate download link if API fails
```

#### RF-006: Creative Library
```
Grid view of creatives:

□ 4 items per row
□ Filter: platform, status, date range
□ Search: title/description
□ Actions: View, Edit, Delete, Archive
□ Pagination (50 per page)
□ Lazy loading
```

#### RF-007: User Management
```
Authentication + Profile:

□ Sign up / Login (OAuth: Google, GitHub)
□ Email verification
□ Profile: name, avatar, bio
□ Platform integrations (TikTok OAuth)
□ Subscription tier display
□ Usage stats
```

#### RF-008: Error Handling & Recovery
```
Robust error recovery:

□ Retry with exponential backoff (1m, 2m, 4m)
□ Max 3 attempts per agent
□ User notifications (browser, email)
□ Clear, actionable error messages
□ Manual recovery options (retry, download, edit)
```

---

## 🚀 FUNCIONALIDADES FUTURAS

### FASE 2 (Weeks 13-24): Multi-Platform Production
```
New:
□ Instagram Reels publishing
□ Facebook Video publishing
□ YouTube Shorts publishing
□ Analytics dashboard (views, likes, shares)
□ Metadata editor (edit captions, hashtags)
□ Scheduling & queue management
□ A/B testing framework
□ Content moderation
□ Advanced prompting (templates)
□ Paid tier ($29-99/mth)
```

### FASE 3 (Weeks 25-36): Enterprise
```
New:
□ Workspace & team management
□ Role-based access control
□ Brand kit (colors, fonts, logos)
□ Webhook integrations
□ API access for agencies
□ LinkedIn publishing
□ Enterprise tier ($499-2K/mth)
```

### FASE 4 (Weeks 37+): AI Personalization
```
New:
□ Creator style learning
□ Trend prediction
□ Multi-language support
□ Audio generation (TTS, music)
□ Mobile app (iOS + Android)
□ Performance prediction
□ Competitive benchmarking
```

---

## ✅ CRITÉRIOS DE SUCESSO

### MVP Phase 1
```
Adoption:
□ 50+ beta users (week 4)
□ 200+ signups (week 12)
□ 20%+ DAU
□ 8-10 min average session

Quality:
□ 85%+ success rate
□ < 5 min E2E latency (P95)
□ < 0.1% error rate
□ COGS < $0.25/video

Satisfaction:
□ NPS > 40
□ 5-star reviews > 50%
□ Support < 1 per 100 users
```

### Phase 2+
```
Business:
□ MRR $5K+ (phase 2)
□ 1000+ active users
□ 50% MOM growth
□ ARPU $15-25
□ Churn < 5% MOM

Product:
□ 90%+ success rate
□ 5 platforms publishing
□ 3-5x more publishing volume
□ Analytics working
```

---

## 🔧 DEPENDÊNCIAS TÉCNICAS

### External APIs

| API | Platform | Status | Timeline |
|-----|----------|--------|----------|
| TikTok Business API | TikTok | 🔶 Pending approval | **APPLY NOW** |
| Meta Graph API | Instagram + Facebook | ✅ Easy | Week 1 |
| YouTube Data API | YouTube | ✅ Easy | Phase 2 |
| Claude API | Anthropic | ✅ Ready | Week 1 |
| Gemini 2.0 Flash | Google | ✅ Ready | Week 1 |
| Grok Imagine API | XAI | 🔶 Pending | Week 1 |

### Tech Stack

```
Frontend: Next.js 15 + TailwindCSS + WebSocket
Backend: Fastify + PostgreSQL + Redis + Bull
Agents: LangChain + Claude + Gemini + Grok
Deploy: Vercel + Railway + Neon
Monitor: Pino + OpenTelemetry + Datadog
```

### Critical Path

```
BLOCKING:
□ TikTok API approval (apply Week 1)
□ Meta OAuth setup (Week 1)
□ Claude + Gemini + Grok credentials (Week 1)

IMPORTANT:
□ Token refresh scheduler
□ Retry + backoff logic
□ WebSocket implementation
□ OAuth flows
```

---

## 📈 ROADMAP

```
PHASE 1: MVP (Weeks 1-12)
├─ Weeks 1-2: Setup + API access
├─ Weeks 3-4: Frontend (form, dashboard)
├─ Weeks 5-7: Agent pipeline
├─ Weeks 8-10: Publishing + TikTok
└─ Weeks 11-12: Testing + polish

PHASE 2: Production (Weeks 13-24)
├─ Weeks 13-16: Instagram + Facebook
├─ Weeks 17-18: YouTube
├─ Weeks 19-20: Analytics
├─ Weeks 21-22: Editor + scheduling
└─ Weeks 23-24: Paid tier launch

PHASE 3: Enterprise (Weeks 25-36)
├─ Weeks 25-28: Workspace + teams
├─ Weeks 29-32: Brand kit + white-label
└─ Weeks 33-36: API + integrations

PHASE 4: Expansion (Weeks 37+)
├─ AI personalization
├─ Mobile apps
└─ International expansion
```

### Resources by Phase

```
PHASE 1: 3 eng + 1 PM + 1 designer (~$150K)
PHASE 2: +1 QA + 1 infra (~$200K)
PHASE 3: +2 eng + 1 PM (~$250K)
PHASE 4: +2 ML eng + 1 PM (open-ended)
```

---

## 🎯 GO/NO-GO CHECKLIST

### MVP Launch Readiness

```
MUST HAVE:
□ TikTok API approved
□ Core pipeline tested
□ Publishing end-to-end
□ Dashboard + real-time status
□ Error handling + retry
□ 50+ beta testers
□ Security review passed

SHOULD HAVE:
□ Analytics
□ Onboarding guide
□ Support setup
□ Monitoring
□ Documentation

PROCEED TO PHASE 2 IF:
✅ 85%+ success rate
✅ NPS > 40
✅ 200+ signups
✅ COGS < $0.25/video
✅ Positive unit economics
```

---

**Status:** ✅ READY FOR DEVELOPMENT
**Next Action:** @sm to create epics + stories
**Prepared by:** Morgan (PM)
**Last Updated:** 11 de Março de 2026

*PRD v2.0 — Executive Edition — Ready for sprint planning*
