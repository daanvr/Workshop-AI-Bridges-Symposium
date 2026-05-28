# Exercise: SPARQL from a plain English question

Have an AI write a [SPARQL](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service)
query from a plain English question, run it on
[query.wikidata.org](https://query.wikidata.org/), and iterate until
the result table is what you actually wanted.

## At a glance

- **Bring**: a question. "Paintings by Turner in UK collections", "Female scientists born in Belgium", "Books published in 1923 in Dutch", anything specific.
- **Deliverable**: a SPARQL query that runs without errors and returns a result table you trust.
- **Time**: 15 to 30 minutes.
- **AI tool**: any chat assistant that can write code (Claude, ChatGPT, Gemini, Copilot).

## Why this exercise

SPARQL is the most powerful tool in the Wikidata stack, and the one
non-coders avoid hardest. AI flattens the learning curve. You stop
needing to remember property numbers and prefix declarations. You
keep needing to know *what you are asking for*.

## The steps

### 1. Write your question in one sentence

Be specific. Vague questions produce vague queries.

Bad: "Stuff about Picasso."

Better: "Paintings by Picasso held in French public collections, with
the year painted and the current location."

Even better: add a soft limit. "First 100 results."

### 2. Ask the AI to draft a query

Open a chat assistant. Use a prompt like:

> Write a SPARQL query for the Wikidata Query Service that answers
> the following question. Use only properties and entities you are
> confident about. Add a `LIMIT 100` at the end. Add brief comments
> with `#` explaining each non-obvious line.
>
> Question: [your question]

### 3. Paste it into query.wikidata.org and run it

Open [https://query.wikidata.org/](https://query.wikidata.org/),
paste the query into the editor, and click the blue play button.

One of three things happens:

- **The query errors.** Read the error, paste it back to the AI, ask for a fix.
- **The query runs but returns zero rows.** Probably over filtered. Tell the AI: "Returns zero rows. Loosen the constraints."
- **The query runs and returns rows.** Look at them.

### 4. Sanity check the rows

Click through two or three rows. Are they actually what you asked for?
A query that returns 200 results that look right is worth more than
one that returns 5000 results you cannot verify.

Common things to spot:

- Wrong language labels (you wanted English, you got German).
- Wrong type of thing (you asked for paintings, you got prints too).
- Missing values where you expected one (a column full of blanks).

### 5. Iterate

Tell the AI what is wrong. Plain language is fine.

> The results include sculptures, but I only want paintings.

> Most of the rows are missing a date. Make the date optional and
> still return the row.

> Add a column for the museum's Wikidata QID, not just the label.

Paste each new query back into the editor and re-run.

### 6. Try a view that fits the data

Above the result table on
[query.wikidata.org](https://query.wikidata.org/) there are small
icons: table, image grid, bubble chart, map, timeline. If your data
has locations or dates, try the matching view. This is free, and
often surprising.

### 7. (Optional) Export

When the result looks right, click the `</>` *Code* button. Copy the
JavaScript snippet. You now have a piece of code that hits the
Wikidata Query Service and returns your data. This is the input to
the [Wikidata to an interactive page](./wikidata-to-interactive-page.md)
exercise. The two link directly.

## Tips

- **Look at example queries first.** The *Examples* button in the
  toolbar at [query.wikidata.org](https://query.wikidata.org/) has
  hundreds of curated queries grouped by theme. Skimming a few gives
  you a feel for what is possible.
- **Tell the AI when the result is wrong, do not start over.** A
  follow up like "you returned 5 rows, I expected hundreds" is faster
  than re-writing the prompt from scratch.
- **Property IDs (P31, P276, and so on) are easy to look up.** Open
  the property's page on Wikidata and check the description. The AI
  will sometimes confidently use the wrong P number. Verifying takes
  seconds.
- **Comments help future you.** Ask the AI to leave the `#` comments
  in. The query becomes a small readable artefact you can come back to.

## Going further

- Take the working query into the
  [Wikidata to an interactive page](./wikidata-to-interactive-page.md)
  exercise and turn the results into a self contained HTML view.
- Run the same question twice with different chat assistants. Compare
  the two queries. The differences are usually instructive.
- Add a federated query (the `SERVICE` keyword) that pulls in data
  from another endpoint, for example a museum's own SPARQL endpoint.
  Ask the AI to write it; you only need to know the endpoint URL.
- Ask the AI for the same question expressed in two different ways
  (one starting from people, one starting from works) and compare
  what changes.
