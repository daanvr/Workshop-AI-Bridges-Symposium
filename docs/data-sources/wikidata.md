# Wikidata

## At a glance

- **Project**: Wikidata, the free and open knowledge base of the Wikimedia movement.
- **Operator**: Wikimedia Foundation.
- **Scope**: General. Over 116 million items covering people, places, works, scientific concepts, biological taxa, organisations, events, and almost everything else. Heavily used as the structured backbone for Wikipedia and Wikimedia Commons.
- **Licence**: All Wikidata content is released under Creative Commons Zero (CC0). You can use it for anything, including commercial use, without attribution (although attribution is appreciated).
- **Why this is here**: For an AI Bridges workshop, Wikidata is the most useful single data source on the web. It is open, structured, multilingual, linked to the GLAM sector through institutional partnerships, and connected to Wikimedia Commons for imagery. Many of the museums in the rest of this folder are partially mirrored on Wikidata under CC0, so Wikidata is often the most permissive way to work with their data.

## Overview

Wikidata is an editable knowledge graph. Every "item" has a Q-number
(`Q42` is Douglas Adams; `Q174728` is the British Museum). Items have
statements built from properties (`P31` is "instance of"; `P276` is
"location"). Statements can carry qualifiers (date ranges, sources,
certainty) and references (where the statement came from).

Wikidata is community-edited, so its quality varies. For well-covered
domains (paintings, films, scientific articles, sovereign states) coverage
is excellent. For long-tail topics coverage can be patchy. Treat it as a
fast-moving open dataset rather than a curated authority.

## API endpoints

Wikidata exposes its data through several different interfaces, each suited
to a different task. For the workshop the most useful are the SPARQL Query
Service and the simple JSON entity endpoint.

### 1. Wikidata Query Service (SPARQL)

- **Type**: SPARQL 1.1 endpoint over the full Wikidata knowledge graph.
- **Web interface**: https://query.wikidata.org/
- **Endpoint URL**: `https://query.wikidata.org/sparql`
- **Authentication**: None required for moderate use.
- **Output formats**: JSON, XML, TSV, CSV (selected via the `Accept` header or `format=` parameter).
- **Documentation**: https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service

#### Graph split (important since May 2025)

The Wikidata Query Service was split into two graphs in May 2025 because the
single graph had become too large to scale. Most workshop queries will be
fine using the standard `query.wikidata.org` endpoint, but for advanced use:

- **Main graph**: `https://query-main.wikidata.org/sparql`, everything except scholarly articles.
- **Scholarly graph**: `https://query-scholarly.wikidata.org/sparql`, only scholarly articles and related publication metadata.
- **Legacy full graph**: `https://query-legacy-full.wikidata.org/sparql`, still contains everything, available until December 2025 as a migration aid. Do not depend on it for any work that needs to run after that.
- Queries that need both halves use SPARQL federation (`SERVICE <endpoint>`).

Reference: https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/WDQS_graph_split

### 2. Entity data over HTTP (JSON, RDF, TTL)

- **Type**: Plain HTTP GET, no SPARQL needed.
- **Pattern**: `https://www.wikidata.org/wiki/Special:EntityData/{QID}.{format}`
- **Authentication**: None.
- **Formats**: `json`, `ttl`, `nt`, `rdf`, `jsonld`.

This is the fastest way to fetch one specific item without learning SPARQL.

### 3. MediaWiki Action API

- **Type**: General-purpose MediaWiki API, JSON.
- **Endpoint**: `https://www.wikidata.org/w/api.php`
- **Use**: Search, autocomplete (`wbsearchentities`), full text search across labels and descriptions, page revision history, editing (for authenticated bots).
- **Documentation**: https://www.wikidata.org/w/api.php

### 4. Bulk dumps

- **Where**: https://dumps.wikimedia.org/wikidatawiki/entities/
- **Use**: When you need the entire knowledge graph. JSON dumps are produced regularly. They are large (~100 GB compressed) but the canonical way to do any large scale Wikidata work.
- **Recommendation**: Do not scrape the API for bulk work, use a dump.

### 5. Wikidata REST API (newer)

- **Endpoint**: `https://www.wikidata.org/w/rest.php/wikibase/v1/`
- **Use**: A simpler REST surface for item retrieval, statements, descriptions and labels. Useful when you want a less verbose JSON than the Action API.
- **Documentation**: linked from https://www.wikidata.org/wiki/Wikidata:REST_API

## Example queries

These are designed to be relevant to a GLAM and AI workshop. All of them run
on https://query.wikidata.org/ unmodified.

### Paintings in the Tate

```sparql
SELECT ?painting ?paintingLabel ?creator ?creatorLabel WHERE {
  ?painting wdt:P31 wd:Q3305213 ;          # instance of: painting
            wdt:P195 wd:Q430682 .           # collection: Tate
  OPTIONAL { ?painting wdt:P170 ?creator . }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
LIMIT 50
```

### Works by Vincent van Gogh that are in London museums

```sparql
SELECT ?work ?workLabel ?collectionLabel WHERE {
  ?work wdt:P170 wd:Q5582 ;                 # creator: Van Gogh
        wdt:P195 ?collection .              # in some collection
  ?collection wdt:P131* wd:Q84 .            # collection located in London
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

### GLAM institutions with a registered Wikipedian-in-residence

```sparql
SELECT DISTINCT ?inst ?instLabel WHERE {
  ?inst wdt:P1830 ?wir .                    # owner of (a Wikipedian-in-residence relation)
  ?wir wdt:P106 wd:Q15041344 .              # occupation: Wikipedian-in-residence
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

### Counts of paintings by collection (a bar chart in the Wikidata Query Service)

```sparql
#defaultView:BarChart
SELECT ?collectionLabel (COUNT(?painting) AS ?count) WHERE {
  ?painting wdt:P31 wd:Q3305213 ;
            wdt:P195 ?collection .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
GROUP BY ?collectionLabel
ORDER BY DESC(?count)
LIMIT 25
```

### Get one item as JSON without writing SPARQL

```
GET https://www.wikidata.org/wiki/Special:EntityData/Q174728.json
```

(`Q174728` is the British Museum.)

## Licensing and what you can do with it

- **All Wikidata content**: CC0. Free to use, free to remix, no attribution
  legally required. Attribution is still appreciated and is a good practice.
- **Suitable for**: training datasets, structured enrichment of other
  collections, building knowledge graphs for retrieval-augmented generation,
  reconciling external IDs to Wikidata, multilingual labels for almost
  anything.

## Fair use and etiquette

Wikidata is run by a non-profit on donated infrastructure. Use it
considerately.

- **Set a meaningful User-Agent.** The Wikimedia Foundation User-Agent policy requires a header that identifies your client and provides a contact (email or URL). A common format is `MyWorkshopClient/0.1 (you@example.org)`. Default Python `requests` user-agents will eventually be blocked. See https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_User-Agent_Policy
- **Cap concurrency.** Three or fewer concurrent connections is the recommended ceiling for unauthenticated traffic. Keep overall request rate below five per second. Authenticated traffic can go a bit higher.
- **Respect `Retry-After`.** A `429 Too Many Requests` response includes a `Retry-After` header. Honour it.
- **For SPARQL specifically**: each query has a 60 second timeout. Heavy, repeated, or expensive queries can get your IP throttled. If your work needs more than that, run a local Blazegraph or Qlever instance from the dumps instead of pounding the public service.
- **Bulk work belongs in dumps.** If you find yourself paging through the API to retrieve more than a few thousand items, switch to a JSON dump.
- **Cache aggressively.** Re-running the same SPARQL repeatedly is wasteful. Cache results client-side.

References:

- API etiquette: https://www.mediawiki.org/wiki/API:Etiquette
- Rate limits: https://www.mediawiki.org/wiki/Wikimedia_APIs/Rate_limits
- Foundation API usage policy: https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_API_Usage_Guidelines

## Caveats and known issues

- **Coverage is uneven.** Wikidata's strength varies by domain. Well-covered: paintings, films, sovereign states, books, scientific articles. Less well-covered: contemporary objects, fashion, design furniture, intangible heritage.
- **Data is editable.** Statements can be wrong, vandalised, or out of date. For high-stakes work, take a dated dump and verify against original sources.
- **The query service split**. If you are following an older tutorial that uses scholarly article data inside a more general query, you may need to add SPARQL federation between the main and scholarly graphs.
- **Labels are language dependent.** Always include the `wikibase:label` service block (as in the examples above), or items will appear as bare Q numbers.

## Useful links

- Wikidata home: https://www.wikidata.org/
- Query service: https://query.wikidata.org/
- Query service documentation: https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service
- Tutorial: https://www.wikidata.org/wiki/Wikidata:SPARQL_tutorial
- Example queries gallery: https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/queries/examples
- Dumps: https://dumps.wikimedia.org/wikidatawiki/entities/
- WikiProject GLAM data registry: https://www.wikidata.org/wiki/Wikidata:WikiProject_GLAM_data_registry
- Foundation user-agent policy: https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_User-Agent_Policy
