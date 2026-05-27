# Exercise: Wikipedia to QuickStatements

**In one line.** Use AI to turn any unstructured text into
[QuickStatements](https://quickstatements.toolforge.org/) commands, verify
every line, and run them against the
[Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) before any
real item.

## At a glance

- **Data source**: any unstructured text. A Wikipedia article is the easiest starting point because the matching Wikidata item is one click away, but the same recipe works for a book extract, a street sign, a museum label, an obituary, or any other prose.
- **Deliverable**: a block of QuickStatements commands, run against the [Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) (Q4115189) first, then a real item if you're confident.
- **AI tool**: any chat assistant that follows precise formatting instructions (Claude, ChatGPT, or similar).
- **Wikidata account**: required, and must be [autoconfirmed](https://www.wikidata.org/wiki/Wikidata:Autoconfirmed_users) (roughly 4 days old with about 50 edits) before QuickStatements will let you run a batch.

## Prompts

Ready to copy prompts for this exercise (article body to QS, references
to QS, verification, date formatting, going back from a Wikidata item
to prose) live in
[../prompts/wikipedia-to-quickstatements.md](../prompts/wikipedia-to-quickstatements.md).
The recipe below has the two main templates inline; the prompts file
expands on them and adds more.

## The recipe in one screen

1. **Find the Wikidata item.** Open a Wikipedia article, click *Wikidata item* in the sidebar.
2. **Copy messy text.** Article body, reference list, or any other prose.
3. **Ask the AI for QuickStatements v2.** Use one of the [prompt templates](#prompt-templates) below (or pick one from [../prompts/wikipedia-to-quickstatements.md](../prompts/wikipedia-to-quickstatements.md)).
4. **Verify every line.** Property, Q ID, date format, source check.
5. **Run on the sandbox.** [quickstatements.toolforge.org](https://quickstatements.toolforge.org/) → *New batch* → paste into V2 → *Import* → *Run*. Check [Q4115189](https://www.wikidata.org/wiki/Q4115189).
6. **Move to a real item only when confident.**

That's the whole loop. The sections below expand each step.

## Why this matters

Unstructured prose is full of facts that never reach Wikidata because
converting them by hand is slow. AI does the conversion in seconds; the
human stays in the loop to verify. Wikipedia is the easiest starting
point because the matching Wikidata item is right there, even if most of
what you extract is already on it. The high value additions usually come
from text Wikipedia never covered: a book chapter, a museum wall label,
an obituary nobody has typed in yet.

## Step by step

### 1. Find the Wikidata item

**Open a Wikipedia article and click *Wikidata item* in the sidebar.**
Keep both tabs open: you'll compare them as you go.

**Practice in the sandbox first.** Use
[Q4115189](https://www.wikidata.org/wiki/Q4115189) as your target until a
full run works end to end. It is wiped periodically and exists for
exactly this.

### 2. Copy messy text

Two angles work well for a first pass. Pick one.

**Article body text.** Copy the opening paragraphs or a section like
*Early life* or *Career*. Dense with claims: dates, places, occupations,
relationships, affiliations. Good for people, organisations, events.

**Reference / sources section.** Copy the citations at the bottom. Good
for adding references to existing statements, which is one of the most
useful and most under done things on Wikidata.

**Anything else.** A book paragraph, a wall label, a sign. The recipe
doesn't change. Just paste the raw text. The AI handles the mess.

### 3. Ask the AI for QuickStatements

**Paste your text into the AI assistant and use a precise prompt.** Two
templates that work well:

#### Prompt templates

**For article body text:**

> Below is text from the Wikipedia article about [subject]. I want to add
> statements about it to the Wikidata Sandbox item Q4115189 (for testing).
> Please extract every factual claim you are confident about and output
> it as QuickStatements v2 commands, one per line, tab separated, target
> item Q4115189. Use real Wikidata property IDs (P31, P569, etc.). For
> dates use the format `+YYYY-MM-DDT00:00:00Z/11`. For items use Q
> identifiers. If you are not sure what property or Q ID to use, leave a
> placeholder in square brackets and a comment line starting with `#`.
> Do not invent facts that are not in the source text.
>
> [paste the article text here]

**For a reference list:**

> Below is the reference list from the Wikipedia article about [subject].
> For each reference, output a QuickStatements v2 line that adds it as a
> reference to a statement on Q4115189. Use the reference properties:
> S248 (stated in) when the source has a Wikidata item, S854 (reference
> URL), S1476 (title), S577 (publication date), S813 (retrieved), S407
> (language), S1433 (published in). Skip any reference you cannot parse
> cleanly. Do not invent URLs or dates.
>
> [paste the references here]

### 4. Verify every line

**Read every line the AI produced.** This is the critical step. For each
one, check:

- **Property.** "Born in London" needs P19 (place of birth), not P17 (country) or some hallucinated ID. Hover on Wikidata to see the label.
- **Q ID.** AI assistants confidently invent Q IDs. Paste each one into the Wikidata search box. If it doesn't resolve to the right entity, look it up and replace it.
- **Date format.** `+YYYY-MM-DDT00:00:00Z/11` for day, `/10` for month, `/9` for year. A bare `1955` will be rejected.
- **Source.** If the claim is not actually in the pasted text, delete the line.

**Delete anything you cannot verify.** Five clean statements beat fifty
noisy ones.

### 5. Run on the sandbox

**Go to [quickstatements.toolforge.org](https://quickstatements.toolforge.org/)** and log in (top right). Then:

1. Click *New batch*.
2. Paste into the **V2** input area (not V1).
3. Click *Import commands*.
4. Read the preview one more time.
5. Click *Run*.

**Check the result.** Open [Q4115189](https://www.wikidata.org/wiki/Q4115189),
refresh, and look for your statements. The sandbox is reset regularly,
so don't worry about clutter.

### 6. Move to a real item carefully

**Repeat steps 2 to 4 with the real Q ID** instead of Q4115189. Before
you click *Run*:

- Re-read every line, with the real subject in mind.
- Prefer additions over changes. Adding a missing reference is low risk; changing an existing date is not.
- If anything looks even slightly off, stop and check the source again.

Your edits are attributed to your account and visible in the item's
history. Be able to justify every line.

## Example output

Skim these to get a feel for the shape; adapt rather than copy.

**Adding basic claims about a person to the sandbox:**

```
Q4115189	P31	Q5	# instance of: human
Q4115189	P21	Q6581072	# sex or gender: female
Q4115189	P569	+1867-11-07T00:00:00Z/11	# date of birth
Q4115189	P19	Q270	# place of birth: Warsaw
Q4115189	P106	Q169470	# occupation: physicist
Q4115189	P166	Q38104	# award received: Nobel Prize in Physics
```

One statement per line: target, property, value, optional `#` comment.
Tab between fields (not spaces, even though it renders aligned).

**Adding a reference to an existing statement:**

```
Q4115189	P569	+1867-11-07T00:00:00Z/11	S854	"https://en.wikipedia.org/wiki/Marie_Curie"	S813	+2026-05-28T00:00:00Z/11
```

Repeat the original statement, then append reference properties prefixed
with `S`. You can stack multiple `S` properties on one line.

**Labels, descriptions, aliases:**

```
Q4115189	Len	"Test subject"	# English label
Q4115189	Den	"a sandbox item used for QuickStatements testing"	# English description
Q4115189	Aen	"QS test"	# English alias
```

`L`, `D`, `A` plus a language code writes to the multilingual fields.

## Tips and pitfalls

**Sandbox first, every time.** Even when you've done this before. The
cost is nothing.

**Tabs, not spaces.** QuickStatements v2 wants literal TAB characters
between fields. If the AI's output looks space aligned, ask it to use
real tabs and check in a plain text editor.

**Property IDs, not labels.** "date of birth" won't work; `P569` will.
Tell the AI explicitly.

**The Q ID problem.** The single most common failure. Treat every Q ID
as suspect. Verify with the search box at
[wikidata.org](https://www.wikidata.org/) or the
[Wikidata Query Service](https://query.wikidata.org/).

**Date precision matters.** `/11` = day, `/10` = month, `/9` = year. If
you only have the year, use `+1867-00-00T00:00:00Z/9`, not a fake
January 1st.

**Small batches.** Twenty to fifty statements at a time. Easy to read,
easy to roll back.

**You can stop a batch.** Hit *Stop* on the batch page; already executed
statements stay, the rest don't run.

**References > new claims.** Adding a source to an unsourced statement
is often more valuable than a new fact. A lot of Wikidata is unsourced.

**QuickStatements 3.0 is coming.** New version in development at
[qs-dev.toolforge.org](https://qs-dev.toolforge.org/). The v2 syntax
above is intended to keep working. See the
[QuickStatements 3.0 user guide](https://meta.wikimedia.org/wiki/QuickStatements_3.0/Documentation/User_guide).

## Going further

- **Improve a real item you care about.** A person, organisation, or place you know well. Fill gaps with references.
- **Batch from a Wikipedia category.** Pick a category (e.g. *British women physicists*), iterate over the articles, extract one or two key claims each.
- **Combine with SPARQL.** Query Wikidata for items missing a property (say P569 date of birth), then use the matching Wikipedia articles as input here.
- **Reverse direction.** Use AI to turn a Wikidata item *into* prose for a missing Wikipedia paragraph. Same bridge, other way.
- **Save what works.** If a prompt reliably produces clean output for a kind of subject (museums, paintings, scholarly works), share it with the workshop.
