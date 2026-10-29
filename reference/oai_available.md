# Test of OAI-PMH service is available

Silently test if OAI-PMH service is available under the URL provided.

## Usage

``` r
oai_available(u, ...)
```

## Arguments

- u:

  base URL to OAI-PMH service

- ...:

  other arguments passed to
  [`id()`](https://docs.ropensci.org/oai/reference/id.md)

## Value

`TRUE` or `FALSE` if the service is available.

## Examples

``` r
if (FALSE) { # \dontrun{
url_list <- list(
  archivesic="http://archivesic.ccsd.cnrs.fr/oai/oai.php",
  datacite = "http://oai.datacite.org/oai",

  # No OAI-PMH here
  google = "http://google.com"
)

sapply(url_list, oai_available)
} # }
```
