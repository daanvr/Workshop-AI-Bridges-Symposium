# Exercise: Converting data from one format to another

Take a dataset in one format (a CSV, a tangled blob of JSON, a spreadsheet
export) and turn it into a more useful one. Along the way, get a feel for the
difference between asking an AI to *transform* your data directly and asking
an AI to *write a script* that does the transformation for you. The two look
similar from the outside and behave very differently in practice.

## At a glance

- **Data source**: Anything tabular or structured. Recommended starting points are a [Wikidata](https://www.wikidata.org/) SPARQL query (returns deeply nested JSON), or a CSV / JSON export from one of the [museum APIs in this repository](../data-sources/index.md).
- **Deliverable**: A second file in a different format than the input. Most useful combinations are CSV to JSON, ugly JSON to readable JSON, structured data to markdown, and tabular data to Wikidata [QuickStatements](https://www.wikidata.org/wiki/Help:QuickStatements).
- **Time**: 20 to 45 minutes.
- **AI tool**: Any chat assistant for the non-deterministic route. For the deterministic route, anything that can write a small script (Python or JavaScript) that you then run yourself, or an agentic coding tool that runs the script for you.

## Prompts

Ready to copy prompts for both routes (Option A direct conversion and
Option B script generation), plus a few less obvious moves (validation,
round tripping, head to head comparison) live in
[../prompts/data-format-conversion.md](../prompts/data-format-conversion.md).
The recipe below references them where relevant.

## What you will learn

Most real work in a GLAM context starts with data in the wrong shape. The
collection management system gives you a CSV that you need as JSON for a web
page. A museum API returns deeply nested JSON when you wanted a flat table.
Someone hands you a spreadsheet that needs to become a Wikidata upload, or a
machine readable record that needs to become human readable documentation.
The conversion itself is rarely the interesting work, but it is almost always
the blocker.

This exercise has two goals. The first is practical: get comfortable using
an AI assistant to do a conversion you would otherwise put off. The second is
conceptual: see, on a small example, the difference between letting the AI
manipulate your data directly and asking it to produce a script you can
inspect, version, and re-run.

## Two ways AI can do this conversion, and why the difference matters

Before you start, it is worth being explicit about the two modes you can work
in. They produce similar looking outputs and have very different properties.

### Option A: the AI reads the data and writes the new version itself

You paste (or upload) the input data into a chat assistant and ask it to
return the converted output. The model reads your rows, "understands" them in
the loose statistical sense, and emits a new file.

This is fast and flexible. It copes with messy headers, inconsistent
capitalisation, and partial data without much instruction. It is also
**non-deterministic**: run it twice and you can get two different answers.
The model can silently:

- skip rows it finds confusing,
- merge rows it thinks are duplicates,
- "fix" what it perceives as typos in your data,
- invent fields that were not in the source,
- subtly change values (round numbers, normalise dates, translate labels).

None of this is necessarily wrong. Sometimes it is exactly what you wanted.
But you have to know it can happen, and you have to review the output before
you trust it. Treat the result the same way you would treat the work of a
fast, slightly careless intern who does not flag their assumptions.

### Option B: the AI writes a script that does the conversion

You describe the conversion in plain language and ask the AI to write a small
script (Python, JavaScript, a shell pipeline) that performs it. You then run
the script yourself, or have an agentic tool run it for you. Your data only
passes through deterministic code.

This is **deterministic**: the same input produces the same output every
time. It is easy to version (commit the script and the input file), easy to
audit (a few dozen lines of code you can read), and easy to re-run on a
larger or refreshed dataset. The trade off is that the AI has to be precise
about edge cases up front. Messy inputs may break the script in ways that
require you to iterate on the code rather than on the result.

### How to choose

A rough rule: if the dataset is small, one off, and you will manually review
every row anyway, Option A is fine. If the dataset is large, will be re-run,
will be published, or feeds into something else (a Wikidata upload, a website,
a printed catalogue), strongly prefer Option B. The case study Shani and Jonathan
have flagged for this workshop, turning an Excel sheet into a Wikidata
QuickStatements upload, is squarely Option B territory: you want a reviewable
artefact and reproducibility, not a one shot rewrite.

Whichever route you pick, the human steering the conversion is the
responsible party for what comes out the other end.

## Conversions a museum or library actually needs

To make this concrete, here are conversion jobs you might genuinely run into
at a GLAM institution. The exercise below works for any of these; pick the
one closest to your real work.

- **CSV export from a collection management system to JSON** for a small website, exhibition microsite, or interactive map.
- **Deeply nested JSON from a museum API to a flat CSV** that a curator can open in Excel and filter.
- **Spreadsheet of acquisitions or loans to Wikidata QuickStatements** for batch upload, with QIDs and property IDs filled in.
- **Bibliographic records (MARC, BibTeX, CSV) to clean JSON** for a reading list, library catalogue widget, or research bibliography.
- **Conservation reports or condition logs (JSON or Excel) to markdown** so they read as documentation rather than data dumps.
- **Audio guide script CSV with timestamps to structured JSON** for an app or a web player.
- **Specimen records from a natural history dataset to GeoJSON** for plotting collection locations on a map.
- **Donor or accession list (CSV) to a printed catalogue (markdown then PDF)**, with consistent formatting per entry.
- **Spreadsheet of objects to RDF/Turtle** for publishing as linked open data.
- **Visitor numbers CSV to a small JSON time series** that a dashboard can load.

The shapes change, the principle does not. You have data in format A, you
want format B, and you would like the conversion to be honest about what it
changes.

## The recipe

You can run this with any input you like. The walk through below uses a
[Wikidata](https://www.wikidata.org/) query because it gives you, for free, a
piece of authentically ugly JSON that almost no human enjoys reading.

### 1. Get a piece of input data

Pick one:

1. **A Wikidata SPARQL result.** Open [https://query.wikidata.org/](https://query.wikidata.org/), run a query (the [Wikidata exercise](./wikidata-to-interactive-page.md) has working starting points), and use the *Download* button to save the result as JSON or CSV. The JSON form is deliberately verbose: every cell becomes an object with `type`, `value`, and sometimes `datatype` and `xml:lang`. It is a textbook example of "machine friendly, human hostile".
2. **A CSV or JSON file from one of the documented museum APIs.** Any of the [data sources](../data-sources/index.md) in this repository will do. The [Victoria and Albert Museum](../data-sources/victoria-and-albert-museum.md), [Wellcome Collection](../data-sources/wellcome-collection.md), and [Science Museum Group](../data-sources/science-museum-group.md) all return verbose JSON that benefits from being restructured.
3. **A spreadsheet or CSV you already have.** A collection export, an acquisition list, an exhibition checklist. Use it. Real data is the most honest test of any approach.

Save the file. Look at it. Decide what the cleaner version should look like:
which fields you actually want, what the column names should be, what the
target format is.

### 2. Describe the conversion clearly, once

Before you talk to the AI, write down in one short paragraph what you want.
Be concrete about:

- the input format and roughly what it contains,
- the output format,
- which fields you want to keep, drop, or rename,
- how to handle missing values, duplicates, and edge cases.

A vague prompt produces a vague conversion. The same paragraph works for
both Option A and Option B below, so it is worth writing once.

### 3a. Try Option A (let the AI do the conversion directly)

Paste the input data (or the first few hundred lines if it is large) into a
chat assistant along with your description from step 2. Ask for the converted
output inline.

For a Wikidata JSON result, a prompt that works well looks like:

> Here is the JSON output of a Wikidata SPARQL query. I want a flat CSV with
> one row per result. For each binding, take the `value` field only and use
> the binding name as the column header. Drop the URI fields where there is
> already a label column with the same prefix. Return only the CSV.

Look at the output. Spot check a handful of rows against the original. Note
anywhere the AI silently changed something (a date format, a label
translation, a row that disappeared). That is the cost of speed; you are
allowed to pay it for small one off jobs, as long as you saw it.

### 3b. Try Option B (have the AI write a script)

Open a chat assistant (or an agentic coding tool) and ask for a script
instead of a result. Same description from step 2, different ask:

> Write a small Python script that reads `query-result.json` (a Wikidata
> SPARQL JSON result) and writes `query-result.csv` with one row per result.
> For each binding, take the `value` field only and use the binding name as
> the column header. Drop URI fields where there is already a label column
> with the same prefix. Handle missing bindings as empty cells. No
> dependencies outside the Python standard library if possible.

Save the script. Read it (it should be short). Run it. Compare the result
with what Option A gave you. Now change the input file, or add a row, or
ask the script to also write a JSON version, and rerun. Notice that you
have something you can keep, share, and put under version control.

### 4. Convert again to markdown for documentation

A conversion that often surprises people: take your structured data, in
whichever format you ended up with, and ask for **markdown**. A list of
objects becomes a sequence of small headed cards. A specimen record becomes
a readable note. A conservation log becomes documentation rather than a
spreadsheet row.

A prompt that works:

> For each object in this JSON array, produce a markdown section. Use the
> `title` field as a level 2 heading, list the other fields as a definition
> list, and put any `image_url` as an embedded image at the top of the
> section. Keep the order of the input.

This is the step that turns data into something a colleague will actually
read.

### 5. (Optional) Convert to Wikidata QuickStatements

If your input is a spreadsheet of objects you intend to upload to Wikidata,
ask the AI to write a script (Option B, please) that emits
[QuickStatements](https://www.wikidata.org/wiki/Help:QuickStatements) v1 or
CSV format. Be explicit about which columns map to which properties, what
the source reference is, and what the language tags should be. Then run the
script, review the output line by line, and upload via the QuickStatements
interface. Never connect generative AI directly to a write endpoint.

## Suggested starting prompts

These are deliberately short. Adapt the field names to your data. A
larger collection lives in
[../prompts/data-format-conversion.md](../prompts/data-format-conversion.md).

**Ugly JSON to clean JSON (restructure):**

> Restructure this JSON so each object has only the fields `id`, `title`,
> `creator`, `date`, `material`, and `image_url`. Where the source nests
> `value` under another object, pull the inner value up. Drop any field that
> is null or an empty string. Return only the new JSON.

**Clean JSON to flat CSV:**

> Convert this JSON array to CSV. One row per object. Columns in this order:
> id, title, creator, date, material, image_url. Quote any value containing
> a comma. Keep the header row.

**CSV to a sequence of markdown cards:**

> Convert this CSV into markdown. For each row, produce a level 2 heading
> with the title, then a short paragraph with creator and date, then a
> bullet list of any remaining columns whose value is not empty. Add a
> horizontal rule between entries.

**CSV to QuickStatements (script please):**

> Write a Python script that reads this CSV and writes a QuickStatements v1
> file. Each row creates a new item (`CREATE`) with `Len` set to the title,
> `Den` set to the description, `P31` set to the value in the `instance_of`
> column (already a QID), and `P195` set to the value in the `collection`
> column (already a QID). Skip any row whose title is empty. Add a comment
> at the top of the file noting how many rows were processed.

## Tips and pitfalls

**Look at the input before you prompt.** Open the file, scroll, see what is
actually in it. AI assistants are happy to describe data they have never
read; if you do not look first, you will not know whether what comes back
matches reality.

**Spot check at least a handful of output rows against the source.** Always.
Especially for the non-deterministic route. The failure mode is not "the
output looks broken"; it is "the output looks fine but two values are quietly
wrong".

**Sample a small subset first.** If you have 10,000 rows, do the conversion
on the first 50. Confirm the shape, the column names, the encoding. Then run
the script (Option B) or ask the model to do the whole batch (Option A).

**Watch out for silent type changes.** Dates become "2024-01-01" or
"1 January 2024" or "01/01/2024" depending on the model's mood. Numbers
become strings. Booleans become "true" instead of `true`. Decide which form
you want and say so in the prompt.

**Encoding matters.** If the source is UTF-8 with accented characters
(common in European collections), make sure the script reads and writes
UTF-8 explicitly. Models tend to default to ASCII safe escapes which will
mangle your `é`s and `ø`s.

**Version control the script, not the chat.** If you are doing Option B,
the script is the artefact. Save it next to the data. A chat transcript is
not a substitute for a committed file.

**Do not connect the AI directly to a live database or write endpoint.**
This is the project wide rule and it applies double here. Generate the
intermediate file. Review it. Upload yourself.

## Going further

- **Round trip the data.** Convert CSV to JSON and then back to CSV with a separate prompt. Diff the two CSVs. Anything that changed is a leak in your conversion, and the diff tells you exactly what the AI tweaked.
- **Add validation.** Ask the AI to extend the Option B script with a few sanity checks (every row has a title, every date parses, every QID matches `^Q\d+$`). Have the script print a short report at the end.
- **Try the same conversion in three formats.** Take one CSV and produce a JSON version, an XML version, and a YAML version of it with the same script. Notice which target format makes the data easier to read by hand and which makes it easier to load into other tools.
- **Compare Option A and Option B head to head.** Run the same conversion both ways on the same input. Diff the outputs. Where they disagree, work out which one is right and why. This is the cheapest possible way to feel the difference between the two modes for yourself.
