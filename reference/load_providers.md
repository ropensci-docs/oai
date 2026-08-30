# Load an updated cache

Load an updated cache

## Usage

``` r
load_providers(path = NULL, envir = .GlobalEnv)
```

## Arguments

- path:

  location where cache is located. Leaving to NULL loads the version in
  the installed package

- envir:

  R environment to load data in to.

## Value

loads the object providers into the working space.

## Details

Loads the data object providers into the global workspace.

## See also

[`update_providers()`](https://docs.ropensci.org/oai/reference/update_providers.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# By default the new providers table goes to directory ".", so just
# load from there
update_providers()
load_providers(path=".")

# Loads the version in the package
load_providers()
} # }
```
