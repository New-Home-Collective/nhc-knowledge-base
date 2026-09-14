# AGENTS.md

Read this before you read or write anything else in this repo.

This repo is not an app. There is no build, no database, no deploy, and no
preview link. It is writing. It holds the company's facts so that every AI
tool New Home Collective uses says the same thing.

It is platform neutral. Claude, ChatGPT, and whatever comes next all read the
same files. Files in here say what is true and where the source lives. They
never name a Claude skill or a ChatGPT action. The tool decides what to do.
The file only decides what is true.

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
`company/compliance.md`. A brand fact recalled from memory is
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
AGENTS.md                        this file, the rules
README.md                        what the repo is and how to point at it

brands/nhc/BRAND-VOICE.md        New Home Collective
brands/be/BRAND-VOICE.md         BE Property Ventures
brands/lake-days/BRAND-VOICE.md  Lake Days, Cabin Stays

company/people.md                team roster, roles, name spelling
company/services.md              what each brand does
company/compliance.md            compliance rules, NHC and BE only
company/writing-rules.md         universal writing rules, all brands
```

Brands do not mix. The universal writing rules apply to all three. The
compliance file applies to New Home Collective and BE Property Ventures only.
Lake Days has no compliance rules here, by owner decision. Everything under
`brands/` applies to that one brand.

Every core file opens with the same four lines: Last updated, Last verified,
Owner, Review cycle. Claims that age on their own (a closing count, an award)
keep their own verification date next to the claim as well.

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

### Duplicates: none outstanding

The five skill files listed here on 11 September 2026 were fixed before
14 September 2026. A search of all 22 organization skills on 14 September
2026 for the office phone, the three retired numbers, the office address,
the BE phone, the review claim, the closing counts, and the brand color
codes found zero copies. Every skill that needs one of those facts now
fetches it from this repo by full URL.

Two skill files still contain a stale typed value on purpose, each fenced
off by its own SKILL.md so it can never ship:

| File | Stale value | Why it is still there |
| --- | --- | --- |
| `nhc-blog-writer/references/seo-ai-checklist.md` | office phone and address in the NAP example | SKILL.md says to ignore that line and read the repo instead |
| `nhc-seller-update-report/assets/report-template.html` | office address in the signature block | SKILL.md says to replace it from the repo before rendering |

Both are candidates for a placeholder token on the next edit of those
skills. They are not a live drift risk today.

### Facts that still need a human

- `company/people.md`: roles carried over unchanged. Bob or Madison confirms.
- `company/services.md`: New Home Collective has no approved service list
  yet. Bob writes it or approves one.
- `brands/lake-days/BRAND-VOICE.md`: property facts undated, and one selling
  point changed for fair housing. Blaire confirms both.
- `brands/be/BRAND-VOICE.md`: six open items, unchanged since August.

### How edits reach main

`main` is protected. Every change goes through a pull request with one
approval, except from a repository admin. Bob's ChatGPT has write access
and edits through pull requests. Madison reviews and merges.

---

## Precedence

This file governs this repo. The app repos, `nhc-ops` and `nhc-cash-offer`,
have their own AGENTS.md files and their own conventions. Do not carry a
decision from one repo into another.
