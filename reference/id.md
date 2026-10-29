# Identify the OAI-PMH service for each data provider.

Identify the OAI-PMH service for each data provider.

## Usage

``` r
id(url, as = "parsed", ...)
```

## Arguments

- url:

  (character) OAI-PMH base url. Defaults to the URL for arXiv's OAI-PMH
  server (http://export.arxiv.org/oai2) or GBIF's OAI-PMH server
  (http://api.gbif.org/v1/oai-pmh/registry)

- as:

  (character) What to return. One of "parsed" (default), or "raw" (raw
  text)

- ...:

  Curl options passed on to
  [`GET`](https://httr.r-lib.org/reference/GET.html)

## Examples

``` r
if (FALSE) { # \dontrun{
# arxiv
id("http://export.arxiv.org/oai2")

# GBIF - http://www.gbif.org/
id("http://api.gbif.org/v1/oai-pmh/registry")

# get back text instead of parsed
id("http://export.arxiv.org/oai2", as = "raw")
id("http://api.gbif.org/v1/oai-pmh/registry", as = "raw")

# curl options
library("httr")
id("http://export.arxiv.org/oai2", config = verbose())
} # }
```
