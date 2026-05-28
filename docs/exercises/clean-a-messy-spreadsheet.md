# Exercise: Clean a messy spreadsheet

Take a real, messy spreadsheet (inconsistent dates, mixed
capitalisation, weird whitespace, blank cells, duplicate rows) and use
an AI assistant to clean it. Do it two ways: once by letting the AI
rewrite the data directly (Option A), once by asking the AI to suggest
deterministic code techniques and write a script you can run and re-run
(Option B). Feel the difference.

## At a glance

- **Bring**: a messy spreadsheet of your own (10s to 100s of rows is ideal). An export from a collection management system, an acquisition log, a contact list, anything you have been avoiding cleaning.
- **Deliverable**: two cleaned versions of the same spreadsheet, plus a small script (from Option B) that you keep.
- **Time**: 30 to 60 minutes.
- **AI tool**: any chat assistant for Option A. For Option B, anything that can write a small Python or JavaScript script you then run, or an agentic coding tool that runs the script for you.

## The two options, in one paragraph

**Option A.** Paste the data into the chat. AI returns a cleaned
version. Fast. Non-deterministic. The AI may silently merge,
re-format, or fix things you did not ask it to.

**Option B.** Paste a sample. Ask the AI to *describe the cleanup
moves* in plain language, then write a deterministic script that does
them. You run the script. Same input gives the same output every
time. You keep the script.

Both produce a cleaner spreadsheet. Only one of them produces something
you can re-run on next quarter's export.

## The steps

### 1. Look at the spreadsheet first

Open it. Scroll. Note what is wrong. Likely candidates:

- Dates in different formats ("2024-01-01", "1 Jan 2024", "01/01/24").
- Names with stray whitespace, mixed case, or different separators.
- Blank rows or blank cells in required columns.
- Duplicates that are not exact duplicates ("Tate" vs "Tate Britain").
- Numbers stored as text.
- A header row that is two rows deep.

Decide what "clean" means *before* you ask the AI. Write the rules
down in one short paragraph.

### 2. Have the AI describe the cleanup moves

Before you ask for any cleaned output, ask for a plan.

> Below is a sample of a messy spreadsheet. List the specific data
> quality problems you see and, for each one, describe the
> deterministic rule that would fix it. Do not modify the data yet.
> Number the rules.
>
> [paste 20 to 50 rows]

Read the list. Tick the rules you agree with. Cross out anything the
AI hallucinated or anything you do not actually want fixed.

This step is the heart of the exercise. The AI is doing what a senior
data person would do: thinking before touching anything.

### 3a. Option A: let the AI rewrite the data directly

Paste a larger chunk of the data (or all of it if it is small) and
your edited list from step 2, and ask:

> Apply the rules in the list above to the rows below. Return the
> cleaned data as CSV. Do not change anything that is not covered by
> a rule. Do not invent values.
>
> [paste the data]

Save the result. Spot check against the original.

This is fast. It is also non-deterministic: if you re-run with the
same input next month, the AI may make different choices.

### 3b. Option B: have the AI write a deterministic script

Same edited list from step 2. Ask for a script instead of a result:

> Write a small Python script that reads `input.csv` and writes
> `cleaned.csv`. It should apply exactly the rules listed above and
> nothing else. Use only the Python standard library if possible.
> Print a short summary at the end (rows in, rows out, rows changed,
> rows dropped).

Save the script. Read it (it should be short). Run it on your data.

Now the rules are written down twice: once in plain English (your list
from step 2) and once in code. Both are reviewable. The script gives
you the same result every time, on this data and on next quarter's
export.

### 4. Compare the two outputs

Open both cleaned files side by side. Diff them if you can. Where they
disagree, work out which is right and why.

Common patterns:

- Option A "fixed" a value it shouldn't have. Option B left it alone.
- Option B failed on an edge case the rules did not cover. Option A
  handled it because the AI used judgment.
- They agree on everything important and disagree only on cosmetics.

### 5. Pick the route you would use for next quarter's export

If the answer is "I would just do it again in the chat", note that.
If the answer is "I want to re-run the script", you have your
artefact already. Save it next to the data.

## Tips

- **Sample before you scale.** Run the cleanup on 50 rows first.
  Confirm the shape of the output. Then run on the full file.
- **Watch silent type changes.** Dates become "2024-01-01" or "1 Jan
  2024" or "01/01/2024" depending on the model's mood. Decide which
  form you want and put it in the rule list.
- **Encoding matters.** If the source has accented characters, make
  sure the Option B script reads and writes UTF-8 explicitly.
- **Keep the script, not the chat transcript.** Chat transcripts
  disappear; a committed `.py` file does not.
- **Do not connect AI directly to a live database.** Always clean an
  intermediate file. Review it. Upload yourself.

## Going further

- **Round trip.** Clean the data with Option B, then ask a fresh AI
  chat to find what is still wrong with it. New eyes catch what the
  rules missed.
- **Add validation.** Extend the Option B script with sanity checks
  (every required column non-empty, every date parses, every ID
  matches a known pattern) and have it print a report.
- **Promote the rules.** Turn the numbered list from step 2 into a
  short markdown file you keep alongside the script. Next time
  someone asks "why is this column blank now?", you can show them
  the rule that did it.
- For the format conversion side of this work (CSV to JSON, JSON to
  markdown, spreadsheet to QuickStatements), see
  [data-format-conversion.md](./data-format-conversion.md).
