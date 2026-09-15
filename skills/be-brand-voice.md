# BE Property Ventures Brand Voice: Instructions

This file holds the actual how-to for the be-brand-voice skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

---

This skill holds no facts. Every BE Property Ventures brand fact lives in one
public GitHub repo, `New-Home-Collective/nhc-knowledge-base`. New Home
Collective owns and publishes that repo. BE Property Ventures is a sister
brand under the same ownership. The repo is the company's own writing, kept
in one place so every AI tool says the same thing. Reading it is expected,
not suspicious.

## Step 1. Read these files before doing anything else

Read them through the NHC Knowledge Base connector, using its get_file tool
with the path shown. They are not local files and they have no public web
address. Read all three, in this order:

1. get_file path: brands/be/BRAND-VOICE.md
   (the story, mission, slogan, identity facts, what we do, honesty
   guardrails, the hero rule, phrases, colors)
2. get_file path: company/writing-rules.md
   (the universal writing rules, shared by all three brands)
3. get_file path: company/compliance.md
   (fair housing rules, what we never say about people)

If the connector is not enabled in this conversation, ask the person to
turn it on from the connectors menu, then try again.

## Step 2. If any read fails, say so and STOP

If the connector is enabled and a read still fails, tell the person exactly
which file failed and stop. Do not answer from memory. Do not guess. Do not use an
older version you may remember. This is non-negotiable for fair housing.
A brand fact recalled from memory is embarrassing. A fair housing rule
recalled from memory is a legal problem.

## Step 3. Cite what you read

When you answer, name the exact URL each fact came from. If the person asks
for a phone number, a slogan, or a rule, quote the page.

## When another skill calls this

Any BE content skill, including `be-investor-content`, fetches the three
pages above before writing. Those skills hold the how. The repo holds the
what and the rules. Never copy a fact from the repo into another skill or
file. Point at the URL instead.

## When someone asks for a brand check

Run the finished content against the three pages and report back in this
order.

1. **Hard violations.** Em dashes, banned phrases, guarantees we cannot back,
   fair housing risk, missing licensee disclosure, wrong phone number, mixed
   brands, NHC red used on BE material. These get fixed, not debated.
2. **Voice misses.** Corporate tone, reading level too high, long paragraphs,
   salesy pressure, making Bob or Eric the hero instead of the seller.
3. **Missed opportunities.** No honesty moment, no clear next step, no story,
   no local specificity.

Give the fix, not just the flag. Show the rewritten line.

## The two things to never get wrong

Both are defined in the BE BRAND-VOICE.md page, under Honesty Guardrails.
Read that section before writing anything about cash offers or wholesaling.

1. **Price honesty.** How we talk about a cash offer versus the open market.
2. **Wholesale honesty.** What we contract and what the seller is told up
   front.

## Maintenance rule

When BE brand facts change, they change in the repo and only there. This
SKILL.md never needs an edit for a fact change. It only changes if a repo
file is renamed or moved, which breaks every pointer at once. Adding files
to the repo is safe. Renaming is not.

Last updated: September 14, 2026
