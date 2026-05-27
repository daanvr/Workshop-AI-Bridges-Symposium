# Science Museum Group

## At a glance

- **Institution**: Science Museum Group, a federation of five UK museums.
- **Locations**:
  - Science Museum, London (Exhibition Road, South Kensington).
  - Science and Industry Museum, Manchester.
  - National Science and Media Museum, Bradford.
  - National Railway Museum, York.
  - Locomotion, Shildon.
- **Focus**: Science, technology, engineering, industry, transport, photography and media.
- **Why this is on the list**: Maintained JSON API following the JSONAPI specification, plus IIIF support and bulk CSV / JSON dumps for academic use.

## Overview

The Science Museum Group has the largest combined science and technology
collection in the UK. Over 500,000 objects and 50,000 archival documents are
published online out of a total collection of roughly 7 million items. The API
is straightforward, the documentation lives on GitHub, and the licensing is
split sensibly between fully open core fields and Creative Commons fields for
longer descriptive text.

## API endpoints

### 1. Collections Online API

- **Type**: REST conforming to the JSONAPI specification, JSON.
- **Base URL**: `https://collection.sciencemuseumgroup.org.uk/`
- **Authentication**: None required for reads. Be polite and rate limit.
- **Main resources**: `/search` (search across all object types), `/objects/{id}`, `/documents/{id}`, `/people/{id}`.
- **Source and documentation**: https://github.com/TheScienceMuseum/collectionsonline/wiki/Collections-Online-API

#### Example requests

Search for objects related to "engine":

```
GET https://collection.sciencemuseumgroup.org.uk/search?q=engine
```

Retrieve a single object:

```
GET https://collection.sciencemuseumgroup.org.uk/objects/co8043037
```

Add `?format=jsonapi` (or send `Accept: application/vnd.api+json`) to force
the machine readable JSON:API output.

### 2. Static dataset dumps

- **Type**: Static CSV and JSON files, plus a single CC licensed image bundle.
- **Where**: https://coimages.sciencemuseumgroup.org.uk/datasets/index.html
- **Use case**: When you want the entire public catalogue locally for analysis or to train a model.

The static dumps are a snapshot of what the API returns, so they are useful as
a stable reference and avoid hammering the live API.

### 3. IIIF endpoints

- **Type**: IIIF Image API.
- **Use**: Deep zoom in the public collection website is powered by IIIF.

The Science Museum Group has explicitly asked that images are not harvested in
bulk from the IIIF or Zoom endpoints. Use the static image dataset for bulk
work and use IIIF for interactive viewing or individual targeted requests.

## Licensing

The Group has split licensing carefully:

- **Title, made, maker and details fields**: Creative Commons Zero (CC0).
- **Descriptions and other text content**: Creative Commons Attribution 4.0 (CC BY 4.0).
- **Images**: licence varies per image. Check the `source.legal.rights.usage` field on each record.

## What you can do with it

Great for any exercise about technology, industrial history, scientific
instruments, photography, transport. The CC0 core fields make it especially
suitable for Wikimedia integration (Wikidata enrichment, Commons uploads of
properly licensed images).

## Caveats and known issues

- Images must not be harvested in bulk from the IIIF or Zoom endpoints. Use the
  static image bundle if you need many images.
- The Group reserves the right to change the API without notice.
- For significant daily exports, the Group asks you to contact them first so
  they can provide a better path than scraping.

## Useful links

- API documentation page: https://www.sciencemuseumgroup.org.uk/our-work/our-collection/using-our-collection-api
- API wiki: https://github.com/TheScienceMuseum/collectionsonline/wiki/Collections-Online-API
- Static datasets: https://coimages.sciencemuseumgroup.org.uk/datasets/index.html
- GitHub organisation: https://github.com/TheScienceMuseum
- Public collection website: https://collection.sciencemuseumgroup.org.uk/
- Digital Lab blog: https://lab.sciencemuseum.org.uk/
