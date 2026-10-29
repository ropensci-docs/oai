# OAI-PMH Client

oai is an R client to work with OAI-PMH (Open Archives Initiative
Protocol for Metadata Harvesting) services, a protocol developed by the
Open Archives Initiative
(https://en.wikipedia.org/wiki/Open_Archives_Initiative). OAI-PMH uses
XML data format transported over HTTP.

## OAI-PMH Info

See the OAI-PMH V2 specification at
[http://www.openarchives.org/OAI/openarchivesprotocol.html](http://www.openarchives.org/OAI/openarchivesprotocol.md)

## Implementation details

oai is built on xml2 and httr. In addition, we give back data.frame's
whenever possible to make data comprehension, manipulation, and
visualization easier. We also have functions to fetch a large directory
of OAI-PMH services - it isn't exhaustive, but does contain a lot.

## Paging

Instead of paging with e.g., `page` and `per_page` parameters, OAI-PMH
uses (optionally) `resumptionTokens`, with an optional expiration date.
These tokens can be used to continue on to the next chunk of data, if
the first request did not get to the end. Often, OAI-PMH services limit
each request to 50 records, but this may vary by provider, I don't know
for sure. The API of this package is such that we `while` loop for you
internally until we get all records. We may in the future expose e.g., a
`limit` parameter so you can say how many records you want, but we
haven't done this yet.

## Acknowledgements

Michal Bojanowski contributions were supported by (Polish) National
Science Center (NCN) through grant 2012/07/D/HS6/01971.

## See also

Useful links:

- <https://docs.ropensci.org/oai/>

- <https://github.com/ropensci/oai>

- Report bugs at <https://github.com/ropensci/oai/issues>

## Author

Scott Chamberlain <myrmecocystus@gmail.com>

Michal Bojanowski <michal2992@gmail.com>
