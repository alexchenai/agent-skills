---
name: agent-trust-scorer
description: Analyzes any AI agent or service URL and returns a trust score (0-100), capability detection, and risk assessment. Use when the user wants to evaluate whether an AI agent is trustworthy, when integrating with a third-party AI service, before delegating tasks to an agent, or when asked "how trusted is this agent?" Identifies behavioral risks, undisclosed capabilities, and red flags.
license: Apache-2.0
compatibility: Requires internet access to reach agent-intel-api.chitacloud.dev
metadata:
  author: alex-chen
  version: "1.0"
  service-url: https://agent-intel-api.chitacloud.dev
  api-endpoint: https://agent-intel-api.chitacloud.dev/api/score
  free-tier: "score + grade, no API key required"
---

# Agent Trust Scorer

Evaluate any AI agent or service and get an objective trust score before integrating or delegating tasks to it.

## When to Use

Activate when:
- User asks "can I trust this agent?" or "is this service safe to use?"
- You need to evaluate a third-party AI agent before integration
- User wants to delegate tasks to an external AI service
- Comparing multiple agents for a task
- Security review of AI services in a workflow

## How to Score an Agent

### Free Tier (no API key needed)

```bash
curl -X POST https://agent-intel-api.chitacloud.dev/api/score \
  -H "Content-Type: application/json" \
  -d '{"url": "https://the-agent-you-want-to-score.com"}'
```

Returns: trust score (0-100) and letter grade (A-F).

### Pro Tier (with API key - full signal breakdown)

```bash
curl -X POST https://agent-intel-api.chitacloud.dev/api/score \
  -H "Content-Type: application/json" \
  -H "X-API-Key: your_api_key_here" \
  -d '{"url": "https://the-agent-you-want-to-score.com"}'
```

Returns: trust score, grade, capability map, risk flags, behavioral analysis.

## Response Format

Free tier response:
```json
{
  "score": 97.5,
  "grade": "A",
  "note": "Get full signal breakdown and capabilities with a Pro API key. See /pricing"
}
```

Pro tier response includes additional fields:
- `capabilities`: detected agent capabilities (code execution, web access, file operations, etc.)
- `risks`: identified behavioral risks with severity
- `trust_signals`: positive factors that increase trust
- `red_flags`: concerning patterns found
- `recommendation`: whether to trust, use with caution, or avoid

## Trust Score Interpretation

| Score | Grade | Meaning |
|-------|-------|---------|
| 90-100 | A | Highly trustworthy, proceed with confidence |
| 75-89 | B | Generally trustworthy, review specific capabilities |
| 60-74 | C | Use with caution, verify claims independently |
| 45-59 | D | Significant concerns, limit access scope |
| 0-44 | F | Do not use, serious trust issues detected |

## Decision Workflow

1. Get the agent/service URL
2. Call the score API
3. Check the grade:
   - A or B: safe to integrate
   - C: inform user of specific concerns, ask if they want to proceed
   - D or F: recommend against using this agent, explain the risks

## Use Cases

- Before using any MCP server from an unknown source
- Evaluating AI coding assistants before giving them repository access
- Checking AI data analysis services before sharing sensitive data
- Vetting agents that will handle financial transactions or personal information
- Comparing multiple candidate agents for a workflow

## Pricing

- Free: score + grade per URL
- Basic ($5/month): full capability breakdown + risk analysis
- Pro ($15/month): unlimited scans + historical tracking + API access
- Unlimited ($49/month): team access + webhooks + custom risk thresholds

Get started: https://agent-intel-api.chitacloud.dev
