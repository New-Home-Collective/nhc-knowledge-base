# Local Expert Content: Instructions

This file holds the actual how-to for the local-expert-content skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

---

**Before writing anything, read these three files live:**

Brand voice and identity facts: brands/nhc/BRAND-VOICE.md
Writing rules: company/writing-rules.md
Fair housing rules, mandatory every time: company/compliance.md

Read them live through the NHC Knowledge Base connector. Call its get_file
tool with the repo-relative path shown. There is no public web address for
these files.

If the connector is not enabled in this conversation, ask the person to turn
it on from the connectors menu, then try again. If it is enabled and a read
still fails, tell the person which file failed and stop. Do not write from
memory.

Use this skill to help real estate agents create posts about restaurants, neighborhoods, events, and local businesses. The goal is to make the agent look like the most connected, knowledgeable person in the area — not just a sales machine.

Local content is the #1 trust-builder that works before a buyer or seller ever reaches out.

---

## Core Rule

The agent is the local guide, not the salesperson.

No real estate pitches inside local content. The community content IS the pitch. When someone sees an agent posting authentically about their town every week, they naturally assume that agent knows the market better than anyone else.

The agent can exist in the post as a neighbor, a regular customer, a community member, or a local enthusiast. Never as a realtor trying to get a listing.

---

## Content Types

This skill handles five types of local expert content:

1. **Restaurant or food spot post** — A favorite place, hidden gem, new opening, or go-to spot
2. **Neighborhood spotlight** — What makes a specific area great to live in
3. **Local business shoutout** — Supporting a shop, service provider, or small business
4. **Community event post** — Promoting or recapping a local event, festival, market, or gathering
5. **Local guide or list post** — "5 best spots for X in [City]" style content

Read which type is needed, then follow the matching workflow below.

---

## Default Workflow

1. Identify the content type from the list above.
2. Ask clarifying questions before drafting (see section below).
3. Draft 3 options unless the agent asks for one.
4. End with improvement questions.

---

## Clarifying Questions to Ask First

Ask 3 to 6 focused questions. Pick the most useful ones for the content type.

**For restaurants and businesses:**
- Follow every rule in company/writing-rules.md. Read it, do not recall it.
- What is the name and type of place?
- What do you personally love about it?
- Is there a specific dish, product, or experience worth highlighting?
- How long have you been going there?
- Any personal story or connection to it?
- Is this a hidden gem, a local institution, or a new spot people should try?

**For neighborhoods:**
- Which neighborhood?
- What is it actually like there day to day? Walkability, noise, traffic, what is within a few minutes.
  (Ask about the PLACE, never about the people. Do not ask or answer who lives there or who it suits.)
- What are the best features — walkability, local businesses, vibe, parks, schools nearby?
- What is the price range or home style there? (Optional, only if agent offers it)
- Any specific streets, blocks, or pockets worth mentioning?
- What do people who live there say they love about it?

**For events:**
- What is the event name, date, and location?
- Who puts it on?
- What makes it worth attending?
- Has the agent been before? Any personal take?
- Is there anything attendees should know (parking, cost, what to bring)?

**For list/guide posts:**
- What is the topic of the list? (Best coffee shops, top hikes, best date nights, etc.)
- How many spots?
- What city or area?
- Any personal favorites to include?

---

## Voice Rules

Write like a neighbor recommending something to another neighbor.

**Do:**
- Use first person ("I love this place," "Every time I'm in the area...")
- Use specific details (menu items, street names, what makes it feel different)
- Keep sentences short and punchy
- Sound enthusiastic without being fake
- Use line breaks often so it reads easily on mobile
- Add a soft CTA at the end (save this post, tag a friend, drop your favorite in the comments)

**Avoid:**
- Real estate language or market updates inside local posts
- Generic language ("great place," "awesome community," "wonderful experience")
- Corporate polish or formal writing
- Hashtag overload (2 to 4 max)
- Em dashes
- Calling it a "hidden gem" if it's already well-known
- Any language that implies what kind of person should or should not live in a neighborhood (Fair Housing)

---

## Fair Housing Rules (mandatory)

These are shared across every brand and live in one place. They are not
written out here.

**Read company/compliance.md through the NHC Knowledge Base connector.**

Read it every time before writing anything that describes a home, a
neighborhood, or a buyer. If the connector is not enabled, ask the person
to turn it on. If the read still fails, say so and stop. Do not
write housing content from memory. A fair housing rule recalled wrong is a
legal problem, not an embarrassment.


## Output Format

By default, draft 3 options:

### Option 1: Personal and Story-Driven
A post built around a personal experience or memory connected to the place or neighborhood.

### Option 2: Educational or Practical
A post that teaches the audience something useful about the place (what to order, when to go, what to look for, what to expect).

### Option 3: List or Roundup Style
A short list or collection of details, tips, or highlights formatted for easy scrolling.

For each option include:
- A strong opening hook (first line must stop the scroll)
- Full post draft
- Soft CTA at the end
- 2 to 4 suggested hashtags

---

## Hook Formulas for Local Content

Use these to open posts. Never start with "I" as the very first word on Facebook or Instagram.

**Place-based hooks:**
- "If you haven't tried [Place Name] yet, we need to talk."
- "One of the most underrated spots in [City] sits right on [Street/Area]."
- "[X] years I've lived here and somehow just discovered [Place Name]."
- "The line at [Place Name] on a Saturday morning tells you everything you need to know."

**Neighborhood-based hooks:**
- "[Neighborhood Name] keeps getting better and most people still haven't figured that out."
- "Every city has that neighborhood. In [City], it's [Neighborhood Name]."
- "Spent the morning walking [Neighborhood Name] and I keep forgetting how good it is."

**Event-based hooks:**
- "This weekend only. Do not miss it."
- "If you've never been to [Event Name], this is your year."

**List-based hooks:**
- "The short list of [City] spots I actually go back to."
- "Saving this for you: the [City] [topic] list I wish I had when I moved here."

---

## Improvement Questions After Drafting

After presenting the 3 options, ask:
- Which one sounds most like you?
- Is there a specific detail you want to add that makes this feel more real?
- Is there any line that sounds too polished or fake?
- Do you want to add or remove the CTA?
- Is there a personal story or connection we can pull in?

---

## Google Authority Notes

When an agent asks about local SEO or building Google presence through local content, add this guidance:

Local content builds Google authority through relevance signals. Post consistently. Use the neighborhood name, city name, and nearby landmarks in the text. When posting to Google Business Profile, include the business or neighborhood name in the first sentence. Tag location on Instagram and Facebook. Link to the NHC website or a relevant neighborhood page when posting to the blog.

See the nhc-blog-writer skill for turning local content into full SEO blog posts for nhcnow.com.

---

## Quick Reference: Content Type Checklist

Before finalizing any draft, silently check:

- [ ] Passes every rule in company/writing-rules.md (read it, do not recall it)
- [ ] Is the agent positioned as a guide, not a salesperson?
- [ ] Is there a real, specific detail that makes this feel authentic?
- [ ] Does it pass the Fair Housing check?
- [ ] Is the reading level simple and conversational?
- [ ] Does the opening hook make someone want to keep reading?
- [ ] Is there a soft CTA?
- [ ] Would a neighbor actually share this with a friend?

If any box is unchecked, fix it before presenting.
