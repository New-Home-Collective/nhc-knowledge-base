# NHC Seller Update Report: Instructions

This file holds the actual how-to for the nhc-seller-update-report skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

Supporting files for this skill live in the knowledge base too. Read each
one with the connector's get_file tool at the path shown:
- skills/nhc-seller-update-report/references/analysis-playbook.md
- skills/nhc-seller-update-report/references/talk-track.md
- skills/nhc-seller-update-report/assets/report-template.html

The `scripts/` folder stays inside the Claude-side skill. Run those scripts
from there. Fetch templates from the paths above, fill them, save the result
locally, then render.

---

---

## Where facts come from (overrides everything below, including the template)

Read these live, every time. Do not use a phone number, an address, or a
brand fact from memory:

Identity facts: brands/nhc/BRAND-VOICE.md
Writing rules: company/writing-rules.md
Fair housing rules: company/compliance.md

Read them through the NHC Knowledge Base connector. Call its get_file
tool with the repo-relative path shown. There is no public web address for
these files.

If the connector is not enabled in this conversation, ask the person to turn
it on from the connectors menu, then try again. If it is enabled and a read
still fails, tell the person which file failed and stop. Do not write from
memory.

`skills/nhc-seller-update-report/assets/report-template.html` carries an `{{OFFICE_ADDRESS}}` placeholder in
the signature block. Fill it from the Identity Facts section of the brand
file above. Check the whole filled template for any typed phone number or
address before rendering. Do not render a report with an address you cannot
verify. A wrong office number has already shipped to the public once.


# NHC Seller Update Report

## What this does

Turns raw showing data into a three-page PDF a seller can hold, plus a talk track for the agent
running the meeting.

The core insight this skill exists to deliver: **sellers do not argue with their own buyers.** When
you show a seller sixteen pieces of unedited feedback from sixteen different agents saying the same
thing, they get to the answer themselves. That is a completely different conversation than an agent
telling them their price is too high.

The report never opens with a problem. It opens with what is working, then lets the data do the
rest.

## Before you build anything

Read `skills/nhc-seller-update-report/references/analysis-playbook.md`. It covers how to pull the MLS data, how to code showing
feedback, and how the price math works. Do not skip it. The analysis is what makes the report worth
handing to a client.

## Step 1: Gather

You need four things. Ask for whatever is missing.

| What | Where it comes from |
|---|---|
| Listing activity report | Agent uploads the ShowingTime PDF |
| Listing details | Pull from MLS by listing ID (`Flex Imagine:ListingsListingSearch`) |
| Comparable sales | Pull closed + under contract within 1.5 miles or the same subdivision |
| Condition read | Ask the agent. You cannot see the house |

That last one matters. Never produce a price range without asking the agent how the home actually
shows, what has been updated, and how the yard or lot presents in person. Square footage and comps
tell you where the market is. Only the agent knows whether this house sits at the top or bottom of
that range.

## Step 2: Classify the listing

The report structure stays the same. The tone and the closing section change based on where the
listing actually sits. Pick one:

**ON TRACK** — Under contract, multiple offers, or strong showing-to-offer conversion.
Report is a confirmation and a thank you. No price section. Closing section is "what happens next."

**EARLY SIGNAL** — Under 30 days, showings happening, no offers yet, feedback showing a pattern.
Report is a heads up. Show the pattern early. Closing section is "things we can fix now" and the
price conversation stays soft. The goal here is to get ahead of it, not to reduce.

**STALLED** — Days on market well past the local average, showings without offers, or traffic
falling off.
Report is the full pricing conversation. This is the version built in the original example.

If the agent has not said which, work it out from the data and tell them which one you picked and
why.

## Step 3: The non-negotiables

These are what make the report land instead of feeling like an attack.

**Open with a win.** Nineteen showings means the marketing worked. Say that first, plainly, before
anything else. A seller who feels blamed stops listening.

**Quote the feedback exactly as submitted.** Do not clean it up, do not paraphrase, do not fix the
typos. The credibility comes from it being raw. Attribute every quote to the agent and brokerage
that wrote it, with the date.

**Mix in the compliments.** If buyers praised the kitchen, that goes on the page next to the
complaints. It proves you are not cherry-picking, and it is true. A wall of only-negative reads as
an agenda.

**Count, do not characterize.** "Eleven of sixteen mentioned the backyard" is a fact. "Everyone
hates the yard" is an opinion. Use the count.

**Separate what can change from what cannot.** A drainage ditch, road noise, a lot line, a floor
plan: these are permanent. Price is the only lever that moves against a permanent condition. Make
that distinction explicit, because it is the whole argument.

**Give options, never an ultimatum.** Always close with three or four honest paths, including at
least one that is not a price reduction. Do not bold or star a recommended option. Let the seller
choose. NHC's job is clarity, not pressure.

**Own our side of it.** If the agent missed something — an unanswered buyer question, feedback
never followed up, a document never pulled — put it in the report. It costs nothing and it buys
enormous credibility right before you ask the seller to move. Ask the agent first, since they may
prefer to handle it verbally.

**End on a question, not an ask.** "Which matters more right now, the price or the timeline?" Their
answer decides everything that follows.

## Step 4: Fair housing guardrails

Showing feedback routinely mentions children, family size, pets, and schools. In a private written
update to your own client, quoting that feedback verbatim is a factual record and is fine.

Everything else follows the shared rules. **Read company/compliance.md through the NHC Knowledge Base connector.**
before writing any commentary. If it cannot be read, say so and stop.

Say what the buyers said. Do not add your own characterization on top of it. If feedback needs
summarizing, summarize by property feature: "the backyard," "the road noise," not "buyers with
kids."

## Step 5: Price guidance

Only for EARLY SIGNAL (soft) and STALLED (full). Never on an ON TRACK report.

Rules that keep this defensible:

1. Anchor to price per finished square foot from closed sales **and** homes currently under
   contract in the same subdivision. Under-contract homes are the better signal because they
   reflect what buyers are agreeing to right now.
2. Always give a **range**, never a single number.
3. Show the arithmetic on the page so the seller can follow it. If the subject is at $258/sqft and
   the neighborhood is transacting at $186 to $216, that gap is the entire conversation.
4. Look for a **structural explanation** before you conclude the seller is just greedy. Unfinished
   attic or basement counted informally, a bath count below the comps, a smaller lot. Finding the
   reason turns "your price is wrong" into "here is why the market reads it differently," which is
   a conversation a seller can accept.
5. State plainly that comps are a guide to market behavior, not an appraisal.
6. Tell the agent to sanity-check the range against the actual condition before delivering it.

Never suggest a trim so small it will not clear the objection. If the last reduction was 3% and
bought a two-week bump, say so and say why another 3% does the same thing.

## Step 6: Build the files

Use `skills/nhc-seller-update-report/assets/report-template.html`. It carries the NHC brand, the print CSS, and the page structure.
Fill the placeholders, delete any section the classification does not call for, then render:

```bash
python3 scripts/render_pdf.py <filled-template.html> <output.pdf>
```

Target three pages. The script reports the page count and flags overflow. If it runs long, tighten
spacing before you cut content, and if you still need to cut, drop a section rather than shrinking
type below readable size.

Save both the PDF and the HTML to the outputs folder and present both. Agents want the PDF for the
meeting and the HTML when they need to change a number.

### Page structure

**Page 1 — the argument.** Masthead, five-stat strip, one-line thesis, the feedback wall, the tally.
This page should work standing alone. If a seller reads nothing else, they get it.

**Page 2 — the money.** Comparable sales table with the subject highlighted, the structural
explanation callout, and any direct competition that just came on the market.

**Page 3 — the path.** Showing traffic over time, the options, and the closing question.

## Step 7: The talk track

Every report ships with a talk track. Read `skills/nhc-seller-update-report/references/talk-track.md` and produce it in the chat,
not as a file. Agents read it on their phone in the car.

It covers the order to walk the pages, what to say at each stop, where to stop talking and let them
read, the three objections that always come, and how to close.

## Voice

NHC brand standards apply to everything on the page:

- Follow every rule in company/writing-rules.md. Read it, do not recall it.
- Conversational, never corporate. Write like a person talking, not a marketing department
- The homeowner is the hero. The agent is the guide
- No hype, no pressure language, no "act now"
- Contractions are good

The report is a trusted advisor document. If a line sounds like it came from a brokerage
marketing team, rewrite it.

## Files

- `skills/nhc-seller-update-report/references/analysis-playbook.md` — MLS queries, feedback coding, price math. Read before building
- `skills/nhc-seller-update-report/references/talk-track.md` — how to run the meeting
- `skills/nhc-seller-update-report/assets/report-template.html` — branded print template
- `scripts/render_pdf.py` — HTML to PDF, checks page count
