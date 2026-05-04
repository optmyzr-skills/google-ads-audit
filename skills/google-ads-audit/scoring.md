# Scoring — A/B/C grading per Optmyzr methodology

This file defines how individual signal results roll up into category scores and an overall account grade.

The grading system mirrors Optmyzr's internal audit (Grade A/B/C) and uses Optmyzr's published color thresholds.

---

## Per-signal scoring

Each signal evaluation produces one of:

| Result | Points | Color |
|---|---|---|
| **PASS** | MaxPoints | 🟢 green |
| **WARNING** | MaxPoints × 0.5 | 🟠 orange |
| **FAIL** | 0 | 🔴 red |
| **N/A** | excluded from category math | ⚪ gray |

`MaxPoints` per signal = **10** (uniform across the curated catalog). Signals can be marked N/A by the audit logic when they don't apply (e.g., "AI Max readiness" when the account has no DSAs and no AI Max enabled — a free-pass signal).

---

## Per-category scoring

For each category:

```
CategoryScore (%) = SUM(applicable signal points) / SUM(applicable signal max points) × 100
```

Most categories have **3 signals** (max 30 points per category). A few categories have more because the underlying area is high-leverage:

| Category | Signal count | Max points |
|---|---|---|
| Cat 4 — Performance Max & Alt Channels | 4 *(added 4.4 Display exclusions in v0.1.2)* | 40 |
| Cat 12 — Ads / RSAs | 5 *(added 12.4 duplicate copy + 12.5 legacy ad types in v0.1.2)* | 50 |
| All other categories | 3 | 30 |

The percentage formula is the same regardless of signal count, since it's `applicable_points / applicable_max × 100`. Category weights (next section) compensate for the extra signal coverage in Cat 4 and Cat 12 — the per-category percentage is what feeds into the weighted overall, not raw point counts.

### Category color badge

Color thresholds match Optmyzr's published grading:

| Category Score | Badge |
|---|---|
| ≥ 90% | 🟢 green |
| ≥ 80% | 🟠 orange |
| < 80% | 🔴 red |

### Category letter grade

| Category Score | Grade |
|---|---|
| 100% | A |
| 80–99% | B |
| 1–79% | C |
| 0% (with applicable signals) | C |
| All signals N/A | — (no grade) |

---

## Overall account scoring

The overall score is a **weighted** average across the 14 categories. Weights reflect the audit's emphasis (conversion tracking + wasted spend + Quality Score get the highest weights, mirroring Optmyzr's audit).

| # | Category | Weight |
|---|---|---|
| 1 | Account & Settings | 5% |
| 2 | Conversion Tracking | 12% |
| 3 | Campaign Structure | 7% |
| 4 | Performance Max & Alt Channels | 8% |
| 5 | Budgets & Spend | 7% |
| 6 | Bidding | 8% |
| 7 | Targeting | 5% |
| 8 | Audiences | 6% |
| 9 | Keywords | 7% |
| 10 | **Quality Score** | **10%** |
| 11 | Search Terms & Negatives | 10% |
| 12 | Ads / RSAs | 8% |
| 13 | Assets / Extensions | 4% |
| 14 | Landing Pages | 3% |
| | **Total** | **100%** |

```
OverallScore = SUM(CategoryScore × Weight) / SUM(Weight)
```

(Sum of weights normalizes correctly even when some categories are entirely N/A — e.g. if PMax category is N/A for a Search-only account, the remaining 13 categories' weights are renormalized to 100%.)

### Overall grade

| Overall Score | Grade | Color |
|---|---|---|
| ≥ 90% | **A** | 🟢 green |
| ≥ 80% | **B** | 🟠 orange |
| < 80% | **C** | 🔴 red |

---

## Calibration based on the pre-audit interview

Use the user's interview answers to adjust scoring fairness. Specifically:

### By account goal (Q1)

- **Lead generation** — Bidding (6.1) emphasizes tCPA/Maximize Conversions; Audiences (8.3) emphasizes excluding existing customers; LP audit (14) emphasizes form-page UX.
- **E-commerce sales** — Bidding (6.1) emphasizes tROAS; Campaign Structure (3.2) penalizes accounts without Shopping/PMax; Audiences emphasizes Customer Match for value-based bidding.
- **Brand awareness** — Don't penalize low ROAS or "weak conversion tracking" signals; emphasize reach metrics, frequency, and audience signals.
- **App installs** — Adjust to App campaign benchmarks; many of the 14 categories are partially N/A.

### By target efficiency (Q2)

- If user provided a **target CPA** and a campaign is hitting it: don't fail it for "high CPC" or "limited by budget" — those are good problems to have.
- If user said **"not sure"**: use Optmyzr's default vertical benchmarks if MCP is connected (`get_industry_insights`); otherwise apply broad-market thresholds.

### By account maturity (Q3)

- **New (<6 months)** — soften penalties on Smart Bidding (still in learning), Quality Score (still settling), and Customer Match (may not have list yet). Don't fail an account for things that genuinely need time.
- **Established (6mo–2yr)** — full scoring applies.
- **Mature (>2yr)** — additionally check that bid strategies aren't stale (eCPC was acceptable in 2019, not 2026); penalize stagnation more aggressively.

---

## Wasted spend dollar estimate

Compute a single headline number: **$X wasted per month**, summing:

- Search Terms with `Cost > threshold AND Conversions = 0` (from Search Terms paste)
- Estimated overspend on low-QS keywords (low-QS keywords with > expected CPC penalty)
- Estimated lost opportunity from `Search lost IS (budget)` × current conv rate × current AOV (e-commerce) or × estimated lead value (lead-gen, if user provided)

This number anchors the report. It's the LinkedIn-shareable hook and the most actionable single line.

Format: round to nearest $10, label as "Estimated wasted/under-utilized spend per month."

---

## Edge cases

- **All signals in a category are N/A** → category excluded from overall score, badge shown as ⚪ gray with "Not applicable to this account."
- **Account has zero spend in last 30 days** → abort, ask user to confirm correct account/date range.
- **Search Terms paste is <30 days** → warn user; flag wasted-spend numbers as "preliminary."
- **PMax skipped (manual paste mode)** → score Category 4 only on what's visible from Campaigns paste; flag in "What this audit can't see" footer.
