---
name: unit-cma-lite
description: Free-data apartment/unit due-diligence pipeline for Australian property (NSW-optimised). Give it a realestate.com.au / Domain listing URL or an address, and it runs a buyer-side CMA using only free public sources — listing facts, comparable sales, official land values, suburb fundamentals, market trends — and outputs a structured HTML report. Trigger with /unit-cma-lite, "research this unit", "is this apartment worth it", "帮我尽调这个公寓". Methodology by Shuai Luo (licensed buyer's agent, Avocado Wealth).
---

# /unit-cma-lite — Free-Data Unit CMA Pipeline

A buyer's-agent-grade due-diligence workflow for apartments/units, using **only free, public data**. Built from the professional six-source pipeline used at [Avocado Wealth](https://avocadowealth.com.au) — this Lite version swaps paid subscriptions (CoreLogic, HtAG, Stash, SuburbsFinder) for free equivalents and honestly flags what it cannot see.

## Core principles (the methodology — read before running)

1. **Price is what the market accepts.** The vendor's purchase price and renovation spend NEVER enter your valuation anchor — they are negotiation-psychology intel only. Your floor anchor = the property's OWN last sale, indexed to today by suburb trend.
2. **Same-building data beats next-door beats suburb.** Build two axes: vertical (this building's sale history, other units in it) and horizontal (same-period sales in comparable buildings). A 3-year-old sale in the same building can beat a fresh sale next door.
3. **Land content is the growth engine.** Whole-block official land value × this unit's share ≈ land content. High land content (>30% of price) + low density (≤30 units) = preferred. Land value rising while unit prices tread water = a mispricing worth catching.
4. **The value-for-money rule.** A typical 2-bed unit should cost ≤ 1/2 the local house median (ideally 1/3–1/4). Above 50% = overpriced. 3-bed units benchmark against 4–5-bed houses. In trophy suburbs use the same-bedroom-count house median instead.
5. **Qualitative reads only.** Describe trends (tightening / softening / buyers waiting / stalemate). Do not invent quantitative advice numbers.
6. **The only deal-killer is flood.** Everything else converts into a price adjustment, not a walk-away.

## Free source map

| Need | Free source | Notes |
|---|---|---|
| Listing facts, comps, history | realestate.com.au / Domain public pages | Sold search (same config, last 6 mo); the property archive page (`/property/unit-X-...`) holds sale/rental history AND photo archives from past campaigns (before/after renovation gold) |
| Official land value | NSW Valuer General, SIX Maps Valuation layer | `https://maps.six.nsw.gov.au/arcgis/rest/services/public/Valuation/MapServer/5/query` — query `address LIKE '<NO> <STREET ABBREV>, <SUBURB>%'` (uppercase). 5-year series per parent block. Free, no login. Other states: QLD (qld.gov.au land valuations), VIC (land.vic.gov.au) |
| Suburb fundamentals | AreaSearch (areasearch.com.au/suburb/...) | Free without login: repeat-sale appreciation %, official bond-board median rents + YoY, infrastructure pipeline, demographics, building approvals |
| Market trends | SQM Research free charts (sqmresearch.com.au) | Vacancy, days-on-market, asking prices by postcode — free chart pages |
| Suburb medians | REA suburb profile (`realestate.com.au/nsw/<suburb>-<postcode>/`) | Medians by bedroom count, DoM, yield — needed for the value-for-money rule |
| Demographics / social-housing proxy | ABS QuickStats (abs.gov.au/census) | Tenure mix; "state housing authority landlord" share ≈ social housing proxy |
| Environment scan | OpenStreetMap Overpass API | Power lines, rail, arterials near the address |
| Geocoding | Listing page embeds property-level lat/lng; else ArcGIS World Geocoder | For the comps map |

## Pipeline

1. **Listing facts**: guide price, spec, strata levies, description claims. Cross-check car space across listing text vs archive records — disagreement = red flag, measure on inspection.
2. **Property archive**: full sale + rental history. Compute the **floor anchor**: last sale × suburb index since. If listed a while, note days on market vs suburb median = your negotiation-leverage gauge.
3. **Land content**: VG land value (5-yr series) for the parent block ÷ number of units (or × entitlement if known from the contract). Report land content as % of asking price, and the block's 5-yr land trend.
4. **Five-tier comps** (last 6 months, same bedroom count): floor (original-condition sales + own-sale-indexed) / peer / ceiling (renovated + parking) / upgrade tier / premium. Each row: photo thumbnail, distance, condition read (original / partly updated / fully renovated — judged from each campaign's description and photos), link. Plot on a Leaflet map, colour-coded by tier.
5. **Same-angle photo pairs**: for renovated listings, pull past-campaign photos from the archive gallery and pair same-room-same-aspect before/after. Label honestly when an angle is missing.
6. **Market context**: SQM charts + REA suburb stats + AreaSearch repeat-sale rate and bond rents. Qualitative reads only. Flag pipeline projects (AreaSearch) that add supply or amenity.
7. **Value-for-money check**: price vs house median per rule 4.
8. **Report**: single HTML file — one-sentence verdict (falsifiable), building profile, land value card, before/after pairs, pricing (own price chain + comps), comps map + table, market context, red flags + inspection checklist. **Every card ends with its sources (platform + basis + date).** Mark estimates as estimates.

## Honest limitations vs the professional version

No automated valuation models (use the own-sale-indexed anchor + comps instead) · no year-built/entitlement records (ask the agent; read the contract) · no street-level social-housing or road-noise grading (use ABS proxy + Street View + your ears) · no campaign-history detail (ask the agent how long it's really been listed and what offers lapsed).

A licensed buyer's agent runs this same methodology with paid data (CoreLogic, HtAG, Stash, SuburbsFinder) and negotiates for you. This Lite version exists so you can make safer decisions on your own — that philosophy is the point.

— Methodology: Shuai Luo, licensed buyer's agent, [Avocado Wealth](https://avocadowealth.com.au) · Engineering: Claude
