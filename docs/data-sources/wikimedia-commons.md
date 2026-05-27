# Wikimedia Commons

## At a glance

- **Project**: Wikimedia Commons, the Wikimedia movement's shared repository of freely licensed media.
- **Operator**: Wikimedia Foundation.
- **Scope**: Over 110 million media files: photographs, scans, audio, video, 3D models, scientific diagrams, maps, logos and more. Used by Wikipedia in 300+ languages and many other projects.
- **Licence**: Every file on Commons must be under a free licence or in the public domain. The most common are CC0, CC BY, CC BY-SA, and various Public Domain marks. Each file's licence is recorded on its file page and is also exposed through Structured Data on Commons.
- **Why this is here**: For any workshop exercise that needs openly licensed imagery at scale, Commons is the obvious entry point. It also pairs naturally with Wikidata through "Structured Data on Commons", which gives every file a unique Wikibase identifier (an M-number) and allows queries that combine media and the Wikidata knowledge graph.

## Overview

Wikimedia Commons looks like a media library to humans but, underneath, has
several useful access paths. The simplest is to treat it as files behind URLs;
the most powerful is to treat it as a Wikibase instance and query it with
SPARQL, federated with Wikidata. In between sit the MediaWiki Action API
and the IIIF wrappers used by community tools.

GLAM institutions have uploaded enormous amounts of material to Commons:
the Metropolitan Museum of Art, the Rijksmuseum, the Smithsonian, the
British Library, the Wellcome Collection, the National Library of Wales,
and many others. The presence of GLAM content makes Commons a useful
entry point even for institutions that do not publish their own API.

## API endpoints

### 1. Direct file URLs

- **Pattern (full file)**: `https://commons.wikimedia.org/wiki/Special:FilePath/{FILENAME}`
- **Pattern (thumbnail)**: `https://commons.wikimedia.org/wiki/Special:FilePath/{FILENAME}?width={N}`
- **Use**: When you already know the filename and just want to download or embed the image.

This is the simplest possible API: an HTTP GET with the file name returns the
file. It also handles the redirect to the actual storage server, so you do
not need to know about the upload host.

#### Example

```
GET https://commons.wikimedia.org/wiki/Special:FilePath/Mona_Lisa,_by_Leonardo_da_Vinci,_from_C2RMF_retouched.jpg?width=800
```

### 2. MediaWiki Action API on Commons

- **Type**: General MediaWiki API, JSON.
- **Endpoint**: `https://commons.wikimedia.org/w/api.php`
- **Use**: Search for files, list category members, get file metadata, image info (size, mime, EXIF), authoring history, and so on.

#### Example: list files in a category

```
GET https://commons.wikimedia.org/w/api.php?action=query&list=categorymembers&cmtitle=Category:Paintings_in_Tate_Britain&cmlimit=50&format=json
```

#### Example: get image info for a file

```
GET https://commons.wikimedia.org/w/api.php?action=query&titles=File:Mona_Lisa,_by_Leonardo_da_Vinci,_from_C2RMF_retouched.jpg&prop=imageinfo&iiprop=url|size|mime|extmetadata&format=json
```

The `extmetadata` field is particularly useful: it contains the licence,
attribution string, creator, source URL and other rights-related fields in
a structured form.

### 3. Wikimedia Commons Query Service (WCQS)

- **Type**: SPARQL endpoint over Structured Data on Commons (SDC).
- **Endpoint**: `https://commons-query.wikimedia.org/`
- **Authentication**: OAuth login with a Wikimedia Commons account is required (this differs from the Wikidata Query Service).
- **Update cadence**: SDC updates flow into the service within minutes; the data is also reloaded weekly from dumps on Mondays.
- **Federation**: Federates with the Wikidata Query Service, so you can join Commons files (M-IDs) and Wikidata items (Q-IDs) in a single query.
- **Documentation**: https://commons.wikimedia.org/wiki/Commons:SPARQL_query_service

The data model that WCQS queries is described in the
[Structured Data on Commons](#structured-data-on-commons-sdc) section below,
which also includes runnable example queries.

### 4. IIIF wrappers

- **Type**: Community-built IIIF Image and Presentation manifests over Commons files.
- **Tool**: https://iiif.toolforge.org/
- **Use**: When a workshop exercise wants to use a Commons file inside a IIIF viewer (Mirador, Universal Viewer) without leaving the IIIF ecosystem.

Commons itself does not natively serve IIIF, but the Toolforge IIIF service
produces valid manifests from any Commons file or category, which is enough
for most teaching cases.

### 5. Bulk dumps

- **Where**: https://dumps.wikimedia.org/commonswiki/
- **Use**: Wholesale work, training datasets, longitudinal analysis. Image files are not in the dumps (they would be enormous); instead the dumps give you the wiki text and structured data. Combine with selective downloads via Special:FilePath when you also need pixels.

## Structured Data on Commons (SDC)

For most of Commons's history every file's description page was just free-form
wikitext: templated, multilingual and almost-but-not-quite machine readable.
In 2019 the Wikimedia Foundation began rolling out **Structured Data on
Commons (SDC)**, which turns each file into a proper Wikibase entity with its
own stable identifier (an "M-ID") and a set of machine-readable statements
that use the same property vocabulary as Wikidata.

In effect, Commons is now a Wikibase instance running alongside Wikidata, and
the two can be queried together via SPARQL federation. For an AI workshop
this is one of the most useful pieces of GLAM infrastructure on the open web:
it lets you ask questions like "find me all openly licensed images of cats in
paintings" in a single query.

### The data model

- Each file on Commons is a Wikibase entity with an identifier of the form `M12345`. The M-ID is stable across renames, so it is the right thing to store if you want to refer back to a specific file later.
- Statements about the file use Wikidata properties (P-numbers). They are reused, not redefined.
- The most useful properties for workshop exercises are:
  - `P180` — **depicts**. The file shows this thing. The single most useful SDC property.
  - `P6243` — **digital representation of**. The file is a digital surrogate of this work (used heavily for paintings, manuscripts, sculptures).
  - `P170` — **creator** (of the file itself, for example the photographer or the uploader).
  - `P571` — **inception** (when the file content was created).
  - `P275` — **copyright licence**.
  - `P7482` — **source of file** (where the file originally came from, often a museum's collection website).
  - `P195` — **collection** (which institution holds the depicted work, when the file is a surrogate of a museum object).
- Files also have **captions**, which are short structured labels in any number of languages, separate from the longer wikitext description.

### How to access SDC

Two main entry points.

**SPARQL via WCQS** is best when you want to ask questions across many files
or federate with Wikidata. See the WCQS endpoint above and the example
queries below.

**The Action API** is best when you already know which file you want. The
`wbgetentities` module returns the file's structured statements:

```
GET https://commons.wikimedia.org/w/api.php?action=wbgetentities&sites=commonswiki&titles=File:Mona_Lisa,_by_Leonardo_da_Vinci,_from_C2RMF_retouched.jpg&format=json
```

The response includes captions, descriptions and a `statements` block keyed by
property ID. This is also how you can read all of a file's `depicts`
statements without writing any SPARQL.

### Depicts examples (the fun ones)

All queries below are designed to run on the
[Wikimedia Commons Query Service](https://commons-query.wikimedia.org/). You
will need to be logged in with a Commons account. The standard prefixes
(`wd:`, `wdt:`, `wikibase:`) work just like on the Wikidata Query Service.

#### 1. Cats on Commons (the hello world of `depicts`)

```sparql
SELECT ?file WHERE {
  ?file wdt:P180 wd:Q146 .          # depicts: domestic cat
}
LIMIT 25
```

Run this and you instantly get 25 random Commons files that the community has
annotated as depicting a cat. Change `Q146` to `Q144` for dogs, `Q726` for
horses, or `Q5113` for birds and you have an exercise for the rest of the
afternoon.

#### 2. Files that depict more than one thing

```sparql
SELECT ?file ?depicts1Label ?depicts2Label WHERE {
  ?file wdt:P180 wd:Q146 ;          # depicts a cat
        wdt:P180 wd:Q5318 .         # and also depicts a book
  SERVICE <https://query.wikidata.org/sparql> {
    wd:Q146 rdfs:label ?depicts1Label .
    wd:Q5318 rdfs:label ?depicts2Label .
    FILTER(LANG(?depicts1Label) = "en")
    FILTER(LANG(?depicts2Label) = "en")
  }
}
LIMIT 25
```

Cats reading books. Useful as a memorable demo of how multiple `depicts`
statements compose; swap the two Q-IDs for whatever pairing fits the audience.

#### 3. The most commonly depicted things on Commons

```sparql
SELECT ?subject ?subjectLabel (COUNT(?file) AS ?n) WHERE {
  ?file wdt:P180 ?subject .
  SERVICE <https://query.wikidata.org/sparql> {
    ?subject rdfs:label ?subjectLabel . FILTER(LANG(?subjectLabel) = "en")
  }
}
GROUP BY ?subject ?subjectLabel
ORDER BY DESC(?n)
LIMIT 50
```

What is Commons really "about"? This query gives you a peek. The top of the
list is almost always heritage architecture, common animals, and the natural
world, because those are what volunteer photographers and GLAM partners have
most enthusiastically annotated.

#### 4. Self-portraits (depicted person is also the creator)

```sparql
SELECT ?file ?personLabel WHERE {
  ?file wdt:P180 ?person ;          # depicts a person
        wdt:P170 ?person .          # whose creator is the same person
  SERVICE <https://query.wikidata.org/sparql> {
    ?person rdfs:label ?personLabel . FILTER(LANG(?personLabel) = "en")
  }
}
LIMIT 25
```

A nice teaching example because the elegant SPARQL pattern (binding `?person`
to both subject and creator) maps so neatly onto the cultural concept of a
self-portrait. The results include both classical self-portraits and modern
selfies.

#### 5. Paintings in the Tate that depict animals

```sparql
SELECT ?painting ?paintingLabel ?animalLabel ?commonsFile WHERE {
  SERVICE <https://query.wikidata.org/sparql> {
    ?painting wdt:P31 wd:Q3305213 ;          # instance of: painting
              wdt:P195 wd:Q430682 ;          # in the Tate collection
              wdt:P18 ?commonsFile .         # has a Commons image
    SERVICE wikibase:label {
      bd:serviceParam wikibase:language "en".
    }
  }
  # Pull the depicts statement from Commons
  ?file schema:contentUrl ?commonsFile ;
        wdt:P180 ?animal .
  ?animal wdt:P279* wd:Q729 .                 # subclass of: animal
  SERVICE <https://query.wikidata.org/sparql> {
    ?animal rdfs:label ?animalLabel . FILTER(LANG(?animalLabel) = "en")
  }
}
LIMIT 25
```

This one demonstrates the cross-project link: discover a painting in Wikidata,
find its Commons image, then pull the SDC `depicts` from Commons. Federation
across two SPARQL services in one query. Replace `Q729` (animal) with `Q11446`
(ship), `Q11707` (restaurant), `Q188784` (musical instrument) and so on, for
many different versions of the same exercise.

#### 6. Pictures of bicycles, ordered by when the photo was taken

```sparql
SELECT ?file ?when WHERE {
  ?file wdt:P180 wd:Q11442 ;        # depicts: bicycle
        wdt:P571 ?when .            # inception of the file content
}
ORDER BY ?when
LIMIT 50
```

Useful for showing how `depicts` combines with other SDC properties.
`P571` is how you ask "when was this picture taken" (when the data is
present). Good for time-series style explorations.

#### Two practical notes on these queries

- SDC coverage is uneven. A query that returns ten thousand results today may
  return twenty thousand in a month, simply because volunteers keep adding
  `depicts` statements. Don't treat counts as the canonical truth about a
  topic; treat them as "how much has been annotated so far".
- `depicts` is community-edited and unreviewed. A file annotated as depicting
  a cat may turn out to be something cat-adjacent. For high-stakes work, do a
  small visual sanity check on a sample before trusting the labels.

## Example workflows

### Find all paintings of the same Tate work on Commons

Use Wikidata to look up the Tate accession number, get the `P18` (image) on
Wikidata if any, and the `P973` (described at URL) to point back to Tate. If
the Wikidata item has no `P18` but does have a Commons category (`P373`),
list the files in that category via the Action API.

### Build a small image classifier dataset for a workshop

1. Pick a Wikidata category (for example "Cornish folk costume") and a date
   range.
2. Use SPARQL on Wikidata to retrieve items in that category that have a
   Commons image (`P18`) and a permissive licence.
3. Fetch the thumbnails via `Special:FilePath`, capped to a reasonable
   resolution to be polite.
4. Persist the licence and attribution string for every image, taken from
   the Action API `extmetadata` field.

### Show how GLAM uploads have grown

The Commons API can list files in a category. GLAM batch uploads almost
always group themselves under a category like `Category:Files from the V&A`
or `Category:Files from the Rijksmuseum`. Count members over time using
`categorymembers` listings.

## Licensing and what you can do with it

- **Files**: Each file has its own free licence. Most are CC0, CC BY, CC BY-SA, or PD. Read the file's licence and respect it (attribution where required, share-alike where required).
- **File metadata** (the wiki text and structured data describing each file): CC0 for the structured data; CC BY-SA 4.0 (and GFDL) for the wiki text descriptions.
- **For AI work**: CC0 and PD files are the most permissive choice for training. CC BY and CC BY-SA files require attribution; CC BY-SA in particular requires share-alike of derivatives, which has implications for downstream models.

## Fair use and etiquette

Same general rules as Wikidata. Specific notes for Commons:

- **User-Agent header is required.** Same policy as the rest of Wikimedia: include a descriptive client name, version and contact. See https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_User-Agent_Policy
- **Respect rate limits.** Three concurrent requests, under five per second for unauthenticated traffic. Honour `Retry-After` on `429` responses.
- **Don't hammer the thumbnail server for many sizes.** Pick the size you actually need and stick with it; each new size requested triggers a re-render the first time.
- **Bulk image downloads should use the dumps and the file URL service, not crawl-by-Action-API.** If you need lots of images, talk to the Commons community first: a dedicated Toolforge job often works better than scraping.
- **Carry the licence and attribution through your pipeline.** This is the part most workshop exercises forget. The `extmetadata` field gives you a canonical attribution string per file; save it next to the file.

References:

- API etiquette: https://www.mediawiki.org/wiki/API:Etiquette
- Rate limits: https://www.mediawiki.org/wiki/Wikimedia_APIs/Rate_limits
- Foundation API policy: https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_API_Usage_Guidelines

## Caveats and known issues

- **WCQS auth.** Unlike the Wikidata Query Service, the Commons SPARQL endpoint requires OAuth. Plan for the login step in any demo.
- **Filenames are unstable.** Files can be renamed; the M-ID (Wikibase ID on Commons) is the stable identifier.
- **Coverage is uneven.** Major institutions have huge Commons categories; smaller ones have very little. Check whether what you need is actually there before designing an exercise around it.
- **Structured data on Commons is still maturing.** Many files have minimal SDC, so SPARQL queries on Commons can return empty results where you would expect data. Falling back to category-based listings via the Action API is often more robust.

## Useful links

- Commons home: https://commons.wikimedia.org/
- Action API sandbox: https://commons.wikimedia.org/wiki/Special:ApiSandbox
- Structured Data on Commons (community hub): https://commons.wikimedia.org/wiki/Commons:Structured_data
- Depicts campaign and guidelines: https://commons.wikimedia.org/wiki/Commons:Depicts
- Commons SPARQL query service: https://commons.wikimedia.org/wiki/Commons:SPARQL_query_service
- Example WCQS queries: https://commons.wikimedia.org/wiki/Commons:SPARQL_query_service/queries/examples
- GLAM structured data tools: https://commons.wikimedia.org/wiki/Commons:Structured_data/GLAM/Tools
- Foundation user-agent policy: https://foundation.wikimedia.org/wiki/Policy:Wikimedia_Foundation_User-Agent_Policy
- IIIF wrapper: https://iiif.toolforge.org/
- Dumps: https://dumps.wikimedia.org/commonswiki/
