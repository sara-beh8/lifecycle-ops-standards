# UTM schema

Attribution dies from inconsistency, not from missing tools. One schema, enforced at link-build time, makes channel reporting a `GROUP BY` instead of a cleanup project.

## The five parameters

| Param | Owns the question | Vocabulary (lowercase, hyphenated, closed list) |
|---|---|---|
| `utm_source` | Where did the click physically happen? | `customer-io`, `linkedin`, `google`, `reddit`, `quora`, `newsletter`, `in-app` |
| `utm_medium` | What kind of placement? | `email`, `paid-social`, `paid-search`, `organic-social`, `referral`, `in-product` |
| `utm_campaign` | Which campaign? | **The campaign's registry slug** — e.g. `grw-lifecycle_cross-sell-ai_smb_v2`. Never freehand. |
| `utm_content` | Which variant/placement inside it? | `email-b_cta-primary`, `tip-block`, `footer-link` |
| `utm_term` | (Paid search only) keyword | auto-populated by the ads platform |

## Rules

1. **`utm_campaign` = registry slug, always.** The registry generates it from the campaign name (lowercase, `_` between name parts, `-` inside parts). One join key across ads platform ↔ email tool ↔ analytics ↔ registry.
2. **Closed vocabularies.** `linkedin`, not `LinkedIn`/`li`/`linked-in` on alternating Tuesdays. New value = PR to this file first.
3. **Build links with a helper, not by hand** — a spreadsheet formula is enough; hand-typed UTMs drift within a week.
4. **Email links carry UTMs even though the email tool tracks clicks** — the email tool sees clicks; only UTMs let the *website* analytics see what those clicks did next.

## Example

Cross-sell email, variant B, primary CTA:

```
?utm_source=customer-io&utm_medium=email&utm_campaign=grw-lifecycle_cross-sell-ai_smb_v2&utm_content=email-b_cta-primary
```

Reporting then needs exactly one line of SQL per question:
which motion drives signups → `GROUP BY utm_campaign`; which variant wins → `GROUP BY utm_content`.
