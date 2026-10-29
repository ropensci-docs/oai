# Get records

Get records

## Usage

``` r
get_records(
  ids,
  prefix = "oai_dc",
  url = "http://api.gbif.org/v1/oai-pmh/registry",
  as = "parsed",
  ...
)
```

## Arguments

- ids:

  The OAI-PMH identifier for the record. One or more. Required.

- prefix:

  specifies the metadata format that the records will be returned in.
  Default: `oai_dc`

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

## Value

a named list of data.frame's, or lists, or raw text

## Details

There are some finite set of results based on the OAI prefix. We will
provide parsers as we have time, and as users express interest. For
prefix types we have parsers for we return a list of data.frame's, for
each identifier, one data.frame for the `header` bits of data, and one
data.frame for the `metadata` bits of data.

For prefixes we don't have parsers for, we fall back to returning raw
XML, so you can at least parse the XML yourself.

Because some XML nodes are duplicated, we join values together of
duplicated node names, separated by a semicolon (`;`) with no spaces.
You can seprarate them yourself easily.

## Examples

``` r
if (FALSE) { # \dontrun{
get_records("87832186-00ea-44dd-a6bf-c2896c4d09b4")

ids <- c("87832186-00ea-44dd-a6bf-c2896c4d09b4", 
  "d981c07d-bc43-40a2-be1f-e786e25106ac")
(res <- get_records(ids))
lapply(res, "[[", "header")
lapply(res, "[[", "metadata")
do.call(rbind, lapply(res, "[[", "header"))
do.call(rbind, lapply(res, "[[", "metadata"))

# Get raw text
get_records("d981c07d-bc43-40a2-be1f-e786e25106ac", as = "raw")

# from arxiv.org
get_records("oai:arXiv.org:0704.0001", url = "http://export.arxiv.org/oai2")
} # }
```
