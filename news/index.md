# Changelog

## oai 0.4.0

CRAN release: 2022-11-10

#### NEW FEATURES

- the requests are now made using
  [`httr::RETRY()`](https://httr.r-lib.org/reference/RETRY.html) rather
  than [`httr::GET()`](https://httr.r-lib.org/reference/GET.html) to
  facilitate retrying with delay control etc. Consult further the
  documentation of ‘httr’ package
  ([\#64](https://github.com/ropensci/oai/issues/64))
- @mbojan takes over package maintenance from
  [@sckott](https://github.com/sckott)

#### MINOR IMPROVEMENTS

- update packages test to catch the ‘cannotDisseminateFormat’
  OAI-PMH-level error correctly
- added package hex logo

## oai 0.3.2

CRAN release: 2021-05-13

#### MINOR IMPROVEMENTS

- vignette fix, use markdown in suggests
- update readme, use ropensci coc

## oai 0.3.0

CRAN release: 2019-09-07

#### NEW FEATURES

- [`id()`](https://docs.ropensci.org/oai/reference/id.md) gains `as`
  parameter so user can ask for different outputs (parsed
  list/data.frame, or raw xml/text)
  ([\#54](https://github.com/ropensci/oai/issues/54))
- most OAI functions changed their default url to
  `http://api.gbif.org/v1/oai-pmh/registry`, while
  [`count_identifiers()`](https://docs.ropensci.org/oai/reference/count_identifiers.md)
  changed it’s default url to `http://export.arxiv.org/oai2`. the
  previous default url for Datacite was too unreliable (was often
  unresponsive)

#### MINOR IMPROVEMENTS

- add grant information for one author
  ([\#48](https://github.com/ropensci/oai/issues/48))
  ([\#49](https://github.com/ropensci/oai/issues/49))
- code of conduct urls fixed
- now using markdown supported documentation
  ([\#56](https://github.com/ropensci/oai/issues/56))
- replace
  [`tibble::as_data_frame`](https://tibble.tidyverse.org/reference/deprecated.html)
  with
  [`tibble::as_tibble`](https://tibble.tidyverse.org/reference/as_tibble.html)
  throughout package

#### BUG FIXES

- fix to
  [`update_providers()`](https://docs.ropensci.org/oai/reference/update_providers.md);
  html page that we scrape had changed
  ([\#57](https://github.com/ropensci/oai/issues/57))

## oai 0.2.2

CRAN release: 2016-11-23

#### NEW FEATURES

- Added new parsers in
  [`get_records()`](https://docs.ropensci.org/oai/reference/get_records.md)
  specific to different OAI prefixes. Currently has parsers for `oai_dc`
  and `oai_datacite`. For prefixes we don’t have parsers for we return
  raw XML so you can parse it yourself.
  ([\#45](https://github.com/ropensci/oai/issues/45))

#### MINOR IMPROVEMENTS

- Replace
  [`xml2::xml_find_one()`](http://xml2.r-lib.org/reference/xml_find_all.md)
  with
  [`xml2::xml_find_first()`](http://xml2.r-lib.org/reference/xml_find_all.md)
  ([\#39](https://github.com/ropensci/oai/issues/39))
- Update URLs in `DESCRIPTION` file
  ([\#43](https://github.com/ropensci/oai/issues/43))
- Using `tibble` now for compact data.frame instead of internal methods
  for the same ([\#44](https://github.com/ropensci/oai/issues/44))
- `as` parameter in
  [`get_records()`](https://docs.ropensci.org/oai/reference/get_records.md)
  now has options `parsed` or `raw`, which replaces `df` `list`, or
  `raw`

## oai 0.2.0

CRAN release: 2016-02-06

#### NEW FEATURES

- A set of new functions for dealing with larger data results:
  [`dump_raw_to_txt()`](https://docs.ropensci.org/oai/reference/dumpers.md),
  [`dump_to_rds()`](https://docs.ropensci.org/oai/reference/dumpers.md),
  and
  [`dump_raw_to_db()`](https://docs.ropensci.org/oai/reference/dumpers.md).
  They can be used with `oai` functions
  [`list_identifiers()`](https://docs.ropensci.org/oai/reference/list_identifiers.md),
  [`list_sets()`](https://docs.ropensci.org/oai/reference/list_sets.md),
  and
  [`list_records()`](https://docs.ropensci.org/oai/reference/list_records.md)
  ([\#9](https://github.com/ropensci/oai/issues/9))
  ([\#15](https://github.com/ropensci/oai/issues/15))
  ([\#21](https://github.com/ropensci/oai/issues/21)) thanks
  [@mbojan](https://github.com/mbojan)

#### MINOR IMPROVEMENTS

- Sped up some tests ([\#19](https://github.com/ropensci/oai/issues/19))
- Better description of OAI protocol in the `DESCRIPTION` file
  ([\#28](https://github.com/ropensci/oai/issues/28))
- Commented about where some internal functions come from
  ([\#31](https://github.com/ropensci/oai/issues/31))
- Import `plyr` for `rbind.fill()`
  ([\#32](https://github.com/ropensci/oai/issues/32))
- Including now some examples using OAI-PMH with GBIF and BHL
  ([\#33](https://github.com/ropensci/oai/issues/33))
- Better error handling!
  ([\#10](https://github.com/ropensci/oai/issues/10))
  ([\#12](https://github.com/ropensci/oai/issues/12))
  ([\#22](https://github.com/ropensci/oai/issues/22))
  ([\#27](https://github.com/ropensci/oai/issues/27)) thanks
  [@mbojan](https://github.com/mbojan)

#### BUG FIXES

- Fixed bug where
  [`list_identifiers()`](https://docs.ropensci.org/oai/reference/list_identifiers.md)
  threw error when no result was found
  ([\#13](https://github.com/ropensci/oai/issues/13))
- Dealing better with bad inputs to `as` parameter - stop with
  informative message now instead of failing without anything returned
  ([\#34](https://github.com/ropensci/oai/issues/34))

## oai 0.1.0

CRAN release: 2015-09-11

- Released to CRAN.
