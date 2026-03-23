# Automate References — N8N AI Patterns & OpenClaw Integration (v7.0)

---

## N8N AI Workflow Templates

### 1. SEO Content Pipeline
```
Trigger (Schedule/Webhook)
  → HTTP Request: keyword research API
  → LLM: generate content brief
  → LLM: write article draft
  → LLM: optimize for SEO
  → Code: generate Schema.org JSON-LD
  → HTTP Request: upload to WordPress (draft)
  → HTTP Request: set Yoast/RankMath meta
  → Slack: notify "New draft ready for review"
```

### 2. Support Ticket Classifier
```
Trigger (Webhook: new ticket)
  → LLM: classify intent (billing/technical/general/urgent)
  → Switch: route by classification
    → urgent: Slack alert + assign senior
    → technical: auto-respond template + assign tech team
    → billing: auto-respond + link to billing portal
    → general: auto-respond FAQ + create ticket
```

### 3. Document Q&A Bot
```
Trigger (Webhook: user question)
  → Qdrant/Pinecone: vector search (embedding user question)
  → Set: inject top-3 relevant chunks as context
  → LLM: answer question using context only
  → If (confidence < 0.7): escalate to human
  → Respond: answer + source references
```

### 4. Website Monitor + Auto-Recovery
```
Trigger (Schedule: every 5min)
  → HTTP Request: health check endpoint
  → If (status ≠ 200):
    → SSH: restart service (pm2 restart / systemctl restart)
    → Wait: 30s
    → HTTP Request: verify recovery
    → If (still down): Slack urgent alert + email team
  → Log: execution result to database
```

### 5. Social Media Auto-Poster
```
Trigger (Webhook: new WordPress post published)
  → HTTP Request: get post content
  → LLM: summarize for social media (Twitter/Facebook/LinkedIn)
  → LLM: generate hashtags
  → Parallel:
    → HTTP Request: post to Twitter API
    → HTTP Request: post to Facebook API
    → HTTP Request: post to LinkedIn API
  → Log: post IDs + engagement tracking
```

---

## N8N AI Node Configuration Cheatsheet

### System Prompt Template
```
You are a [ROLE]. Your task is to [SPECIFIC_ACTION].

RULES:
- [constraint 1]
- [constraint 2]
- Always respond in [FORMAT]: JSON/Markdown/Plain text

INPUT: {user_input}
OUTPUT: {expected_format}
```

### Recommended Model Selection
| Task | Model | Temperature | Reason |
|---|---|---|---|
| Classification | gpt-4o-mini | 0.1 | Fast, accurate, cheap |
| Content writing | claude-sonnet | 0.7 | Creative, high quality |
| Data extraction | gpt-4o-mini | 0.0 | Precise, structured |
| Complex reasoning | claude-opus / gpt-4o | 0.3 | Maximum capability |
| Translation | gpt-4o-mini | 0.3 | Good multi-language |

---

## OpenClaw Integration Guide

### Skill File Structure
```
skill-name/
├── SKILL.md              # Main instructions (YAML frontmatter required)
├── references/            # Detailed patterns, templates
│   ├── patterns.md
│   └── templates.md
└── scripts/              # Helper scripts (optional)
    └── helper.sh
```

### YAML Frontmatter Required Fields
```yaml
---
name: skill-name           # lowercase, no spaces
description: "Clear description of what this skill does and when to trigger it. Include Vietnamese trigger words for bilingual users."
---
```

### Token Optimization Rules
```
✅ SKILL.md: overview + commands (< 500 lines)
✅ references/: detailed info loaded on-demand
✅ Use checklists (□) instead of paragraphs
✅ Tables for structured data
❌ Don't repeat info between SKILL.md and references/
❌ Don't include code examples in SKILL.md (put in references/)
```

---

## N8N Webhook Security Hardening

```
1. HMAC Signature Verification:
   → N8N Header Auth: send X-Signature header
   → Receiving end: verify HMAC-SHA256(body, secret) === X-Signature

2. IP Whitelisting:
   → Only allow N8N server IP to hit webhooks
   → nginx: allow [N8N_IP]; deny all;

3. Rate Limiting:
   → nginx: limit_req_zone $binary_remote_addr zone=webhook:10m rate=10r/s;

4. Timeout Protection:
   → Set execution timeout in N8N settings
   → Max payload size: 16MB default (adjust if needed)

5. Credential Storage:
   → Use N8N credential system (encrypted at rest)
   → Never hardcode in workflow JSON
   → Rotate API keys quarterly
```
