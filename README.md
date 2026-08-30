# ControlPlane.ai
### Accenture Innovation Challenge

ControlPlane.ai is an intelligent guardrail and governance engine designed to analyze multi-part user prompts, perform real-time intent and safety checks, inject dynamic instructions into LLMs, and validate responses through a multi-tier verification layer before final delivery.

---

## Architecture Overview

ControlPlane.ai introduces a **two-layer AI evaluation architecture** positioned directly around the Core AI model.

```text
                    ┌─────────────────┐
                    │      USER       │
                    │     PROMPT      │
                    └────────┬────────┘
                             │
                             ▼
                 ┌─────────────────────┐
                 │   PROMPT ANALYZER   │
                 │                     │
                 │ • Safety Check      │
                 │ • Intent Detection  │
                 │ • Risk Tagging      │
                 │ • Missing Data      │
                 └──────────┬──────────┘
                            │
                            ▼
                    ┌───────────────┐
                    │    CORE AI    │
                    │ GPT / Gemini  │
                    │ Claude / etc. │
                    └───────┬───────┘
                            │
                            ▼
                ┌──────────────────────┐
                │   RESPONSE CHECKER   │
                │                      │
                │ • Hallucination      │
                │ • Bias               │
                │ • Data Leakage       │
                │ • Safety             │
                └───────────┬──────────┘
                            │
                            ▼
                  ┌──────────────────┐
                  │ DECISION ROUTER  │
                  └────────┬─────────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
        ┌──────────┐  ┌──────────┐  ┌──────────┐
        │ ESCALATE │  │   EDIT   │  │  REJECT  │
        └────┬─────┘  └────┬─────┘  └────┬─────┘
             │             │             │
             ▼             ▼             ▼
           USER          USER          BLOCK
                           │
                           ▼
                 ┌──────────────────┐
                 │ HUMAN REVIEW     │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ FEEDBACK LOOP    │
                 │                  │
                 │ Tune thresholds  │
                 │ using decisions  │
                 └──────────────────┘
