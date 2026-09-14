# NHC Knowledge Base

One place the company's facts live, so every AI tool says the same thing.

Claude, ChatGPT, and anything we adopt later all read from here. The repo is
platform neutral on purpose. No file in it names a Claude skill, a ChatGPT
action, or any other tool. A file says what is true and where the source
lives. The tool that reads it decides what to do with it.

When the office phone number changes, it changes in one file and every tool
is correct the next time it runs.

This is not an app. Nothing builds, nothing deploys, nothing writes to a
database. It is a set of written files.

**Before you change anything, read [AGENTS.md](AGENTS.md).** It holds the four
rules this repo runs on.

---

## What is in here

| Folder | What it holds |
| --- | --- |
| `brands/` | Brand voice and identity facts for New Home Collective, BE Property Ventures, and Lake Days, Cabin Stays. One file per brand. |
| `company/` | Facts that are true across all three brands. `people.md` (roster and spelling), `services.md` (what each brand does), `compliance.md` (fair housing and compliance, NHC and BE only), `writing-rules.md` (how we write). |

Each file says at the top what it owns. If a fact is not in the file that owns
it, it does not exist yet, and the answer is to add it there rather than write
it down somewhere else.

---

## How a skill or prompt points at a file

A skill, a custom GPT, or a prompt should never contain a fact from this repo.
It should contain an instruction to go read it. Give the full web address, not
a bare file path. A bare path gets misread as a local file.

Write it like this:

```
Fetch this web page:
https://raw.githubusercontent.com/New-Home-Collective/nhc-knowledge-base/main/brands/nhc/BRAND-VOICE.md

Use the office phone number exactly as written in the Identity Facts section.
Do not use a phone number from memory or from any other file.

If you cannot open that page, say so and stop. Do not answer from memory.
```

Three things make that work. The instruction says "fetch this web page," so
the tool knows it is a URL. It names the section, so there is no guessing. And
it says what to do when the read fails, which is to stop rather than improvise.

This wording is proven. It is what every Claude skill uses today, and a fresh
chat with no setup reads the files correctly with it.

---

## Access

The repo is public. Any AI tool can read these files with no account, no
invite, and no setup.

That is deliberate. Nothing in here is secret. It is brand voice, writing
rules, and fair housing rules, all of it either already public or harmless if
it were. Anything operational or sensitive belongs somewhere else. Sadie's
phone prompt used to live here and now lives in the `nhc-ops` repo.

If a read does fail, the skill still says so and stops. It never answers from
memory.

---

## Changing a fact

1. Find the file that owns the fact.
2. Change it there.
3. Search the other repos and the skills for the old value. If a copy turns
   up, delete the copy and put a pointer in its place.
4. If the fact can go stale, update the verification date next to it.

Changes to `main` go through a pull request that Madison approves. Keep each
one small enough that reading it is quick.
