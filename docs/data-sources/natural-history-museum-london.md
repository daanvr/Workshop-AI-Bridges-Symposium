# Natural History Museum, London

## At a glance

- **Institution**: Natural History Museum, one of the largest natural history collections in the world.
- **Location**: Cromwell Road, South Kensington, London SW7 5BD.
- **Focus**: Botany, entomology, mineralogy, palaeontology, zoology. Specimens, not artworks.
- **Why this is on the list**: The Data Portal is a genuine open data platform built on CKAN, with a maintained REST API, no authentication for reads, and tens of millions of specimen records. Probably the strongest pure open data offering of any UK museum.

## Overview

The Natural History Museum publishes its scientific collection data through a
Data Portal built on the open source CKAN platform. The portal is the same
software the UK Government uses for `data.gov.uk`, so the data is well
structured and well behaved. The Museum has been digitising specimens at large
scale and the portal exposes millions of records through both human and machine
readable interfaces.

The data is also pushed to GBIF (the Global Biodiversity Information Facility),
which means many of the records can be obtained either directly from the
Museum's API or from GBIF's aggregator. For a UK-focused workshop, calling the
Museum directly is more pedagogically useful.

## API endpoints

### 1. Data Portal API (CKAN action API)

- **Type**: REST, JSON.
- **Base URL**: `https://data.nhm.ac.uk/api/3/`
- **Authentication**: Not required for reads. An API key is needed only if you want to upload datasets.
- **Action endpoints**: `action/package_search` (dataset metadata), `action/datastore_search` (rows from individual resources), `action/datastore_search_sql` (SQL queries against datastore resources).
- **Documentation**: https://naturalhistorymuseum.github.io/dataportal-docs/

#### Example requests

Search the datastore for five specimen records:

```
GET https://data.nhm.ac.uk/api/3/action/datastore_search?resource_id=05ff2255-c38a-40c9-b657-4ccb55ab2feb&limit=5
```

(The resource ID above is the specimen collection. Other resources have their
own IDs which you can discover through `package_search`.)

List datasets matching a keyword:

```
GET https://data.nhm.ac.uk/api/3/action/package_search?q=Darwin
```

### 2. Darwin Core Archive downloads

- **Type**: Bulk download, Darwin Core Archive (DwC-A) format.
- **Where**: Each dataset's page on the Data Portal has a Download tab.
- **Use case**: When you want to work locally with the full dataset instead of paginating through the API.

Darwin Core is the international standard for occurrence and specimen data, so
the same files load directly into tools like GBIF's R packages, OpenRefine and
QGIS.

## Licensing

Licensing is set per dataset and is shown on each dataset's page. The bulk of
the specimen data is openly licensed (typically CC0 or CC BY 4.0), but always
check the dataset page before reusing the data.

## What you can do with it

This is the source to use if your workshop involves natural sciences,
biodiversity, geographic mapping, or any domain where specimen-level data is
the right abstraction. Practical examples: build a map of where Darwin's
beetles were collected; run NLP over collector notes; train a tagger on
species labels.

## Caveats and known issues

- Some resources are very large. Use pagination (`limit` and `offset`) when
  iterating through the API.
- The portal contains everything from CSVs to 3D models. Filter on resource
  type if you only want one format.
- The data is scientific, not art-historical. If your exercise is about
  paintings or design objects, pick a different source.

## Useful links

- Data Portal home: https://data.nhm.ac.uk/
- API reference: https://naturalhistorymuseum.github.io/dataportal-docs/
- Collection specimens dataset: https://data.nhm.ac.uk/dataset/collection-specimens
- Data Portal paper (Oxford Database, 2019): https://academic.oup.com/database/article/doi/10.1093/database/baz038/5432299
- NHM science services: https://www.nhm.ac.uk/our-science/services/data.html
