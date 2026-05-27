# National Gallery, London

## At a glance

- **Institution**: The National Gallery, the United Kingdom's national collection of Western European painting from the 13th to the early 20th century.
- **Location**: Trafalgar Square, London WC2N 5DN.
- **Focus**: Painting (Botticelli, Van Eyck, Velázquez, Rembrandt, Turner, Van Gogh, and so on). The collection is small in number (~2,400 works) but very high profile.
- **Why this is on the list**: A genuine API exists, but the licence is restrictive (CC BY-NC-ND). Useful for teaching what "machine readable but not fully open" looks like in practice.

## Overview

The National Gallery exposes its catalogue through an Elasticsearch endpoint
sitting behind Knowledge Integration's CIIM middleware. This is a maintained
service. There is also an older RDF / CIDOC-CRM project visible on the
National Gallery Research Wiki, and a beta endpoint at `data.ng-london.org.uk`
which is now deprecated.

The licence is the headline caveat. Text data is published under
CC BY-NC-ND 4.0, which means no commercial use and no derivatives. For
research and educational analysis this is fine; for republishing or remixing
the data it is not.

## API endpoints

### 1. Elasticsearch API (current)

- **Type**: Elasticsearch 7.17 query syntax over HTTP.
- **Base URL**: `https://data.ng.ac.uk/es/public/_search`
- **Method**: HTTP GET or POST with a JSON Elasticsearch query as the body.
- **Output**: JSON in the CIIM middleware's standard structure.
- **Documentation**: https://www.nationalgallery.org.uk/documentation/ngacuk/collection-data/elasticsearch-api
- **Help**: https://www.nationalgallery.org.uk/documentation/ngacuk/help

#### Example request

Match against the title field:

```
GET https://data.ng.ac.uk/es/public/_search
Content-Type: application/json

{
  "query": {
    "match": {
      "title": "Sunflowers"
    }
  }
}
```

(Many HTTP clients including curl support sending a body with GET; if your
client refuses, POST will work too.)

### 2. Beta NG API (deprecated)

- **Where it used to live**: `https://data.ng-london.org.uk/`
- **Status**: No longer kept up to date. The National Gallery explicitly tells
  you not to use it for live systems.
- **Why mention it**: Older tutorials and blog posts still link to it; participants will hit those and need to know to redirect.

### 3. Linked Data / RDF

- **Status**: Discussed on the National Gallery Research Wiki (https://research.nationalgallery.org.uk/wiki/research/National_Gallery_API and https://research.ng-london.org.uk/wiki/index.php/National_Gallery_RDF). Data has been mapped to CIDOC-CRM; the public delivery of that data has changed over the years.
- **Use case**: Research projects that want CIDOC-CRM compliant statements about the collection.

## Licensing

- **Text data**: Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0).
- **Images**: high resolution images of the collection are available on the public website; reuse terms vary and are stricter than a CC BY licence. Always check per record.

## What you can do with it

- Build search and exploration interfaces over a small, high-value collection.
- Teach the difference between "open API" and "open data". The Gallery's API is
  open to use programmatically but the licence prevents derivative works.
- Combine with Wikidata, which has separately captured a great deal of National
  Gallery metadata under CC0.

## Caveats and known issues

- The CC BY-NC-ND licence prevents the most common Wikimedia uses (no
  derivatives means even basic translations and remixes are not permitted).
- Documentation is light by comparison to V&A or Wellcome; the
  Elasticsearch DSL is powerful but assumes prior familiarity.
- Old beta endpoints are still discoverable on the web. Make sure participants
  use `data.ng.ac.uk` and not `data.ng-london.org.uk`.

## Useful links

- API documentation: https://www.nationalgallery.org.uk/documentation/ngacuk/collection-data/elasticsearch-api
- Documentation hub: https://www.nationalgallery.org.uk/documentation/ngacuk/help
- Research wiki: https://research.nationalgallery.org.uk/wiki/research/National_Gallery_API
- Collection website: https://www.nationalgallery.org.uk/paintings
