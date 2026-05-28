# Exercise: QuickStatements from your own CSV

Take a small CSV you brought with you, ask an AI to turn it into
[QuickStatements](https://quickstatements.toolforge.org/), and run it
against the
[Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) (Q4115189).
This is the live demo, repeated by you, on your own data.

## At a glance

- **Bring**: a small CSV (10 to 30 rows is ideal). A list of objects, people, books, exhibitions, places, anything structured. Use a real spreadsheet from your work if you can.
- **Deliverable**: a verified block of QuickStatements commands, executed against the Wikidata Sandbox.
- **Time**: 20 to 30 minutes.
- **AI tool**: any chat assistant that follows precise formatting (Claude, ChatGPT, Gemini, Copilot).
- **Wikidata account**: required, and must be [autoconfirmed](https://www.wikidata.org/wiki/Wikidata:Autoconfirmed_users) before QuickStatements will let you run a batch.

## Why the sandbox

The [Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) item
exists exactly so you can write garbage to a real Wikidata item
without harming anything. It is wiped periodically. Practising here
gives you the full end to end experience (auth, batch, run, verify)
with zero downside if something goes wrong.

Do not move to a real item until at least one full run on the sandbox
worked the way you expected.

## The steps

### 1. Look at your CSV

Open it. Confirm the column names. Decide which columns map to which
[Wikidata properties](https://www.wikidata.org/wiki/Wikidata:List_of_properties).
A few common ones:

- `P31` instance of
- `P17` country
- `P569` date of birth
- `P570` date of death
- `P195` collection
- `P276` location

If you do not know the property for a column, leave it. The AI can
suggest candidates, and you decide.

### 2. Describe what you want, once

Write one short paragraph that says:

- what the rows are (people, paintings, books, events),
- which columns to use,
- which property each column maps to (where you know),
- that the target item is the sandbox, Q4115189.

You will paste this together with the CSV in the next step.

### 3. Prompt the AI

Paste the description from step 2, then the CSV, and ask for
QuickStatements v2:

> Here is a CSV. Each row should become a set of QuickStatements v2
> commands that add statements to the Wikidata Sandbox item Q4115189
> (for testing). Use real Wikidata property IDs. For dates use the
> format `+YYYY-MM-DDT00:00:00Z/11`. For items use Q identifiers. If
> you are not sure what property or Q ID to use, leave a placeholder
> in square brackets and add a comment line starting with `#`. Do not
> invent values that are not in the CSV.
>
> [paste your paragraph from step 2]
>
> [paste the CSV]

### 4. Verify every line

Read each line. Check:

- Property IDs (P numbers) match what you intended.
- Q IDs point to the right thing. Click through if you are unsure.
- Dates use the `+YYYY-MM-DDT00:00:00Z/11` format.
- No placeholders in square brackets remain unfilled.
- The AI did not invent values that are not in your source data.

This is the most important step. Do not skip it.

### 5. Run on the sandbox

Open
[quickstatements.toolforge.org](https://quickstatements.toolforge.org/),
log in with your Wikidata account, click **New batch**, paste the
commands into the V2 box, **Import**, then **Run**.

Then open
[Q4115189](https://www.wikidata.org/wiki/Q4115189) and confirm the
statements are there.

### 6. Move to a real item only when confident

Once a sandbox run worked end to end and you trust the output, you
can repeat the process targeting a real item. Change the target Q ID
in your prompt and verify again before running.

## Tips

- Smaller is better for a first pass. 5 rows that work beats 100 rows
  you cannot trust.
- If a date column has mixed formats ("1923", "March 1923", "1923-03"),
  ask the AI to convert them all to the same precision before
  generating commands.
- If you are uploading references, look at the references prompt in
  [wikipedia-to-quickstatements.md](./wikipedia-to-quickstatements.md).
  The mechanics are the same.
- Never connect the AI directly to a Wikidata write endpoint. Always
  generate the QuickStatements block, review it, and paste it in yourself.

## Going further

- Convert the same CSV via two routes (let the AI write the QS
  directly, or have it write a small Python script that produces the
  QS file) and diff the two outputs. See
  [data-format-conversion.md](./data-format-conversion.md) for the
  reasoning behind the two routes.
- Add references to each statement so the import does not just put
  facts on the item but also their source.
- Once a sandbox run looks clean, prepare the same upload for a real
  item you care about, and verify a second time before running.
