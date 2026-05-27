# Prompts

Short, copyable prompts you can paste into a chat assistant. They are
grouped by the [exercise](../exercises/index.md) they go with, but most
of them are general enough that you can lift them straight out and use
them on your own data.

The point of this folder is to show **variety**: the same basic move
(ask AI to do a thing) can be turned into a SPARQL query, a HTML page,
a QuickStatements batch, a small Python script, a sanity check, or even
a critique of the AI's previous answer. Skim a file, find one that
looks close to what you want, copy it, change the bracketed bits, and
go.

Prompts are not holly, please modify, concatenate, compres, ...

For the why behind that, plus patterns like *roast me*, *review what
you just did*, *suggest improvements as a numbered list*, and the
*babble* prompt, see [How to prompt](./how-to-prompt.md). Read it
first if this is your first time thinking about prompts as a craft.

## Files in this folder

- [How to prompt](./how-to-prompt.md): general advice, patterns, and the most important point of all: prompts are not holy.
- [Prompts for: Wikidata to an interactive page](./wikidata-to-interactive-page.md): writing and debugging SPARQL, picking a visualisation, building self contained HTML, iteration moves.
- [Prompts for: Wikipedia to QuickStatements](./wikipedia-to-quickstatements.md): article body to QS, references to QS, verification, date formatting, going from Wikidata back to prose.
- [Prompts for: Converting data from one format to another](./data-format-conversion.md): direct (Option A) conversions, script generation (Option B), validation, round tripping, format jumps.

## How to read a prompt

Each prompt sits in a fenced block so you can copy it cleanly. Anything
in `[square brackets]` is a slot for you to fill in. Lines starting with
`>` outside the fenced block are notes from us, not part of the prompt.

```
Write [a SPARQL query / a Python script / an HTML page] that does
[the thing], using [these constraints].
```

If a prompt is doing something non obvious (asking AI to grade its own
output, comparing two routes, requesting a specific style of error
handling) there is a one line note above it saying why.

## A note on prompts as a craft

Prompts are not a magic incantation. The good ones are short, specific,
and honest about what the data actually looks like. The bad ones are
long, vague, and assume the model knows what you want. The fastest way
to get better at this is to copy a working prompt, change one thing,
and watch what changes in the output.
