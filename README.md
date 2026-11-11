# lifecycle-ops-standards

**The boring rails that make growth governable.** Naming conventions, UTM schema, a campaign registry template, and segment governance patterns for lifecycle/CRM programs.

## Why this exists

Every lifecycle program I've inherited had the same disease: campaigns running in parallel for years, named by whoever built them, untrackable in analytics, with overlapping audiences and no renewal process. You can't optimize what you can't find, and you can't govern what you can't name.

This repo is the fix — the standards layer I now build *first* at any company, before touching a single campaign. The patterns are generalized from systems I built for a multi-campaign lifecycle program; all examples use a fictional company.

## What's here

| File | What it gives you |
|---|---|
| [`naming-conventions.md`](naming-conventions.md) | Campaign, workflow, and asset naming schema — parseable by humans AND dashboards |
| [`utm-schema.md`](utm-schema.md) | UTM structure that makes channel attribution automatic instead of archaeological |
| 🔒 `campaign-registry-template.csv` | The single-source-of-truth registry: one row per campaign, status, owner, segment, renewal log |
| [`eligibility-segments.md`](eligibility-segments.md) | The baseline-eligibility + always-exclude pattern that prevents mis-sends by construction |

## What's public and what's on request

The naming, UTM and eligibility standards are public. The campaign registry template (🔒) is **available on request**: [LinkedIn](https://www.linkedin.com/in/sara-beheyt/).

## The core idea

A campaign is an artifact; a **governed estate** is an asset. Four rules:

1. **Name things so a query can find them.** If your dashboard needs a manual mapping table, your names failed.
2. **One registry, no exceptions.** Every campaign is a row. Every renewal is logged. The registry outlives every owner.
3. **Eligibility is layered, not per-campaign.** One master baseline segment (who may EVER be emailed) ANDed into every campaign + shared always-exclude lists. Campaign-level logic only handles campaign-level questions.
4. **Renewal is scheduled, not heroic.** Every campaign gets a review date at birth. Stale campaigns are found by process, not by accident.

## Story

These standards are one layer of a larger system — a lifecycle program where old campaigns generate their own successors. Full case study: [sara-beh8.github.io](https://sara-beh8.github.io)
