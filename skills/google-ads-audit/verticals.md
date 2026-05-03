# Industry verticals reference list

The Optmyzr MCP's `get_industry_insights` accepts a `vertical_name` parameter and silently maps it to "the closest supported vertical." If the input doesn't match anything close, it can return a wildly wrong vertical without warning (e.g., "Non-Profit" → "Sports:Outdoor Sport" because of an account targeting bicycles).

This file is a **curated working list** of vertical names commonly accepted by Optmyzr's industry benchmarks. Use it as the canonical reference when:

1. **Calling `get_industry_insights`** — pick the most accurate vertical from this list rather than free-typing.
2. **Surfacing options to the user** — when the resolved vertical doesn't match what was sent (poor resolution), present this list and ask the user to choose.

> ⚠️ This list is hardcoded based on common industry categorizations and verified Optmyzr resolutions. It may go stale. Track Jira **AI-493** for adding a `list_industry_verticals` MCP endpoint that exposes the canonical list directly. When that ships, replace this file with a runtime call.

---

## Common verticals

### Retail & Commerce
- E-Commerce (general)
- Retail
- Apparel & Fashion
- Beauty & Personal Care
- Consumer Electronics
- Home & Garden
- Food & Drink
- Office & Business Supplies

### Services & B2B
- B2B / Software (SaaS)
- Technology
- Internet & Telecom
- Industrial
- Marketing & Advertising
- Consulting & Professional Services

### Finance & Insurance
- Finance
- Insurance
- Banking
- Investment & Trading

### Health & Wellness
- Health & Medical
- Pharmacy
- Fitness & Wellness
- Dental
- Mental Health

### Education
- Education
- Higher Education
- K-12
- Online Courses
- Language Learning

### Legal & Government
- Law & Legal
- Government & Public Services

### Real Estate & Construction
- Real Estate
- Construction
- Architecture & Design
- Property Management

### Travel & Hospitality
- Travel & Tourism
- Hospitality
- Restaurants
- Airlines

### Automotive
- Auto (Sales)
- Auto Services & Repair
- Auto Parts

### Sports & Recreation
- Sports & Outdoor Sport
- Recreation & Leisure
- Outdoor Adventure

### Career & Workforce
- Career & Employment / Jobs
- Recruiting
- HR & Workforce

### Charity & Non-Profit
- Charity & Non-Profit
- Religious Organizations
- Advocacy & Public Interest

### Entertainment & Media
- Entertainment
- Media & Publishing
- Gaming
- Streaming Services

### Dating & Personals
- Dating & Personals

### Other
- Other / Miscellaneous

---

## How the skill uses this list

In `SKILL.md` Step 3b.4 ("Vertical selection for industry benchmarks"):

1. **First inference** — try to guess the right vertical from the account name, domain, and the user's stated goal. Pick from the list above.
2. **First call** to `get_industry_insights(vertical_name=<your guess>)`.
3. **Inspect response** — does the resolved vertical share a meaningful substring with what you sent?
   - "Charity & Non-Profit" → "Charity & Non-Profit": ✅ good match
   - "Charity & Non-Profit" → "Sports:Outdoor Sport": ❌ poor match — needs user input
4. **On poor match** — show the user this list (collapsed by group) and ask them to pick.
5. **Re-call** with their choice.
6. **Always tell the user** which vertical was used in the report header.

## Worth-flagging response patterns

If `get_industry_insights` returns:

- A vertical with `"Sports:..."` for a non-sports account — likely a "bike/equipment/outdoor" mis-match
- A vertical with `"Travel..."` for a non-travel account — likely a "destination/trip/booking" mis-match
- A vertical wildly different from any reasonable category for the account's keyword profile

…then surface the list and ask the user. Don't trust the silent resolution.
