# Eligibility segments — the baseline + always-exclude pattern

The most common lifecycle incident is not a bad email; it's a good email to the wrong account — a churned customer, an account mid-escalation, someone in an active sales cycle. Per-campaign exclusion lists don't scale: every new campaign re-invents them, and every miss is a support ticket (or a lost renewal).

## The pattern

**Layer 0 — Master eligibility baseline (one segment, ANDed into every campaign, no exceptions):**

```
IS an active account
AND has a valid, deliverable email
AND has NOT opted out of marketing communications
AND is NOT in a protected state (offboarding, legal hold, payment dispute)
```

**Layer 1 — Always-exclude segments (shared, maintained centrally):**

- `excl_active-sales-cycle` — open opportunity in CRM
- `excl_onboarding` — accounts inside the guided onboarding window
- `excl_renewal-window` — accounts in renewal conversations
- `excl_recent-escalation` — support escalation in the last N days

**Layer 2 — Campaign-level logic** answers only campaign-level questions ("has feature X", "automation rate < Y%"). It never re-implements layers 0–1.

## Why layered beats per-campaign

- **Mis-sends become impossible by construction**, not by vigilance — new campaigns inherit safety on day one
- **One place to update** when a new protected state appears (update the baseline; every campaign is instantly correct)
- **Auditable**: "who can we email at all?" has one answer, not fifteen

## Implementation notes (tool-agnostic)

- In Customer.io / Braze / Iterable: build baseline + excludes as named segments; campaign trigger = `baseline AND campaign_logic AND NOT (each exclude)`
- Document the baseline's definition in the campaign registry with an owner and a review date — it's the single most load-bearing object in the workspace
- Test with a canary: a known-excluded fixture account that should never receive anything; alert if it ever does
