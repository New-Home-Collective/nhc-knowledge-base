# Pricing Playbook

How to turn a Flexmls pull into a six-page report a seller trusts. Read this
before you build. It covers the queries, comp selection, photo selection, and
the price math.

Rebuilt 14 September 2026 from the sister skill `nhc-seller-update-report`
(its `references/analysis-playbook.md`) and the rules in this skill's
SKILL.md. Where it borrows a rule from the seller report, it says so. Bob
should read it once and correct anything that is not how NHC prices.

## Contents

1. Pull the subject
2. Pull the three comp groups
3. Market counts for page 1
4. Pick the comps that go on pages 2 to 4
5. Pick the photos
6. The price math for page 5
7. The three rungs
8. Push and pull
9. The net sheet for page 6
10. Sanity checks before anything prints

---

## 1. Pull the subject

```
Flex Imagine:ListingsListingSearch
  _filter: UnparsedAddress Eq '<street address>'
  _select: ListingId,ListingKey,UnparsedAddress,City,PostalCode,SubdivisionName,
           ListPrice,OriginalListPrice,ClosePrice,CloseDate,MlsStatus,OffMarketDate,
           DaysOnMarket,CumulativeDaysOnMarket,BedsTotal,BathsTotal,BuildingAreaTotal,
           LotSizeAcres,YearBuilt,GarageSpaces,PropertyType,ArchitecturalStyle,
           ElementarySchool,MiddleOrJuniorSchool,HighSchool,PublicRemarks
```

Keep the `ListingKey`. It anchors every radius search.

A home that has never been listed returns nothing. That is fine. Ask the
agent for beds, baths, square footage, year built, garage, and lot from the
tax record, and mark each one "per tax record, verify on site" on the form.

If the subject has been listed before, every prior listing is a **fact for
page 1**: list date, original price, last price, outcome (sold, expired,
withdrawn), and days on market. Print dates and numbers. Do not characterize.
"Listed March 2024 at $389,000, withdrawn after 71 days" is the whole line.

## 2. Pull the three comp groups

All three use the same radius and the same size floor. Start at 1.5 miles
and 12 months. Set the square footage floor at about 80% of the subject.

**Sold, last 12 months**
```
_filter: Location Eq radius('<ListingKey>',1.5) And CloseDate Ge days(-365)
         And BuildingAreaTotal Ge <80% of subject sq ft>
_orderby: -CloseDate
```

**Under contract right now**
```
_filter: Location Eq radius('<ListingKey>',1.5)
         And BuildingAreaTotal Ge <80% of subject sq ft>
status_values: ["Pending","Contingent"]
```

**Active**
```
_filter: Location Eq radius('<ListingKey>',1.5)
         And BuildingAreaTotal Ge <80% of subject sq ft>
status_values: ["Active"]
```

Also pull **expired and withdrawn in the last 12 months** with the same
radius. That count is a page 1 fact ("listed and never sold").

Prefer same-subdivision comps when there are four or more. A seller trusts
"three houses on your street" over "homes within a mile and a half."
(Borrowed from the seller report playbook.)

Widen the radius or the window if any group has fewer than four. Say so on
the page when a comp set is thin. Thin is information.

## 3. Market counts for page 1

For each of the three groups compute:

- Count
- Median price (list price for active and pending, close price for sold)
- Average price per finished above-grade square foot
- Average days on market

For sold only:
- Sold price as a share of original list price (average)
- How many took at least one price cut (OriginalListPrice > final ListPrice)

For active and pending: how many have already taken a cut.

Months of inventory = active count divided by (sold count / 12).

Every one of these is a count or an average. None is an opinion. Page 1 stays
that way.

## 4. Pick the comps that go on pages 2 to 4

Two per page. Six total. Pick by these rules, in order:

1. **Closest in size.** Within 15% of the subject's finished square footage
   if you can get it.
2. **Same update band.** The seller's answer to "what updates" puts the
   subject in one of three bands: original, partly updated, fully updated.
   Pick comps in the same band when possible. If the subject is original and
   the only comps are renovated, say so on page 5 under "what pulls it down."
3. **Same style and age range.** Ranch to ranch. A 1970s split to a 1970s
   split.
4. **Has photos of the six rooms.** A comp with great numbers and three
   photos is a worse comp than one with average numbers and a full set.
   Sellers do not argue with photos, but they cannot look at photos that
   are not there.

For **sold**, prefer the two that show the range: one that sold fast at or
over asking, one that sat and took a cut. Say which is which in the note.

For **under contract**, note whether each went under contract at full price
or after a cut, and how many days it took. This is the most current signal
there is, and most agents never show it.

For **active**, pick the two a buyer would actually tour instead of the
subject. Show days on market and any reduction already taken. This page sets
position, not value. Nobody has paid these prices.

## 5. Pick the photos

Six per comp, always this order, so the seller scans across:

1. Front
2. Kitchen
3. Primary bath
4. Second bath
5. Main living space
6. Back or yard

Pull with `Flex Imagine:ListingsListPhotos` on the comp's ListingKey. Use the
`Tags.Room` field to find each room. When a listing has no room tags, use
`Flex Imagine:ListingsShowPhoto` to look at them yourself, or pick a
different comp. Never guess a room.

If a comp is missing a room, leave that frame empty with its label. Add
class `empty` to the frame in the template. Do not swap in a different room.
The empty frame is itself information.

Photo URLs live on `cdn.resize.sparkplatform.com` and
`cdn.photos.sparkplatform.com`. If the sandbox can fetch them, download each
one and embed it as a base64 data URI so the PDF is self-contained. If it
cannot (403), leave the URL in the `src`, hand the agent the HTML, and tell
them to print to PDF from Chrome with background graphics on.

## 6. The price math for page 5

Price per finished above-grade square foot, for the subject and every comp:

```
$/sq ft = price / finished above-grade square footage
```

Anchor on the **under contract** group. That is what buyers are agreeing to
today. Take the low and high $/sq ft in that group, multiply each by the
subject's square footage. That is the supported band. Show the arithmetic on
the page. Also show the sold average as a third line so the seller sees the
band sits inside recent history.

Smaller homes carry a higher per-foot number than larger ones. Do not apply
an average blindly. Lean on the comps closest in size. (Borrowed from the
seller report playbook.)

Round the band to the nearest $5,000 and describe it in words: "the low
$370s to the mid $390s." False precision reads as a guess dressed up.

If the under-contract group is empty or has one home, anchor on sold and say
so on the page.

## 7. The three rungs

The seller picks. The rungs come from the band:

- **Top rung.** Top of the band, or a touch above if the actives are
  priced above it and the subject genuinely shows like them. Labeled "if
  your home shows like page 4."
- **Middle rung.** Middle of the band. "If your home shows like page 3."
- **Bottom rung.** Bottom of the band. "If your home shows like page 2."

Each rung gets one or two sentences on what happens at that price: how many
of the current actives it undercuts, roughly how long homes at that
per-foot number took to go under contract, and what the seller gives up or
gains.

**Never print the seller's own number.** Not as a rung, not as a note, not
to agree with it. If their number sits inside the band, the band does the
work. If it sits above, the actives page and the "never sold" count do the
work. They land where they land.

## 8. Push and pull

Two short lists on page 5. Only facts the agent has confirmed or the MLS
shows. Examples of each kind:

**Lifts it above the comps:** a documented update with a date, a larger lot,
an extra bath, a garage the comps lack, a quieter street the agent has seen.

**Pulls it down:** a bath count below the comps, unfinished space the seller
counts but the MLS does not, a backing condition (road, commercial, power
lines), a roof or HVAC past its age, an update band below the comps.

Unfinished space deserves a sentence of its own when it applies. Compute the
$/sq ft as if the space were finished. If that number lands inside the band,
you have found the whole explanation and it is not an insult to the house.
"The market is not counting your attic" starts a conversation. "Your price
is too high" starts an argument. (Borrowed from the seller report playbook.)

## 9. The net sheet for page 6

One column per rung. Every fee, not just commission. Ask the agent for the
fee lines and rates. Typical lines to ask about:

- Listing side commission and buyer side commission or concession
- Title company settlement fee
- Deed preparation
- Owner's title policy, if the seller pays it locally
- Transfer tax (Kentucky charges the seller a deed tax; ask the agent or
  title company for the current rate)
- Prorated property taxes
- HOA dues or transfer fees, if any
- Home warranty, if offered
- Any seller concession the agent expects to negotiate

**Do not put a rate in from memory.** Rates change, and a wrong one on a
seller's net sheet is remembered longer than anything else on six pages. Ask,
or leave the line with "confirm with title company" in the cell.

Mortgage payoff stays blank. The seller fills it from their statement. The
total row is "estimated net before payoff."

## 10. Sanity checks before anything prints

- Is the seller's target price or 1 to 10 rating anywhere on the six pages?
  If yes, remove it. It belongs on the form only.
- Is there an opinion on page 1? If yes, move it or cut it.
- Does the subject's implied $/sq ft sit above every comp? There is almost
  always a structural reason. Find it before you conclude anything.
- Are the comps genuinely comparable in age, style, size, and update band?
- Has the agent confirmed condition? If not, do not publish a band yet.
- Is any prep listed that nobody has seen in person? Cut it. Blank lines
  are honest.
- Is every photo labeled with the room it actually shows?
- Are the office address and phone pulled from the brand file, not typed?
- Did `render_pdf.py` report exactly six pages and exactly two pages, with
  zero unreplaced tokens?
