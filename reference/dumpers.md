# Result dumpers

Result dumpers are functions allowing to handle the chunks of results
from OAI-PMH service "on the fly". Handling can include processing,
writing to files, databases etc.

## Usage

``` r
dump_raw_to_txt(
  res,
  args,
  as,
  file_pattern = "oaidump",
  file_dir = ".",
  file_ext = ".xml"
)

dump_to_rds(
  res,
  args,
  as,
  file_pattern = "oaidump",
  file_dir = ".",
  file_ext = ".rds"
)

dump_raw_to_db(res, args, as, dbcon, table_name, field_name, ...)
```

## Arguments

- res:

  results, depends on `as`, not to be specified by the user

- args:

  list, query arguments, not to be specified by the user

- as:

  character, type of result to return, not to be specified by the user

- file_pattern, file_dir, file_ext:

  character respectively: initial part of the file name, directory name,
  and file extension used to create file names. These arguments are
  passed to [`tempfile()`](https://rdrr.io/r/base/tempfile.html)
  arguments `pattern`, `tmpdir`, and `fileext` respectively.

- dbcon:

  DBI-compliant database connection

- table_name:

  character, name of the database table to write into

- field_name:

  character, name of the field in database table to write into

- ...:

  arguments passed to/from other functions

## Value

Dumpers should return `NULL` or a value that will be collected and
returned by the function using the dumper.

`dump_raw_to_txt` returns the name of the created file.

`dump_to_rds` returns the name of the created file.

`dump_xml_to_db` returns `NULL`

## Details

Often the result of a request to a OAI-PMH service are so large that it
is split into chunks that need to be requested separately using
`resumptionToken`. By default functions like
[`list_identifiers()`](https://docs.ropensci.org/oai/reference/list_identifiers.md)
or
[`list_records()`](https://docs.ropensci.org/oai/reference/list_records.md)
request these chunks under the hood and return all concatenated in a
single R object. It is convenient but insufficient when dealing with
large result sets that might not fit into RAM. A result dumper is a
function that is called on each result chunk. Dumper functions can write
chunks to files or databases, include initial pre-processing or
extraction, and so on.

A result dumper needs to be function that accepts at least the
arguments: `res`, `args`, `as`. They will get values by the enclosing
function internally. There may be additional arguments, including `...`.
Dumpers should return `NULL` or a value that will be collected and
returned by the function calling the dumper (e.g.
[`list_records()`](https://docs.ropensci.org/oai/reference/list_records.md)).

Currently result dumpers can be used with functions:
[`list_identifiers()`](https://docs.ropensci.org/oai/reference/list_identifiers.md),
[`list_records()`](https://docs.ropensci.org/oai/reference/list_records.md),
and
[`list_sets()`](https://docs.ropensci.org/oai/reference/list_sets.md).
To use a dumper with one of these functions you need to:

- Pass it as an additional argument `dumper`

- Pass optional addtional arguments to the dumper function in a list as
  the `dumper_args` argument

See Examples. Below we provide more details on the dumpers currently
implemented.

`dump_raw_to_txt` writes raw XML to text files. It requires `as=="raw"`.
File names are created using
[`tempfile()`](https://rdrr.io/r/base/tempfile.html). By default they
are written in the current working directory and have a format
`oaidump*.xml` where `*` is a random string in hex.

`dump_to_rds` saves results in an `.rds` file via
[`saveRDS()`](https://rdrr.io/r/base/readRDS.html). Type of object being
saved is determined by the `as` argument. File names are generated in
the same way as by `dump_raw_to_txt`, but with default extension `.rds`

`dump_xml_to_db` writes raw XML to a single text column of a table in a
database. Requires `as == "raw"`. Database connection `dbcon` should be
a connection object as created by
[`DBI::dbConnect()`](https://dbi.r-dbi.org/reference/dbConnect.html)
from package DBI. As such, it can connect to any database supported by
DBI. The records are written to a field `field_name` in a table
`table_name` using
[`DBI::dbWriteTable()`](https://dbi.r-dbi.org/reference/dbWriteTable.html).
If the table does not exist, it is created. If it does, the records are
appended. Any additional arguments are passed to
[`DBI::dbWriteTable()`](https://dbi.r-dbi.org/reference/dbWriteTable.html)

## References

OAI-PMH specification
<https://www.openarchives.org/OAI/openarchivesprotocol.html>

## See also

Functions supporting the dumpers:
[`list_identifiers()`](https://docs.ropensci.org/oai/reference/list_identifiers.md),
[`list_sets()`](https://docs.ropensci.org/oai/reference/list_sets.md),
and
[`list_records()`](https://docs.ropensci.org/oai/reference/list_records.md)

## Examples

``` r
if (FALSE) { # \dontrun{

### Dumping raw XML to text files

# This will write a set of XML files to a temporary directory
fnames <- list_identifiers(from="2018-06-01T",
                           until="2018-06-14T",
                           as="raw",
                           dumper=dump_raw_to_txt,
                           dumper_args=list(file_dir=tempdir()))
# vector of file names created
str(fnames)
all( file.exists(fnames) )
# clean-up
unlink(fnames)


### Dumping raw XML to a database

# Connect to in-memory SQLite database
con <- DBI::dbConnect(RSQLite::SQLite(), dbname=":memory:")
# Harvest and dump the results into field "bar" of table "foo"
list_identifiers(from="2018-06-01T",
                 until="2018-06-14T",
                 as="raw",
                 dumper=dump_raw_to_db,
                 dumper_args=list(dbcon=con,
                                  table_name="foo",
                                  field_name="bar") )
# Count records, should be 101
DBI::dbGetQuery(con, "SELECT count(*) as no_records FROM foo")

DBI::dbDisconnect(con)




} # }
```
