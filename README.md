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
| `skills/` | Step-by-step instructions for specific jobs (bio writing, blog writing). These hold no facts. They point at `brands/` and `company/` for every fact. |

Each file says at the top what it owns. If a fact is not in the file that owns
it, it does not exist yet, and the answer is to add it there rather than write
it down somewhere else.

---

## How a skill or prompt points at a file

A skill, a custom GPT, or a prompt should never contain a fact from this repo.
It should contain an instruction to go read it through the NHC Knowledge Base
connector, using the repo-relative path.

Write it like this:

```
Read this file from the NHC Knowledge Base connector:
brands/nhc/BRAND-VOICE.md

Use the office phone number exactly as written in the Identity Facts section.
Do not use a phone number from memory or from any other file.

If the connector is not enabled, ask the person to enable it and try again.
If it is enabled and the read still fails, say so and stop. Do not answer
from memory.
```

Three things make that work. It names the connector, so the tool knows how
to get in. It names the file and the section, so there is no guessing. And it
says what to do when the read fails, which is to stop rather than improvise.

Do not use a `raw.githubusercontent.com` URL. Those never worked reliably in
chat and the repo is private now, so they do not work at all.

---

## Access

The repo is private. AI tools read it through the NHC Knowledge Base
connector, which is authenticated. Each person has to have that connector
enabled in their own Claude conversations or the skills cannot reach these
files.

Nothing in here is secret. It is brand voice, writing rules, and fair housing
rules. Private means access is deliberate, not accidental. Anything
operational or sensitive still belongs somewhere else. Sadie's phone prompt
used to live here and now lives in the `nhc-ops` repo.

If a read fails, the skill says so and stops. It never answers from memory.

---

## Changing a fact

1. Find the file that owns the fact.
2. Change it there.
3. Search the other repos and the skills for the old value. If a copy turns
   up, delete the copy and put a pointer in its place.
4. If the fact can go stale, update the verification date next to it.

Edit the file and save to `main`. No pull request, no approval. Keep each
change small enough that the next person can read it quickly.
