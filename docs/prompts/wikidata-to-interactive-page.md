# Prompts: Wikidata to an interactive page

Companion to the [Wikidata to an interactive page](../exercises/wikidata-to-interactive-page.md)
exercise. These prompts cover everything from writing the SPARQL to
shipping a self contained HTML file, plus a few less obvious moves
(asking AI to critique its own visualisation, asking it to suggest a
question worth querying).

Anything in `[square brackets]` is a slot for you to fill in.

## Writing the SPARQL

Natural language to SPARQL, no preamble.

```
Write a SPARQL query for the Wikidata Query Service that returns
[what you want, in plain English]. Return only the query, with brief
comments on each line. Include the wikibase:label service. Limit to
[N] results.
```

Same idea, but stricter about what to return.

```
Write a SPARQL query for query.wikidata.org. Goal: [one sentence].
Constraints:
- Output exactly these columns: [col1, col2, col3].
- Include human readable labels in English.
- Include a LIMIT.
- No OPTIONAL blocks unless strictly needed.
Return only the query.
```

## Fixing the SPARQL

When the editor underlines something in red.

```
This SPARQL query gives the error: [paste exact error]. Fix it. Explain
in one sentence what was wrong.

[paste query]
```

When the query runs but returns nothing.

```
This query runs but returns zero rows. I expected at least a few.
Suggest two reasons it might be filtering too tightly, and rewrite the
query to be more permissive while still answering: [one sentence].

[paste query]
```

## Picking a visualisation

Useful when you have results but no idea what to do with them.

```
Here are the first five rows of a Wikidata query result:

[paste 5 rows of JSON or a screenshot of the result table]

Suggest three different ways to visualise the full result set in a
single HTML page. For each, name the JavaScript library, the chart
type, and one weakness of the choice for this specific data.
```

## Building the HTML page

The workhorse prompt for the exercise.

```
Below is a JavaScript snippet exported from the Wikidata Query Service.
Write a single self contained HTML file that runs this query in the
browser and displays the results as [a Leaflet map / a vis-timeline /
a Chart.js bar chart / a sortable HTML table]. Use CDN imports only.
No build step, no frameworks, no API keys. The file should open
directly in a browser by double clicking it. Add a small "Data:
Wikidata" credit at the bottom.

[paste the exported JS]
```

Same prompt, with extra polish baked in.

```
[as above, plus:]
Also:
- Cache the query result in a JS variable on first load; do not re-fetch
  on user interaction.
- On each item, show a tooltip with the label and a link back to its
  Wikidata page.
- Use a colour palette that works for someone with red/green colour
  blindness.
- Make the layout responsive for mobile.
```

## Iterating

Once the first version is open in a browser. Keep these short.

```
The map works. Now:
- add a filter dropdown for [property];
- when a marker is clicked, open a side panel with all fields.
```

```
The timeline is too dense. Group items by decade. Show a small bar per
decade with the count, and reveal individual items on hover.
```

## Asking for a second opinion (from the same AI)

Useful, slightly unusual.

```
Here is the HTML you wrote. Pretend you are a different AI assistant
reviewing this code for the workshop. List three concrete improvements,
ordered by impact. Do not rewrite the file; just point to lines.

[paste the HTML]
```

## Asking the AI to suggest the question

For when you do not have one yet.

```
I want to make a small interactive page from Wikidata data, in the
GLAM / cultural heritage space. Suggest five questions that:
- can be answered with a single SPARQL query under 60 seconds,
- return data that is genuinely interesting to look at (not just a list),
- and visualise well in one of: a map, a timeline, or a bar chart.
For each, give the one line description, the suggested chart type, and
the rough shape of the query.
```

## Going further

Combining two queries on one page.

```
I have two Wikidata queries. Query A returns [paintings in a museum
with coordinates of their depicted place]. Query B returns [the
birthplaces of their painters]. Write a single self contained HTML
page with a Leaflet map that shows both as separate layers with a
legend and a toggle. Use the existing exported JavaScript snippets
below verbatim.

Query A:
[paste]

Query B:
[paste]
```

Cross referencing with a museum API.

```
For each row in this Wikidata result, the column [field] contains the
museum's internal object ID. Write a JavaScript function that, given
that ID, fetches the full record from the [V&A / Wellcome / Science
Museum Group] API (see [link to that data source doc]) and returns
[image URL, full description, license]. Use only the browser fetch
API. Handle 404s gracefully.
```

---

Related: [exercise file](../exercises/wikidata-to-interactive-page.md),
[index of prompts](./index.md), [index of exercises](../exercises/index.md).
