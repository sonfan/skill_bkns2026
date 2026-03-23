---
name: automate
description: "N8N workflow automation, OpenClaw agent skills, and API integration. Use for /n8n (build N8N workflows), /n8n-ai (AI-powered N8N workflows), /openclaw (OpenClaw automation), /pipeline (multi-step automation), /monitor-flow (workflow monitoring), /integrate (API/webhook integration), /mcp (design MCP tools). Triggers on: N8N, automation, webhook, API integration, workflow, tự động hóa, integrate, MCP tool, OpenClaw, pipeline, AI workflow."
---

# Automate Skill — N8N AI + OpenClaw + API Design + MCP Tools (v7.0)

> 📂 Chi tiết bổ sung: `automate/references/n8n-ai-patterns.md`

---

## /n8n-ai [task]
> AI-powered N8N workflow — LLM nodes, vector store, AI agent

```
AI WORKFLOW PATTERNS:

  PATTERN 1 — SIMPLE LLM CHAIN:
    Trigger → Data extraction → LLM (prompt template) → Output
    Use when: summarize, classify, extract, translate

  PATTERN 2 — AI AGENT:
    Trigger → AI Agent node → Tools (HTTP, Code, DB) → Response
    Use when: complex reasoning, multi-step decisions, data lookup
    Tools to attach: Calculator, HTTP Request, Postgres, Custom Code

  PATTERN 3 — RAG (Retrieval-Augmented Generation):
    Trigger → Vector Store lookup → Inject context → LLM → Response
    Use when: Q&A over documents, knowledge base, support bots
    Vector stores: Pinecone, Qdrant, Supabase pgvector

  PATTERN 4 — CONTENT PIPELINE:
    Trigger → Research (HTTP) → LLM outline → LLM draft → Review → Publish
    Use when: SEO articles, social media, newsletters
    Anti-pattern: 1 monolithic prompt. Split: outline → draft → polish

  PATTERN 5 — CLASSIFICATION + ROUTING:
    Trigger → LLM classify intent → Switch node → Different handlers
    Use when: email triage, support tickets, form processing

AI NODE BEST PRACTICES:
  □ System prompt: clear role + constraints + output format
  □ Temperature: 0.1-0.3 (factual), 0.7-0.9 (creative)
  □ Output format: force JSON mode khi cần structured output
  □ Token limit: set max tokens phù hợp (không để unlimited)
  □ Error handling: LLM can fail → try/catch mandatory
  □ Cost tracking: log token usage per execution
  □ Retry: max 2 retries on LLM timeout/rate limit

VECTOR STORE INTEGRATION:
  □ Embedding model: text-embedding-3-small (cheap) or large (quality)
  □ Chunk size: 500-1000 tokens, overlap 100-200
  □ Metadata: source, date, category (for filtered search)
  □ Similarity threshold: 0.7+ for relevant results
```

---

## /openclaw [task]
> OpenClaw / Antigravity automation patterns

```
OPENCLAW SKILL MANAGEMENT:
  □ Skill structure: SKILL.md + references/ + scripts/
  □ YAML frontmatter: name, description (trigger keywords)
  □ Progressive disclosure: SKILL.md overview → references/ details
  □ Token efficiency: keep SKILL.md under 500 lines

OPENCLAW AGENT PATTERNS:
  □ Browser sub-agent: visual testing, form filling, screenshots
  □ Terminal commands: code execution, build, deploy
  □ File management: create, edit, search code
  □ Multi-agent: parallel tasks with sync points

OPENCLAW + N8N INTEGRATION:
  □ N8N webhook → trigger Antigravity task
  □ Antigravity → N8N HTTP Request (trigger workflow)
  □ Shared credentials: environment variables
  □ Status sync: N8N monitors Antigravity task completion

WORKFLOW AUTOMATION IDEAS:
  □ Auto-deploy on git push (N8N webhook → build → deploy)
  □ SEO content pipeline (N8N research → Antigravity write → WordPress publish)
  □ Site monitoring (N8N schedule → health check → alert)
  □ Client onboarding (form submit → N8N process → Antigravity scaffold project)
```

---

## /pipeline [flow]
> Multi-step automation pipeline design

```
PIPELINE ARCHITECTURE:

  STEP 1 — DEFINE PIPELINE:
    □ Trigger: what starts the pipeline?
    □ Steps: ordered list of actions
    □ Dependencies: which steps depend on previous output?
    □ Parallel opportunities: which steps can run simultaneously?
    □ Error strategy: per step (retry/skip/abort)

  STEP 2 — DESIGN:
    ┌─────────┐    ┌──────────┐    ┌──────────┐    ┌────────┐
    │ TRIGGER │───▶│ PROCESS  │───▶│ TRANSFORM│───▶│ OUTPUT │
    └─────────┘    └──────────┘    └──────────┘    └────────┘
         │              │               │               │
         ▼              ▼               ▼               ▼
    [Webhook]     [API/LLM/DB]    [Format/Filter]  [Publish/Store]
         │              │               │               │
         └──────────────┴───────────────┴───────────────┘
                              │
                        ┌─────────┐
                        │ VERIFY  │ ← Automated quality check
                        └─────────┘

  STEP 3 — IMPLEMENT:
    □ N8N workflow or code-based?
    □ State management: where to persist intermediate results
    □ Observability: log each step execution + metrics
    □ Alerting: notify on step failure
    □ Idempotency: safe to re-run if interrupted

COMMON PIPELINES:
  SEO:      keyword research → brief → draft → optimize → schema → publish
  Deploy:   lint → test → build → deploy staging → smoke test → deploy prod
  Support:  ticket received → classify → route → auto-respond or escalate
  Data:     extract → validate → transform → load → verify
```

---

## /monitor-flow [id]
> N8N workflow monitoring + error alerting

```
MONITORING CHECKLIST:
  □ Execution history: success rate last 24h/7d/30d
  □ Execution time: avg, p95, slowest
  □ Error analysis: group by error type, frequency
  □ Queue depth: pending executions (nếu queue-based)
  □ Resource usage: memory, API call count

ALERTING SETUP:
  □ Error rate > 10% in 1h → Slack alert
  □ Execution > 5min → timeout warning
  □ 3 consecutive failures → urgent alert
  □ API rate limit hit → pause + notify
  □ Workflow disabled unexpectedly → alert

DASHBOARD (N8N internal or external):
  □ Active workflows count
  □ Executions/hour chart
  □ Error rate trend
  □ Top failing workflows
  □ Estimated API costs

→ Chi tiết: references/n8n-ai-patterns.md
```

---

## /n8n [task]
> Thiết kế và implement N8N workflow automation

```
WORKFLOW DESIGN PROTOCOL:

STEP 1 — DEFINE (trước khi mở N8N)
  □ Trigger: gì kích hoạt workflow? (webhook/schedule/event/manual)
  □ Input: data gì vào? Format? Source?
  □ Output: data gì ra? Destination?
  □ Error scenarios: những gì có thể fail?
  □ Idempotency: chạy 2 lần có safe không?

STEP 2 — ARCHITECTURE
  □ Single workflow vs modular (sub-workflows)?
  □ State management: cần track state không?
  □ Error handling: retry logic, dead letter queue
  □ Rate limiting: external API có limits không?
  □ Parallel execution safe không?

STEP 3 — IMPLEMENT
  TRIGGER NODES:
    Webhook → set respond: "Last Node" hoặc "Immediately"
    Schedule → định nghĩa timezone rõ ràng

  DATA VALIDATION (luôn có sau trigger):
    □ Validate required fields
    □ Type coercion nếu cần
    □ Sanitize strings (XSS prevention)

  CORE LOGIC NODES:
    □ HTTP Request: set timeout (30s default), error handling
    □ Code Node: document rõ input/output, handle exceptions
    □ Set Node: tên variables rõ ràng, không abbreviate

  ERROR HANDLING (bắt buộc):
    □ Try/Catch wrapping cho risky operations
    □ Error workflow (n8n Error Trigger)
    □ Slack/email alert khi critical failure
    □ Log errors với đủ context để debug

  RESPONSE/OUTPUT:
    □ Consistent response format
    □ Status codes đúng (200/201/400/500)
    □ Log successful execution với key metrics

STEP 4 — TEST
  □ Test với sample data trước production
  □ Test error paths (không chỉ happy path)
  □ Test rate limit behavior
  □ Test với null/empty inputs

STEP 5 — DOCUMENT
  □ Workflow description rõ ràng
  □ Node names mô tả action
  □ Sticky notes cho complex logic
  □ Env variables documented
```

---

## ANTI-PATTERNS (không được làm)
```
❌ Hardcode API keys trong workflow (dùng n8n credentials)
❌ Chaining 20+ nodes mà không có error handling
❌ Dùng Google Sheets làm database (race conditions)
❌ Monolithic prompt trong 1 AI node (modularize)
❌ No timeout trên HTTP Request nodes
❌ No retry logic cho external API calls
❌ Log sensitive data (PII, tokens, passwords)
❌ 1 workflow làm mọi thứ (modularize thành sub-workflows)
```

---

## /integrate [service]
> API integration design và implementation

```
PRE-INTEGRATION CHECKLIST:
  □ Read official API docs (không guess)
  □ Authentication type: API Key / OAuth2 / JWT / Basic?
  □ Rate limits: requests/minute, requests/day?
  □ Pagination: cursor / page / offset?
  □ Webhooks available? (prefer over polling)
  □ SDK có sẵn? (prefer over raw HTTP)

INTEGRATION ARCHITECTURE:
  □ Abstraction layer: không gọi thẳng API ở business logic
  □ Retry với exponential backoff (3 retries, 1s/2s/4s)
  □ Circuit breaker: fail fast nếu service down
  □ Response caching nếu data ít thay đổi
  □ Webhook signature verification
  □ Idempotency keys cho write operations

ERROR HANDLING:
  □ 400: log request, return clear error message
  □ 401/403: refresh token / notify user
  □ 429: respect Retry-After header, pause + retry
  □ 500: retry với backoff, alert on persistent failure
  □ Timeout: set reasonable timeout (10-30s)

WEBHOOK SECURITY:
  □ Verify signature (HMAC-SHA256)
  □ Idempotency: store processed event IDs
  □ Respond 200 quickly, process async
  □ HTTPS only
```

---

## /mcp [tool-name]
> Design và implement MCP Tool cho N8N hoặc Antigravity

```
MCP TOOL DESIGN PRINCIPLES:
  □ Single responsibility: một tool = một action
  □ Name: verb_noun format (get_post_list, create_draft)
  □ Description: đủ rõ để AI biết khi nào dùng
  □ Input schema: JSON Schema, validate ngay
  □ Output: consistent { success, data, error }
  □ Error messages: actionable

IDEMPOTENCY:
  □ GET: always idempotent
  □ POST/create: check duplicates, return existing
  □ Use idempotency key cho critical operations

8-TOOL SEO PIPELINE REFERENCE:
  tool_1_keyword_research → topic → keyword list
  tool_2_content_gen      → keyword, brief → article draft
  tool_3_image_gen        → topic, style → image URL
  tool_4_media_upload     → image URL → wp media ID
  tool_5_taxonomy         → category → term ID
  tool_6_publish_draft    → post data → post ID
  tool_7_seo_meta         → post ID, meta → updated post
  tool_8_verify           → post ID → verification report
```
