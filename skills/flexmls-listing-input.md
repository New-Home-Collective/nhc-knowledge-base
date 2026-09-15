# FlexMLS Listing Input & Audit Skill: Instructions

This file holds the actual how-to for the flexmls-listing-input skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

---

**Before writing anything, read these three files live:**

Brand voice and identity facts: brands/nhc/BRAND-VOICE.md
Writing rules: company/writing-rules.md
Fair housing rules, mandatory every time: company/compliance.md

They hold the official NHC voice, identity facts, writing rules, fair housing
rules, brand colors, and approved social proof.

Read them live through the NHC Knowledge Base connector. Call its get_file
tool with the repo-relative path shown. There is no public web address for
these files.

If the connector is not enabled in this conversation, ask the person to turn
it on from the connectors menu, then try again. If it is enabled and a read
still fails, tell the person which file failed and stop. Do not write from
memory.

This skill does two things:
1. **Input mode** — gather all required information from the agent before they sit down at flexMLS
2. **Audit mode** — review a listing already in progress and flag anything incomplete, inconsistent, or likely to block publishing

Both modes end with the same output: a **Listing Input Summary** organized by flexMLS section.

---

## How to Start

When this skill is triggered, ask the agent:

> "Are we filling out a new listing from scratch, or double-checking one that's already entered?"

- **New listing** → work through the intake questions section by section
- **Audit / double-check** → ask the agent to share what they have (or pull from Drive/prior conversation), then compare against the required fields below and flag gaps

Either way, do not guess or fill in fields the agent hasn't confirmed. Flag unknowns clearly.

---

## Intake Order

Work through sections in this order — it matches the flexMLS left nav top to bottom.

For each section, ask only for what's missing. If the agent has already shared information that answers a field (address, beds/baths, school district, etc.), use it — don't re-ask.

---

## Section 1 — Listing Information

**Gather:**
- Listing agent name (must be active MLS member)
- Co-listing agent name (optional)
- Property type (almost always Residential)
- Property sub type: Single Family Residence / Condo / Townhouse / Multi-Family / Land / Other

**Flag if:**
- No listing agent confirmed

---

## Section 2 — Address

**Gather:**
- Street number (e.g. 103)
- Street name — name only, no suffix (e.g. "Boreing" not "Boreing Drive")
- Street suffix (Drive, Lane, Court, Road, Way, etc.)
- Street direction prefix (N/S/E/W — only if part of the address)
- Unit number (condos/apartments only)
- County
- City
- ZIP code

**Flag if:**
- Street name and suffix are combined — they are separate fields in flexMLS
- County or ZIP is missing

> **Tip:** The Google Address Search bar at the top of the Address section can auto-fill — but always verify Street Name vs. Street Suffix are split correctly after auto-fill.

---

## Section 3 — Tax & Legal

**Gather:**
- Subdivision name (use "City Limits" if no subdivision; HOA name if applicable)
- Parcel number (from county PVA)
- Tax rate (numeric, e.g. 8.56 — from county records)
- Elementary school
- Middle/junior school
- High school
- High school district
- Property condition: New Construction or To Be Built? (only check if applicable — leave blank for existing homes)
- Design Review District YN (Yes/No — most listings: No)

**Flag if:**
- Parcel number or tax rate unknown — direct agent to county PVA
  - Laurel County: https://laurelpva.com
  - Fayette County: https://fayettepva.com
  - Other counties: https://qpublic.net/ky/kypvas/
- Any school field is blank

---

## Section 4 — Contract

**Gather:**
- List price
- Listing contract date (date the listing agreement was signed)
- Expiration date (when the listing agreement expires)
- Status: Active / Coming Soon / Active Under Contract
- If Coming Soon: Start Showing Date
- Possession: At Closing / Negotiable / Day of Closing / Other
- Terms accepted: Conventional / Cash / FHA / VA / USDA / Other (can select multiple)
- Buyer agency compensation (amount or %)
- Office Exclusive YN (Yes = listing will NOT appear on Zillow, Realtor.com, or any third-party sites — confirm intentional)
- Seller contributions YN
- Dual/variable rate commission YN
- Special listing conditions: None / REO/Foreclosure / Short Sale / Estate / etc.

**Flag if:**
- Coming Soon: Start Showing Date is the same as Listing Contract Date — not allowed
- Coming Soon: Start Showing Date is more than 14 days out — not allowed
- Office Exclusive = Yes and agent may not have intended that
- Buyer agency compensation is blank
- List price is missing

---

## Section 5 — Showings

**Gather:**
- Occupant type: Occupied / Vacant / Owner Occupied / Tenant Occupied
- Showing requirements (select all that apply):
  CBS Code / Call Listing Agent / Call Listing Office / Call Manager / Call Owner /
  Call Tenant / Key In Office / Leave Message and Show / Listing Agent Must Accompany /
  No Sign / Restricted Hours / Show Anytime / Showing Service / Other
- Lockbox location (where the lockbox is physically placed)
- Showing contact name and phone
- Showing considerations (optional, check if applicable):
  Electricity Not On / Inconsistent Cell Service / Limited Visibility From Road /
  Minimal Exterior Lighting / Minimal Interior Lighting / No Exterior Lighting /
  No Heat / No Interior Lighting / No Interior Lighting / Pet(s) on Premises /
  Remote Location

**Flag if:**
- No showing requirement selected (at least 1 required)
- Occupied but no showing contact provided

---

## Section 6 — Association / Community

**Gather:**
- Association YN (Yes or No)
- If Yes:
  - Association name
  - Fee amount
  - Fee frequency (Monthly / Annual / etc.)
  - What the fee includes (lawn, trash, pool, exterior maintenance, etc.)
  - Community features (Pool, Clubhouse, Tennis Courts, Gated, etc.)

**Flag if:**
- Association YN = Yes but HOA documents have not been uploaded to the Documents tab

---

## Section 7 — Interior

**Gather:**
- Bedrooms total
- Bathrooms full (toilet + sink + shower or tub)
- Bathrooms half (toilet + sink only)
- Above grade finished area (sq ft)
- Below grade finished area (0 if none)
- Above grade unfinished area (0 if none)
- Below grade unfinished area (crawl space / unfinished basement — 0 if none)
- Living area source: Public Records / Appraiser / Owner / Estimated
- Fireplace YN — if Yes: type (Wood Burning, Gas, Electric, etc.)
- Interior features (check all that apply):
  Ceiling Fan(s) / Walk-In Closet(s) / Eat-In Kitchen / Breakfast Bar /
  Entrance Foyer / In-Law Floorplan / Primary First Floor / Soaking Tub /
  Wet Bar / Central Vacuum / Elevator / Other
- Appliances included (check all that apply):
  Dishwasher / Range / Microwave / Refrigerator / Washer / Dryer /
  Disposal / Double Oven / Gas Range / Cooktop / Trash Compactor /
  Vented Exhaust Fan / Self Cleaning Oven / Other / None
- Flooring types (Hardwood / LVP / Carpet / Tile / etc.)
- Basement: Yes/No — if Yes: Full / Partial / Crawl / Walk-Out / Finished / Unfinished
- Cooling: Central Air / Window Unit(s) / None / Other
- Heating: Forced Air / Heat Pump / Electric / Natural Gas / Propane / Other

**Flag if:**
- Sq ft doesn't match what's in public records (note discrepancy — agent should choose the correct source)
- Bathrooms Full + Half don't add up to the total stated (e.g. "3 baths" but only 2 full + 0 half entered)

---

## Section 8 — Parking Information

**Gather:**
- Garage YN (Yes or No)
- If Yes: number of garage spaces, attached or detached
- Carport YN — if Yes: number of spaces
- Parking features: Garage / Carport / Driveway / Off Street / On Street / None / Other

**Flag if:**
- No parking feature selected

---

## Section 9 — Building

**Gather:**
- Year built
- Year built source: Public Records / Appraiser / Owner / Estimated
- Architectural style: Ranch / Two Story / Colonial / Cape Cod / Split-Level / Craftsman / Other
- Construction materials: Brick / Vinyl Siding / Wood Frame / Stone / Fiber Cement / Other
- Foundation: Crawl Space / Slab / Block / Poured Concrete / Other
- Roof type: Shingle / Metal / Rubber / Other
- Number of stories

**Flag if:**
- Year built is unknown — required field; pull from PVA if needed
- Year built is before 1978 — **Lead-Based Paint Disclosure required** in Documents tab

---

## Section 10 — Lot

**Gather:**
- Lot size (numeric)
- Lot size unit: Acres or Square Feet
- Lot size source: Public Records / Appraiser / Owner / Estimated
- Lot features: Corner Lot / Wooded / Level / Sloped / Cul-De-Sac / Flood Zone / Other
- Fencing: Yes/No — if Yes: type (Privacy, Chain Link, Wood, etc.)
- Other structures on property (storage building, barn, workshop, etc.)
- Pool YN — if Yes: In Ground / Above Ground / Community

**Flag if:**
- Lot size missing — pull from PVA if needed

---

## Section 11 — Utilities

**Gather:**
- Sewer: Public Sewer / Septic Tank / None
- Water source: Public / Well / Other
- Electric: On Property / Underground / Overhead Utilities
- Gas: Natural Gas / Propane / None
- Internet/DSL availability (optional — note if known)

---

## Section 12 — Remarks

**Gather:**
- Public Remarks (MLS marketing copy — syndicated to Zillow, Realtor.com, etc.)
- Private Remarks (agent-to-agent notes — NOT syndicated; use for showing instructions, lockbox details, offer submission info)
- Driving directions (from a major road — optional but helpful)

**Flag if:**
- Public Remarks are missing — this field shows a red error badge ("1") in the nav and will block publishing
- Public Remarks contain: contact info, URLs, fair housing-sensitive language, or agent name/brokerage (not allowed on most MLS systems)
- Public Remarks exceed ~1,000 characters

> **Tip:** If the agent doesn't have Public Remarks yet, offer to draft them using the listingcraft-residential-content skill.

---

## Section 13 — Rooms (optional)

Recommended but not required. If the agent wants to include room dimensions:

- Room type (Living Room, Kitchen, Primary Bedroom, etc.)
- Level (Main, Upper, Lower, Basement)
- Approximate dimensions (length x width)

---

## Media Checklist

### Photos
- [ ] Photos uploaded in the Photos tab
- [ ] Minimum recommended: 25 photos
- [ ] Photos are in the correct display order
- [ ] No text overlays, logos, or watermarks on MLS photos

> **Tip:** If photos need to be organized or renamed, use the listing-photo-organizer skill first.

### Documents
| Document | Required When |
|---|---|
| Seller's Disclosure | Always — required before publishing |
| Lead-Based Paint Disclosure | Home built **before 1978** |
| HOA Documents | Association YN = Yes |

---

## Pre-Publish Audit Checklist

Run through this before clicking Publish Listing:

- [ ] All left nav sections show a green checkmark
- [ ] No red error badges (Remarks "1" is the most common)
- [ ] List price entered
- [ ] Status is correct (Active vs. Coming Soon)
- [ ] Coming Soon: Start Showing Date is set, not same as contract date, within 14 days
- [ ] Buyer agency compensation entered
- [ ] Parcel number verified
- [ ] Tax rate entered
- [ ] All 4 school fields complete
- [ ] At least 1 photo uploaded
- [ ] Seller's Disclosure in Documents tab
- [ ] Lead-Based Paint Disclosure uploaded if pre-1978
- [ ] HOA docs uploaded if Association YN = Yes
- [ ] Public Remarks complete and clean (no contact info, no agent name)
- [ ] Private Remarks include showing instructions and lockbox details

---

## Listing Input Summary Output Format

Once all fields are gathered and verified, produce a summary in this format:

---

### LISTING INPUT SUMMARY — [Address]

**LISTING INFORMATION**
- Property Type: [value]
- Sub Type: [value]
- Listing Agent: [name]
- Co-Listing Agent: [name or N/A]

**ADDRESS**
- Street Number: [value]
- Street Name: [value]
- Street Suffix: [value]
- City / County / ZIP: [value]

**TAX & LEGAL**
- Subdivision: [value]
- Parcel #: [value]
- Tax Rate: [value]
- Schools: [Elementary] / [Middle] / [High School] ([District])

**CONTRACT**
- Status: [value]
- List Price: $[value]
- Contract Date: [value]
- Expiration: [value]
- Possession: [value]
- Terms: [value]
- Buyer Agency Compensation: [value]
- Office Exclusive: [Yes/No]

**SHOWINGS**
- Occupant Type: [value]
- Showing Requirements: [list]
- Lockbox Location: [value]
- Showing Contact: [name / phone]

**ASSOCIATION**
- HOA: [Yes/No]
- Fee: [amount / frequency or N/A]

**INTERIOR**
- Beds: [value] | Full Baths: [value] | Half Baths: [value]
- Sq Ft Above Grade: [value] | Below Grade: [value]
- Living Area Source: [value]
- Fireplace: [Yes/No]
- Interior Features: [list]
- Appliances: [list]
- Flooring: [list]
- Basement: [Yes/No + type]
- Cooling: [value] | Heating: [value]

**PARKING**
- Garage: [Yes/No + spaces] | Carport: [Yes/No]
- Parking Features: [list]

**BUILDING**
- Year Built: [value] | Source: [value]
- Style: [value]
- Construction: [value]
- Foundation: [value] | Roof: [value]
- Stories: [value]

**LOT**
- Lot Size: [value acres/sq ft] | Source: [value]
- Lot Features: [list]
- Other Structures: [list or None]
- Pool: [Yes/No]

**UTILITIES**
- Sewer: [value] | Water: [value]
- Electric: [value] | Gas: [value]

**REMARKS**
- Public Remarks: [full text]
- Private Remarks: [full text]
- Directions: [text or TBD]

**MEDIA**
- Photos: [# uploaded or "not yet"]
- Seller's Disclosure: [uploaded / not yet]
- Lead-Based Paint: [uploaded / N/A / not yet]
- HOA Docs: [uploaded / N/A / not yet]

**FLAGS / MISSING**
- [List any fields still needed or issues to resolve before publishing]

---

*This summary is ready to be used to enter or verify the listing in flexMLS.*
