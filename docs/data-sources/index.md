# Data sources

This folder lists data sources that workshop participants can pull cultural
heritage data from. It contains two kinds of source:

1. **Wikimedia projects** (Wikidata and Wikimedia Commons), the open knowledge
   graph and media library of the Wikimedia movement. These are the most
   useful general-purpose starting points and the natural fit for an AI
   Bridges workshop.
2. **Individual institutions in the UK** with their own collection APIs.
   London-focused, with a UK national lens where useful.

Each source has its own file with the endpoint URLs, licensing, examples and
caveats so that participants can make an informed choice about which one to
work with. Where a source has more than one API endpoint (for example a
metadata API plus a IIIF image API) each endpoint is documented separately
inside that source's file.

## How to read these notes

For each source you will find:

- A short overview of the institution.
- Every API endpoint it exposes, with base URLs and authentication notes.
- At least one concrete request example you can paste into a browser or curl.
- Licensing of metadata and images.
- Known caveats (frozen datasets, intermittent endpoints, rate limits).
- Links to the official developer documentation.

## Scope

This list only includes institutions that publish a programmatic interface
(API, SPARQL endpoint, or downloadable structured dataset) to their
collection. Major UK museums whose collections are accessible only through a
human-facing website (for example the National Portrait Gallery London, the
Imperial War Museums, the Horniman, National Museums Scotland and the Royal
Collection Trust) are deliberately not listed here, because they are not data
sources in the sense this workshop needs. If you specifically want to work
with one of those collections, the practical route is to go through Wikidata,
Europeana or GBIF rather than the institution directly.

## Quick comparison

| Source | API status | Metadata licence | IIIF | Notes |
|---|---|---|---|---|
| [Wikidata](./wikidata.md) | Active, fully documented | CC0 | n/a (SPARQL graph) | Open knowledge graph, federates with everything |
| [Wikimedia Commons](./wikimedia-commons.md) | Active, fully documented | Per-file free licences (CC0, CC BY, CC BY-SA, PD) | Via Toolforge wrapper | 110M+ media files, federates with Wikidata |
| [Wellcome Collection](./wellcome-collection.md) | Active, well documented | Mostly open (CC0 / CC BY where applicable) | Yes (Image and Presentation) | Cleanest open API in London |
| [Victoria and Albert Museum](./victoria-and-albert-museum.md) | Active, well documented | V&A terms (personal and educational use) | Yes (Image and Presentation) | ~1M records, 470k IIIF manifests |
| [Natural History Museum, London](./natural-history-museum-london.md) | Active, well documented | Per dataset (typically CC0 or CC BY) | No (specimen data, not artworks) | Best UK natural sciences open data |
| [Science Museum Group](./science-museum-group.md) | Active, JSON:API | Split (CC0 core fields, CC BY descriptions) | Yes, but not for bulk harvest | Includes National Railway Museum, Science and Media Museum |
| [British Museum](./british-museum.md) | SPARQL endpoint, historically intermittent | Images CC BY-NC-SA 4.0; metadata via SPARQL | Yes, internal to Collection Online | Symbolic for GLAM-Wiki (first residency, 2010) |
| [National Gallery, London](./national-gallery-london.md) | Active Elasticsearch API | CC BY-NC-ND 4.0 (no derivatives) | Limited | Machine readable but not fully open |
| [Tate](./tate.md) | Frozen snapshot on GitHub | CC0 metadata | No | Last updated October 2014, great for teaching |

## Picking a source for an exercise

A few quick heuristics. **Start with Wikidata and Wikimedia Commons** when in
doubt: both are CC0 at the metadata layer, both have stable APIs that have
been used in countless exercises before, and Wikidata can act as a hub that
links out to almost every other source on this list. Use Commons whenever the
exercise needs openly licensed images at scale.

Then, for institution-specific work: use Wellcome if you want everything to
"just work" with open licences and good documentation. Use the V&A if you
want a famous London art and design collection with strong IIIF support. Use
the Natural History Museum if you want to demonstrate work on biodiversity
or specimen data instead of art. Use the Science Museum Group for
technology, industry and transport history. Use the British Museum if you
want to make the Wikimedia and GLAM-Wiki story explicit, but verify the
SPARQL endpoint is live on the day. Use Tate when you specifically want a
fully CC0 institution example and you can accept that the data is frozen at
2014.

## Responsible use

The Wikimedia projects in particular run on donated infrastructure. Every
source file on a Wikimedia project (Wikidata, Commons) includes a "Fair use
and etiquette" section covering the User-Agent header policy, concurrency
limits, and what to do for bulk work. Read it before pointing scripts at
those endpoints. The same general principles (descriptive User-Agent,
modest concurrency, honouring `Retry-After`, caching) apply to every other
source in this list as well.
