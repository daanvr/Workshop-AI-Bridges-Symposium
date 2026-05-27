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

## More to come

Further exercises will be added in the run up to the workshop. The
[repository README](../../README.md) is the canonical index; if an exercise
is published it will be listed there too.
