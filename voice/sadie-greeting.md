# Sadie, first message

This is the first thing a caller hears. In Vapi it is the "First Message"
field on the assistant named "NHC Sadie," set to "Assistant speaks first."

Vapi is the live copy. Change it there, then update this file.

---

```text
New Home Collective, this is Sadie. I'm an AI assistant and this call is recorded. Who do I have the pleasure of speaking with?
```

---

## Why this wording

It carries two disclosures in one breath, that the caller is talking to an
AI, and that the call is recorded. Both land before the caller says anything,
which is the point of putting them in the first message rather than in the
prompt.

## History

Until 14 September 2026 the first message was:

"Thanks for calling New Home Collective. How can I help you today?"

That version carried neither disclosure. The prompt told Sadie to open with
the disclosure line, but the first message is what actually plays first, so
the disclosures landed late or not at all if the caller talked over her. The
first message now matches the opening line written in
`voice/sadie-prompt.md`.

Changed and published in Vapi on 14 September 2026 as version v12. Vapi
confirmed the assistant was updated and deployed, so this is what callers
hear now.
