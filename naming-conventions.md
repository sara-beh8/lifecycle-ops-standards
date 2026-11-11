# Campaign naming conventions

Names are an API. A human should read intent at a glance; a dashboard should parse ownership, motion, and audience with one split on `|` or `_`. I first built this pattern running paid search for car-rental brands in 2015 (per-market tracking) and rebuilt it for AI-driven lifecycle in 2026 — it survives every stack.

## Campaign names

```
[TEAM Scope] Motion | Audience | Variant
```

| Part | Values (example set) | Rule |
|---|---|---|
| `TEAM Scope` | `[GRW Lifecycle]`, `[GRW Onboarding]`, `[MKT Newsletter]` | Bracketed prefix = owning team. Never rename on handover — add owner in the registry instead. |
| `Motion` | `Cross-Sell`, `Winback`, `Adoption`, `Weekly Email` | The job the campaign does, not the asset type |
| `Audience` | `SMB`, `Commercial`, `Trial`, `Dormant` | Segment shorthand — must match a registry-documented segment |
| `Variant` | `V2`, `Test-SubjectLine`, `Gaia` | Only when parallel versions exist |

Examples:

```
[GRW Lifecycle] Cross-Sell AI Assistant | SMB | V2
[GRW Lifecycle] Winback Disabled Feature | Commercial
[GRW Lifecycle] Weekly Email | All Active | Test-Personalization
```

## Anti-patterns (all found in the wild)

- ❌ `New campaign FINAL v3 (copy)` — unparseable, unownable
- ❌ Owner initials in names (`JD_winback`) — names outlive people
- ❌ Renaming a running campaign — breaks historical reporting; version in the registry instead
- ❌ Three generations of prefixes coexisting (`[Scale]`, `[Scaled CX]`, `[DG x Scaled]`) — migrate or map, never accumulate

## Workflow / action names inside campaigns

`{step-number} {verb} {object}` → `01 fetch account-context`, `02 branch first-time?`, `03 send email-B`. The number makes flow diagrams and debugging sane.

## Migration playbook for an inherited estate

1. Inventory everything into the registry AS-IS (old names in a `legacy_name` column)
2. Define the new schema; map legacy → new in the registry, not in the tool
3. Rename only at natural version bumps (a rebuild, a renewal) — never mid-flight
4. After 2 renewal cycles the estate converges without ever breaking a report
