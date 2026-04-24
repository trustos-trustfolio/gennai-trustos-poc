# Trust OS for GovAI (Gennai PoC)

Trust OS adds a verification layer to government AI systems.

This repository demonstrates how to integrate Trust OS with Gennai-compatible AI applications.

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

## Why this matters

Most AI systems generate answers but cannot prove how they were produced.

Trust OS enables:

* Verifiable AI decisions
* Audit-ready outputs
* Explainability for government use
* Integrity layer for public systems

---

## Positioning

Gennai provides the AI execution layer.
Trust OS provides the verification layer.

Together, they enable:

"Trustworthy Government AI"

---

## Use Cases

* Administrative decision support
* Legal / regulatory AI
* Public service automation
* Audit-compliant AI workflows

---

## Status

PoC (Proof of Concept)
