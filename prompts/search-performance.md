# Search performance questions

## Compare reporting periods

> For [property], retrieve the same search-performance recipe for [period A] and [period B] using get_gsc_period_datasets. Use web search and final data. Compare native totals and daily trends in the client. State date lengths, aggregation and filters; don't manufacture zero rows for missing queries.

## Inspect a landing page's queries

> For [property] and [dates], use get_gsc_page_queries for the exact page [URL]. Retrieve all available pages of that dataset within a budget of [maximum tool calls]. Keep the URL unchanged. Which query rows does Google expose, and what coverage limits apply?

## Look up pages for a query

> Use get_gsc_query_pages for query [query] and [dates]. Show the returned landing pages with clicks, impressions, native CTR and average position. Distinguish exact matching from regex matching; don't describe average position as a fixed rank.

## Inspect search appearance categories

> Retrieve available search appearance categories for [property] and [dates] using get_gsc_search_appearances. Explain that categories may overlap and totals should not be added as independent traffic.

## Compare properties or search surfaces

> Retrieve the same bounded recipe for [properties] using get_gsc_property_datasets, or [surfaces] using get_gsc_surface_datasets. Preserve independent errors and dates. Do not add overlapping properties or treat a surface with no returned rows as proof of no audience.

## Check indexed-version evidence

> Inspect these supplied URLs inside [property] using inspect_gsc_urls: [URLs]. Show each native outcome, last crawl evidence when returned and unresolved results. Don't call this a live crawl, sitewide index audit or proof that all pages are indexed.

## Review sitemaps

> List submitted sitemaps for [property]. For a selected sitemap, retrieve its metadata. Explain what the current source reports without treating deprecated indexed counters as a complete index inventory.
