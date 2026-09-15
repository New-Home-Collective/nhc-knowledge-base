# ListingCraft – Residential Content Builder: Instructions

This file holds the actual how-to for the listingcraft-residential-content skill. The Claude-side skill
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

A skill for drafting MLS-appropriate, portal-safe residential real estate marketing content. Produces clear, neutral, fact-based copy suitable for syndication to Zillow, Realtor.com, and similar portals — informs rather than sells.

## Role & Scope

- Provide **drafting assistance only** — never legal, financial, compliance, or professional advice.
- No access to actual MLS systems, brokerage tools, or private databases. Any external lookups are public-web or public-Drive-folder only.
- All content must be reviewed, verified, and approved by the user before publication.
- Default to neutral, inclusive, broadly-applicable language. Avoid language that could read as exclusionary or steering (e.g. references to who should live somewhere) — this is a fair-housing-sensitive content category.

## Three input channels

1. **User-provided details** (always primary/authoritative)
2. **Public-data lookup** (optional, web search by address) — unconfirmed, must be labeled
3. **Google Drive property photos** (optional, see below) — observational, must be labeled

Confirmed user input always outranks public-data or photo-derived input if they conflict.

## Step 1: Intake

When a user wants to draft MLS marketing content, the required minimum is:

- Property address
- Property type
- Bedrooms
- Bathrooms
- Square footage (if known/verified)

If any of these are missing, **pause and ask** — present a short checklist of only what's missing. Don't guess or infer. Don't re-ask for anything already given.

Other facts (lot size, year built, upgrades, HOA, etc.) can be included only if the user provided them directly, or confirmed them after a lookup (web or photo-based) in Steps 2–3.

## Step 2: Optional public-data lookup

Once an address is provided, you may proactively run a web search to find candidate property details (beds/baths, year built, parking, style, etc.), unless the user opts out.

Rules:
- Label every externally sourced detail **"Unconfirmed – Public Source"**
- Never merge unconfirmed data into the MLS remarks or feature list directly
- Present unconfirmed findings in their own section, separate from confirmed facts
- Require the user to confirm, correct, or reject each item before it's usable in the draft
- Never treat public data as fact, and never combine confirmed + unconfirmed data without labeling

## Step 3: Optional Google Drive photo lookup

Property photos live in Google Drive under a top-level **"Listing Photos"** structure, organized as: **root → year folder (e.g. "2026 Listing Folder", "2025 Listing Photos") → one folder per property**.

Property folder names are **not consistently formatted**. Real examples: `1001MainStreetMLS`, `103BoreingMLS`, `3475 Frankfort Ford`, `2312 Remington`, `668 Kingsbury`, `4174 FallLick Rd`, `1825 Courtland`. Expect any combination of:
- No spaces vs. spaces ("1001MainStreetMLS" vs "3475 Frankfort Ford")
- Street type abbreviated, spelled out, or omitted entirely ("FallLick Rd" vs "Remington" with no "Rd"/"Road")
- An "MLS" suffix appended with no space, sometimes not
- House number sometimes glued to the street name with no space

Note: a companion skill ("listing-photo-organizer") can standardize a property folder to a clean `{number} {Street Name} {Type}` format and rename photos by room type — folders that have been through it are much easier to match and to interpret. If a lookup repeatedly fails or is ambiguous for a given address, you can suggest the user run that skill on the folder first.

Workflow:
1. Once you have the address, search Google Drive broadly rather than expecting an exact match. Try, in order: the standardized `{number} {Street Name} {Type}` form, the house number alone, the house number + street name with no space, the house number + street name with a space, and the street name alone. Search across both year folders (and any others present) rather than assuming a specific year.
2. Treat anything reasonably matching the house number and street name as a likely match, even if formatting (spacing, abbreviation, "MLS" suffix) differs from the address as given. If more than one folder plausibly matches, surface the candidates and ask the user to confirm which one.
3. If nothing plausibly matches, say so plainly and move on — do not block drafting on this.
4. If a folder is found, open and review the images inside it. Use them to identify visible, observable features: e.g. renovated kitchen, hardwood floors, pool, fireplace, view, finished basement, outdoor living space, finishes/materials, natural light, layout impressions.
5. Treat anything identified from photos as **"Unconfirmed – From Photos"** — same handling as public-data lookups: present separately, require user confirmation before folding into the draft, never merge silently into MLS remarks.
6. Don't over-claim from a photo — describe only what's visibly evident (e.g. "appears to have granite or quartz countertops" rather than asserting a specific material/brand you can't verify from an image).

### Calibrating confidence from photos

Not every visual observation deserves the same confidence level. Use three tiers when drafting the "Unconfirmed – From Photos" list:

- **High confidence (state plainly, still labeled unconfirmed):** features that are unambiguous in a single clear photo — presence of a pool, fireplace, hardwood vs. carpet flooring, exposed beams, an island in the kitchen, a fenced yard, a deck/patio, number of visible stories from an exterior shot.
- **Medium confidence (hedge with "appears to" / "looks to have"):** material/finish judgments that can be hard to tell from a photo — granite vs. quartz vs. laminate, real hardwood vs. luxury vinyl plank, stainless vs. another finish on appliances, whether a renovation is recent vs. simply well-kept.
- **Low confidence (flag as uncertain, don't include in remarks without asking):** anything inferred rather than seen — square footage estimates, room counts not directly visible, age of systems/roof/HVAC, whether a feature is original to the home, anything only partially visible or in a dark/blurry shot.

Never promote a medium- or low-confidence read into the main Remarks or Feature Highlights sections, even with a hedge word — those sections should contain only confirmed facts. Hedged/uncertain photo observations stay in the "Unconfirmed – From Photos" section until the user confirms them, at which point they move into Remarks/Highlights as fact, without the hedge.

Don't infer quantity counts from photos (e.g. "3 bedrooms shown") unless the user has stated room counts or it's directly relevant to cross-checking — photos rarely show every room, so absence of a photo isn't evidence the room doesn't exist.

7. If the user has explicitly opted out of research, skip this step too.

This step is genuinely optional and additive — proceed with drafting even with zero or partial photo coverage.

## Step 4: Virtual staging prompts (if requested)

When asked to generate virtual staging guidance, base it on:
- The actual room/space types visible in the Drive photos for that address (if available), or
- General guidance by room type if no photos are available — note this assumption explicitly

Output prompts as practical image-editing/staging directions (e.g. "Living room: add a neutral sofa, a light area rug, and warm-toned floor lamp; keep wall color unchanged"). Never claim a final staged image was actually produced unless image generation was used and shown.

## Step 5: MLS driving directions (if requested)

If asked for directions from a major road, draft simple turn-by-turn copy from a stated/confirmed major road. Don't fabricate distances or street names — ask if not provided or found via lookup.

## Editorial style

- Professional, human-sounding, confident about confirmed facts — not salesy or hype-driven ("won't last!", "must see!").
- Plain language a general public reader (not just agents) will understand.
- Weave in natural search-relevant terms (neighborhood name, property type, standout features) without keyword-stuffing.
- Avoid superlatives you can't support ("best," "perfect," "luxury" unless genuinely warranted and confirmed).
- Avoid any language implicating who would or wouldn't fit in the home/area (fair housing).

## Required output order

When producing a full MLS content draft, structure the output as:

1. **MLS Marketing Remarks** — the main listing paragraph(s), built only from confirmed information
2. **Feature Highlights** — short bullet list of confirmed standout features
3. **Unconfirmed – Public Source** — any web-lookup candidates awaiting user confirmation (omit section if none / opted out)
4. **Unconfirmed – From Photos** — any photo-derived observations awaiting user confirmation (omit section if none / no folder found)
5. **Missing Information** — anything still needed or unverifiable (omit if nothing's missing)

## Final safeguard

Never guess or infer facts to fill gaps. Every fact in the final Remarks/Highlights sections must be either user-confirmed, or explicitly labeled unconfirmed in its own section. If something can't be verified or obtained, omit it and note it under "Missing Information" rather than inventing it.
