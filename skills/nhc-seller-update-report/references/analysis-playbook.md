# Analysis Playbook

How to turn a ShowingTime PDF and an MLS pull into something worth handing a seller.

## Contents

1. Pulling the MLS data
2. Reading the activity report
3. Coding the showing feedback
4. The price math
5. Traffic over time
6. Finding the structural explanation
7. Things that look like signal but are not

---

## 1. Pulling the MLS data

Get the subject listing first. The listing ID is on page 1 of the ShowingTime report.

```
Flex Imagine:ListingsListingSearch
  _filter: ListingId Eq '<id>'
  _select: ListingId,UnparsedAddress,ListPrice,OriginalListPrice,MlsStatus,BedsTotal,
           BathsTotal,BuildingAreaTotal,LotSizeAcres,YearBuilt,SubdivisionName,
           DaysOnMarket,CumulativeDaysOnMarket,ListingKey,PublicRemarks,GarageSpaces,
           ElementarySchool,MiddleOrJuniorSchool,HighSchool
```

Keep the `ListingKey`. It is the anchor for radius searches.

**Closed comps** — last 12 months, within 1.5 miles, filtered to a comparable size floor:

```
_filter: Location Eq radius('<ListingKey>',1.5) And CloseDate Ge days(-365)
         And ClosePrice Ge <floor> And BuildingAreaTotal Ge <sqft floor>
_orderby: -CloseDate
```

**Current competition** — active, pending, and contingent in the same price band:

```
_filter: Location Eq radius('<ListingKey>',1.5) And ListPrice Bt <low>,<high>
         And BuildingAreaTotal Ge <sqft floor>
status_values: ["Active","Pending","Contingent"]
```

Prefer same-subdivision comps over radius comps when there are enough of them. A seller trusts
"four houses on your streets" more than "homes within a mile and a half."

Widen the radius or the date window if you get fewer than four usable comps. Say so on the page if
the comp set is thin, since that is itself useful information.

---

## 2. Reading the activity report

Pull these off page 1 and the activity log:

- List date, original price, current price, every price change with date and amount
- Total showings, showings in last 30 days, showings in last 7 days
- Agent previews and agent inquiries (zero of both is a signal worth naming)
- Status changes, especially Coming Soon to Active
- Canceled showings and the stated reason
- Second showings, which are the strongest buyer signal in the whole document

**Second showings deserve special attention.** A buyer who came back twice and still walked is the
closest you got to an offer. Whatever stopped them is the real objection. Read that feedback
carefully, twice.

**Canceled showings** are usually noise, but a cancellation reason like "determined the home is not
in the needed school zone" is real information about who the marketing is attracting.

---

## 3. Coding the showing feedback

Read every written comment. Then tag each one by the primary reason the buyer passed:

- **Permanent property condition** — lot, drainage, road noise, floor plan, location, lot size
- **Correctable condition** — clutter, smell, paint, staging, deferred maintenance, photos
- **Price** — stated directly
- **Buyer fit** — needed a different bedroom count, had a home to sell, changed their mind
- **Positive** — anything complimentary, even from a buyer who passed

Then count. The count is the headline.

**The pattern to look for:** when a single permanent condition shows up in more than half the
written responses, the price is wrong for that condition. That is the whole finding. Price is not
usually the loudest complaint in the data, and that is fine. Say it directly: fewer buyers said
"too high" than said "the backyard," but the backyard cannot change and the price can.

**Watch the response rate.** Sixteen written responses out of nineteen showings is excellent. Four
out of nineteen means the agent is not chasing feedback, and that is its own problem worth
mentioning to the agent privately, not in the seller report.

**Do not over-read a single comment.** One buyer disliking the upstairs is a preference. Five
buyers naming the same thing is a market signal. Only elevate what repeats.

**Pick 10 to 12 quotes for the wall.** Lead with the repeating objection, then include three or four
genuine compliments. Keep them short. Trim to the sentence that carries the point, but never change
the words inside the quote.

---

## 4. The price math

Compute price per finished above-grade square foot for the subject and every comp.

```
$/sqft = price / finished above-grade square footage
```

Build three groups:

1. **Closed** in the subdivision or radius, last 12 months
2. **Under contract right now** — this is the strongest signal, because it is what buyers are
   agreeing to today
3. **The subject**

Then find the honest range. Use the under-contract band as your primary anchor. Smaller homes
normally carry a higher per-foot number than larger ones, so do not apply the average blindly to a
small subject. Look at the comps closest in size.

To get to a range: take the low and high of the under-contract $/sqft band, apply both to the
subject's finished square footage, then adjust for condition based on what the agent told you.

Present it as "based on the comps this lands in the low $600s," not "$612,400." False precision
reads as a guess dressed up.

**Sanity checks before you publish a number:**

- Does the subject's $/sqft sit above every single comp? If so, there is almost always a structural
  reason. Find it before you conclude anything.
- Are the comps genuinely comparable in age, style, and finish level?
- Has the agent confirmed condition? If not, do not publish a range yet.

---

## 5. Traffic over time

Chart showings per week. The shape matters more than the total.

The pattern to look for is what happened around each price change. A reduction that works produces
a sustained lift. A reduction that is too small produces a one or two week spike and then a return
to baseline. That spike-and-fade shape is the single cleanest proof that the last cut was not deep
enough, and sellers understand it instantly when they see the bars.

Also worth naming: traffic that was strong at launch and has decayed steadily is normal listing
behavior. Traffic that never started is a marketing or price-at-launch problem, which is a
different conversation.

---

## 6. Finding the structural explanation

Before concluding the seller is simply overpriced, look for why the market reads the home
differently than they do. Common ones:

- **Unfinished space counted informally.** A roughed-in attic, an unfinished basement, a bonus room
  over the garage. The seller is pricing space the MLS does not count and buyers cannot use yet.
  Compute what the $/sqft would be if it were finished. If that number lands inside the comp range,
  you have found the whole explanation and it is not an insult to the house.
- **Bath count below the comps.** Very common and rarely mentioned in feedback, because buyers leave
  over something more visible first.
- **Garage or parking below the neighborhood norm.**
- **Lot that is large on paper but small in usable area.** Drainage easements, culverts, slopes.
- **A backing condition** — road, commercial, power lines.

This step matters because it changes the emotional register of the whole meeting. "Your price is
too high" starts an argument. "The market is not counting your attic" starts a conversation.

---

## 7. Things that look like signal but are not

- **A single "too high" comment.** Agents check that box reflexively.
- **Low agent previews.** Previews are mostly extinct. Zero is normal now, though it is still worth
  showing on the stat strip.
- **One canceled showing.** Buyers cancel. Three or more with the same stated reason is a pattern.
- **Feedback from the listing team's own agents.** Discount it. It is not arm's length.
- **Comparing to a much larger home's $/sqft.** Larger homes always carry a lower per-foot number.
  Compare to size-adjacent comps.
