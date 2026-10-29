# Update the locally stored OAI-PMH data providers table.

Data comes from <http://www.openarchives.org/Register/BrowseSites>. It
includes the oai-identifier (if they have one) and the base URL. The
website has the name of the data provider too, but not provided in the
data pulled down here, but you can grab the name using the example
below.

## Usage

``` r
update_providers(path = ".", ...)
```

## Arguments

- path:

  Path to put data in.

- ...:

  Curl options passed on to
  [`httr::GET()`](https://httr.r-lib.org/reference/GET.html)

## Details

This table is scraped from
<http://www.openarchives.org/Register/BrowseSites>. I would get it from
<http://www.openarchives.org/pmh/registry/ListFriends>, but it does not
include repository names.

This function updates the table for you. Does take a while though, so go
get a coffee.

## See also

[`load_providers()`](https://docs.ropensci.org/oai/reference/load_providers.md)

## Examples

``` r
if (FALSE) { # \dontrun{
update_providers()
load_providers()
} # }
```
