# List OAI-PMH identifiers

List OAI-PMH identifiers

## Usage

``` r
list_identifiers(
  url = "http://api.gbif.org/v1/oai-pmh/registry",
  prefix = "oai_dc",
  from = NULL,
  until = NULL,
  set = NULL,
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

- prefix:

  Specifies the metadata format that the records will be returned in.

- from:

  specifies that records returned must have been created/update/deleted
  on or after this date.

- until:

  specifies that records returned must have been created/update/deleted
  on or before this date.

- set:

  specifies the set that returned records must belong to.

- token:

  a token previously provided by the server to resume a request where it
  last left off.

- as:

  (character) What to return. One of "df" (for data.frame; default),
  "list", or "raw" (raw text)

- ...:

  Curl options passed on to
  [`GET`](https://httr.r-lib.org/reference/GET.html)

## Examples

``` r
if (FALSE) { # \dontrun{
# from
recently <- format(Sys.Date() - 1, "%Y-%m-%d")
list_identifiers(from = recently)

# from and until
list_identifiers(from = '2018-06-01T', until = '2018-06-14T')

# set parameter - here, using ANDS - Australian National Data Service
list_identifiers(from = '2018-09-01T', until = '2018-09-05T',
  set = "dataset_type:CHECKLIST")
} # }
```
