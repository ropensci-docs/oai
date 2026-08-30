# List available metadata formats from various providers.

List available metadata formats from various providers.

## Usage

``` r
list_metadataformats(
  url = "http://api.gbif.org/v1/oai-pmh/registry",
  id = NULL,
  ...
)
```

## Arguments

- url:

  (character) OAI-PMH base url. Defaults to the URL for arXiv's OAI-PMH
  server (http://export.arxiv.org/oai2) or GBIF's OAI-PMH server
  (http://api.gbif.org/v1/oai-pmh/registry)

- id:

  The OAI-PMH identifier for the record. Optional.

- ...:

  Curl options passed on to
  [`GET`](https://httr.r-lib.org/reference/GET.html)

## Examples

``` r
if (FALSE) { # \dontrun{
list_metadataformats()

# no metadatformats for an identifier
list_metadataformats(id = "9da8a65a-1b9b-487c-a564-d184a91a2705")

# metadatformats available for an identifier
list_metadataformats(id = "ad7295e0-3261-4028-8308-b2047d51d408")
} # }
```
