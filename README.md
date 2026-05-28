# Workshop: AI Bridges Symposium

Materials for the workshop given by Daan van Rossum and Shani Evenstein
Sigalov at the **AI Bridges Symposium**, London, 28 May 2026.

This repository is the single place where workshop participants can find
everything they need: documentation, tools, knowledge references, exercise
descriptions, and (later) the slide deck. It is updated in the run-up to and
during the workshop.

## How to use this repository

The README you are reading is the index. Every other file in the repository is
linked from here, so you should never have to dig through folders by hand to
find something. If something is missing from this index, it is either
work in progress (not yet published) or an oversight; in the latter case
please open an issue.

## Contents

### Documentation (`docs/`)

A tree of markdown files organised by topic. Browse `docs/` directly on GitHub
or jump straight into a section below.

#### Setup (`docs/setup/`)

How to get the tools you need for the workshop running, with no local
install required. Each guide walks you through signing in, connecting
GitHub, and either working in an existing repository or creating a new
one.

- [Set up Claude Code in the browser](./docs/setup/claude-code-web.md): Anthropic's cloud coding agent at claude.ai/code.
- [Set up Jules (Google's Gemini coding agent) in the browser](./docs/setup/jules-web.md): Google's Jules at jules.google.com.
- [Set up OpenAI Codex in the browser](./docs/setup/openai-codex-web.md): OpenAI's Codex at chatgpt.com/codex.

#### Data sources (`docs/data-sources/`)

Reference notes on data sources the workshop can use: the Wikimedia projects
plus UK cultural heritage institutions whose collection data is accessible
programmatically. Use this when picking a dataset for an exercise.

- [Index of data sources](./docs/data-sources/index.md)

Wikimedia projects:

- [Wikidata](./docs/data-sources/wikidata.md)
- [Wikimedia Commons](./docs/data-sources/wikimedia-commons.md)

UK institutions with active, well documented APIs:

- [Wellcome Collection](./docs/data-sources/wellcome-collection.md)
- [Victoria and Albert Museum](./docs/data-sources/victoria-and-albert-museum.md)
- [Natural History Museum, London](./docs/data-sources/natural-history-museum-london.md)
- [Science Museum Group](./docs/data-sources/science-museum-group.md)

UK institutions, documented but with caveats:

- [British Museum](./docs/data-sources/british-museum.md)
- [National Gallery, London](./docs/data-sources/national-gallery-london.md)
- [Tate](./docs/data-sources/tate.md)

### Prompts (`docs/prompts/`)

Short, copy ready prompts grouped by the exercise they go with.
Demonstrates the variety of things a chat AI can do once you ask
precisely: write SPARQL, build self contained HTML pages, extract
QuickStatements, generate a conversion script, critique its own
output.

- [Index of prompts](./docs/prompts/index.md)
- [How to prompt](./docs/prompts/how-to-prompt.md): general advice and patterns (roast me, review what you just did, numbered improvements list, the babble prompt). Read this first.
- [Prompts for: Wikidata to an interactive page](./docs/prompts/wikidata-to-interactive-page.md)
- [Prompts for: Wikipedia to QuickStatements](./docs/prompts/wikipedia-to-quickstatements.md)
- [Prompts for: Converting data from one format to another](./docs/prompts/data-format-conversion.md)

### Slides

The slide deck will be added closer to the workshop date. This section will
link to it once it is in the repository.

### Exercises (`docs/exercises/`)

Hands on exercises participants can work through during (and after) the
workshop. Each one is self contained and pairs an open data source with an
AI assistant to produce something small and visible.

- [Index of exercises](./docs/exercises/index.md)
- [Wikidata to an interactive page](./docs/exercises/wikidata-to-interactive-page.md): query Wikidata via SPARQL, export the query as JavaScript, and ask an AI to turn the result into a self contained HTML visualisation.
- [Wikipedia to QuickStatements](./docs/exercises/wikipedia-to-quickstatements.md): take messy text from a Wikipedia article (body or references) and have an AI assistant turn it into QuickStatements, verified line by line and run against the Wikidata Sandbox before any real item.
- [Converting data from one format to another](./docs/exercises/data-format-conversion.md): take CSV, ugly JSON, or a spreadsheet and convert it to clean JSON, CSV, markdown, or QuickStatements. Compares the non-deterministic route (AI rewrites the data directly) with the deterministic route (AI writes a script you run).
- [SPARQL from a plain English question](./docs/exercises/sparql-from-a-question.md): turn a plain English question into a working SPARQL query, run it on query.wikidata.org, and iterate until the result table is what you wanted.
- [QuickStatements from your own CSV](./docs/exercises/quickstatements-from-csv.md): bring a small CSV and repeat the live demo on your own data, sandbox first.
- [QuickStatements from a prose blob](./docs/exercises/quickstatements-from-prose.md): extract claims from a museum label, catalogue entry, obituary, or press release, and run them on the Wikidata Sandbox.
- [Clean a messy spreadsheet](./docs/exercises/clean-a-messy-spreadsheet.md): clean a real spreadsheet two ways (let the AI rewrite the data, or have the AI suggest deterministic rules and write a script) and compare the routes.
- [Have the AI grill you](./docs/exercises/ai-grills-you.md): bring something you have already made and use the AI as a sceptical interviewer. The output is a sharper understanding of your own work.

### Tools

Any scripts, notebooks or helper tools provided for the workshop will be
documented from here.

## About the workshop

AI Bridges is a Wikimedia community initiative. The London symposium on
28 May 2026 brings together GLAM (galleries, libraries, archives and museums)
practitioners, Wikimedians, and AI researchers around the question of how AI
tools can responsibly support open knowledge work. This workshop is one
session inside that day.

## Status

This repository is being prepared during May 2026. Expect frequent additions
in the days leading up to the workshop. After the event the repository will
remain online as a reference.
