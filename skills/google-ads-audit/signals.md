# Signals — the 14 categories with top-3 signals each

Each category has 3 high-impact signals. For each signal, this file lists:
- **What it checks** — the question being asked
- **Pass / Warning / Fail thresholds**
- **Data source** — which paste (or MCP call) supplies the answer
- **Recommended fix** — the action to suggest if the signal fails
- **MCP-only depth** — additional depth available only with the Optmyzr MCP, if any

Total: ~42 curated signals. The full Optmyzr audit covers ~93. The remaining ~50 stay Optmyzr-only.

---

## Category 1 — Account & Settings

### 1.1 Account-level negatives are in use
- **Checks:** Are account-level negative keyword lists configured? An account without any account-level negatives almost always has cross-campaign waste.
- **Pass:** ≥1 account-level negative list applied to ≥1 campaign
- **Warning:** Lists exist but applied to <50% of campaigns
- **Fail:** No account-level negative lists
- **Data:** Inferable from Search Terms paste (excluded keywords) + cross-campaign waste pattern. With MCP: directly queryable.
- **Fix:** Create a shared negative list; populate with 20–50 universal blocks (free-intent, job-seeker, competitor, irrelevant terms); apply to all Search campaigns.

### 1.2 Ad rotation is set to "Optimize"
- **Checks:** Is ad rotation on the Google-recommended "Optimize: Prefer best performing ads"? "Rotate indefinitely" disables Google's ML-based rotation and is almost never the right choice in 2026.
- **Pass:** All campaigns set to Optimize
- **Warning:** Some on Rotate indefinitely (justifiable for testing)
- **Fail:** Most or all on Rotate indefinitely
- **Data:** Campaigns paste (if Ad rotation column was included) or ask user.
- **Fix:** Switch to Optimize unless running an A/B test that requires equal rotation.

### 1.3 Time zone & currency match the business
- **Checks:** Account time zone matches the operating market; currency matches the billing.
- **Pass:** Matches
- **Warning:** Mismatch but business is global (acceptable in some cases)
- **Fail:** Clear mismatch (e.g., US business set to UTC)
- **Data:** Requires user confirmation (not in paste); ask in pre-audit interview if not obvious.
- **Fix:** Cannot be changed once set — flag for awareness only; advise creating new account if material.

---

## Category 2 — Conversion Tracking

### 2.1 Primary vs. secondary conversion actions configured correctly
- **Checks:** Smart Bidding optimizes against primary conversions only. If everything is marked "Primary," the system can't focus.
- **Pass:** 1–3 primary conversions, with secondary actions for view-through metrics
- **Warning:** All conversions marked the same; primary list >5
- **Fail:** No primary/secondary distinction; or conversion-includes-conversions inflated by micro-events
- **Data:** Requires user input — ask "How many conversion actions does your account have, and how many are marked Primary?" With MCP: limited visibility (MCP exposes account performance, not conversion-action config) — still ask.
- **Fix:** Mark only the conversions you want to bid on as Primary; demote view-throughs and micro-events to Secondary.

### 2.2 Enhanced Conversions (with hashed first-party data) is enabled
- **Checks:** Enhanced Conversions captures hashed email/phone for better attribution, especially with privacy changes (iOS, Consent Mode).
- **Pass:** Enabled with first-party data hashed and sent (via gtag, GTM, or Google Ads API)
- **Warning:** Enabled but inconsistent (only some conversion actions)
- **Fail:** Not enabled
- **Data:** Ask user — "Is Enhanced Conversions enabled on your conversion actions?"
- **Fix:** Enable Enhanced Conversions on all key conversion actions; for forms, capture email/phone and pass via gtag. Critical post-2024.

### 2.3 Consent Mode v2 is implemented (EU/EEA)
- **Checks:** For accounts with EU/EEA traffic, Consent Mode v2 is required (since March 2024). Without it, modeled conversions are blocked and ad personalization breaks.
- **Pass:** Implemented (basic or advanced); modeled conversions present
- **Warning:** Implemented but only basic mode (advanced is preferred)
- **Fail:** Not implemented; account targets EU/EEA
- **Data:** Ask user — "Does your account target EU/EEA users? If yes, is Consent Mode v2 implemented?"
- **Fix:** Implement Consent Mode v2 — basic at minimum, advanced ideally. Critical for EU advertisers.
- **MCP-only depth:** none — this is a tag-side configuration, not an in-account setting.

---

## Category 3 — Campaign Structure

### 3.1 Brand and non-brand campaigns are separated
- **Checks:** Brand-term traffic has very different CPCs, conv rates, and intent than non-brand. Mixing them kills both bidding and reporting clarity.
- **Pass:** Brand and non-brand are in clearly separate campaigns
- **Warning:** Some brand campaigns exist but not consistently separated
- **Fail:** Brand keywords mixed into non-brand Search campaigns
- **Data:** Campaigns paste — look at campaign names for "brand"/"non-brand"/"generic"; cross-check with Keywords paste for the brand term presence.
- **Fix:** Create dedicated brand campaign(s); move all brand keywords; add brand as a campaign-level negative on non-brand campaigns.

### 3.2 Campaign type mix matches the goal
- **Checks:** A lead-gen account heavy on PMax can leak budget; an e-commerce account without Shopping/PMax leaves money on the table.
- **Pass:** Campaign mix is appropriate to the stated goal (interview Q1)
- **Warning:** Some misalignment (e.g., display campaigns dominating spend on a lead-gen account)
- **Fail:** Major mismatch (e.g., e-commerce account with no Shopping/PMax, or lead-gen account where PMax > 70% of spend with no Search support)
- **Data:** Campaigns paste (Type column + Cost) cross-referenced with interview Q1.
- **Fix:** Re-balance — if e-commerce, ensure Shopping/PMax + branded Search; if lead-gen, anchor on Search with PMax as a tested supplement, not the dominant channel.

### 3.3 Naming convention is consistent
- **Checks:** Inconsistent naming = no labels = no rule-based optimization possible. Common patterns: `[Geo]_[Type]_[Theme]_[Match]` or `[Funnel]_[Product]_[Audience]`.
- **Pass:** Clear, parseable convention used across ≥80% of campaigns
- **Warning:** Convention used inconsistently
- **Fail:** No discernible naming convention
- **Data:** Campaigns paste — pattern-match the campaign name strings.
- **Fix:** Adopt a naming convention; apply via Bulk Edit or labels. Especially important for accounts using Optmyzr Rule Engine, scripts, or any automation.

---

## Category 4 — Performance Max & Alt Channels

### 4.1 PMax has audience signals + search themes configured
- **Checks:** PMax without audience signals is "guess-mode." Search themes (released 2024) further direct PMax toward intent themes you care about.
- **Pass:** Each PMax asset group has ≥1 audience signal AND search themes configured
- **Warning:** Some asset groups missing one or the other
- **Fail:** No audience signals; no search themes
- **Data:** PMax paste (Paste 5) if available; otherwise ask user. With MCP: limited (MCP doesn't fully expose PMax internals — flag as Optmyzr platform unlock).
- **Fix:** Add audience signals (Customer Match list, in-market, custom segments). Add search themes that reflect the intent you want PMax to chase.

### 4.2 Brand exclusions applied to PMax
- **Checks:** Without brand exclusions, PMax cannibalizes your branded Search traffic (cheaper clicks pulled into PMax, inflating its apparent ROAS).
- **Pass:** Brand exclusions applied at account or campaign level
- **Warning:** Applied to some PMax campaigns but not all
- **Fail:** No brand exclusions; brand campaigns exist in parallel
- **Data:** Ask user. With MCP: queryable indirectly via competitive overlap with brand campaigns.
- **Fix:** Apply brand exclusions to all PMax campaigns; verify brand Search campaign IS hasn't been silently siphoned.

### 4.3 AI Max for Search readiness (where applicable)
- **Checks:** AI Max for Search (2026 feature) extends Broad Match + Smart Bidding with AI-generated headlines and dynamic search themes. Accounts on legacy DSAs or conservative Broad Match should evaluate readiness.
- **Pass:** AI Max enabled with completeness (assets diverse, negatives strong, conversion tracking healthy)
- **Warning:** Enabled but conversion tracking weak or negatives thin (will accelerate waste)
- **Fail:** Account has DSA campaigns and hasn't evaluated AI Max migration; or AI Max enabled with no negative-list discipline
- **Data:** Ask user; cross-check Search Terms paste for negative-list strength.
- **Fix:** Don't enable AI Max until conversion tracking + negatives are strong; if running DSAs, plan migration in 2026 (Google has signaled DSA consolidation into AI Max).

### 4.4 Display campaign placement exclusion lists *(added v0.1.2)*
- **Checks:** Display campaigns *without* placement exclusion lists serve ads to low-quality apps (mobileapps.google.com), parked domains, and adult content categories — wasting budget and distorting Display performance data. This signal applies to any campaign whose `Type` is `Display`, `Demand Gen`, or `Performance Max` (PMax serves Display/Demand Gen inventory).
- **Pass:** All Display / Demand Gen / PMax campaigns have account-level OR campaign-level placement exclusion lists applied; common categories excluded (mobile apps, gambling-if-not-relevant, sensitive content).
- **Warning:** Some Display campaigns have exclusions, others don't; or coverage is partial (e.g., mobile apps excluded but no content category exclusions).
- **Fail:** Active Display campaigns with **no** placement exclusion lists configured.
- **Data:** Cannot be directly fetched via the current MCP. Inference path: if account has Display/PMax campaigns AND `get_competitor_insights` shows mobileapps.google.com in shared placements, exclusions are likely missing. Otherwise: ask user OR include as a paste-fill prompt.
- **MCP-mode fallback:** Cannot directly verify. Default to WARNING when Display campaigns are present and the user hasn't confirmed exclusions. Recommend the fix proactively.
- **Fix:** Create a shared placement exclusion list. Standard exclusions: `mobileapps.google.com` categories, parked domains, "Below the fold" placements (Display only), and any vertical-specific irrelevant categories. Apply to all Display, Demand Gen, and PMax campaigns.

---

## Category 5 — Budgets & Spend

### 5.1 Search lost IS (budget) is acceptable
- **Checks:** "Search lost IS (budget)" tells you how much volume you're missing because of budget constraints — pure opportunity cost on profitable campaigns.
- **Pass:** Profitable campaigns have <10% Search lost IS (budget)
- **Warning:** 10–25% on profitable campaigns
- **Fail:** >25% on profitable campaigns OR any campaign with high lost-IS-budget AND a tCPA/tROAS hitting target
- **Data:** Campaigns paste — `Search lost IS (budget)` column.
- **Fix:** For each profitable campaign with high budget-lost IS, raise budget proportionally. Estimate uplift: `current conversions × (lost IS budget % / current IS %)`.

### 5.2 Budget pacing is healthy
- **Checks:** Are campaigns hitting daily caps consistently? Daily caps that limit are fine for capped budgets, but unintentional caps are silent revenue loss.
- **Pass:** No campaigns flagged as "Limited by budget" (unless intentional)
- **Warning:** Some campaigns limited but spend < 30% of total
- **Fail:** Material campaigns capped daily, with high lost IS (budget)
- **Data:** Campaigns paste (status messages) + Search lost IS (budget). With MCP: same data via `get_ppc_report`.
- **Fix:** Raise budgets on profitable campaigns; lower on the wasteful ones flagged elsewhere; consider portfolio bid strategies with shared budgets.

### 5.3 Shared budget hygiene
- **Checks:** Shared budgets across mixed-performance campaigns drag everything to the lowest common denominator.
- **Pass:** Shared budgets only across similar-performance campaigns
- **Warning:** Some shared budgets across mismatched campaigns
- **Fail:** Single shared budget covering 5+ campaigns of varying performance
- **Data:** Campaigns paste (Budget column — same budget value across multiple campaigns).
- **Fix:** Split shared budgets along performance lines; group only campaigns with similar tCPA/tROAS targets.

---

## Category 6 — Bidding

### 6.1 Bid strategy aligns with stated goal
- **Checks:** tCPA/Maximize Conversions for lead-gen; tROAS/Maximize Conversion Value for e-commerce. Manual CPC in 2026 is rarely justifiable.
- **Pass:** All material campaigns on a Smart Bidding strategy aligned to goal type
- **Warning:** Some material campaigns on Manual CPC or Maximize Clicks
- **Fail:** Most material campaigns on Manual CPC, Maximize Clicks, or Enhanced CPC (eCPC is being deprecated)
- **Data:** Campaigns paste — `Bid strategy type` column, weighted by Cost.
- **Fix:** Migrate to Smart Bidding aligned to goal. For accounts with strong conversion data, target tCPA or tROAS; for accounts still building data, Maximize Conversions.

### 6.2 ECPC deprecation flag
- **Checks:** Enhanced CPC is being deprecated by Google. Accounts still using it need to migrate.
- **Pass:** No campaigns on eCPC
- **Warning:** A few campaigns on eCPC (low spend share)
- **Fail:** Material spend on eCPC
- **Data:** Campaigns paste — `Bid strategy type = Enhanced CPC`.
- **Fix:** Migrate to a Smart Bidding strategy. For low-conversion campaigns, Maximize Conversions; for high-conversion, tCPA.

### 6.3 Smart Bidding learning periods are not getting interrupted
- **Checks:** Frequent budget/bid/structural changes restart the learning period (~7-14 days), wasting spend on calibration.
- **Pass:** No major bidding changes in last 30 days; campaigns past learning
- **Warning:** Some recent changes; learning still active on a few campaigns
- **Fail:** Repeated mid-period changes; learning interrupted multiple times
- **Data:** Requires Change History — ask user OR use MCP `ChangeHistory` report (this is a Tier-2 MCP unlock).
- **Fix:** Hold structural changes for 14 days post-launch; batch changes into windows; use Drafts & Experiments to test instead of editing live.

---

## Category 7 — Targeting

### 7.1 Location targeting is set to "Presence" (not "Presence or interest")
- **Checks:** Default "Presence or interest" includes anyone *interested in* your target location — including users from far away. Almost always leaks budget.
- **Pass:** All campaigns set to "Presence: People in or regularly in your locations"
- **Warning:** Some on "Presence or interest"
- **Fail:** Most or all on the default "Presence or interest"
- **Data:** Not in Campaigns paste — ask user OR check the geographic locations report (advanced). With MCP: check via account settings if exposed.
- **Fix:** For each campaign, edit Locations → Location options → choose "Presence" only. Re-evaluate after 14 days.

### 7.2 Ad scheduling reflects business hours where it matters *(sharpened v0.1.2)*
- **Checks:** For lead-gen accounts where calls/forms are answered only in business hours, after-hours spend with no follow-up is waste. For local service accounts, off-hours dayparts often have very different intent and conversion rates than business hours. The default of "always on, no adjustments" is rarely optimal.
- **Pass:** Schedule reflects business hours OR is intentionally 24/7 with documented reason; bid adjustments for off-hours are calibrated (typically -30% to -100% for low-conversion hours).
- **Warning:** Schedule exists but is the same on every campaign (no segmentation between e-com and lead-gen sub-campaigns) OR no bid adjustments applied to a meaningful schedule.
- **Fail (lead-gen):** **No ad schedule configured on any campaign in a lead-gen account.** Off-hours leads that go to voicemail or unwatched forms have a fraction of the conversion rate of business-hours leads — running 24/7 wastes budget on the worst-converting times.
- **Fail (general):** Schedule is 24/7 with no bid adjustments, AND change history shows no recent dayparting work.
- **Data:** Not in CampaignPerformance MCP response — ask user OR check ChangeHistory for schedule-related changes (`Change Type=AdSchedule` or similar). For paste mode: typically requires user input.
- **MCP-mode fallback:** If `ChangeHistory` shows zero ad-schedule changes ever AND account is lead-gen, treat as FAIL with the explicit recommendation to add at minimum a -50% bid adjustment for 12am–5am as a starting point.
- **Fix:** Add ad schedule with bid adjustments for after-hours. For lead-gen with phone-answered conversions: -100% (off) for non-business hours. For lead-gen with web forms: -50% for low-intent hours, retest after 30 days. For e-commerce: typically leave 24/7 unless conversion rate clearly drops at specific hours.

### 7.3 Device bid adjustments aren't masking systemic issues
- **Checks:** Aggressive device adjustments (e.g., -100% mobile, +50% desktop) often mask landing page or conversion-tracking issues rather than real performance differences.
- **Pass:** Device adjustments are modest (±20%) and based on actual device-level conv rate data
- **Warning:** One device class adjusted by ±50%
- **Fail:** Device adjusted by -100% (excluded entirely) or +/- huge values without conversion data to support it
- **Data:** Ask user OR check device-segmentation report. With MCP: limited.
- **Fix:** Reset extreme device adjustments. If mobile genuinely underperforms, fix the mobile landing page first, then re-evaluate.

---

## Category 8 — Audiences

### 8.1 Customer Match list uploaded
- **Checks:** Customer Match (uploading hashed customer lists) unlocks remarketing, Smart Bidding signal richness, and PMax audience signals. Free, high-impact, often skipped.
- **Pass:** Active Customer Match list ≥1000 hashed records, refreshed in last 90 days
- **Warning:** List exists but stale (>90 days) or small (<1000 records)
- **Fail:** No Customer Match list
- **Data:** Ask user. With MCP: limited.
- **Fix:** Export your customer list from your CRM, hash via Google Ads upload, refresh quarterly. Use as audience signal in PMax + observation/exclusion in Search.

### 8.2 Remarketing audiences in observation mode (not targeting)
- **Checks:** Observation mode lets Smart Bidding *use* the audience as a signal without restricting reach. Targeting mode restricts reach to that audience only — usually wrong for Search.
- **Pass:** Audiences attached in Observation mode across Search campaigns
- **Warning:** Mix of targeting and observation
- **Fail:** No audiences attached to Search campaigns
- **Data:** Ask user OR check audience tab. With MCP: limited.
- **Fix:** Add remarketing, in-market, and Customer Match audiences in Observation mode to Search campaigns. Don't restrict reach unless the campaign is specifically remarketing-only.

### 8.3 Exclusion audiences applied where appropriate
- **Checks:** Lead-gen accounts should exclude existing customers from prospecting campaigns; e-commerce accounts may exclude past 30-day converters from acquisition campaigns.
- **Pass:** Exclusions applied to relevant campaigns
- **Warning:** Some exclusions but inconsistent
- **Fail:** No exclusion audiences applied; spending on existing customers in prospecting
- **Data:** Ask user.
- **Fix:** Build "Existing Customers" audience (Customer Match list); apply as exclusion to acquisition/prospecting campaigns.

---

## Category 9 — Keywords

### 9.1 Keyword cannibalization
- **Checks:** Same keyword text + match type appearing in 2+ ad groups means they bid against each other; CPCs inflate, Quality Score splits.
- **Pass:** No high-spend keyword cannibalization (same kw text + match type with combined spend >1% of account in multiple ad groups)
- **Warning:** Minor cannibalization on low-spend keywords
- **Fail:** Material cannibalization on high-spend keywords
- **Data:** Keywords paste — group by `keyword + match type`, count distinct ad groups.
- **Fix:** For each cannibalized keyword: consolidate into the higher-Quality-Score ad group; pause or negative-out the duplicates.

### 9.2 Match type strategy reflects 2026 best practice
- **Checks:** In 2026, Broad Match + Smart Bidding is Google's recommended default. Pure Exact-only with Manual CPC is dated. Mixed strategy (Broad + Phrase + Exact) is fine but should be intentional.
- **Pass:** Strategy is intentional — either Broad-Match-w/-Smart-Bidding-dominant, or a deliberate Exact/Phrase emphasis with strong negative discipline
- **Warning:** Heavy Broad Match without Smart Bidding (high waste risk); or 100% Exact with no Broad/Phrase exploration
- **Fail:** Broad Match running with Manual CPC (high waste); or zero Broad Match with stagnant volume on Smart Bidding accounts
- **Data:** Keywords paste — distribution of match types weighted by spend, cross-referenced with Campaigns paste's bid strategy.
- **Fix:** If Broad with Manual CPC: switch to Smart Bidding before expanding Broad. If Exact-only with stagnant volume: introduce Phrase/Broad in a controlled experiment.

### 9.3 Zero-impression / paused-but-active keywords cleanup
- **Checks:** Keywords with 0 impressions in 30 days are clutter; they don't hurt but they hide signal. Disapproved keywords actively hurt Quality Score.
- **Pass:** <5% of enabled keywords have 0 impressions in 30 days; 0 disapproved
- **Warning:** 5–15% zero-impression; few disapproved
- **Fail:** >15% zero-impression OR any disapproved keywords still enabled
- **Data:** Keywords paste — count `Impressions = 0` and `Status = Disapproved`.
- **Fix:** Pause zero-impression keywords (or delete); fix or remove disapproved keywords (usually trademark or policy issues).

---

## Category 10 — Quality Score ⭐ (Optmyzr's signature)

> **MCP-mode note:** As of MCP v0.1, `get_ppc_report` does not return Quality Score columns. When in MCP mode and the user opts for "full depth," paste-fill the Keywords export (paste #2 in `reports.md`). When the user opts for "fast," use the **MCP-mode fallback** described per signal below — it provides a directional read on QS health without the actual scores. Either way, this category produces a real signal, never N/A.

### 10.1 Account-weighted average Quality Score
- **Checks:** The single most-cited PPC metric, but only meaningful when **weighted by spend**. A QS-3 keyword burning $5k/mo matters more than 100 QS-10 keywords burning $5/mo.
- **Pass:** Spend-weighted average QS ≥7
- **Warning:** Spend-weighted average QS 5–6
- **Fail:** Spend-weighted average QS <5
- **Data:** Keywords paste — compute `SUM(Cost × QS) / SUM(Cost)` across all enabled keywords with QS values.
- **MCP-mode fallback:** Without QS columns, infer from CTR + CPC outliers. Compute spend-weighted CTR; compare to vertical avg from `get_industry_insights`. Keywords whose CTR is in the bottom 25% of the account AND whose CPC is materially above account median → likely low-QS proxy. Report as "Inferred QS health: warning" with a clear note: *"Direct QS not available in MCP. Paste-fill the Keywords report for the actual score."*
- **Fix:** Identify the 10 highest-spend keywords with the worst inferred QS proxy (low CTR + high CPC). For each, diagnose which QS component is likely failing (see 10.3) and target that.

### 10.2 Low-QS spend share
- **Checks:** What % of total spend is going to keywords with QS ≤4? Every dollar there pays a CPC penalty (often +30-50% vs. higher-QS competitors).
- **Pass:** <10% of spend on QS ≤4 keywords
- **Warning:** 10–25%
- **Fail:** >25%
- **Data:** Keywords paste — `SUM(Cost where QS ≤4) / SUM(Cost)`.
- **MCP-mode fallback:** Without QS, use CPC vs. vertical-median as a proxy. % of spend going to keywords with CPC >2× vertical-median CPC ≈ low-QS spend share proxy. Same thresholds, marked as "inferred." Always include the explicit caveat in the report.
- **Fix:** Top 10 low-QS / high-spend keywords get the most attention. Likely fixes: (a) move keyword to a tighter ad group with relevant ad copy → fixes Ad Relevance; (b) rewrite RSAs to include the keyword theme → fixes Expected CTR; (c) improve landing page with on-page keyword + speed + mobile → fixes LP Experience.

### 10.3 Quality Score component diagnosis (Expected CTR / Ad Relevance / LP Experience)
- **Checks:** QS is composed of three signals. The fix differs depending on which is "Below Average."
- **Pass:** All three components "Average" or "Above Average" on majority of spend
- **Warning:** One component "Below Average" on a few high-spend keywords
- **Fail:** ≥1 component "Below Average" on >20% of high-spend keywords
- **Data:** Keywords paste — the Expected CTR / Ad Relevance / Landing page experience columns.
- **MCP-mode fallback:** Components can be approximated:
  - **Expected CTR** proxy → keyword's CTR vs. account median CTR (low CTR with high impressions → likely "Below Average" Expected CTR)
  - **Ad Relevance** proxy → keyword text appearing literally in any of the RSA's headlines (from `AdPerformance` data). If keyword theme is absent from all RSAs in the ad group → likely "Below Average" Ad Relevance
  - **LP Experience** proxy → cannot be inferred without fetching the LP; mark as "not assessable in MCP-only mode; paste-fill or run a Landing Pages check"
- **Fix:** Group failures by component. **Below-Average Expected CTR** → improve ad copy, especially headlines, with the keyword. **Below-Average Ad Relevance** → tighter ad groups; the ad must obviously be about the keyword. **Below-Average LP Experience** → faster page, on-page keyword presence, mobile-friendly, content depth.

---

## Category 11 — Search Terms & Negatives

> **MCP-mode note:** As of MCP v0.1, `get_ppc_report` does not have a SearchTermPerformance option. When in MCP mode and the user opts for "full depth," paste-fill the Search Terms Report (paste #3 in `reports.md`). When the user opts for "fast," use the **MCP-mode fallback** described per signal below — keyword-level inference for wasted spend; less precise but always produces a real signal.

### 11.1 Wasted spend on irrelevant search terms
- **Checks:** Search terms with >$10 spend AND 0 conversions in 30 days are concrete leakage. The threshold scales with account size.
- **Pass:** <5% of total spend on zero-conv terms (with cost > threshold)
- **Warning:** 5–15%
- **Fail:** >15% — significant leak
- **Data:** Search Terms paste — `SUM(Cost where Conversions = 0 AND Cost > $10) / SUM(Cost)`.
- **MCP-mode fallback:** Use **keyword-level** zero-conv spend instead. From `PositiveKeywordPerformance`, compute `SUM(Cost where Conversions = 0 AND Cost > $10) / SUM(Cost)`. Report it as "Zero-conversion **keyword** spend share" with a note: *"For exact search-term-level wasted spend (and specific query examples for negatives), paste-fill the Search Terms Report."* This is directionally accurate but coarser — broad-match keywords often have many converting *terms* even if the keyword as a whole has 0 conv at the threshold.
- **Fix:** Surface the top 10 wasted-spend search terms (or keywords, in fallback mode) by cost. Cluster thematically (informational, job-seeker, competitor, free-intent, irrelevant). Recommend specific negatives — Exact Match `[term]` for one-off queries, Phrase Match `"theme"` for patterns. Never Broad Match negatives.

### 11.2 Lin-Rodnitzky ratio
- **Checks:** Single-number account-health metric: avg CPA across all search terms / avg CPA across converting search terms only.
- **Pass:** 1.5–2.0 (healthy)
- **Warning:** 2.0–3.0 (some inefficiency, prune negatives)
- **Fail:** >3.0 (significant inefficiency) OR <1.5 (potentially over-restricted; missing growth volume)
- **Data:** Search Terms paste — compute as described in `reports.md`.
- **MCP-mode fallback:** Compute keyword-level L-R proxy: avg CPA across all keywords / avg CPA across converting keywords only. Less granular but uses the same logic at one level up. Report as "Keyword-level L-R proxy" with the same threshold ranges. Note that broad-match-heavy accounts will see very different keyword-level vs term-level ratios — flag accordingly.
- **Fix:** If >3.0: aggressive negative-keyword work, especially on Broad and Phrase. If <1.5: consider testing additional Broad/Phrase volume; account may be over-pruned.

### 11.3 Negative keyword list coverage
- **Checks:** Are negative lists actively maintained? An account with only campaign-level negatives and no shared lists usually has gaps.
- **Pass:** ≥1 active shared negative list applied to all Search campaigns; recent additions visible in Search Terms paste
- **Warning:** Lists exist but applied to <50% of campaigns; or no recent additions in 30 days
- **Fail:** No shared negative lists; campaign-level negatives only
- **Data:** Search Terms paste — `Added/Excluded` column shows recent additions; ask user about shared lists.
- **MCP-mode fallback:** Cannot directly assess shared negative lists from MCP data. Inference: if `PositiveKeywordPerformance` shows broad-match keywords with high spend and zero conversions persisting across multiple weeks (use ChangeHistory for the time signal), it's a strong signal that negative-list work is not being done. Report as "Likely needs negative-list work — paste-fill Search Terms for specifics."
- **Fix:** Create themed shared negative lists (e.g., "Universal Junk", "Job Seekers", "Competitor Brand Names"); apply to all relevant Search campaigns.

---

## Category 12 — Ads / RSAs

### 12.1 Ad Strength distribution
- **Checks:** Ad Strength replaces some of QS's old role for ads. "Poor" or "Average" Ad Strength typically means missing assets, weak diversity, or excess pinning.
- **Pass:** ≥80% of active RSAs at "Good" or "Excellent"
- **Warning:** 60–80% Good/Excellent
- **Fail:** <60% Good/Excellent
- **Data:** Ads paste (4a) — `Ad strength` column.
- **Fix:** For each Poor/Average RSA: add headlines (target ≥8 unique), add descriptions (target ≥3), reduce pinning to absolutely-required positions only.

### 12.2 ≥3 active ads per ad group
- **Checks:** Google's testing engine works best with 3+ ads per ad group.
- **Pass:** ≥95% of active ad groups have ≥3 active ads
- **Warning:** 80–95%
- **Fail:** <80% — many ad groups running solo or duo
- **Data:** Ads paste (4a) — group by Ad group, count active ads.
- **Fix:** For ad groups with 1-2 ads, add an additional RSA variant (test different value props, CTAs, structure).

### 12.3 RSA asset count and pinning sanity *(sharpened v0.1.2)*
- **Checks:** Per RSA, count distinct headlines and descriptions; check pinning patterns. The threshold isn't just "any one ad is good" — it's the **median** RSA in the account. If most RSAs are under-spec'd, Google's testing engine has nothing to optimize against.
- **Pass:** Median active RSA has ≥10 headlines and ≥3 descriptions; pinning only on legally-required positions or critical brand mentions; <20% of RSAs in the account have <8 headlines.
- **Warning:** Median active RSA has 7–9 headlines and ≥3 descriptions; some over-pinning; 20–50% of RSAs have <8 headlines.
- **Fail:** Median active RSA has <7 headlines OR <3 descriptions; **OR ≥50% of active RSAs have <8 headlines** (Google's recommended floor); OR every position pinned in any active RSA.
- **Data:** AdPerformance — count Headlines / Descriptions per RSA (typically pipe- or semicolon-separated). Compute median across active RSAs. Pinning may require paste-fill.
- **MCP-mode fallback:** Same calculation; the median check works directly on AdPerformance data without needing QS columns.
- **Fix:** Identify all RSAs below 8 headlines / 3 descriptions. Add variations targeting different value props, CTAs, and search-intent angles. Refresh assets quarterly. Unpin everything except brand and legal positions.

### 12.4 Duplicate ad copy across ad groups *(added v0.1.2)*
- **Checks:** When the same headline string or description string appears in many ad groups, Google's Ad Relevance and Quality Score signals suffer — and Performance Max / RSA testing degenerates because the system has nothing to test. This is one of the highest-leverage hidden findings: it's invisible to scorecard-style audits but obvious from spend-weighted ad copy data.
- **Pass:** No single headline string or description string appears in more than 15% of active ads in the account.
- **Warning:** A single headline or description string appears in 15–40% of active ads (e.g. a generic brand tagline used in too many ad groups).
- **Fail:** **A single headline or description string appears in ≥40% of active ads.** Verified failure pattern: a directory-style account where "Comprehensive Local Directory" was the H1 in 82% of active ads, dragging Ad Relevance below average across the entire account.
- **Data:** AdPerformance — paginate to cover top-spend ads (50+ recommended). For each ad: split Headlines and Descriptions on their delimiter into individual strings. Aggregate counts of `(string → set of ad groups)`. Flag any string appearing in 15%+ of active ad groups.
- **MCP-mode fallback:** Direct calculation from AdPerformance. No paste-fill needed.
- **Fix:** Identify the top-3 most-repeated headlines and descriptions. Rewrite each ad group's primary RSA H1 to reflect that ad group's specific theme/keyword (e.g., "Whakatane Sports Clubs" not "Comprehensive Local Directory"). Use the ad group name or its top keyword as the basis for the H1. Refresh in batches of 10–20 ad groups to avoid disrupting the entire account at once.

### 12.5 Legacy ad types still serving *(added v0.1.2)*
- **Checks:** Expanded Text Ads (sunset 30 June 2022) and the older standard Text Ads (sunset 2018) continue to serve in some accounts long after their format is deprecated. They get fewer impressions, no Smart Bidding optimization, and are eventually retired entirely. Any active ETA or TextAd in 2026 is dead weight.
- **Pass:** Zero active ETAs and zero active TextAds in the account.
- **Warning:** 1–5 active ETAs across the account; no TextAds.
- **Fail:** ≥6 active ETAs OR any active TextAd; OR an entire ad group running ETA-only with no RSA fallback.
- **Data:** AdPerformance — `Ad Type` column. Count rows where `Ad Type` is `ExpandedTextAd` or `TextAd` and `Ad Status = Enabled`.
- **MCP-mode fallback:** Direct calculation from AdPerformance. No paste-fill needed.
- **Fix:** Pause all ETAs and TextAds in Google Ads Editor (filter by Ad Type, bulk-pause). Before pausing, verify each affected ad group has at least one active RSA — if not, create one first. ETAs that have been serving for years often have keyword-rich copy worth porting into the new RSA's headlines.

---

## Category 13 — Assets / Extensions

> **MCP-mode note:** As of MCP v0.1, the Optmyzr MCP does not expose asset/extension coverage data. When in MCP mode and the user opts for "full depth," paste-fill the Assets export (paste #4b in `reports.md`). When the user opts for "fast," use the **MCP-mode fallback** below — which is a directional check based on common gaps; less precise than the paste flow but still produces a real signal.

### 13.1 Sitelink coverage
- **Checks:** Sitelinks are free real estate. Campaigns without sitelinks get smaller, less compelling ads.
- **Pass:** Every active Search campaign has ≥4 sitelinks
- **Warning:** Some campaigns missing or have <4
- **Fail:** Most campaigns have no sitelinks
- **Data:** Assets paste (4b) — Asset type = Sitelink, count per campaign.
- **MCP-mode fallback:** Cannot directly count sitelinks via current MCP. Inference: if the account's CTR is below vertical median per `get_industry_insights`, it's likely (but not certain) that asset coverage is incomplete — flag as "Asset coverage likely incomplete; paste-fill Assets export or expand sitelinks across campaigns to confirm." Never report PASS in fallback mode (we can't confirm); cap at WARNING.
- **Fix:** Add 4+ sitelinks per campaign. Use either account-level sitelinks (broad reuse) or campaign-level (specific to message). Refresh quarterly.

### 13.2 Callout & structured snippet coverage
- **Checks:** Callouts (e.g., "Free Shipping", "24/7 Support") and structured snippets add detail without taking PPC space.
- **Pass:** ≥4 callouts and ≥1 structured snippet per active campaign
- **Warning:** Some coverage but inconsistent
- **Fail:** Few campaigns have either
- **Data:** Assets paste — Asset type = Callout / Structured snippet.
- **MCP-mode fallback:** Cannot directly assess. Default recommendation in fallback mode: "Verify ≥4 callouts and ≥1 structured snippet per active campaign; this is a near-universal gap. Paste-fill Assets export to confirm exact coverage."
- **Fix:** Add 4+ callouts (USPs, differentiators); add 1+ structured snippet (Services / Categories / Models).

### 13.3 Image, call, and other key assets present where applicable
- **Checks:** Image assets in Search ads, call assets for lead-gen, location for local. These are highly impactful and often overlooked.
- **Pass:** Image assets on Search campaigns; call asset on lead-gen accounts; location on local accounts
- **Warning:** Some present, inconsistent application
- **Fail:** Account is local/lead-gen and core assets missing
- **Data:** Assets paste + interview Q1 (account type).
- **MCP-mode fallback:** Cannot directly assess. Use interview answers to make targeted recommendations: lead-gen → "verify call asset + lead form asset are configured"; local → "verify location asset is configured"; e-commerce → "verify image assets are configured." Cap at WARNING. Cite the gap in the "what this audit can't see" section.
- **Fix:** Match asset types to account: e-commerce → image; lead-gen → call + lead form; local → location + call.

---

## Category 14 — Landing Pages

### 14.1 Landing page mobile friendliness & speed
- **Checks:** A slow or non-mobile-friendly LP destroys QS (LP Experience component) AND conversion rate. Critical signal.
- **Pass:** Top-spend LPs pass Google's Mobile-Friendly test and load in <2.5s on mobile
- **Warning:** Some pass, some fail; load times 2.5–4s
- **Fail:** Top-spend LPs fail mobile-friendly OR load >4s on mobile
- **Data:** Sample top 5 final URLs from Ads paste; the skill should fetch these (via WebFetch) and check load time + mobile responsiveness. With MCP: same approach but on a fuller URL list.
- **Fix:** Run PageSpeed Insights on each failing LP. Common fixes: image optimization, lazy load, defer JS, remove unused CSS. For mobile-friendliness: viewport meta tag, tap-target sizing, readable font sizes.

### 14.2 Message match between ad and landing page
- **Checks:** Does the LP's H1, hero copy, and CTA mirror the ad's promise? Mismatch tanks conversion rate AND LP Experience score.
- **Pass:** Top ads' headlines/promises clearly mirrored in LP H1 + hero
- **Warning:** Generic LP that doesn't reflect specific ad copy
- **Fail:** LP is homepage (no specific match) for non-brand campaigns
- **Data:** Sample 3-5 highest-spend ads and their final URLs; the skill fetches the LP and compares headlines.
- **Fix:** Build campaign-specific LPs; or at minimum, ensure the LP H1 echoes the ad's primary headline. For high-spend keywords, custom LPs.

### 14.3 Broken or redirected URLs
- **Checks:** Final URLs that 404, redirect to a different page, or return non-200 silently kill conversions.
- **Pass:** All sampled top-spend final URLs return 200 directly
- **Warning:** Some redirects (acceptable if intentional and same-domain)
- **Fail:** Any 404s, 5xx errors, or cross-domain redirects on top-spend ads
- **Data:** Sample top 10 final URLs from Ads paste; HEAD request each. With MCP: same plus URL-checker tool integration.
- **Fix:** Replace broken URLs immediately; for redirects, decide whether to update the ad to the destination URL.

---

## Cross-cutting note: Top 5 Findings

After evaluating all 14 categories, surface the **5 highest-impact findings** at the top of the report. Rank by:

- **Impact** (estimated $ wasted/month or opportunity lost/month)
- **Confidence** (how sure are we from the data)
- **Ease** (how quickly can the user fix it)

Each Top 5 finding should have:
- One-line headline
- Estimated $ impact/month
- Specific fix (1-2 sentences)
- Which category it came from (link to scorecard below)

This is the LinkedIn-shareable hero. Make it count.
