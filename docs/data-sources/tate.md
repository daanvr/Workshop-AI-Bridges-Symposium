# Tate

## At a glance

- **Institution**: Tate, the United Kingdom's national collection of British art and international modern and contemporary art.
- **Locations**:
  - Tate Britain, Millbank, London SW1P 4RG.
  - Tate Modern, Bankside, London SE1 9TG.
  - Tate Liverpool.
  - Tate St Ives.
- **Focus**: Modern, contemporary and British art from the 16th century to the present.
- **Why this is on the list**: The Tate metadata dump is the most permissive (CC0) and one of the most analysed open cultural datasets in the world. The catch is that it has not been updated since October 2014.

## Overview

Tate released its collection metadata as a GitHub repository in 2013. The
dataset covers around 70,000 artworks owned or jointly owned by Tate (including
those in ARTIST ROOMS with the National Galleries of Scotland) and around
3,500 associated artists. It is released under Creative Commons Zero, meaning
participants can do anything they want with the metadata, including
commercial use.

Tate decided not to keep the dataset updated. The repository is now a frozen
snapshot of the collection as of October 2014. It is still extremely useful
for teaching, reproducible examples, and any exercise where you want a
consistent dataset of known size; it is not useful if you need to know the
current state of the collection.

## API endpoints

There is no live REST or IIIF API. The "endpoint" is the GitHub repository:

### 1. GitHub metadata repository

- **Type**: Static JSON and CSV files in a Git repository.
- **URL**: https://github.com/tategallery/collection
- **Structure**: artists in `/artists/{letter}/{slug}.json`; artworks in `/artworks/{prefix}/{group}/{accession}.json`. Flattened CSVs are also provided.
- **Licence**: CC0 metadata. Images are not included.

#### Example access

You can fetch one artwork's JSON directly:

```
GET https://raw.githubusercontent.com/tategallery/collection/master/artworks/a/000/a00001-1035.json
```

Or, more usefully, clone the whole repository and work locally:

```
git clone https://github.com/tategallery/collection.git
```

### 2. Opendatasoft mirror

- **URL**: https://public.opendatasoft.com/explore/dataset/the-tate-collection/api/
- **What it is**: A third party mirror of the Tate CSV exposed through Opendatasoft's hosted API, useful if you want HTTP queries over the data without cloning the repository yourself.
- **Caveat**: Opendatasoft is not Tate. The data is still the 2014 snapshot.

## Licensing

- **Metadata**: Creative Commons Zero (CC0). No restrictions.
- **Images**: not included in the dataset. Tate images on the website have separate copyright and reuse terms.

## What you can do with it

This is the dataset that started a small wave of cultural analytics
experiments around 2013 to 2015 (visualisations of accession patterns, gender
balance in collecting, subject co-occurrence, and so on). Excellent for
introductory data science exercises, especially anything tabular. CC0 makes
it ideal for Wikidata round trips.

## Caveats and known issues

- The data is frozen at October 2014. Anything Tate has acquired, deaccessioned
  or reattributed since then is missing or out of date. Be honest about that
  with participants.
- The repository does not contain images.
- Tate has said it has no plans to resume updating the dataset.

## Useful links

- Main GitHub repository: https://github.com/tategallery/collection
- Tate's blog post about open data: https://www.tate.org.uk/about-us/projects/transforming-tate-britain-archives-access/archives-access-project-open-data-brings
- Opendatasoft mirror: https://public.opendatasoft.com/explore/dataset/the-tate-collection/api/
- Public collection website: https://www.tate.org.uk/art
