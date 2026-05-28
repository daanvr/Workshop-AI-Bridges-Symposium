# Exercise: QuickStatements from a prose blob

Take a piece of free text about an object, a person, or a place
(museum wall label, catalogue entry, obituary, biography sketch,
press release) and use an AI assistant to extract claims as
[QuickStatements](https://quickstatements.toolforge.org/). Run them
against the [Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189)
first.

This is the same recipe as
[Wikipedia to QuickStatements](./wikipedia-to-quickstatements.md),
but the source is anything that is *not* Wikipedia. That is the point:
the highest value claims for Wikidata often come from text that nobody
has typed into a wiki yet.

## At a glance

- **Bring**: any prose about one subject. A museum wall label, an exhibition catalogue entry, an obituary, a press release, a paragraph from a book, a printed sign you photographed.
- **Deliverable**: a verified block of QuickStatements commands, run against the [Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) (Q4115189).
- **Time**: 20 to 30 minutes.
- **AI tool**: any chat assistant that follows precise formatting (Claude, ChatGPT, Gemini, Copilot).
- **Wikidata account**: required and [autoconfirmed](https://www.wikidata.org/wiki/Wikidata:Autoconfirmed_users).

## The steps

### 1. Pick one piece of text

One subject, one source. A museum label about a single object works
well. So does a single obituary, or one catalogue entry. Two pages of
prose about ten different things is harder; start small.

### 2. Decide where the claims should land

For practice: the
[Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) (Q4115189).
For later: a real item, but only after the sandbox run worked.

### 3. Prompt the AI

Paste the text and ask for QuickStatements v2:

> Below is a [museum label / catalogue entry / obituary / press
> release / paragraph] about [subject]. Extract every factual claim
> you are confident about and output it as QuickStatements v2
> commands, one per line, tab separated, target item Q4115189 (the
> Wikidata Sandbox, for testing). Use real Wikidata property IDs (P31,
> P569, P276, and so on). For dates use the format
> `+YYYY-MM-DDT00:00:00Z/11`. For items use Q identifiers. If you are
> not sure what property or Q ID to use, leave a placeholder in
> square brackets and a comment line starting with `#`. Do not invent
> facts that are not in the source text.
>
> [paste the text]

### 4. Verify every line

Read each line against the source. Check:

- Each claim is actually in the text. Cross off anything invented.
- Property IDs (P numbers) point to the property you expect.
- Q IDs point to the right thing. Click through if you are unsure.
- Dates use `+YYYY-MM-DDT00:00:00Z/11`.
- No square bracket placeholders remain unfilled.

If a claim is in the text but the AI did not pick it up, add it by hand.

### 5. Add a source reference

Unsourced statements are a bigger problem on Wikidata than missing
ones. Ask the AI to add a reference block to each line, citing the
text you used:

> For each statement above, add a reference using S854 (reference URL)
> if a URL is available, S1476 (title), S577 (publication date) if
> known, and S248 (stated in) if the source is a Wikidata item.
> Otherwise add a brief note in a `#` comment line saying where the
> text came from.

### 6. Run on the sandbox

Open
[quickstatements.toolforge.org](https://quickstatements.toolforge.org/),
log in, **New batch**, paste into V2, **Import**, **Run**. Then check
[Q4115189](https://www.wikidata.org/wiki/Q4115189).

### 7. Move to a real item only when confident

Change the target Q ID to the actual item. Verify again. Then run.

## Tips

- **Start with text you can read fast.** A four sentence wall label is
  easier than a five page biography. You can always do a longer source next.
- **One subject per run.** If the text covers an artist and three of
  their works, do the artist first, then each work separately.
- **The AI will be more eager than you want.** It will extract claims
  that are *implied* but not *stated*. Cross those out.
- **Photograph a label, then OCR the text.** Most chat assistants will
  read an image of a museum label directly. That is often the fastest
  way to get from a museum visit to a usable text blob.

## How this differs from the Wikipedia exercise

[Wikipedia to QuickStatements](./wikipedia-to-quickstatements.md)
gives you a matching Wikidata item one click away in the sidebar. This
exercise removes that crutch: you have to identify the right item
yourself, or create one. That is closer to real GLAM workflows, where
most useful source text does not come with a Wikidata link attached.

## Going further

- Compare the AI's extraction with what is already on the existing
  Wikidata item for the subject. Any claim that is in the prose but
  not on Wikidata is a candidate addition.
- Try the same text with two different chat assistants. The
  differences in what they each extract tell you something about both
  the text and the models.
- For long sources (a full obituary, an entire catalogue entry), run
  the prompt in passes: dates first, places second, relationships
  third. Smaller passes are easier to verify.
