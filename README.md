# Trust OS for GovAI / Gennai PoC

Experimental implementation of Trust OS verification on top of GovAI outputs.

This repository demonstrates how Trust OS can add a lightweight verification layer to government AI workflows, including Gennai-compatible RAG / LLM outputs.

Trust OS is not the AI execution layer.

Trust OS is the verification layer.

---

## What this does

This PoC adds a verification record after AI response generation.

Instead of only returning an AI answer, the system:

1. Receives a user question
2. Generates an AI response using GovAI / RAG / LLM
3. Hashes the input, output, and references
4. Attaches a Trust OS verification record
5. Returns a structured JSON response

---

## Architecture

```txt
User Input
  ↓
GovAI / Gennai-compatible RAG / LLM
  ↓
Trust OS Verification Layer
  ↓
Verifiable JSON Output
```

---

## Example Request

```json
{
  "inputs": {
    "question": "フレックスタイム制について教えてください",
    "n_queries": 3,
    "output_in_detail": false,
    "tags": "労務"
  }
}
```

---

## Example Response

```json
{
  "outputs": "フレックスタイム制は...",
  "trust_os": {
    "decision_id": "tos_xxx",
    "input_hash": "sha256...",
    "answer_hash": "sha256...",
    "reference_hash": "sha256...",
    "risk_level": "LOW",
    "recommendation": "ALLOW_WITH_AUDIT_LOG",
    "verified": true
  }
}
```

---

## Noise Reduction Design

Trust OS is not designed to verify every AI output.

Verifying every response can create unnecessary audit noise, storage cost, and operational complexity.

Instead, Trust OS is designed as a selective verification layer.

The goal is to verify outputs that are high-risk, policy-relevant, human-impacting, or audit-sensitive.

---

## Selective Verification

Trust OS can be triggered only when specific conditions are met.

Example trigger conditions:

- High-risk decision
- Legal or regulatory impact
- Financial consequence
- Public service eligibility
- Human-impacting recommendation
- Policy-sensitive workflow
- Audit-sensitive administrative process

---

## What Trust OS Records

Trust OS does not need to store full raw data.

A minimal verification record may include:

- decision_id
- input_hash
- output_hash
- reference_hash
- risk_level
- recommendation
- reason_codes
- timestamp
- verification_status

This keeps the record lightweight, structured, and audit-ready.

---

## Where Trust OS Should Be Applied

Trust OS is most useful when AI outputs affect important decisions.

Recommended use cases:

- Subsidy screening
- Administrative eligibility checks
- Legal or regulatory interpretation
- Financial risk assessment
- AML / compliance workflows
- Procurement evaluation support
- Public service decision support
- High-impact citizen-facing workflows

---

## What Should Not Be Verified

Not every AI response needs verification.

Trust OS does not need to be applied to:

- General FAQ answers
- Low-risk summarization
- Internal brainstorming
- Drafting assistance with no decision impact
- Casual text generation
- Non-critical search support

This prevents audit noise and keeps the system practical.

---

## Design Principle

Not every AI decision needs verification.

But critical decisions must be verifiable.

Trust OS focuses on high-impact decisions where accountability matters.

---

## Why this matters

Most AI systems generate answers but cannot prove how they were produced.

Trust OS enables:

- Verifiable AI decisions
- Audit-ready outputs
- Explainability for government use
- Integrity records for public systems
- Decision traceability before execution

---

## Positioning

Gennai provides the AI execution layer.

Trust OS provides the verification layer.

Together, they demonstrate a path toward trustworthy government AI.

---

## Status

PoC / Experimental Extension

This repository is not the main Trust OS API.

The main Trust OS production API is available through:

```txt
https://trustos-core-gateway-v2-7jm9owrs.an.gateway.dev
```

---

## Related Projects

- Gennai / Digital Agency OSS  
  https://github.com/digital-go-jp/genai-ai-api

- Trust OS SDK  
  https://www.npmjs.com/package/trust-os-sdk

- Trust OS API  
  https://github.com/trustos-trustfolio/trustos-api-clean
