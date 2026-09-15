# Lake Days Content Skill: Instructions

This file holds the actual how-to for the lake-days-blog-writer skill. The Claude-side skill
file only points here. Edit this file to change how the skill behaves. Facts
are never repeated here. They live in the brand and company files and are
read live, every time, through the NHC Knowledge Base connector.

Last updated: 2026-09-15
Last verified: 2026-09-15
Owner: Madison Feldman
Review cycle: as needed

Supporting files for this skill live in the knowledge base too. Read each
one with the connector's get_file tool at the path shown:
- skills/lake-days-blog-writer/references/seo-ai-checklist.md

---

Produces any written content for **LakeDaysCabinStays.com**, the Lake Cumberland cabin rental brand. Blog posts get the full SEO pipeline below. Short pieces (a cabin description, a caption, two lines) skip to Step 6 and Step 7 but never skip Step 0.

For New Home Collective real estate content, use the `nhc-blog-writer` skill. Do not mix the two brands in one piece.

## Step 0: Fetch the brand file. Always. Before one word.

This skill holds no facts. Read this file now through the NHC Knowledge Base
connector's get_file tool:

brands/lake-days/BRAND-VOICE.md

Read the Property Facts section before writing anything. The cabins have no lake views, no hot tubs, and no private docks. The only rental cabins are the ones named in that file. Never invent a cabin name. Writing otherwise is false advertising and has to be rewritten before it ships.

If the connector is not enabled, ask the person to turn it on and try again.
If it is enabled and the read still fails, say so and STOP. Do not write Lake Days content from memory. Not two lines, not a caption, nothing.

Then read the writing rules the same way: company/writing-rules.md

Lake Days has no compliance rules in the repo, by owner decision. Do not read company/compliance.md.

For blog posts, also read `skills/lake-days-blog-writer/references/seo-ai-checklist.md` before finalizing.

---

## Step 1: Identify the Blog Target

Confirm before writing:

1. **Topic or keyword?** If not given, suggest 3 options based on season.
2. **Primary keyword** (exact phrase to rank for — ask if unknown)
3. **Blog type** — see list below
4. **Audience** — vacationer, family, couple, group, first-time visitor, repeat guest

### Blog Types
- Trip planning guide ("Weekend at Lake Cumberland: The Ultimate Guide")
- Local intel ("Best Restaurants Near Lake Cumberland KY")
- Cabin tips ("What to Pack for a Lake Cumberland Cabin Trip")
- Activity roundup ("Best Things to Do at Lake Cumberland")
- Booking guide ("How to Book a Lake Cumberland Cabin Rental")
- Seasonal content ("Lake Cumberland in Fall: Why It's Underrated")

---

## Step 2: Keyword Research Frame

Even without a live search tool, build the keyword strategy:

**Primary keyword** — the exact phrase, usually 3-6 words (e.g., "Lake Cumberland cabin rentals")
**Secondary keywords** — 3-5 supporting phrases (variations, related terms)
**LSI keywords** — natural language phrases an AI or Google would expect to see in this content
**Featured snippet target** — identify one question this post should own ("What is there to do at Lake Cumberland?")
**People Also Ask targets** — list 3-5 PAA questions to answer inside the post

Always include:
- Lake Cumberland (lake name every time)
- Destination-intent phrases ("cabin rental," "vacation," "getaway," "things to do")
- Seasonal modifiers when relevant ("summer," "fall," "weekend")

---

## Step 3: Blog Structure (SEO + AI Optimized)

Every post follows this structure. Do not skip sections.

### Title (H1)
- Include primary keyword near the front
- 50-60 characters ideal
- Curiosity or value hook ("Why," "How," "Best," "What," numbered lists)
- No clickbait. Real, specific, useful.

### Meta Description
- 150-160 characters
- Include primary keyword
- End with a soft CTA ("Learn more," "Start here," "See what's available")
- Written for humans, not robots

### Introduction (150-200 words)
- Open with a specific scene, moment, or statement — not a generic opener
- State what the reader will learn
- Include primary keyword naturally in first 100 words
- No "In this blog post, we will discuss..." ever

### Table of Contents (for posts 1,000+ words)
- Jump links to each H2
- Helps AI and Google parse structure

### Body Sections (H2 + H3 structure)
- Each H2 = a major topic
- Each H3 = a subtopic or supporting point
- Include primary or secondary keyword in at least 2-3 H2s naturally
- One FAQ-style H2 near the bottom (see Step 4)
- Use short paragraphs (2-4 sentences max)
- Use bullet lists and numbered lists where natural
- Bold key terms on first use
- Every 300-400 words, reset with a new H2 or visual break

### FAQ Section (required)
- H2: "Frequently Asked Questions About [Topic]"
- 3-5 Q&A pairs
- Questions formatted as People Also Ask-style questions
- Answers: 40-80 words each, direct and complete
- This section targets featured snippets and AI Overviews

### Conclusion (100-150 words)
- Summarize the value
- Include a clear CTA
  - Visit LakeDaysCabinStays.com, book now, or DM on Instagram

### Internal Links (minimum 2-3)
- Link to relevant pages already on the site
- Booking page, individual cabin pages, Instagram

### External Links (1-2)
- Link to one authoritative source (city data, tourism board, MLS stats)
- Opens in new tab
- Never link to competitors

---

## Step 4: On-Page SEO Requirements

Run every post through this before finishing:

- [ ] Passes every rule in company/writing-rules.md (read it, do not recall it)
- [ ] Primary keyword in H1 (title)
- [ ] Primary keyword in first 100 words of body
- [ ] Primary keyword in meta description
- [ ] Primary keyword in at least one H2
- [ ] Primary keyword used 3-6x total (not stuffed)
- [ ] Secondary keywords distributed naturally throughout
- [ ] All images have ALT text with keyword (note in post as `[IMAGE ALT: ...]`)
- [ ] Slug suggested: short, keyword-forward, no dates (e.g., `/neighborhoods-lexington-ky`)
- [ ] Word count 1,000-2,000 for most posts; 800+ minimum
- [ ] Schema type noted: Article, FAQPage, LocalBusiness, or Place
- [ ] Internal links included (2-3 minimum)
- [ ] External link to authority source (1)
- [ ] Meta description written (150-160 char)
- [ ] Table of contents for posts 1,000+ words

---

## Step 5: AI Search Optimization (GEO — Generative Engine Optimization)

Google AI Overviews, ChatGPT, and Perplexity pull from content that is:

**Clear and structured**
- Write like you're answering a specific question, not writing an essay
- Use headers that match how people search ("Best things to do at Lake Cumberland in the fall")
- Answer the question directly in the first sentence under each header

**Authoritative and local**
- Include real local data, real place names, real specifics
- Cite sources or stats where possible (even a year-old stat beats no stat)
- Mention Lake Cumberland specifically, plus real area names (Jamestown, Russell Springs, Burnside, Somerset)
- Never invent amenities. See the property facts in the Lake Days brand file, brands/lake-days/BRAND-VOICE.md.

**Conversational and complete**
- AI pulls complete, self-contained answers — write each FAQ answer as if it's the only thing the reader sees
- Avoid vague language ("it depends," "varies widely") — AI skips those
- Use "you" and "your" often — personalized answers get pulled more

**E-E-A-T signals (Experience, Expertise, Authoritativeness, Trust)**
- Attribute the post to a real person when possible (Bob Sophiea, Blaire Sophiea)
- Include first-hand experience statements ("We've hosted guests here since 2020...")

**Structured data notes**
- Flag FAQ sections for FAQPage schema
- Flag local business mentions for LocalBusiness schema
- Flag reviews/testimonials when included

---

## Step 6: Brand Voice

This skill holds no brand facts. Read them live, every time:

Brand voice and identity facts: brands/lake-days/BRAND-VOICE.md
Writing rules, shared by every brand: company/writing-rules.md
Lake Days has no compliance rules in the repo, by owner decision. Do not read company/compliance.md for Lake Days content. It is for the real estate brands only.

Read them live through the NHC Knowledge Base connector. Call its get_file
tool with the repo-relative path shown. There is no public web address for
these files.

If the connector is not enabled in this conversation, ask the person to turn
it on from the connectors menu, then try again. If it is enabled and a read
still fails, tell the person which file failed and stop. Do not write from
memory.


---

## Step 7: Final QA Checklist

Before delivering the post, confirm:

- [ ] Brand voice matches Lake Days (never NHC)
- [ ] Primary keyword hits confirmed (H1, intro, H2, meta)
- [ ] FAQ section included with 3-5 Q&As
- [ ] CTA included in conclusion
- [ ] Internal links noted (2-3)
- [ ] Meta description written (150-160 chars)
- [ ] Slug suggested
- [ ] Schema type flagged
- [ ] Image ALT text noted for any images mentioned
- [ ] Author attribution included
- [ ] NO claims of lake views, hot tubs, or private docks anywhere in the post
- [ ] Word count 1,000+ (or 800+ for shorter formats)

---

## Output Format

Deliver the post in this order:

```
BLOG POST: [Title]
BRAND: LakeDaysCabinStays.com
SLUG: /suggested-url-slug
META DESCRIPTION: [150-160 chars]
SCHEMA TYPE: [Article / FAQPage / LocalBusiness]
PRIMARY KEYWORD: [keyword]
WORD COUNT: ~[X]

---

[Full blog post with all headers, body, FAQ, and conclusion]

---

SEO NOTES:
- Keyword hits: [list]
- Internal link suggestions: [list]
- External link suggestion: [1 source]
- Image ALT text notes: [list]
- Schema implementation notes
```
