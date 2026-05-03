---
description: Run a comprehensive Google Ads account audit (14 categories, ~42 signals)
---

Run the **Google Ads Audit** skill on the user's Google Ads account.

The audit covers 14 categories (Quality Score, Performance Max, conversion tracking, audiences, landing pages, wasted spend, RSAs, bidding, and more) and produces a graded report with prioritized findings, a wasted-spend estimate, and a 7-day action plan.

If the Optmyzr MCP server is connected (look for `mcp__*__get_active_accounts` and `mcp__*__get_ppc_report`), pull data live and surface additional Tier-2 signals (Auction Insights, industry benchmarks, change history, feed health). Otherwise, walk the user through the 4-paste manual flow with a conditional 5th paste for PMax.

Follow the skill's `SKILL.md` for the orchestration, `reports.md` for paste flow, `signals.md` for the signal catalog, `scoring.md` for grading, and `output-template.md` for the final report format.

Begin with: **Step 1 (detect data source) → Step 2 (30-second pre-audit interview)**, then proceed.
