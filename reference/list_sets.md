# List sets

List sets

## Usage

``` r
list_sets(
  url = "http://api.gbif.org/v1/oai-pmh/registry",
  token = NULL,
  as = "df",
  ...
)
```

## Arguments

- url:

  (character) OAI-PMH base url. Defaults to the URL for arXiv's OAI-PMH
  server (http://export.arxiv.org/oai2) or GBIF's OAI-PMH server
  (http://api.gbif.org/v1/oai-pmh/registry)

- token:

  (character) a token previously provided by the server to resume a
  request where it last left off

- as:

  (character) What to return. One of "df" (for data.frame; default),
  "list", or "raw" (raw text)

- ...:

  Curl options passed on to
  [`GET`](https://httr.r-lib.org/reference/GET.html)

## Examples

``` r
if (FALSE) { # \dontrun{
# Get back a data.frame
list_sets()

# Get back a list
list_sets(as = "list")

# Get back raw text
list_sets(as = "raw")

# curl options
library("httr")
list_sets(config = verbose())
} # }
```
