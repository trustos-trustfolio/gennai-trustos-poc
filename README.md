# Trust OS for GovAI (Gennai PoC)

This adds a verification layer to GovAI (Gennai-compatible AI)

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

## Run Example

curl -X POST https://YOUR_API_ENDPOINT/invoke \
  -H "Content-Type: application/json" \
  -d @example/curl.json

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
