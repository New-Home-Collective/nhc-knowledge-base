# NHC Home Equity Report: Instructions

This file holds the actual how-to for the nhc-home-equity-report skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

Supporting files for this skill live in the knowledge base too. Read each
one with the connector's get_file tool at the path shown:
- skills/nhc-home-equity-report/references/pricing-playbook.md
- skills/nhc-home-equity-report/assets/field-form-template.html
- skills/nhc-home-equity-report/assets/report-template.html

The `scripts/` folder stays inside the Claude-side skill. Run those scripts
from there. Fetch templates from the paths above, fill them, save the result
locally, then render.

---

## What this does

Ships **two files every time**:

1. **Home Equity Report** — six-page PDF the seller holds during the appointment
2. **Listing Appointment Field Form** — two-page PDF, prefilled, that the agent writes on at the house

Plus a talk track in the chat. Never deliver one without the other. The report is what the seller
reads. The form is what the agent captures on. An agent who shows up with the report and no form
ends up taking notes on the back of the report, which is the document they are trying to hand over.

The core insight this skill exists to deliver: **sellers do not argue with photos.** When a homeowner
looks at a kitchen that sold in eleven days next to a kitchen that has been sitting ninety, they
arrive at their own price. That is a completely different conversation than an agent telling them
what their house is worth.

This follows Nick McLean's Seller High Output Productivity pricing method. The report never opens
with an opinion. It opens with facts, then evidence, then the seller picks.

## Before you build anything

Read these files first through the NHC Knowledge Base connector (get_file).
This skill holds no brand facts:

Identity facts (office address and phone for the signature block): brands/nhc/BRAND-VOICE.md
Writing rules: company/writing-rules.md
Fair housing and compliance: company/compliance.md

If the connector is not enabled, ask the person to turn it on and try again. If a read still fails, say so and stop. Never type the office address or phone from memory. The templates carry `OFFICE_ADDRESS` and `OFFICE_PHONE` tokens for a reason.

Then read `skills/nhc-home-equity-report/references/pricing-playbook.md`. It covers the Flexmls queries, how to pick comps, how to
choose photos, and how the price math works. Do not skip it. The analysis is what makes this worth
handing to a client.

## Step 1: Ask five questions first

Never start pulling data until you have these. Ask them together, in one message, using
`ask_user_input_v0` where the answers are short. Do not guess and do not skip.

| Ask | Why it matters |
|---|---|
| **Who are the seller or sellers?** Full names | Goes on both documents. Also tells you how many decision makers have to be in the room |
| **What is the property address?** | Everything anchors off this. Confirm the spelling against the MLS before it prints |
| **What updates did the seller mention?** | Changes which comp band applies. A seller who says "new kitchen in 2024" is not in the same band as one who says nothing |
| **How does the seller rate their home, 1 to 10?** | The single most useful number you will get. It tells you where they think they sit before they see a single photo |
| **When is the appointment?** | Prints on the form and tells you how much time you have |

**The 1 to 10 rating is the one to press on.** If the agent does not have it, ask them to get it.
It does two things. It tells you which rung on page 5 to expect them to land on, and at the
appointment it gives the agent the best follow-up question in the business: *what would make it a 10?*
That answer is the prep list, in the seller's own words, for free.

**Do not put the rating or the seller's target price in the Home Equity Report.** The rating belongs
on the agent's form. It shapes how you write page 5, it never appears on the page.

Two more worth asking when the agent has them: the lead source, and how long they have owned it.
Both prefill onto the form.

## Step 2: Gather

| What | Where it comes from |
|---|---|
| Subject property | `Flex Imagine:ListingsListingSearch` by street address. Keep the `ListingKey` |
| Prior listing history | Same call. Pull `OriginalListPrice`, `DaysOnMarket`, `OffMarketDate`, `MlsStatus` |
| Sold comps | Closed, last 12 months, radius off the ListingKey |
| Under contract comps | Pending and Contingent, same radius |
| Active comps | The competition |
| Market counts | Counts and medians across all three statuses |
| Photos | `Flex Imagine:ListingsListPhotos` on each comp you feature |
| Condition read | **Ask the agent.** You cannot see the house |

That last one is not optional. Never produce a price range without asking the agent how the home
actually shows, what has been updated, when, and what it cost. The MLS tells you where the market is.
Only the agent knows whether this house sits at the top or bottom of that range.

Also ask whether the seller has a number in mind. Use it to shape the conversation, **never put it in
the report.** See the rules below.

## Step 3: The four rules that keep this honest

**Page one is facts only.** Property characteristics and market counts. No target price, no seller's
hoped-for number, no recommendation, no opinion. A seller who sees their own number printed on page
one stops reading and starts defending it. Facts first buys you the rest of the report.

**Never print the seller's target.** Even to agree with it. If they said $350,000 and the evidence
supports $350,000, the report shows the band and lets them land there. They own the number. That is
the entire mechanism.

**Only recommend prep you have actually seen.** If the agent has not walked the house, the prep
section is blank lines the agent fills in on site. Do not invent "finish the basement" or "add mulch"
from an MLS record. Invented advice is the fastest way to lose credibility with a seller who knows
their own house. What you may always list is what NHC genuinely does for every listing: professional
photography, video, drone, MLS, syndication.

**Count, do not characterize.** "Eleven of nineteen sold below their first asking price" is a fact.
"Most sellers overprice" is an opinion. Use the count.

## Step 4: Page structure

Six pages. Each one does one job.

**Page 1, the facts.** Masthead, five property stats, market snapshot table. Active, pending, sold
counts. Median price, average price per finished square foot, average days on market, months of
inventory, original list to sold ratio, how many took a price cut, how many never sold. If the
subject has listing history, it goes here as a fact with dates, not as a judgement.

**Page 2, sold.** Two comps, six photos each. What buyers actually paid. Closed price, days on
market, what they gave back from the first asking price.

**Page 3, under contract.** Two comps, six photos each. The most current signal there is. Most
agents never show this page. Note whether each went under contract at full price or after a cut.

**Page 4, active.** Two comps, six photos each. Nobody has paid these prices. This page sets
position, not value. Show days on market and any reduction already taken.

**Page 5, where your home lands.** The price-per-foot arithmetic on the page, the supported band, then
three price rungs the seller picks from based on how they scored the photo pages. Plus the honest
push-and-pull table: what lifts this home above the comps, what pulls it down.

**Page 6, the money.** Net sheet at all three rungs, every fee not just commission, mortgage payoff
left blank for the seller's statement. Then prep, next steps, and the closing question.

## Step 5: Photo selection

Six photos per comp, always in this order so the seller can scan across:

1. Front
2. Kitchen
3. Primary bath
4. Second bath
5. Main living space
6. Back or yard

Use the `Tags.Room` field from `ListingsListPhotos` to find them. When a listing has no room tags,
either use `Flex Imagine:ListingsShowPhoto` to identify them yourself, or pick a different comp. Do
not guess. A mislabeled bathroom in a seller-facing report is worse than one fewer comp.

If a comp is missing a room, leave that frame empty with its label rather than substituting a
different room. The empty frame is itself information.

## Step 6: The Zestimate

The report carries the current Zestimate as a property fact on page 1. Getting it is a two-step
process because **Zillow cannot be fetched directly.** A `web_fetch` against a Zillow property page
returns a 429 and the page never loads. This is not a network setting, it is Zillow blocking
automated traffic, and it will not change.

So:

1. Run a `web_search` for `<full address> Zestimate`. Sometimes the result snippet carries the number.
   When it does, use it and note the date you pulled it.
2. When it does not, **ask the agent.** They can pull it up on their phone in ten seconds. Ask for
   the number and the date they looked.

**Never invent a Zestimate and never estimate one from the comps.** If nobody has it by the time
you build, print `Not pulled` in the cell with a note that the agent will add it. A blank is honest.
A made-up number is the fastest way to lose a seller who checks.

Always label it as Zillow's automated estimate with the date. It is a third-party fact, not our
opinion, and page 1 is a facts page.

**Why it goes on page 1 at all.** The Zestimate is usually already in the seller's head before you
walk in. Naming it as one fact among eight, next to real market counts, is stronger than ignoring
it and letting them hold it privately against everything you say. It is also the one number on
page 1 that page 5 will quietly correct.

## Step 7: Build the files

Build **both** documents.

**The report.** Use `skills/nhc-home-equity-report/assets/report-template.html`. Fill every placeholder, then render. Target six pages.

**The form.** Use `skills/nhc-home-equity-report/assets/field-form-template.html`. Fill the thirteen tokens from the intake answers
and the MLS pull, then render. Target two pages, meant to print on one sheet double-sided.

```bash
python3 scripts/render_pdf.py <filled.html> <output.pdf>
```

The script flags unreplaced tokens, page overflow, and a page count that misses the target (6 for the report, 2 for the form). It measures at print width, so what it reports is what prints. A non-zero exit means fix it before delivering.

### What prefills onto the form

| Token | Source |
|---|---|
| `SELLERS`, `PROPERTY`, `APPT`, `SOURCE` | The intake questions |
| `UPDATES` | What the seller told the agent, in their words |
| `SELLER_RATING` | The 1 to 10 answer |
| `MLS_SUMMARY` | Beds, baths, sq ft, year, lot, garage, style, schools |
| `TAX_SQFT`, `TAX_BEDBATH`, `TAX_GARAGELOT` | MLS record, so the agent verifies against it on site |
| `OWNED` | Last sale date from the MLS, when there is one |
| `ZESTIMATE_LINE` | Same value as the report, or `agent to pull` |
| `PRIOR_HISTORY` | Prior listings with dates, prices, and outcomes |

Everything else stays blank. **The form is a capture tool, not a summary.** Prefilling a field the
agent should be asking about at the house defeats the point. Prefill only what is on record, and the
callout at the top of the form says plainly that every line needs verifying.

Target six pages for the report and two for the form.

**One thing that will bite you.**

**Photos need the CDN allowlisted.** The images live on `cdn.resize.sparkplatform.com` and
`cdn.photos.sparkplatform.com`. If those hosts are not on the workspace network allowlist, the
sandbox gets a 403 and renders empty frames. The photo frames have fixed heights so the layout holds
either way. When the CDN is blocked, hand the agent the HTML and tell them to open it in Chrome and
print to PDF with background graphics ON, scale at 100%, and headers and footers off. When the CDN is
allowlisted, download each photo and embed it as a base64 data URI so the PDF is self-contained.

Save the PDF and HTML for both documents and present all four. Agents want the PDFs for the meeting
and the HTML when a number changes. Name them so they sort together, for example
`NHC-Home-Equity-Report-<address>.pdf` and `NHC-Field-Form-<address>.pdf`.

## Step 8: Fair housing

These are shared across every brand and live in one place. They are not
written out here.

**Read company/compliance.md through the NHC Knowledge Base connector.**

Read it every time before writing anything that describes a home, a
neighborhood, or a buyer. If the connector is not enabled, ask the person
to turn it on. If the read still fails, say so and stop. Do not
write housing content from memory. A fair housing rule recalled wrong is a
legal problem, not an embarrassment.


## Step 9: The talk track

Every report ships with a talk track produced in the chat, not as a file. Agents read it on their
phone in the car.

Cover the order to walk the pages, the two permission questions to get before page five, where to
stop talking and let them look at photos, the three objections that always come, and how to close.

The two permission questions, asked before any number appears:

> Can I tell you what you need to hear instead of what you want to hear?

> If you land on a price I think hurts your goals, is it okay that I say so?

Get both yeses on page four. Without them you cannot be honest on page five without breaking rapport.

## Voice

NHC brand standards apply to every word on the page. Read the `nhc-brand-voice` skill if you need the
full rules. The short version:

- Follow every rule in company/writing-rules.md. Read it, do not recall it.
- Conversational, never corporate
- The homeowner is the hero, the agent is the guide
- No hype, no pressure language
- Contractions are good
- End on a question, not an ask

## Files

- `skills/nhc-home-equity-report/references/pricing-playbook.md`: Flexmls queries, comp selection, photo selection, price math, net sheet. Read before building
- `skills/nhc-home-equity-report/assets/report-template.html`: branded six-page seller report. Photo frames are a 3 by 2 grid per comp
- `skills/nhc-home-equity-report/assets/field-form-template.html`: two-page agent capture form, prints on one sheet double-sided
- `scripts/render_pdf.py`: HTML to PDF, checks page count, overflow, and unreplaced tokens

All four were rebuilt on 14 September 2026 after the originals went missing. The templates share their print styling with `nhc-seller-update-report` so the two documents look like a set. Bob should read the pricing playbook once and correct anything that is not how NHC prices.
