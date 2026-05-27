# British Museum

## At a glance

- **Institution**: The British Museum, founded 1753, holds a global collection of around 8 million objects.
- **Location**: Great Russell Street, London WC1B 3DG.
- **Focus**: World cultures, archaeology, ethnography, prints and drawings, coins and medals.
- **Why this is on the list**: Symbolically central to GLAM-Wiki (Liam Wyatt's 2010 residency at the British Museum is widely regarded as the start of the Wikipedian-in-residence movement). The Museum publishes a SPARQL / Linked Data endpoint and makes 1.9 million images freely available for non-commercial use, although the SPARQL endpoint has a history of reliability issues.

## Overview

The British Museum has been an early adopter of Linked Open Data. The
collection metadata is modelled using the CIDOC Conceptual Reference Model
(CIDOC-CRM) and exposed through a SPARQL endpoint. In parallel, the public
Collection Online site uses IIIF behind the scenes for deep zoom and has been
the source for very large image releases. There is no documented public
REST or JSON API for general queries; the SPARQL service is the canonical
machine readable interface.

## API endpoints

### 1. SPARQL / Linked Data endpoint

- **Type**: SPARQL 1.1 endpoint over RDF data modelled in CIDOC-CRM.
- **Base URL**: `https://collection.britishmuseum.org/`
- **SPARQL endpoint**: `https://collection.britishmuseum.org/sparql`
- **Output formats**: XML or JSON for SELECT queries; RDF/XML, Turtle and N-Triples for CONSTRUCT queries.
- **Authentication**: None required.

#### Example query

A minimal SPARQL query asking for the labels of ten things:

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?s ?label WHERE {
  ?s rdfs:label ?label .
} LIMIT 10
```

You can submit this via:

```
GET https://collection.britishmuseum.org/sparql?query=PREFIX...&format=json
```

(URL-encode the query when sending it.)

### 2. Collection Online (IIIF, internal)

- **Type**: IIIF Image API used to power deep zoom inside the Collection Online site.
- **Status**: Used by the Museum's own viewer rather than offered as a documented public API. There is no IIIF Presentation manifest discovery comparable to the V&A or Wellcome.
- **Public collection site**: https://www.britishmuseum.org/collection

### 3. Image downloads (non-API)

- **Where**: Through Collection Online, after agreeing to non-commercial terms.
- **Scope**: Roughly 1.9 million images of objects.
- **Licence**: Creative Commons Attribution-NonCommercial-ShareAlike 4.0 (CC BY-NC-SA 4.0).
- **Commercial use**: Routed through British Museum Images (https://www.bmimages.com/), the Museum's commercial picture service.

This is not an API, but it is the most accessible bulk source of British Museum
imagery for educational and research use.

## Licensing

- **Metadata via SPARQL**: published as Linked Open Data; specific licensing terms are documented on the Museum's website. Treat as research-use friendly.
- **Object images**: CC BY-NC-SA 4.0 for the openly downloadable set.
- **Commercial imagery**: separate licensing via bmimages.com.

## What you can do with it

- Demonstrate the GLAM-Wiki story and Wikimedia's long relationship with the British Museum.
- Show CIDOC-CRM modelling in action (this is one of the longer running cultural heritage SPARQL endpoints in production).
- Use the openly downloadable images for non-commercial workshop exercises.

## Caveats and known issues

- **Reliability of the SPARQL endpoint**: it is widely reported as intermittent. Multiple Programming Historian threads and other community reports describe outages and slow queries over the years. Do not rely on it for a live demo without testing it the same day.
- **No public REST API**: if you want a quick JSON over HTTP demo, pick a different museum.
- **IIIF is not publicly documented as an API**: the deep zoom uses IIIF but the Museum does not publish manifests for third party reuse the way Wellcome and the V&A do.

## Useful links

- Collection Online: https://www.britishmuseum.org/collection
- Linked Data / SPARQL service home: https://collection.britishmuseum.org/
- Copyright and permissions: https://www.britishmuseum.org/terms-use/copyright-and-permissions
- Images and photography terms: https://www.britishmuseum.org/terms-use/copyright-and-permissions/images-and-photography
- British Museum Images (commercial): https://www.bmimages.com/
- Background on the first GLAM-Wiki residency (2010): https://en.wikipedia.org/wiki/Liam_Wyatt
