# Prompts: Converting data from one format to another

Companion to the [data format conversion](../exercises/data-format-conversion.md)
exercise. The two routes (Option A: AI rewrites the data; Option B: AI
writes a script you run) get separate prompts here. Most of them are
also useful on their own, well outside the exercise.

Anything in `[square brackets]` is a slot for you to fill in.

## Option A: AI rewrites the data directly

Ugly Wikidata JSON to a flat CSV.

```
Below is the JSON output of a Wikidata SPARQL query. Convert it to a
flat CSV. One row per result. For each binding, take the value field
only and use the binding name as the column header. Drop URI columns
when a label column with the same prefix exists. Return only the CSV.

[paste JSON]
```

Nested API JSON to a flatter object shape.

```
Restructure this JSON so each object has only these fields, at the top
level: [id, title, creator, date, material, image_url]. Where the
source nests value under another object, pull the inner value up.
Drop any field that is null or empty. Return only the new JSON.

[paste JSON]
```

JSON to markdown documentation.

```
For each object in this JSON array, produce a markdown section. Use
the title field as a level 2 heading. List the other fields as a
definition list. If there is an image_url field, embed it as an image
at the top of the section. Keep the input order. Return only the
markdown.

[paste JSON]
```

CSV to a sequence of cards.

```
Convert this CSV into markdown. For each row produce: a level 2
heading with the title, a short paragraph combining creator and date,
then a bullet list of any remaining columns whose value is not empty.
Horizontal rule between entries.

[paste CSV]
```

## Option B: AI writes a script

The exact same conversion but as a script you can read, version, and rerun.

```
Write a small Python script that reads `query-result.json` (a Wikidata
SPARQL JSON result) and writes `query-result.csv` with one row per
result. For each binding, take the value field only and use the
binding name as the column header. Drop URI columns where there is
already a label column with the same prefix. Treat missing bindings
as empty cells. Use only the Python standard library. The script
should be runnable as `python convert.py`.
```

Same idea, JavaScript flavour, runnable in Node.

```
Write a small Node.js script that does the same conversion. Use only
built-in modules. Print a one line summary at the end: "N rows
written".
```

A script that goes the other way (CSV to clean JSON).

```
Write a Python script that reads `input.csv` and writes `output.json`
as a list of objects. Use the first row as keys. Coerce columns named
exactly [date, modified, accessioned] into ISO 8601 strings if they
parse, otherwise leave as the original string. Read and write UTF-8.
```

## Validation and sanity

Add validation to a script you already have.

```
Here is a small conversion script I am about to run on 12,000 rows.
Extend it with sanity checks that print a short report at the end:
- how many rows were skipped and why,
- how many output rows had any field that was empty,
- count of unique values in [column X],
- any row where [date field] does not parse as a date.
Do not change the conversion logic. Add the checks around it.

[paste script]
```

Sanity checking the output of an Option A conversion.

```
Here are the first 50 rows of an input CSV and the first 50 rows of
the converted JSON. Spot check them against each other. List any row
where a value looks like it was silently changed (date format, label
translation, rounding, missing field). Be specific: row number, field,
input value, output value.

[paste input rows]

[paste output rows]
```

## Round tripping (a cheap diff trick)

```
Step 1: Convert this CSV to JSON with [the conversion rules from
above].
Step 2: Convert the resulting JSON back to CSV with the inverse rules.
Step 3: Diff the original CSV against the round tripped CSV and list
every cell that changed. Explain in one line each why it changed.

[paste CSV]
```

## A vs B head to head

For the "compare the two routes" Going Further item.

```
You will do the same conversion twice on the data below.
Route A: read the data and emit the converted output directly.
Route B: write a small Python script that performs the conversion;
do not run it.
Then list the three differences you expect between the two outputs,
in your own words, before I run the script.

Conversion: [describe in one paragraph]

[paste data]
```

## Specialised format jumps

Specimen records to GeoJSON for a map.

```
Below is a JSON array of natural history specimens. Each has fields
[id, species, collected_lat, collected_lon, collected_date, country].
Write a small Python script that converts the array to a GeoJSON
FeatureCollection. Each Feature should be a Point at (lon, lat). All
other fields go into properties. Skip rows where lat or lon are
missing or non-numeric. Read/write UTF-8.
```

Bibliographic blob to clean JSON.

```
Below is messy bibliographic data (mix of BibTeX style, free text,
and inline URLs). Restructure each entry as a JSON object with these
keys: title, authors (array of strings), year (integer or null),
venue, url, type ("article" | "book" | "chapter" | "other"). If a
field is missing, omit it rather than guessing. Return only the JSON
array.

[paste bibliography]
```

CSV to QuickStatements via a script (because writing to a shared knowledge base wants a deterministic route).

```
Write a Python script that reads `objects.csv` and writes
`objects.qs` in QuickStatements v1 format. Each row creates a new
item (CREATE) with:
- Len = the title column
- Den = the description column
- P31 = the value in instance_of (already a QID)
- P195 = the value in collection (already a QID)
Skip any row with an empty title. Prepend a comment line counting
how many rows were converted and how many skipped. Do not run the
script; just write it.
```

## Suggesting the conversion

When you have data but no plan.

```
Here are five rows of a CSV I exported from a museum's collection
management system. Suggest three useful target formats I could convert
it to, why each is useful, and the rough conversion rules. Do not do
the conversion yet.

[paste 5 rows]
```

---

Related: [exercise file](../exercises/data-format-conversion.md),
[index of prompts](./index.md), [index of exercises](../exercises/index.md).
