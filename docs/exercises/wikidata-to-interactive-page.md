# Exercise: Wikidata to an interactive page

Use the Wikidata Query Service to fetch real cultural heritage data, then ask
an AI assistant to turn that data into a self contained HTML page that
visualises it in an interesting way (a map, a timeline, a chart, a gallery).

## At a glance

- **Data source**: [Wikidata](https://www.wikidata.org/), queried via the [Wikidata Query Service](https://query.wikidata.org/) (SPARQL).
- **Deliverable**: One self contained `.html` file you can open in a browser, that shows the data from your query in a way that suits the data (map for places, timeline for dates, chart for counts, and so on).
- **Time**: 30 to 60 minutes, depending on how much you iterate.
- **AI tool**: Any chat assistant that can write code (Claude, ChatGPT, or similar). You will paste data and code into it and ask for HTML back.

## Prompts

Ready to copy prompts for every step of this exercise (writing the
SPARQL, debugging it, choosing a visualisation, building and iterating
on the HTML) live in
[../prompts/wikidata-to-interactive-page.md](../prompts/wikidata-to-interactive-page.md).
The recipe below references them where relevant.

## What you will learn

Wikidata is, in practice, the connective tissue between most of the cultural
heritage data on the open web. Once you can pull data out of it with a query
and hand the result to an AI assistant, you can build small, sharable visual
tools quickly. The point of this exercise is not to write perfect SPARQL. It
is to feel how short the path is from "a question I find interesting" to
"a working page I can show someone".

## The recipe

### 1. Find or write a query

Open [https://query.wikidata.org/](https://query.wikidata.org/). You have three ways to get a starting query:

1. **Browse the examples.** Click the *Examples* button in the toolbar. There are a few hundred curated queries grouped by theme (art, museums, science, sports, and so on). Pick one that looks close to what you want and run it.
2. **Ask an AI to write one for you.** Describe what you want in plain language ("paintings by Turner in UK collections, with their year and current location") and ask the AI to write a SPARQL query for the Wikidata Query Service. Paste the result into the editor and run it.
3. **Modify an existing query.** Start from one of the suggestions further down this page, change a property or an entity ID, and see what happens.

Whichever route you pick, do not get stuck polishing SPARQL. As soon as the
result table looks roughly right, move on.

### 2. Test it in the query service

Run the query (the blue play button on the left of the editor). You should
see a table of results below. Two things to check:

- **Does it return something?** If the result is empty, your query is filtering too tightly. Loosen a constraint and try again, or ask the AI to fix it.
- **Are the rows what you expected?** Open a few rows. Click through the entity links to confirm you are pulling the right kind of thing.

If you have geographic data, try the map view in the result toolbar (the
small icons above the table). If you have dates, try the timeline view. This
is a quick sanity check, not the final visualisation.

### 3. Export the query as JavaScript

When the result looks right, click the `</>` *Code* button in the editor
toolbar. A small panel opens with the query packaged as runnable code in
several languages. Select **JavaScript**. Copy the whole block.

What you get back is a small JavaScript snippet that hits the Wikidata Query
Service over HTTPS and returns your results as JSON. This is the bridge: it
is plain code, the AI understands it, and you can paste it straight into a
chat.

### 4. Ask the AI to build the page

Open your AI assistant and paste in the JavaScript. Then ask for an HTML
page. A prompt that works well looks roughly like this:

> Here is a JavaScript snippet that fetches data from Wikidata. Please write
> a single self contained HTML file that runs this query in the browser and
> displays the results as [a map / a timeline / a sortable table / a bar
> chart]. Use [Leaflet / vis-timeline / Chart.js / plain HTML] via CDN. No
> build step, no frameworks, no API keys. The file should open directly in
> a browser.

For a copy ready version of this prompt (and several variants for the
follow up steps below), see
[../prompts/wikidata-to-interactive-page.md](../prompts/wikidata-to-interactive-page.md).

Tell the AI what shape the data is in (you can paste a row or two from the
query result so it knows what fields it has to work with). Be explicit about
the visualisation you want and which library, otherwise the AI tends to
default to a plain table.

### 5. Save, open, iterate

Save the response as `index.html` (or whatever name you like) and open it in
a browser. From here it is iteration. Things that are worth asking for:

- Tooltips on hover with the item label and a link back to Wikidata.
- Filtering by a property (date range, type, location).
- Better styling (colours, legend, responsive layout).
- A second view of the same data (a table next to the map, for example).

Each iteration is a short message to the AI describing what to change. Do
not edit the HTML by hand unless you want to.

## Suggested query starting points

These are small, working queries you can paste straight into
[query.wikidata.org](https://query.wikidata.org/) and adapt. They are
deliberately simple. Treat them as a base camp, not the finished thing.

### Map: museums in London with coordinates

```sparql
SELECT ?museum ?museumLabel ?coord WHERE {
  ?museum wdt:P31/wdt:P279* wd:Q33506.   # instance of museum (or subclass)
  ?museum wdt:P131+ wd:Q84.              # located in London
  ?museum wdt:P625 ?coord.               # has coordinate location
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

Good for a Leaflet map with markers and pop ups. Change `Q84` (London) to
another city's Wikidata ID to retarget it, or change `Q33506` (museum) to
`Q207694` (art gallery), `Q7075` (library), or any other type.

### Timeline: works in the Tate collection

```sparql
SELECT ?work ?workLabel ?creatorLabel ?date WHERE {
  ?work wdt:P195 wd:Q430682.   # in the Tate collection
  ?work wdt:P571 ?date.        # date of inception
  OPTIONAL { ?work wdt:P170 ?creator. }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
ORDER BY ?date
LIMIT 500
```

Good for vis-timeline or a horizontal scatter. Swap `Q430682` (Tate) for
`Q213322` (V&A), `Q6373` (British Museum), `Q1419759` (Wellcome Collection)
or any other collection's Wikidata ID.

### Chart: top materials in the V&A collection

```sparql
SELECT ?materialLabel (COUNT(?work) AS ?count) WHERE {
  ?work wdt:P195 wd:Q213322.   # in the V&A collection
  ?work wdt:P186 ?material.    # made from material
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
GROUP BY ?materialLabel
ORDER BY DESC(?count)
LIMIT 20
```

Good for a Chart.js bar chart. Swap `P186` (material) for `P136` (genre),
`P135` (movement), or `P170` (creator) to count differently.

## Tips and pitfalls

**Watch the timeout.** The Wikidata Query Service kills queries after about
60 seconds. If your query times out, add a `LIMIT`, narrow the type filter,
or precompute by adding a more selective constraint near the top.

**Labels are a service, not a property.** If you forget the
`SERVICE wikibase:label { ... }` block, you will get opaque entity IDs
instead of human readable labels. Always include it.

**The export gives you a CORS friendly URL.** The exported JavaScript hits
`https://query.wikidata.org/sparql` with a GET request. It works directly
from a static HTML file with no proxy. You do not need a server.

**The AI will sometimes hallucinate properties.** If a generated query
references a property that does not exist, the editor will underline it in
red. Hover for the message, paste that back to the AI, and it usually fixes
itself.

**Cache results during iteration.** If you are iterating on the
visualisation, ask the AI to fetch once and store the result in a variable,
rather than re-fetching on every interaction. The query service is shared
infrastructure and unnecessary requests are not friendly.

**Credit the source.** Wikidata is CC0, but a small "Data: Wikidata" link
at the bottom of your page is polite and makes the page more trustworthy
when you share it.

## Going further

Once the basic page works, a few directions worth exploring:

- **Combine two queries.** Pull works from a museum and the birthplaces of their creators, and show both layers on the same map.
- **Add a search box.** Let the user type a name or a theme; rebuild the query string in JavaScript and re-run it against the endpoint.
- **Cross reference with a museum API.** Use the Wikidata IDs in your result to look up extra fields (high resolution images, full descriptions) on the museum's own API. The [data sources](../data-sources/index.md) folder lists which museums expose what.
- **Publish it.** A single HTML file is trivially hostable: drop it on GitHub Pages, Netlify, or a Wikimedia tool account, and you have a public page in minutes.
