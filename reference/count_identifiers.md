# Count OAI-PMH identifiers for a data provider.

Count OAI-PMH identifiers for a data provider.

## Usage

``` r
count_identifiers(url = "http://export.arxiv.org/oai2", prefix = "oai_dc", ...)
```

## Arguments

- url:

  (character) OAI-PMH base url. Defaults to the URL for arXiv's OAI-PMH
  server (http://export.arxiv.org/oai2) or GBIF's OAI-PMH server
  (http://api.gbif.org/v1/oai-pmh/registry)

- prefix:

  Specifies the metadata format that the records will be returned in

- ...:

  Curl options passed on to
  [`GET`](https://httr.r-lib.org/reference/GET.html)

## Details

Note that some OAI providers do not include the entry `completeListSize`
(<http://www.openarchives.org/OAI/openarchivesprotocol.html#FlowControl>)
in which case we return an NA - which does not mean 0, but rather we
don't know.

## Examples

``` r
if (FALSE) { # \dontrun{
count_identifiers()

# curl options
# library("httr")
# count_identifiers(config = verbose())
} # }
```
