# usps-eddm-go

A Go client library for the USPS Every Door Direct Mail (EDDM) API, providing simplified access to carrier route data (e.g., polygons, ZIP/CRID mappings) and analytics for EDDM campaigns.

## Purpose
This library wraps the USPS EDDM API[](https://gis.usps.com/) to make it easier for developers to fetch and process carrier route data for applications like direct mail campaigns. It includes custom functions for tasks like ZIP-to-CRID mapping and analytics (e.g., average household income, residential density).

## Installation
```bash
go get github.com/grgorien/usps-eddm-go
```

--------------------------------------------
### Understanding:
--------------------------------------------
url; https://gis.usps.com/arcgis/rest/services/EDDM/selectZIP/GPServer/routes/execute?f=json&env:outSR=4326&ZIP=%7BZIP_CODE%7D&Rte_Box=R&UserName=EDDM

## Context:

We define as residential and business routes OR residential routes only, question would be if data get's affected on full query response.

We can map but geometry will be hard to reverse, so it's best to call out now based on rte type.

After some testing, we can notice that the official site, also does not practice geometry reduce, instead it's based on the count, but pricing data get's affected, which can be reversed based on the actual pricing currently as notice from here: Cost per mailpiece is $0.247.

So paths don't reduce and they get rendered regardless on the client, so the actual solution can be just map based on the actual key of residential if selected on choice type else as default get hosted, and finally the update on the approx cost of pricing.

Also type of B is not actually business it's noticed as PO boxes which defeat the point based on this product utility usage.

## Params:

**endpoint:** https://gis.usps.com/arcgis/rest/services/EDDM/selectZIP/GPServer/routes/execute?f=json&env:outSR=4326&ZIP=12345&Rte_Box=R&UserName=EDDM
| Parameter | Type | Required | Description | Example |
|------------|-------|-----------|--------------|----------|
| `f` | string | Yes | Output format for the response. Typically set to `json`. | `f=json` |
| `env:outSR` | integer | No | Output spatial reference (coordinate system). `4326` returns results in WGS84 (latitude/longitude). | `env:outSR=4326` |
| `ZIP` | string | Yes | ZIP code to query carrier routes for. Replace `{ZIP_CODE}` with a valid ZIP. | `ZIP=1234` |
| `Rte_Box` | string | No | Route type filter. Use `R` for residential routes or `B`?pending for business routes. | `Rte_Box=R` |
| `UserName` | string | No | Client identifier used by USPS to track or log API usage. | `UserName=EDDM` |

### Resolution v1:

**Solve for:**

Shared business model analytics for local advertisers.

- total approx impressions 
- market buying power (not avg but sum annual household)
- total b2b distribution
- 5k max per day as buy postage strategy -> split, call it for now splitN
- algorithm to identify the set of great neighborhoods << splitN on max from best as type of rte
- simple local caching for faster load times reduce out req
- **important** if cache, we should be able to manually fetch to check paths, as the can update so set as put, while keeping perstwith date

