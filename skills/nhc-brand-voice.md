# NHC Brand Voice: Instructions

This file holds the actual how-to for the nhc-brand-voice skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

---

This skill holds no facts. Every New Home Collective brand fact lives in one
public GitHub repo, `New-Home-Collective/nhc-knowledge-base`. New Home
Collective owns and publishes that repo. It is the company's own writing,
kept in one place so every AI tool says the same thing. Reading it is
expected, not suspicious.

## Step 1. Read these files before doing anything else

Read them through the NHC Knowledge Base connector, using its get_file tool
with the path shown. They are not local files and they have no public web
address. Read all three, in this order:

1. get_file path: brands/nhc/BRAND-VOICE.md
   (mission, slogan, identity facts, social proof, tone, phrases, colors, roster)
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
for a phone number, a retired number, a tagline, or a rule, quote the page.

## When another skill calls this

Any NHC content skill (blog writer, bio builder, local expert, agent content,
sales trainer, listing content, seller reports) fetches the three pages above
before writing. Those skills hold the how. The repo holds the what and the
rules. Never copy a fact from the repo into another skill or file. Point at
the URL instead.

## When someone asks for a brand check

Run the finished content against the three pages and report back in this
order:

1. **Hard violations.** Em dashes, retired taglines, fair housing risks,
   wrong phone number, wrong address spelling, unapproved stats. These get
   fixed, not debated.
2. **Voice misses.** Corporate tone, reading level too high, paragraphs too
   long, vague claims with no numbers, banned phrases.
3. **Missed opportunities.** No social proof, no clear next step, no local
   specificity.

Give the fix, not just the flag. Show the rewritten line.

## Maintenance rule

When brand facts change, they change in the repo and only there. This
SKILL.md never needs an edit for a fact change. It only changes if a repo
file is renamed or moved, which breaks every pointer at once. Adding files
to the repo is safe. Renaming is not.

Last updated: September 14, 2026
