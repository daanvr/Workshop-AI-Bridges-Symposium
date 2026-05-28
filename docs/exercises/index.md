# Exercises

Hands on exercises for the AI Bridges Symposium workshop. Each exercise is
self contained: it tells you what you will build, what data source you will
work with, and walks you through the steps.

You can do them in any order, and you do not need to finish one to try
another. Pick the one that lines up with what you want to learn.

## How the exercises are structured

Every exercise file follows roughly the same shape:

- **At a glance**: data source, deliverable, rough time, what AI tool you need.
- **What you will learn**: the point of the exercise, not just the steps.
- **The recipe**: numbered steps from blank page to working result.
- **Suggested starting points or variations**: small pieces you can paste and adapt.
- **Tips and pitfalls**: things that will trip you up, and how to handle them.
- **Going further**: ideas if you finish early or want to keep going after the workshop.

The exercises are designed to be doable with a chat AI (Claude, ChatGPT, or
similar) and a browser. No local setup beyond a text editor is required.

Each exercise has a companion file of copy ready prompts at
[../prompts/](../prompts/index.md). If you are mid exercise and want a
prompt template to start from, that is where to look.

## Available exercises

### [Wikidata to an interactive page](./wikidata-to-interactive-page.md)

Pull cultural heritage data out of [Wikidata](https://www.wikidata.org/)
with a SPARQL query, export the query as JavaScript from the [Wikidata
Query Service](https://query.wikidata.org/), and ask an AI assistant to
turn the result into a single self contained HTML page (map, timeline,
chart, or whatever fits the data).

- **Data source**: Wikidata.
- **Deliverable**: `index.html` you can open in a browser.
- **Good for**: anyone who wants a quick, visible result and a feel for how AI bridges open data and a working interface.

### [Wikipedia to QuickStatements](./wikipedia-to-quickstatements.md)

Take messy text from a Wikipedia article (article body or reference
list) and use an AI assistant to turn it into
[QuickStatements](https://quickstatements.toolforge.org/) commands.
Practise against the Wikidata Sandbox first, then move to a real item
when you trust the output.

- **Data source**: any Wikipedia article (prose or references).
- **Deliverable**: a verified block of QuickStatements commands, run against the [Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) (Q4115189) first.
- **Good for**: anyone who wants to feel the discipline of using AI to write to a shared knowledge base, with humans verifying every line.

### [Converting data from one format to another](./data-format-conversion.md)

Take a dataset in one format (CSV, ugly JSON from an API, a spreadsheet
export) and turn it into something more useful: clean JSON, a flat CSV,
markdown documentation, or a Wikidata QuickStatements upload. The exercise
walks through the same conversion two ways: letting the AI rewrite the data
directly (fast, non-deterministic) versus asking the AI to write a script
that does it (reproducible, reviewable), and shows you when to reach for
each.

- **Data source**: Anything tabular or structured. Examples use Wikidata SPARQL results and exports from the documented museum APIs.
- **Deliverable**: A converted file (JSON, CSV, markdown, QuickStatements) plus, in the deterministic route, a small script you keep.
- **Good for**: anyone whose real work starts with data in the wrong shape, and anyone who wants to feel the difference between AI as transformer and AI as script writer.

### [SPARQL from a plain English question](./sparql-from-a-question.md)

Have an AI write a [SPARQL](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service)
query from a plain English question, run it on
[query.wikidata.org](https://query.wikidata.org/), and iterate until
the result table is what you actually wanted.

- **Data source**: Wikidata.
- **Deliverable**: a working SPARQL query plus a result table you trust.
- **Good for**: anyone who has avoided SPARQL because the syntax looks intimidating. AI flattens the curve; you keep needing to know what you are asking for.

### [QuickStatements from your own CSV](./quickstatements-from-csv.md)

Bring a small CSV (your own work data, ideally) and repeat the live
demo: ask the AI to turn it into QuickStatements and run the result
against the Wikidata Sandbox before any real item.

- **Data source**: a CSV you bring (10 to 30 rows).
- **Deliverable**: verified QuickStatements commands, executed on the [Wikidata Sandbox](https://www.wikidata.org/wiki/Q4115189) (Q4115189).
- **Good for**: anyone who liked the demo and wants the same loop on their own data.

### [QuickStatements from a prose blob](./quickstatements-from-prose.md)

Take free text about a single subject (museum wall label, catalogue
entry, obituary, press release) and extract claims as QuickStatements.
Same recipe as the Wikipedia exercise, but the source is anything
that is not Wikipedia. That is where the highest value additions to
Wikidata usually live.

- **Data source**: any prose about one subject.
- **Deliverable**: verified QuickStatements commands with source references, run on the Wikidata Sandbox.
- **Good for**: GLAM staff sitting on labels, catalogues, and biographies that nobody has typed into a wiki yet.

### [Clean a messy spreadsheet](./clean-a-messy-spreadsheet.md)

Take a real, messy spreadsheet and clean it two ways: once by letting
the AI rewrite the data directly (non-deterministic), once by asking
the AI to suggest deterministic rules and write a script you can
re-run on next quarter's export. Feel the difference.

- **Data source**: a messy spreadsheet you bring.
- **Deliverable**: two cleaned files (one from each route) plus a small script you keep.
- **Good for**: anyone whose real work starts by cleaning a spreadsheet, and anyone who wants to feel the gap between AI as transformer and AI as script writer.

### [Have the AI grill you](./ai-grills-you.md)

Bring something you have already made (a draft, a project plan, a
dataset, an idea) and use the AI as a sceptical interviewer. The
output is a sharper understanding of your own work, not a new
artefact.

- **Data source**: anything of yours.
- **Deliverable**: a list of weaknesses, gaps, and unanswered questions, plus your answers to the ones that matter.
- **Good for**: anyone preparing to present, publish, or commit to something, and anyone curious about prompting beyond "make me a thing".

## Bring your own use case

If none of the menu options match what you actually want to try, do
that instead. The workshop is more useful when you work on something
real. Tell us what you brought; we will help you scope it down to
something you can move on in 30 minutes.

## More to come

Further exercises will be added in the run up to the workshop. The
[repository README](../../README.md) is the canonical index; if an exercise
is published it will be listed there too.
