# Blog Writer — Instructions

This file holds the actual how-to for writing NHC blog posts for NHCnow.com.
The Claude-side skill file only points here. Edit this file to change how
blog posts get written. Facts (brand voice, phone number, address, fair
housing rules) are never repeated here. They live in brands/nhc/BRAND-VOICE.md,
company/writing-rules.md, and company/compliance.md. Read those live, every
time, before writing.

For Lake Days / Cabin Stays content, use the lake-days-blog-writer skill.
Do not mix the two brands in one post.

Last updated: 2026-09-14
Last verified: 2026-09-14
Owner: Madison Feldman
Review cycle: as needed

---

Before writing anything, read these three files live:
- Brand voice and identity facts: brands/nhc/BRAND-VOICE.md
- Writing rules: company/writing-rules.md
- Fair housing rules, mandatory every time: company/compliance.md

If you cannot open them, say so and stop. Do not write from memory.

---

## Step 1: Identify the Blog Target

Confirm before writing:
1. **Topic or keyword?** If not given, suggest 3 options based on brand and season.
2. **Primary keyword** (exact phrase to rank for, ask if unknown)
3. **Blog type** — see list below
4. **Audience** — buyer, seller, investor, agent recruit, local, relocating

### NHC Blog Types
- Neighborhood guide ("Best Neighborhoods in Lexington KY for Families")
- Market update ("Lexington KY Housing Market — [Month Year]")
- Buyer guide ("How to Buy a Home in Lexington KY")
- Seller guide ("How to Sell Your House Fast in Lexington KY")
- Cash offer explainer ("How the NHC Cash Offer Program Works")
- Lifestyle/moving guide ("Moving to Lexington KY: What to Know")
- Recruiting/agent content ("Join the Best Real Estate Team in Lexington KY")

---

## Step 2: Keyword Research Frame

Even without a live search tool, build the keyword strategy:
- **Primary keyword** — the exact phrase, usually 3-6 words
- **Secondary keywords** — 3-5 supporting phrases
- **LSI keywords** — natural language phrases an AI or Google would expect
- **Featured snippet target** — one question this post should own
- **People Also Ask targets** — 3-5 PAA questions to answer inside the post

Always include: Lexington KY (city + state), neighborhood names when
relevant, transaction-intent phrases ("buy," "sell," "homes for sale," "cash offer").

---

## Step 3: Blog Structure (SEO + AI Optimized)

Every post follows this structure. Do not skip sections.

### Title (H1)
Primary keyword near the front. 50-60 characters ideal. Curiosity or value
hook ("Why," "How," "Best," "What," numbered lists). No clickbait.

### Meta Description
150-160 characters. Include primary keyword. End with a soft CTA. Written
for humans, not robots.

### Introduction (150-200 words)
Open with a specific scene, moment, or statement, not a generic opener.
State what the reader will learn. Include primary keyword naturally in the
first 100 words. Never open with "In this blog post, we will discuss..."

### Table of Contents (for posts 1,000+ words)
Jump links to each H2. Helps AI and Google parse structure.

### Body Sections (H2 + H3 structure)
Each H2 is a major topic, each H3 a subtopic. Primary or secondary keyword
in at least 2-3 H2s naturally. One FAQ-style H2 near the bottom. Short
paragraphs (2-4 sentences max). Bullet and numbered lists where natural.
Bold key terms on first use. Reset with a new H2 or visual break every
300-400 words.

### FAQ Section (required)
H2: "Frequently Asked Questions About [Topic]." 3-5 Q&A pairs, formatted as
People Also Ask-style questions. Answers 40-80 words each, direct and
complete. Targets featured snippets and AI Overviews.

### Conclusion (100-150 words)
Summarize the value. Include a clear CTA: call/text the office line (use
the number from brands/nhc/BRAND-VOICE.md, never typed here), visit
nhcnow.com, or mention a specific service.

### Internal Links (minimum 2-3)
Link to relevant pages already on the site: neighborhood pages, cash offer
page, listings, agent profiles, awards page.

### External Links (1-2)
One authoritative source (city data, tourism board, MLS stats). Opens in
new tab. Never link to competitors.

---

## Step 4: On-Page SEO Requirements

Run every post through this before finishing:
- Passes every rule in company/writing-rules.md (read it, do not recall it)
- Primary keyword in H1 (title)
- Primary keyword in first 100 words of body
- Primary keyword in meta description
- Primary keyword in at least one H2
- Primary keyword used 3-6x total (not stuffed)
- Secondary keywords distributed naturally throughout
- All images have ALT text with keyword, noted as `[IMAGE ALT: ...]`
- Slug suggested: short, keyword-forward, no dates (e.g., `/neighborhoods-lexington-ky`)
- Word count 1,000-2,000 for most posts, 800+ minimum
- Schema type noted: Article, FAQPage, LocalBusiness, or Place
- Internal links included (2-3 minimum)
- External link to authority source (1)
- Meta description written (150-160 char)
- Table of contents for posts 1,000+ words

---

## Step 5: AI Search Optimization (GEO)

Google AI Overviews, ChatGPT, and Perplexity pull from content that is:

**Clear and structured** — write like you're answering a specific question,
not writing an essay. Headers match how people search. Answer the question
directly in the first sentence under each header.

**Authoritative and local** — include real local data, real place names,
real specifics. Cite sources or stats where possible. Mention at least one
approved stat from the Social Proof section of brands/nhc/BRAND-VOICE.md.
Pull the numbers from there, do not type them from memory.

**Conversational and complete** — write each FAQ answer as if it's the only
thing the reader sees. Avoid vague language ("it depends," "varies widely").
Use "you" and "your" often.

**E-E-A-T signals** — attribute the post to a real person when possible
(Bob Sophiea, Cameron Effoe, Blaire Sophiea). Include experience statements
grounded in an approved stat from brands/nhc/BRAND-VOICE.md. Add a brief
author bio at the bottom.

**Structured data notes** — flag FAQ sections for FAQPage schema, flag
local business mentions for LocalBusiness schema, flag reviews/testimonials
when included.

---

## Step 6: Final QA Checklist

Before delivering the post, confirm:
- Brand voice matches NHC (never Lake Days)
- Primary keyword hits confirmed (H1, intro, H2, meta)
- FAQ section included with 3-5 Q&As
- CTA included in conclusion
- Internal links noted (2-3)
- Meta description written (150-160 chars)
- Slug suggested
- Schema type flagged
- Image ALT text noted for any images mentioned
- Author attribution included
- No fair housing violations in any neighborhood content
- Word count 1,000+ (or 800+ for shorter formats)

---

## Output Format

Deliver the post in this order:

```
BLOG POST: [Title]
BRAND: NHCnow.com
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
