# AGENTS.md

Read this before you read or write anything else in this repo.

This repo is not an app. There is no build, no database, no deploy, and no
preview link. It is writing. It holds the company's facts so that every AI
tool New Home Collective uses says the same thing.

---

## The four rules

### 1. A fact lives in exactly one file

One file owns each fact. Everything else points at that file. Pointing means
naming the file and the section, not repeating what it says.

If you find the same fact written down in two places, that is a bug. Fix it by
deleting one copy and replacing it with a pointer, not by updating both.

### 2. Never copy a fact out of this repo

Do not paste a fact from here into a skill, a prompt, a template, a website, or
another repo. Link to the file instead.

This rule has already cost us once. A skill called `nhc-bio-builder` kept its
own copy of the office phone number in a file named `references/nhc-brand.md`.
The real office number changed. The copy did not. Bios went out to the public
with a phone number that did not reach us. That file was retired rather than
updated, and the same treatment applies to any duplicate found from here on.

### 3. A tool that cannot reach this repo must say so and stop

If a skill, a prompt, or an assistant tries to read a file here and the read
fails, the correct behavior is to tell the person it could not reach the file
and stop. It must not answer from memory, and it must not guess.

This matters most for the fair housing rules in
`brands/nhc/BRAND-VOICE.md`. A brand fact recalled from memory is
embarrassing. A fair housing rule recalled from memory is a legal problem.

This repo is public, so any AI tool can read it with no account, no invite,
and no connector setup. A read should only fail if GitHub is down or the file
was renamed. Either way rule 3 still applies: say so and stop.

### 4. Nothing with a live source goes in here

If a number changes on its own somewhere else, it does not belong in this
repo. Keep out anything sourced from Follow Up Boss, the MLS, Supabase, or a
Google review count pulled today. Referral income stays out as well.

Published claims are written on purpose and reviewed on purpose. The approved
review claim is "1,200+ five-star Google reviews," never a scraped count.
Approved numbers carry a verification date and get re-verified, they do not
get wired to a live feed.

---

## Layout

```
AGENTS.md                      this file, the rules
README.md                      what the repo is and how to point at it

brands/nhc/BRAND-VOICE.md      New Home Collective
brands/be/BRAND-VOICE.md       BE Property Ventures
brands/lake-days/BRAND-VOICE.md  Lake Days, Cabin Stays

company/people.md              team roster and roles
company/services.md            what we offer
company/compliance.md          fair housing and disclosure rules
```

Brands do not mix. The universal writing rules apply to all three. The New
Home Collective identity facts apply only to New Home Collective.

This repo is public. Nothing operational and nothing sensitive belongs in it.
Sadie's phone prompt used to live here and was moved to the `nhc-ops` repo,
at `docs/sadie-prompt.md`, because Ops owns Sadie and the routing behind her.
No credentials, no keys, no phone scripts.

---

## How to write in here

Plain English. Short sentences. No em dashes. Say what a thing does before you
name it. These are the same rules the brand files ask for, and this repo
follows its own rules.

Every fact that can go stale gets a verification date next to it in the file
that owns it.

---

## Pending work

### Duplicates still outstanding

These five files each hold their own copy of a fact this repo owns. They are
the remaining drift risk. All copies matched the source when measured on
11 September 2026, so nothing is wrong in public right now. They become
pointers once the access method for agents is settled.

| File | Line | Duplicated fact |
| --- | --- | --- |
| `nhc-bio-builder/SKILL.md` | 108 | office phone |
| `nhc-blog-writer/SKILL.md` | 100 | office phone |
| `nhc-blog-writer/references/seo-ai-checklist.md` | 96 | office phone and office address |
| `nhc-content-machine/SKILL.md` | 73 | office phone |
| `nhc-seller-update-report/assets/report-template.html` | 457 | office address |

Six copies of two facts across five files. Line numbers are from
11 September 2026 and will drift as those files are edited, so search for the
value rather than trusting the line number.

`nhc-bio-builder/references/nhc-brand.md` is already done. It is a short file
that points at the real source and holds no facts of its own. Use it as the
model for the five above.

---

## Precedence

This file governs this repo. The app repos, `nhc-ops` and `nhc-cash-offer`,
have their own AGENTS.md files and their own conventions. Do not carry a
decision from one repo into another.
