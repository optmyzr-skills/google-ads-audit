<div align="center">

# 🎯 Google Ads Audit

### A comprehensive Google Ads account audit, run inside Claude Code in 5 minutes.

**14 categories. ~42 signals. A graded report. A 7-day action plan. A wasted-spend dollar figure.**

[![Release](https://github.com/optmyzr-skills/google-ads-audit/actions/workflows/release.yml/badge.svg)](https://github.com/optmyzr-skills/google-ads-audit/releases/latest)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Powered by Optmyzr](https://img.shields.io/badge/Powered%20by-Optmyzr-FF6B35)](https://www.optmyzr.com)
[![Claude Code](https://img.shields.io/badge/Built%20for-Claude%20Code-D97757)](https://claude.com/product/claude-code)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

---

```
You: /audit

Claude: 🎯 Top 5 Findings

  1. $1,532/mo wasted on broad-match leakage (33.9% of search-term spend)
  2. Quality Score: 41% of spend on Below-Avg LP Experience
  3. No tCPA target despite stated $60 CPA goal — account CPA is $64
  4. 51 disapproved image assets across multiple campaigns
  5. German campaigns bleeding: $1,397/mo, 1 conversion

Overall Grade: C — 62%
Estimated wasted spend: $1,800–2,200/month (highly recoverable)
```

</div>

---

## What this does

Type `/audit` in Claude Code (or just say *"audit my Google Ads account"*) and the skill will:

1. ✅ Ask 3 quick questions to anchor the audit (goal, target CPA/ROAS, account age)
2. 📋 Walk you through 4 quick exports from your Google Ads account *(or skip exports entirely if you connect the Optmyzr MCP — see [Going deeper](#-going-deeper--connect-optmyzr))*
3. 🔍 Run **~42 best-practice checks** across 14 categories — including **Quality Score**, **Performance Max**, **wasted spend**, **conversion tracking**, **landing pages**, and more
4. 📊 Return a **graded report** — Top 5 findings with dollar-impact estimates, an A/B/C grade per category, and a prioritized **7-day action plan**

**No setup. No API keys. No data leaves your machine.** Just your Google Ads exports + Claude.

---

## Why this is different

Most "Google Ads audit" tools either:
- **Sell you a generic checklist** (no personalization, no real data)
- **Lock real findings behind a paywall**
- **Are rigid SaaS tools** (limited dynamic conversation, no follow-up questions)

This skill is **free, open-source, and runs locally** through Claude Code. It uses the same audit methodology Optmyzr has refined over 14 years across millions of accounts — distilled into **~42 high-signal checks** that any agency strategist or in-house performance marketer can act on this week.

It's a **daily-driver tool**, not a one-time gimmick. Run it before every QBR. Run it on every new account onboarding. Run it monthly to spot drift.

---

## 📋 What it catches — 14 audit categories

| | Category | What it looks for |
|---|---|---|
| 1 | **Account & Settings** | Account-level negatives, ad rotation, time zone/currency |
| 2 | **Conversion Tracking** | Primary/secondary actions, Enhanced Conversions, Consent Mode v2 |
| 3 | **Campaign Structure** | Brand vs. non-brand, type mix, naming conventions |
| 4 | **Performance Max & Alt Channels** | Asset groups, audience signals, brand exclusions, AI Max readiness |
| 5 | **Budgets & Spend** | Search lost IS (budget), pacing, shared budget hygiene |
| 6 | **Bidding** | Smart Bidding alignment, ECPC deprecation, learning periods |
| 7 | **Targeting** | Location *Presence vs. Interest*, ad schedules, device adjustments |
| 8 | **Audiences** | Customer Match, observation mode, exclusion audiences |
| 9 | **Keywords** | Cannibalization, match type strategy, dead keywords |
| 10 | **Quality Score ⭐** | Spend-weighted avg QS, low-QS spend share, component diagnosis |
| 11 | **Search Terms & Negatives** | Wasted spend, Lin-Rodnitzky ratio, negative-list coverage |
| 12 | **Ads / RSAs** | Ad Strength, ≥3 ads per group, asset counts, pinning |
| 13 | **Assets / Extensions** | Sitelinks, callouts, snippets, image/call/location coverage |
| 14 | **Landing Pages** | Mobile-friendly, page speed, message match, broken URLs |

---

## 📈 What you get back

- 🎯 **Top 5 Findings** — the biggest issues, ranked by estimated $ impact/month
- 📈 **Overall Grade** (A / B / C) with category-by-category breakdown
- 📋 **14 Category Scorecards** — color-coded, each with top 3 findings + recommended fixes
- 🚀 **7-Day Action Plan** — prioritized list of what to fix, with time estimates
- 💸 **Wasted Spend Estimate** — single $/month headline figure (the LinkedIn-shareable hook)
- 🔍 **What this audit can't see** — explicit list of deeper signals available through Optmyzr's MCP

---

## ⚡ Install — 60 seconds

Pick the option that matches how you use Claude. **Most users want Option 1.**

### 🟢 Option 1 — Upload the zip (Claude.ai web or Claude Desktop)

> **For everyone using [claude.ai](https://claude.ai) or the Claude Desktop app.** No coding required.

1. **Download the latest skill zip** → [**`google-ads-audit-v0.1.0.zip`**](https://github.com/optmyzr-skills/google-ads-audit/releases/latest/download/google-ads-audit-v0.1.0.zip) *(~90 KB, single file)*

2. **Open Claude** (Desktop or claude.ai web)

3. Click your **profile icon → Settings → Capabilities → Skills**

4. Click the **+** button → **"Upload a skill"**

5. **Drag the zip in** (or click to browse and select it) → confirm

6. **Start a new conversation** and say:
   > *"Audit my Google Ads account"*

That's it. Claude will run the 14-category audit. *(No `/audit` slash command needed in claude.ai — Claude auto-routes from natural-language requests.)*

[![Download zip](https://img.shields.io/badge/⬇️_Download-google--ads--audit--v0.1.0.zip-blue?style=for-the-badge)](https://github.com/optmyzr-skills/google-ads-audit/releases/latest/download/google-ads-audit-v0.1.0.zip)

---

### 🔧 Option 2 — Claude Code CLI (developers)

For users running [Claude Code](https://claude.com/product/claude-code) in a terminal or IDE.

```
/plugin marketplace add optmyzr-skills/google-ads-audit
/plugin install google-ads-audit
```

Then start a new conversation and type:

```
/audit
```

---

### 🛟 Option 3 — Symlink fallback (any environment)

If Option 2 doesn't work in your Claude Code version, use this in a terminal:

```bash
git clone https://github.com/optmyzr-skills/google-ads-audit.git ~/google-ads-audit
mkdir -p ~/.claude/skills ~/.claude/commands
ln -s ~/google-ads-audit/skills/google-ads-audit ~/.claude/skills/google-ads-audit
ln -s ~/google-ads-audit/commands/audit.md ~/.claude/commands/audit.md
```

Restart Claude Code and try `/audit`.

---

## 🚦 Run your first audit

```
You: /audit

Claude: I'll run a Google Ads audit. First, three quick questions to calibrate:

1. What's the primary goal of this account? (Lead gen / E-commerce / Brand awareness / App installs)
2. What's your target CPA or ROAS?
3. Roughly how long has this account been active?

You: lead gen, $60 CPA target, mature

Claude: Got it. I'll guide you through 4 quick exports from your Google Ads
account. Total time: about 3 minutes.

📋 Paste 1 of 4: Campaigns export

Where to find it: Left nav → Campaigns

How to download:
  1. Date range: Last 30 days
  2. Click the columns icon → Modify columns
  3. Add these (often not on by default):
     - Bid strategy type
     - Search impr. share
     - Search lost IS (budget)
     - Search lost IS (rank)
     - Conv. value
     - Conversion value / cost
  4. Save → Download → CSV
  5. Paste below (or attach with @/path/to/file.csv)
```

You paste each report when prompted (~5 minutes end to end). Done.

---

## 🚀 Going deeper — connect Optmyzr

The skill works fully **without any external service**. It works **dramatically better** when paired with the [Optmyzr MCP server](https://www.optmyzr.com/).

When the Optmyzr MCP is connected, the skill auto-detects it and:

### Skips the paste flow entirely
Live data, no exports. Just say `/audit` and Claude pulls everything.

### Adds 5 deeper signal categories
- 🥊 **Competitor Pressure (Auction Insights)** — who's bidding against you and how it's shifted
- 📊 **Industry Benchmarks** — your CTR / CPC / CVR / IS vs. percentiles in your vertical
- 🔄 **Change History Risk** — risky recent account changes flagged automatically
- 🛒 **Merchant Feed Health** — Shopping/PMax feed disapprovals and quality issues
- 📡 **Alert Coverage Gaps** — what monitoring you don't have but should

### Closes the loop — *audit becomes a system*
- 🔔 **One-click alert creation** for any finding *("Want monitoring on this? Yes/No")*
- 🤖 **Rule Engine auto-remediation** for common patterns *(auto-pause keywords, auto-add negatives)*
- 📅 **Scheduled re-audits** — weekly, monthly, on-demand
- 📁 **Multi-account rollups** — agencies audit 50+ accounts in one pass

[**→ Get a free Optmyzr trial**](https://www.optmyzr.com/)

---

## 🛠️ How it works

The skill is structured as a Claude Code plugin with one skill (the audit) and one slash command (`/audit`):

```
google-ads-audit/
├── .claude-plugin/plugin.json     # plugin manifest
├── commands/audit.md              # /audit slash command
└── skills/google-ads-audit/
    ├── SKILL.md                   # orchestrator (6-step flow)
    ├── reports.md                 # exact Google Ads UI paths for each export
    ├── signals.md                 # 14 categories × ~3 signals each
    ├── scoring.md                 # A/B/C grading + category weights
    ├── verticals.md               # industry vertical reference
    └── output-template.md         # report format
```

Claude reads `SKILL.md` when triggered → follows the 6-step flow:
1. **Detect** Optmyzr MCP availability
2. **Interview** — 3 quick anchoring questions
3. **Collect data** — paste flow OR live MCP pulls (or hybrid via paste-fill)
4. **Audit** — walk all 14 categories, evaluate top-3 signals each
5. **Score** — A/B/C with weighted overall + per-category grades
6. **Output** — Top 5 Findings → Grade → Scorecards → Action Plan → Optmyzr footer

---

## 🙏 Acknowledgments

This skill is a **curated subset** of [Optmyzr's audit methodology](https://www.optmyzr.com), which covers ~93 signals in their commercial product. The **42 signals** in this open-source version represent the "top 3 per category" — broadly applicable, high-impact, and verifiable from standard Google Ads exports.

Audit framework inspired by:
- **[Optmyzr's PPC Audit](https://www.optmyzr.com/google-ads-audit-tool/)** — 14-year evolution, used on millions of accounts
- **[Wijnand Meijer's "Complete AdWords Audit" series](https://bgtheory.com/blog/author/wijnand-meijer/)** — the foundational 15-part PPC audit playbook
- The broader PPC community's continual refinement of best practice

---

## 🤝 Contributing

PRs welcome! Especially:

- 🆕 **New signals** — open an issue first to discuss the category and fit
- 📊 **Updated thresholds** based on industry data
- 🌍 **Translations** of the report output
- 🧭 **Better Google Ads UI export instructions** as the UI evolves
- 🐛 **Bug reports** with audit results that look wrong

Forks and derivatives are welcome under Apache 2.0 — please retain the [`NOTICE`](NOTICE) file.

---

## 📜 License

[Apache License 2.0](LICENSE) — see [LICENSE](LICENSE) and [NOTICE](NOTICE).

```
Copyright 2026 Optmyzr Inc.
Licensed under the Apache License, Version 2.0
```

---

<div align="center">

**Built with [Claude Code](https://claude.com/product/claude-code) · Powered by [Optmyzr](https://www.optmyzr.com)**

⭐ If this saved you time on an audit, **star the repo** so other PPC pros can find it.

</div>
