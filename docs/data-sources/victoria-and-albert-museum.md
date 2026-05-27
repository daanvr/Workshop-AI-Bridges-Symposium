# Victoria and Albert Museum (V&A)

## At a glance

- **Institution**: Victoria and Albert Museum, the world's largest museum of applied arts, decorative arts and design.
- **Location**: Cromwell Road, South Kensington, London SW7 2RL. Additional sites at V&A East (Stratford) and V&A Dundee.
- **Focus**: Art, design, fashion, ceramics, sculpture, photography, performance.
- **Why this is on the list**: One of the few large London museums with a maintained, well documented Collections API, plus extensive IIIF coverage. The licensing is restrictive for commercial use but the API itself is open to anyone.

## Overview

The V&A holds more than 2.8 million objects. Around 1 million records are
exposed through the public Collections API, with roughly 470,000 IIIF manifests
backing the digitised images. The API was rebuilt as version 2 in 2021 and is
actively maintained. The V&A also participates in the Linked Art project and
has signalled future plans to expose data as JSON-LD.

## API endpoints

### 1. Collections API (v2)

- **Type**: REST, returns JSON and CSV.
- **Base URL**: `https://api.vam.ac.uk/v2/`
- **Authentication**: None required.
- **Main resources**: `/objects/search` (search), `/object/{systemNumber}` (single object), `/objects/cluster` (faceted clustering for visualisation).
- **Documentation**: https://developers.vam.ac.uk/guide/v2/welcome.html
- **OpenAPI specification**: available from the developer docs.

#### Example requests

Search for ceramics:

```
GET https://api.vam.ac.uk/v2/objects/search?q=ceramic&page_size=15
```

Retrieve a single object record:

```
GET https://api.vam.ac.uk/v2/object/O18762
```

Return results as CSV instead of JSON:

```
GET https://api.vam.ac.uk/v2/objects/search?q=william+morris&response_format=csv
```

The Quick Start in the developer guide includes Python examples that work
directly with pandas, so it is well suited to teaching.

### 2. IIIF Image API

- **Type**: IIIF Image API.
- **Base URL pattern**: `https://framemark.vam.ac.uk/collections/{IDENTIFIER}/{REGION}/{SIZE}/{ROTATION}/{QUALITY}.{FORMAT}`
- **Documentation**: https://developers.vam.ac.uk/guide/v2/images/iiif.html

The Collections API includes IIIF base URLs for each record that has a
digitised image. From there you can construct any standard IIIF image URL for
crops, thumbnails or full resolution downloads.

### 3. IIIF Presentation API

- **Type**: IIIF Presentation API (manifests describing multi-image objects).
- **Documentation**: https://developers.vam.ac.uk/guide/v2/images/iiif.html

Manifest URLs are returned in the Collections API record for digitised objects
and can be loaded directly into IIIF viewers.

## Licensing

- **Metadata and images**: governed by the V&A website terms of use, section 9.3 (https://www.vam.ac.uk/info/va-websites-terms-conditions). Personal and educational use is permitted. Commercial use requires a separate licence.
- This is more restrictive than CC0 or CC BY. Make sure participants who plan to publish derivative work or to use the data in commercial settings understand the difference.

## What you can do with it

Particularly strong for design, fashion and material culture exercises. The
clustering endpoint is unusual and useful for visualisation. IIIF support makes
it a good fit for image-heavy workflows (deep zoom, region cropping, training
classifiers on cropped detail).

## Caveats and known issues

- The licence is the main thing to watch. The V&A reserves commercial use, so
  the data is open to access but not fully open in the Creative Commons sense.
- Bulk export is not the API's strong point. For large datasets, the V&A asks
  you to open an issue on https://github.com/vanda/etc-docs/issues so they can
  help you.

## Useful links

- Developer portal: https://developers.vam.ac.uk/
- API guide: https://developers.vam.ac.uk/guide/v2/welcome.html
- Data explorations notebooks: https://developers.vam.ac.uk/notebooks/data-explorations/
- GitHub organisation: https://github.com/vanda
- Public collection website: https://collections.vam.ac.uk/
