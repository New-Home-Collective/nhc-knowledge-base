# NHC Knowledge Base

One place the company's facts live, so every AI tool says the same thing.

Claude, ChatGPT, and anything we adopt later all read from here. When the
office phone number changes, it changes in one file and every tool is correct
the next time it runs.

This is not an app. Nothing builds, nothing deploys, nothing writes to a
database. It is a set of written files.

**Before you change anything, read [AGENTS.md](AGENTS.md).** It holds the four
rules this repo runs on.

---

## What is in here

| Folder | What it holds |
| --- | --- |
| `brands/` | Brand voice and identity facts for New Home Collective, BE Property Ventures, and Lake Days, Cabin Stays. One file per brand. |
| `company/` | Facts that are true across all three brands. Team roster, services, compliance. |
| `voice/` | The prompts Sadie uses to answer the phone. Operational, and sensitive. |

Each file says at the top what it owns. If a fact is not in the file that owns
it, it does not exist yet, and the answer is to add it there rather than write
it down somewhere else.

---

## How a skill points at a file

A skill should never contain a fact from this repo. It should contain an
instruction to go read it.

Write it like this:

```
Read brands/nhc/BRAND-VOICE.md from the New-Home-Collective/nhc-knowledge-base
repository. Use the office phone number exactly as written in the Identity
section. Do not use a phone number from memory or from any other file.

If you cannot reach that file, say you could not reach it and stop. Do not
answer from memory.
```

Two things make that work. The skill names the file and the section, so there
is no guessing. And the skill says what to do when the read fails, which is to
stop rather than improvise.

---

## Access

The repo is private. Reading it requires access to the `New-Home-Collective`
GitHub organization.

A tool without that access will fail to read the file and will stop, which is
the behavior we want. It is not a broken skill. It is the safety rule doing
its job. The fix is to grant access, never to paste the fact into the skill.

---

## Changing a fact

1. Find the file that owns the fact.
2. Change it there.
3. Search the other repos and the skills for the old value. If a copy turns
   up, delete the copy and put a pointer in its place.
4. If the fact can go stale, update the verification date next to it.

There is no review step beyond Bob or Madison reading the change. Keep the
commit small enough that reading it is quick.
