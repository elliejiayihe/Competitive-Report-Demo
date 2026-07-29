# Competitive-Report-Demo

## What this is
This is a **de-identified version** of a real competitive analysis report I built during my internship. It's meant to be shared in a portfolio, an interview, or with anyone outside the company — it demonstrates the analysis, methodology, and reporting approach without exposing any real brand, product, or company data.

**Nothing about the underlying work is fabricated.** Every number, percentage, trend, table, and conclusion is identical to the original report. Only the names have been swapped for fictional stand-ins, and all charts were rebuilt from scratch (same data, new labels) since the originals were static images with the real brand names baked in.


## What this demo shows

- Competitive spec-share analysis using Dodge Construction Central data (NEAR search syntax, CSI-style category crosswalks)
- Year-over-year methodology comparisons, including a real analytical judgment call (flagging when two years' search methods weren't apples-to-apples, so a stat couldn't be responsibly reported as "growth")
- Multi-cut analysis: by product category, by building/market type, by state, and by finish (matte black)
- Executive framing: a "What's Next" section that translates findings into recommended follow-ups, without overstepping into decisions that belong to leadership


**Data source and search mechanics**
- All spec counts come from Dodge Construction Central, a database of published construction project specifications (basis-of-design documents, not just bid awards).
- Each brand/collection was tracked using a `NEAR()` proximity search — e.g. `NEAR(("Solstice","Meridian"),10,true)` — which finds instances where the collection name and manufacturer name appear within 10 words of each other. This is more reliable than a plain keyword search because it filters out incidental mentions (e.g. a spec that happens to name-drop a manufacturer in an unrelated context).
- Each formula also OR's in the specific model/SKU numbers for that collection (e.g. `"M-9262" OR "M-9279" OR ...`), since specs frequently cite a model number without spelling out the collection name at all.

**Two-tier search design (and why it mattered)**
- The first pass for each brand was a single **combined formula**: collection name + manufacturer name (NEAR search) + the full list of model numbers, run as one search.
- On top of that, I layered **separate per-category searches** — Grab Bars, Hooks, Dispensers, and so on — each targeting the model numbers specific to that product line.
- This two-tier approach exists because the combined formula alone systematically undercounts: Trevino's per-category searches summed to 224 specs, more than double the 105 the combined collection formula returned on its own, because many specs cite a series code (like "9T1") without the collection name ("Trevino") appearing anywhere nearby. Skipping the per-category layer would have made Trevino's real market presence look less than half of what it is — and the same undercounting pattern held for Solstice and Castellan.

**The core analytical judgment call: separating real growth from measurement artifacts**
This is the part I was most careful about. When comparing this year's call-out to the 2024–2025 call-out, some collections showed big jumps — but not all of them meant the same thing:
- **Solstice (+44%) and NOIR (+15%)** used the *identical* search formula both years, just with a longer, more complete model-number list. Growth here is real and like-for-like.
- **Castellan (0 → 34) and VSI Matte Black (14 → 48)** looked like dramatic growth, but the increase was entirely explained by *new SKU codes added to the search this year that weren't searched for last year* — the name-only, apples-to-apples portion of each formula was flat (0 and 14, respectively) in both periods.
- I flagged this distinction explicitly rather than letting the raw percentage change stand on its own, because reporting "Castellan grew from 0 to 34" or "VSI's share tripled" without that context would have been a measurement-method artifact dressed up as a market trend — the kind of mistake that leads to bad strategic calls downstream.

**Cross-checking conclusions across multiple cuts**
Rather than relying on one summary stat, each finding was checked against at least two independent breakdowns before being stated as a conclusion:
- The product-category leadership claims (e.g. "Solstice leads in 6 of 8 comparable categories") were verified against both raw spec counts *and* market-share percentages, to make sure a small-sample category wasn't distorting the picture.
- The "Trevino's real strength is Sanitary Disposal" conclusion was checked at the building-type level too — confirming Trevino led in *every* building segment for that category, not just in aggregate, which rules out the possibility that one unusual project was driving the whole number.
- Where data was too thin to be meaningful (e.g. categories with n/a or zero on one side), those rows were called out separately as "not chart-worthy" rather than folded into charts where they'd visually overstate confidence.

**Explaining anomalies before drawing conclusions from them**
Where a number looked surprising, I looked for a structural explanation before treating it as a competitive signal — e.g. Solstice's zero specs in the Soap Dispenser/Faucet category was flagged as most likely a product-launch timing lag (specs take a few months to show up in Dodge after a new line ships), not evidence of competitive weakness, with a specific recommended re-check date (Q4 2026/Q1 2027) rather than a permanent conclusion.

