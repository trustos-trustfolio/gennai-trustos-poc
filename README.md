# Trust OS for GovAI (Gennai PoC)

This adds a verification layer to GovAI (Gennai-compatible AI), enabling auditable AI decisions for government use.
Trust OS adds a verification layer to government AI systems.

---

## What this does

This PoC adds a verification layer after AI decision generation.

Instead of only returning an answer, the system:

1. Generates AI response (RAG / LLM)
2. Hashes input, output, and references
3. Attaches a verifiable Trust OS record
4. Returns a structured JSON response

---

## Architecture

User Input  
↓  
GovAI (RAG / LLM)  
↓  
Trust OS Layer  
↓  
Verifiable JSON Output  

![Architecture](architecture.png)
---

## Run Example

curl -X POST https://YOUR_API_ENDPOINT/invoke \
  -H "Content-Type: application/json" \
  -d @example/curl.json

---

## Example Response

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

---

## Noise Reduction Design

Trust OS is not designed to verify every AI output.

Verifying every decision can create unnecessary noise, storage cost, and operational complexity.

Instead, Trust OS is designed as a selective verification layer.

The goal is to verify decisions that are high-risk, policy-relevant, or audit-sensitive.

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

This avoids creating unnecessary logs for low-risk AI outputs.

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

## Example Trust OS Record

{
  "decision_id": "tos_govai_001",
  "input_hash": "sha256...",
  "output_hash": "sha256...",
  "reference_hash": "sha256...",
  "risk_level": "HIGH",
  "recommendation": "REVIEW_REQUIRED",
  "reason_codes": [
    "POLICY_RELEVANT",
    "PUBLIC_IMPACT",
    "AUDIT_REQUIRED"
  ],
  "verification_status": "VERIFIED"
}

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

These areas require explainability, auditability, and accountability.

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

## Why this matters

Most AI systems generate answers but cannot prove how they were produced.

Trust OS enables:

- Verifiable AI decisions
- Audit-ready outputs
- Explainability for government use
- Integrity layer for public systems

---

## Positioning

Gennai provides the AI execution layer.  
Trust OS provides the verification layer.  

Together, they enable:

"Trustworthy Government AI"

---

## Use Cases

- Administrative decision support
- Legal / regulatory AI
- Public service automation
- Audit-compliant AI workflows

---

## Local Test (Optional)

python lambda/app.py

---

## Status

PoC (Proof of Concept)

---

## Related Projects

- Gennai (Digital Agency OSS)
  https://github.com/digital-go-jp/genai-ai-api

- Trust OS Extension (this repo)
  https://github.com/trustos-trustfolio/gennai-trustos-poc
