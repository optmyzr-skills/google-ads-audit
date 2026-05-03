# Reports — paste targets and Google Ads UI paths

This file describes exactly what to ask the user for, where to click in the Google Ads UI to download each report, and which columns must be present.

When in manual paste mode, walk through these one at a time. Don't dump all four asks at once — ask for one, wait for the paste, parse it, then ask for the next.

---

## Paste 1 — Campaigns export

**Why:** powers Account & Settings, Campaign Structure, Budgets & Spend, Bidding, Targeting overview, and the PMax detection trigger.

### Where to find it in Google Ads

Left nav → **Campaigns**. (Make sure you're in the Campaigns *view*, not the Overview dashboard.)

### How to download

1. Set the date range to **Last 30 days** (top-right date picker).
2. Click the **Columns** icon (3 stacked bars at top of the table) → **Modify columns**.
3. Verify the columns below are enabled — most are on by default, the **bold** ones often need to be added.
4. Save columns → click the **Download** icon (down-arrow) → **CSV** or **Google Sheets**.
5. Open the file, copy all rows (header + data), paste in chat.

#### Columns to enable (must add — usually NOT on by default)
- **Bid strategy type**
- **Search impr. share**
- **Search lost IS (budget)**
- **Search lost IS (rank)**
- **Conv. value**
- **Conversion value / cost** (ROAS proxy)

#### Already there by default (just verify they're checked)
- Campaign name
- Campaign status
- Campaign type
- Budget
- Cost
- Clicks
- Impressions
- CTR
- Avg. CPC
- Conversions
- Cost / conv.
- Conv. rate

### Prompt to user

> **Paste 1 of 4: Campaigns export**
>
> 1. In Google Ads, click **Campaigns** in the left nav
> 2. Date range: **Last 30 days**
> 3. Click the columns icon (3 bars) → Modify columns. Add any of these that aren't already enabled:
>    - **Bid strategy type**
>    - **Search impr. share**
>    - **Search lost IS (budget)**
>    - **Search lost IS (rank)**
>    - **Conv. value**
>    - **Conversion value / cost**
> 4. Save → click the download icon → CSV
> 5. Paste below (or attach with `@/path/to/file.csv`)

### What to do after paste

- Confirm the column set looks right. If key columns are missing, ask the user to re-export.
- Detect PMax campaigns: any row where `Campaign type` contains "Performance Max". *(See SKILL.md Step 3a — any PMax presence triggers Paste 5 prompt.)*
- Note the highest-spend campaigns by Cost — they get scoring priority.
- If the account has 0 campaigns or 0 cost, abort gracefully: "I don't see any spending campaigns. Are you sure this is the right account / date range?"

---

## Paste 2 — Keywords export with Quality Score

**Why:** powers Keywords, **Quality Score** (the Optmyzr signature category), Cannibalization detection, and Match-Type strategy.

### Where to find it in Google Ads

Left nav → **Audiences, keywords, and content** → **Search keywords**.

### How to download

1. Set the date range to **Last 30 days**.
2. Click the **Columns** icon → **Modify columns**.
3. Verify the columns below — **bold** ones almost always need to be added (the four QS columns are off by default).
4. Save columns → **Download** icon → CSV.
5. Paste contents in chat (or attach with `@/path/to/file.csv`).

#### Columns to enable (must add — NOT on by default)
- **Quality Score**
- **Expected CTR (hist.)** *(sometimes labeled "Exp. CTR (hist.)" in the export)*
- **Ad relevance**
- **Landing page exp.** *(may be labeled "Landing page experience" in the column picker)*
- **Search impr. share**

#### Already there by default (just verify)
- Keyword
- Match type
- Status
- Ad group
- Campaign
- Cost
- Clicks
- Impressions
- Conversions
- Conv. value
- Avg. CPC

### Prompt to user

> **Paste 2 of 4: Keywords with Quality Score**
>
> 1. Left nav → **Audiences, keywords, and content** → **Search keywords**
> 2. Date range: **Last 30 days**
> 3. Click the columns icon → Modify columns. Add these (all four QS columns are off by default):
>    - **Quality Score**
>    - **Expected CTR (hist.)**
>    - **Ad relevance**
>    - **Landing page exp.**
>    - **Search impr. share**
> 4. Save → Download → CSV
> 5. Paste below (or attach with `@/path/to/file.csv`)

### What to do after paste

- Tally Quality Score distribution (1-3 / 4-6 / 7-10) and spend-weighted average.
- Calculate spend share of low-QS keywords (QS ≤4).
- Detect cannibalization: same keyword text + match type appearing in 2+ ad groups. Flag any with combined spend > 1% of account total. **Note:** in multi-language / multi-region accounts (e.g. brand kw in `…CA, US & EU | English` + `…BE, DACH & LU | German` + `…ES & LATAM | Spanish`), this is intentional language separation — flag as PASS-with-note, don't recommend consolidation.
- Track which keywords have the worst of the three QS components — that drives the recommended fix:
  - Below-Avg **Expected CTR** → ad copy work (improve headlines, include keyword)
  - Below-Avg **Ad Relevance** → tighter ad groups (the ad must obviously be about the keyword)
  - Below-Avg **LP Experience** → landing page work (speed, mobile, on-page keyword presence, content depth)

---

## Paste 3 — Search Terms Report (30 or 90 days — both accepted)

**Why:** powers Search Terms & Negatives, wasted spend estimate, Lin-Rodnitzky ratio, and feeds the Top 5 Findings with concrete dollar figures.

### Accepted date ranges

This paste accepts **either 30 days or 90 days** of search-term data. Both work. The skill **must auto-detect the actual window** from the CSV's date-range header (line 2 of the export, e.g. `"January 30, 2026 - April 29, 2026"`) and **normalize all monetary outputs to a per-month basis** so reports are comparable across runs.

- **30 days (preferred default)** — fastest match to the rest of the audit, no normalization needed
- **90 days** — more reliable wasted-spend signal, especially for low-volume accounts (<150 conv/mo) or where seasonality matters. Multiply totals by `30 / actual_days` to express as monthly.

If the CSV's date range falls outside 25–95 days, **ask the user to re-export** with a clean 30 or 90 day window. Don't try to estimate from arbitrary windows — the wasted-spend headline number must be trustworthy.

### Where to find it in Google Ads

**Two equivalent paths** (use whichever is faster for you):
- **A.** Left nav → **Insights and reports** → **Search terms** *(dedicated view, recommended)*
- **B.** Left nav → **Audiences, keywords, and content** → **Search keywords** → click the **Search terms** tab at the top of the table

Both produce the same data.

### How to download

1. Set the date range to **Last 30 days** (or **Last 90 days** for low-volume accounts — see "Accepted date ranges" above).
2. Click the **Columns** icon → **Modify columns**.
3. Verify the columns below — **bold** ones often need to be added.
4. Save → **Download** icon → CSV.
5. Paste in chat (or attach with `@/path/to/file.csv`).

#### Columns to enable (often need to add)
- **Conv. value**
- **Keyword** *(the matched keyword that triggered the search term — sometimes off by default)*
- **Added/Excluded** *(shows whether the term has been added as a keyword or excluded as a negative — critical for negative-list maintenance check)*

#### Already there by default
- Search term
- Match type *(the matched keyword's match type)*
- Campaign
- Ad group
- Cost
- Clicks
- Impressions
- Conversions
- Conv. rate
- Cost / conv.

### Prompt to user

> **Paste 3 of 4: Search Terms Report**
>
> 1. Left nav → **Insights and reports** → **Search terms** *(or Search keywords → Search terms tab)*
> 2. Date range: **Last 30 days** *(90 days also fine for low-volume accounts — I'll auto-normalize to monthly)*
> 3. Click the columns icon → Modify columns. Add if not already enabled:
>    - **Conv. value**
>    - **Keyword** (the matched keyword)
>    - **Added/Excluded** status
> 4. Download as CSV → paste below (or attach with `@/path/to/file.csv`)

### What to do after paste

**Step 1 — detect window:** Read line 2 of the CSV (the date-range header). Extract start and end dates. Compute `actual_days = (end - start) + 1`. Compute `month_factor = 30 / actual_days`.

**Step 2 — handle "Month" column (Google segments by month):** If the CSV has a `Month` column, the same search term will appear once per month it generated traffic. Aggregate by `(search_term, campaign)` summing Cost / Clicks / Impressions / Conversions / Conv. value before computing any metrics.

**Step 3 — compute metrics, all normalized to monthly:**

- **Wasted spend** = `SUM(Cost) where Conversions = 0 AND Cost > threshold`, then × `month_factor` for the headline figure.
  - Threshold: `$10` for accounts >$1k/mo, `$5` for smaller. Threshold applies to the **window total**, not per-month, since one expensive search term may have accumulated cost slowly.
- **Lin-Rodnitzky-style ratio** = `(avg CPC across all terms) / (avg CPC across converting terms only)`. Window-independent — no normalization needed.
  - <1.5 → very efficient (potentially over-restricted; missing volume)
  - 1.5–2.0 → healthy
  - 2.0–3.0 → some inefficiency, worth pruning
  - >3.0 → significant inefficiency, urgent negatives review
- **Top wasted terms** — surface the top 10–15 by window-total cost, but display each as `$X over Y days = ~$Z/mo` so the user sees both the raw number and the normalized rate.

**Step 4 — disclose the window in the output:** Always state the actual date range used in the report header (e.g. `"Period analyzed: 30 Mar 2026 → 28 Apr 2026 (with 90-day search-term context, normalized to monthly)"`). Trust depends on transparency.

- Identify thematic clusters of wasted spend (e.g., job-seeker queries, free-intent, competitor names, informational) for negative-list recommendations.

---

## Paste 4 — Ads & Assets export

**Why:** powers Ads / RSAs (Ad Strength, asset counts, pinning), Assets / Extensions coverage.

This is **two exports** because Google Ads separates Ads from Assets. Either submit them as **two separate file attachments**, or combine the contents into one paste separated by a `---` line.

### Where to find each

- **Ads:** Left nav → **Campaigns** → click any campaign → **Ads** sub-tab. *(Or use the "Ads" view at the top-level left nav if your account layout shows it.)*
- **Assets:** Left nav → **Ads & assets** → **Assets**. *(Newer Google Ads UI; older accounts may show this as "Ads & extensions" → "Extensions / Assets".)*

### 4a — Ads export

#### Where: Campaigns → drill into a campaign (or "Ads" view) → Ads sub-tab

1. Date range: **Last 30 days**.
2. Click the **Columns** icon → **Modify columns**.
3. Verify the columns below — **Ad strength** is the one most likely missing.
4. **Download** → CSV.

##### Columns to enable (must add)
- **Ad strength**

##### Already there by default (just verify)
- Ad type
- Headlines
- Descriptions
- Status
- Campaign
- Ad group
- Final URL
- Impressions
- Clicks
- Conversions
- Cost

### 4b — Assets export

#### Where: Ads & assets → Assets

1. Date range: **Last 30 days** (or All time — coverage check is window-insensitive).
2. View: **All** or filter by asset type.
3. Click the **Columns** icon → verify the columns below.
4. **Download** → CSV.

##### Columns to enable (often need to add)
- **Status reason** *(catches Disapproved assets — the silent killer)*
- **Last updated**
- **Performance** label *(if available — Google shows "Best / Good / Low / Learning" for some asset types)*

##### Already there by default
- Asset
- Asset type
- Status
- Source / Added by
- Associated campaign(s) / ad group(s)
- Impressions
- Clicks

### Prompt to user

> **Paste 4 of 4: Ads & Assets**
>
> Two quick exports — attach them as separate files (`@/path/4a.csv` then `@/path/4b.csv`), or paste them together separated by a line containing only `---`.
>
> **First — Ads:**
> 1. Click into a campaign → **Ads** sub-tab *(or use the top-level Ads view)*
> 2. Date range: **Last 30 days**
> 3. Add column: **Ad strength**
> 4. Download → CSV
>
> **Then — Assets:**
> 1. Left nav → **Ads & assets** → **Assets**
> 2. Add columns:
>    - **Status reason** *(catches disapprovals)*
>    - **Last updated**
> 3. Download → CSV
>
> Attach or paste both below.

### What to do after paste

- For each RSA: check Ad Strength (Poor/Average = WARNING; Excellent/Good = PASS), count headlines (≥8 = PASS, 5-7 = WARNING, <5 = FAIL), count descriptions (≥3 = PASS, 2 = WARNING, 1 = FAIL).
- Per ad group: count active RSAs (≥3 = PASS, 2 = WARNING, 1 = FAIL).
- For Assets: per campaign, check coverage of: sitelinks (≥4), callouts (≥4), structured snippets (≥1), image (≥1 for Search), call (≥1 if account is lead-gen), location (≥1 if account is local).
- Flag pinning patterns: if any RSA has every position pinned, flag as over-constrained.

---

## Paste 5 — PMax / Asset Groups (CONDITIONAL)

**Trigger:** ask for this paste **whenever the Campaigns export (manual flow) or `CampaignPerformance` MCP response (MCP flow) shows at least one campaign with `Type` containing "Performance Max" — regardless of size or spend share.**

The trigger is **presence**, not threshold. A "PMax Test" campaign with $50/mo spend still earns the prompt, because:
- Cat 4 (Performance Max & Alt Channels) cannot be properly scored without asset-group-level data
- Small/test PMax campaigns are often the *most* in need of an audit (signals not yet tuned, asset diversity often thin)
- Prompting only on large PMax misses the early-signal opportunity advertisers most benefit from

The user can always type **skip** if they don't want to paste-fill — that's their choice, but the prompt should always appear.

**Why:** PMax has unique audit dimensions not visible in standard exports — asset group health, audience signal quality, brand exclusion presence, search themes utilization.

### Where to find it in Google Ads

Left nav → **Campaigns** → click into any **Performance Max** campaign → **Asset groups** tab at the top of the campaign page.

For accounts with many PMax campaigns, ask the user to paste the top 3 by spend.

### How to download

1. From inside a PMax campaign, click the **Asset groups** tab.
2. Date range: **Last 30 days**.
3. Click the **Columns** icon → **Modify columns**.
4. Verify the columns below.
5. **Download** → CSV.

#### Columns to enable (often need to add)
- **Performance label** *(Best / Good / Low / Learning — Google's asset-group performance grade)*
- **Listing groups** *(only relevant for Shopping/retail PMax with product feeds)*

#### Already there by default
- Asset group name
- Status
- Impressions
- Clicks
- Cost
- Conversions
- Conv. value
- Cost / conv.

### Prompt to user (always shown when PMax detected)

> **Optional Paste 5: PMax Asset Groups**
>
> I see [N] PMax campaign(s) in your account [— "Optmyzr Performance Max - Test", "..."]. PMax has unique audit dimensions (asset groups, audience signals, brand exclusions, search themes) that aren't in any other export — and these are often where the biggest optimizations sit.
>
> For your top PMax campaign(s) by spend:
> 1. Click into the campaign
> 2. Click the **Asset groups** tab
> 3. Set date range: Last 30 days
> 4. Download CSV → paste below
>
> Or type **skip** to move on (PMax findings will be limited to top-level campaign data — no asset-group, signal, or brand-exclusion analysis).

### What to do after paste

- Count asset groups per PMax campaign (≥2 with diverse signals = PASS).
- Per asset group: check signal richness (audience signals provided, search themes set, asset variety).
- Flag any PMax campaign with brand-keywords-as-search-themes (cannibalization risk) or no brand exclusions.
- If the account has Shopping context, note that without Merchant Feed details (MCP-only), feed-level audit is partial.

---

## After all pastes are done

Confirm with the user:
> "Got all the data I need. Running the audit across 14 categories now — this takes about 30 seconds."

Then proceed to Step 4 in `SKILL.md`: walk the 14 categories from `signals.md`, score per `scoring.md`, format per `output-template.md`.
