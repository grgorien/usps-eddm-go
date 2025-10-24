# usps-eddm-go

A Go client library for the USPS Every Door Direct Mail (EDDM) API, providing simplified access to carrier route data (e.g., polygons, ZIP/CRID mappings) and analytics for EDDM campaigns.

## Purpose
This library wraps the USPS EDDM API[](https://gis.usps.com/) to make it easier for developers to fetch and process carrier route data for applications like direct mail campaigns. It includes custom functions for tasks like ZIP-to-CRID mapping and analytics (e.g., average household income, residential density).

## Installation
```bash
go get github.com/grgorien/usps-eddm-go


--------------------------------------------

### Understanding:
url; https://gis.usps.com/arcgis/rest/services/EDDM/selectZIP/GPServer/routes/execute?f=json&env:outSR=4326&ZIP=%7BZIP_CODE%7D&Rte_Box=R&UserName=EDDM
--------------------------------------------

