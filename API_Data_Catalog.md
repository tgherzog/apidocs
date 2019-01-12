---
title: Data Catalog API
---

The **Data Catalog API** provides information about the thousands of development-relevant
datasets available through the [World Bank Data Catalog](https://datacatalog.worldbank.org).
The Data Catalog is built on the [DKAN platform](https://getdkan.org). DKAN provides a
[CKAN-compatible API][ckan] for
reading metadata from the data catalog; the World Bank's Data Catalog API is based on this
service.

All Data Catalog API endpoints follow the form:

<https://datacatalog.worldbank.org/api/3/action/[action_name]>

where *action_name* is one of the supported endpoints discussed below.


### Changes from the CKAN-compatible API ###

API users should refer to the [CKAN Dataset API][ckan], with the following changes and
limits:

* Support is limited to the [site_read,][1] [package_list][2], [current_package_list_with_resources][3],
  [package_show][4] and [resource_show][5] endpoints

* [package_list][1] returns uuid strings as dataset identifiers instead of package names

* [package_show][4] and [resource_show][5] accept uuid's, Drupal node IDs (nid's) or the value from the
  `name` field as values for the `id` query parameter. All three are included in the response from these endpoints.

* For performance reasons, [current_page_list_with_resources][3] returns 150 packages by default
  instead of the entire package list. You will need to make multiple API calls to return
  the entire list, using the `limit` query parameter to adjust the response size, and the
  `offset` parameter to return sequential pages. A `limit` value of no more than 50 seems to
  provide reasonable performance. For example, the request below demonstrates how to return the 3rd page
  of 20 search results (i.e., datasets 41-60):

  <https://datacatalog.worldbank.org/api/3/action/current_package_list_with_resources?limit=20&offset=40>

[ckan]: https://dkan.readthedocs.io/en/latest/apis/ckan-dataset.html

[1]: https://dkan.readthedocs.io/en/latest/apis/ckan-dataset.html#site-read
[2]: https://dkan.readthedocs.io/en/latest/apis/ckan-dataset.html#package-list
[3]: https://dkan.readthedocs.io/en/latest/apis/ckan-dataset.html#current-package-list-with-resources
[4]: https://dkan.readthedocs.io/en/latest/apis/ckan-dataset.html#package-show
[5]: https://dkan.readthedocs.io/en/latest/apis/ckan-dataset.html#resource-show
