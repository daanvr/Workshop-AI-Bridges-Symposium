# Wellcome Collection

## At a glance

- **Institution**: Wellcome Collection, part of the Wellcome Trust.
- **Location**: 183 Euston Road, London NW1 2BE.
- **Focus**: Health, medicine, the human condition. Books, manuscripts, archives, art and objects.
- **Why this is on the list**: Probably the most permissive and best documented open data offering of any cultural heritage institution in London. Open licences across most of the collection, mature IIIF support, no authentication required, all in-house code is open source under MIT.

## Overview

Wellcome Collection is a free museum and library in central London. Its data
strategy is unusually open for the UK museum sector: most of the metadata is
machine readable, most of the digitised images are openly licensed, and the
developer documentation is genuinely maintained. If you want a clean demo of
"fetch open cultural data over an API and do something with it", this is the
safest pick.

## API endpoints

Wellcome publishes more than one API. They are designed to be used together: you
discover and search using the Catalogue API, and then load images and structured
manifests using the IIIF APIs.

### 1. Catalogue API

- **Type**: REST, JSON.
- **Base URL**: `https://api.wellcomecollection.org/catalogue/v2/`
- **Authentication**: None required.
- **Main resources**: `/works` (the catalogued items), `/images` (individual images that have been catalogued), `/concepts` (subjects, people, places).
- **Documentation**: https://developers.wellcomecollection.org/docs/catalogue

#### Example request

Search for works about anatomy:

```
GET https://api.wellcomecollection.org/catalogue/v2/works?query=anatomy&pageSize=5
```

Get a single work by its identifier:

```
GET https://api.wellcomecollection.org/catalogue/v2/works/a223uyqr
```

If a work has been digitised, the response includes IIIF manifest links you can
hand straight to a IIIF viewer or to the IIIF Image API.

### 2. IIIF Image API

- **Type**: IIIF Image API, version 3 (and 2 for older content).
- **Base URL pattern**: `https://iiif.wellcomecollection.org/image/{IDENTIFIER}/{REGION}/{SIZE}/{ROTATION}/{QUALITY}.{FORMAT}`
- **Authentication**: None for openly licensed images.
- **Documentation**: https://developers.wellcomecollection.org/api/iiif

#### Example request

Get the full image at default size:

```
https://iiif.wellcomecollection.org/image/B0009453.jpg/full/full/0/default.jpg
```

Get a 400 pixel wide thumbnail:

```
https://iiif.wellcomecollection.org/image/B0009453.jpg/full/400,/0/default.jpg
```

### 3. IIIF Presentation API

- **Type**: IIIF Presentation API, used to describe digitised works with multiple pages or images.
- **Base URL pattern**: `https://iiif.wellcomecollection.org/presentation/{IDENTIFIER}`
- **Documentation**: https://developers.wellcomecollection.org/api/iiif

The Catalogue API response for a digitised work includes the Presentation
manifest URL directly. Drop that URL into any IIIF viewer (Mirador, Universal
Viewer, Clover) to render the full work with metadata, pages and search.

## Licensing

- **Metadata**: openly available through the Catalogue API.
- **Images**: most digitised images are openly licensed. Common licences are CC BY 4.0 and CC0; some content is in copyright and is not exposed through the open IIIF endpoints. Each image record carries its own licence statement, so always read the `license` field per item.
- **Software**: Wellcome publishes its services as open source under the MIT licence: https://github.com/wellcomecollection.

## What you can do with it

Suitable for almost any workshop exercise that needs cultural heritage data:
search, retrieval, image analysis, image generation with IIIF manifests,
linking to Wikidata, training a small classifier on tagged subjects, building a
Wikipedia or Wikimedia Commons enrichment pipeline.

## Caveats and known issues

- The "Wellcome Images" brand was retired several years ago. Old tutorials may
  still point at `wellcomeimages.org`; that is no longer the canonical entry
  point. Use the Catalogue API and IIIF endpoints under
  `wellcomecollection.org` instead.
- Some content (in copyright film, sensitive material, third party content) is
  catalogued but not openly available. Filter on `items.locations.license` if
  you want to be sure you only retrieve openly licensed assets.

## Useful links

- Developers home: https://developers.wellcomecollection.org/
- Catalogue API docs: https://developers.wellcomecollection.org/docs/catalogue
- IIIF docs: https://developers.wellcomecollection.org/docs/iiif
- GitHub organisation: https://github.com/wellcomecollection
- Public collection website: https://wellcomecollection.org/
