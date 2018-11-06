---
---

# Data Catalog API #

The **Data Catalog API** provides information about the thousands of development-relevant
datasets available through the [World Bank Data Catalog](https://datacatalog.worldbank.org).
The Data Catalog is built on the [DKAN platform](https://getdkan.org). DKAN provides a
[CKAN-compatible API][ckan] for
reading metadata from the data catalog; the World Bank's Data Catalog API is based on this
service.

API users should refer to the [CKAN Dataset API][ckan], with the following changes and
limits:

* Support is limited to the `site_read`, `package_list`, `current_package_list_with_resources`,
  `package_show` and `resource_show` endpoints

* `package_list` returns uuid strings as dataset identifiers instead of package names

* `package_show` and `resource_show` accept either uuid's or Drupal node IDs (nid's) as the `id`
  query parameter. Both are included in the response from these endpoints.

* For performance reasons, `current_page_list_with_resources` returns 150 packages by default
  instead of the entire package list. You will need to make multiple API calls to return
  the entire list, using the `limit` query parameter to adjust the response size, and the
  `offset` parameter to return sequential pages. A `limit` value of no more than 50 seems to
  provide reasonable peformance. The request below demonstrates how to return the 3rd page
  of 20 search results (i.e., datasets 41-60):

  `https://datacatalog.worldbank.org/api/3/action/current_package_list_with_resources?limit=20&offset=40`
