# Google Search Console MCP

A **Google Search Console MCP Model Context Protocol (MCP) server built by Typenode**, wrapping Google's official Search Console API. Its **18 read-only tools** let AI assistants such as Claude and ChatGPT retrieve your data and answer questions in plain language.

**Runs on Typenode.** The repository contains tool contracts, permission requirements and usage recipes. The implementation runs on Typenode and is not included here. You need your own Typenode Workspace and Google connection; there is no standalone npm or Python server here.

**[Get this template](https://typenode.ai/templates/google-search-console-mcp)** · **[Setup instructions](docs/setup.md)** · **[Copy-paste prompts](prompts/getting-started.md)**

> Current interface reference: the maintainer installations have live evidence. Independent customer installation of the latest published snapshot still needs verification. These JSON contracts are documentation, not executable workflows. See [verification](docs/verification.md).

## What can you do with it?

Built for SEO and marketing managers who want to ask questions about their own authorised data. The tools retrieve native reports and useful preset datasets; your AI client performs the comparison, interpretation and explanation.

| Question | Retrieval tool | Evidence supplied |
|---|---|---|
| How did Google Search performance change between two months? | `get_gsc_period_datasets` | Retrieve comparable datasets; the AI client calculates and explains changes. |
| Which queries show my product page in search? | `get_gsc_page_queries` | Choose a page and dates; retrieve the query rows Google makes available. |
| Which pages appear for a particular query? | `get_gsc_query_pages` | Inspect the pages associated with a supplied query filter. |
| How does performance vary by country or device? | `query_gsc_performance` | Choose dimensions and filters for a bounded native report. |
| What does Google report about the indexed version of these URLs? | `inspect_gsc_urls` | Inspect a supplied list of up to 20 URLs; this is not a sitewide census. |
| Which sitemaps are submitted for my property? | `list_gsc_sitemaps` | Read submitted sitemap metadata without submitting or deleting anything. |

See [more task recipes](prompts/search-performance.md), including limitations that should remain visible in an answer.

## Available tools

The names and descriptions below match the saved server bindings. The linked JSON files document each tool's input/output contract. No Google configuration write tools are included.

### Properties

| Tool | What it retrieves |
|---|---|
| [`list_gsc_properties`](tools/list_gsc_properties.json) | List Google Search Console properties accessible to the connected Google identity, preserving exact property identifiers and permission levels. |
| [`get_gsc_property`](tools/get_gsc_property.json) | Get one exact Google Search Console property record. Returns the same fields as property discovery, with a direct lookup outcome. |
### Search performance and presets

| Tool | What it retrieves |
|---|---|
| [`query_gsc_performance`](tools/query_gsc_performance.json) | Retrieve Google Search Console performance using supported dimensions, filters and aggregation. Returns one bounded page of source rows; pagination does not guarantee exhaustive data. |
| [`get_gsc_performance_totals`](tools/get_gsc_performance_totals.json) | Retrieve Google's aggregate performance for a property and filter scope. Totals come from a separate source query, never from summing displayed detail rows. |
| [`get_gsc_performance_time_series`](tools/get_gsc_performance_time_series.json) | Retrieve daily or recent hourly Google Search Console performance. Preserve reported timestamps, missing intervals and available incomplete-data metadata. |
| [`get_gsc_page_queries`](tools/get_gsc_page_queries.json) | Retrieve observed search queries for an exact page or explicit page filter. Returns a bounded page; omitted query identities are not reconstructed. |
| [`get_gsc_query_pages`](tools/get_gsc_query_pages.json) | Retrieve observed pages for an exact query or explicit query filter. Returns source performance rows without judging overlap between pages. |
| [`get_gsc_page_query_rows`](tools/get_gsc_page_query_rows.json) | Retrieve performance grouped by page and query, with optional country/device detail. Returns source rows for client-side analysis, subject to Google's detail limits. |
| [`get_gsc_search_appearances`](tools/get_gsc_search_appearances.json) | Retrieve observed search appearance categories and source metrics for a scope. Use returned categories as filters in a subsequent performance query. |
| [`get_gsc_available_dates`](tools/get_gsc_available_dates.json) | Retrieve dates with reported performance in an explicit window and search surface. Missing dates do not establish zero traffic or a universal freshness boundary. |
### Dataset bundles

| Tool | What it retrieves |
|---|---|
| [`get_gsc_performance_overview`](tools/get_gsc_performance_overview.json) | Retrieve separate source totals and daily performance, optionally with one detail dataset. At most three source requests; each dataset retains its own scope and continuation. |
| [`get_gsc_period_datasets`](tools/get_gsc_period_datasets.json) | Retrieve the same performance report for supplied named periods. At most six independent source requests; returns datasets without matching rows or calculating changes. |
| [`get_gsc_surface_datasets`](tools/get_gsc_surface_datasets.json) | Retrieve the same performance report for selected search surfaces. At most six independent source requests; preserve per-surface results and failures without combining metrics. |
| [`get_gsc_property_datasets`](tools/get_gsc_property_datasets.json) | Retrieve the same performance report for supplied Google Search Console properties. At most six independent source requests; each property retains its own result and continuation. |
### Sitemaps and URL inspection

| Tool | What it retrieves |
|---|---|
| [`list_gsc_sitemaps`](tools/list_gsc_sitemaps.json) | List submitted sitemap records for a property, optionally within a sitemap index. Returns Google's metadata, not the sitemap XML URL inventory. |
| [`get_gsc_sitemap`](tools/get_gsc_sitemap.json) | Get one submitted sitemap's Google Search Console metadata, warnings and errors. Deprecated indexed counts do not establish indexed coverage. |
| [`inspect_gsc_url`](tools/inspect_gsc_url.json) | Retrieve Google's full indexed-version inspection result for one property-member URL. This is not a live test or an indexing request. |
| [`inspect_gsc_urls`](tools/inspect_gsc_urls.json) | Retrieve indexed-version inspection results for up to 20 supplied URLs, with independent outcomes. Each attempted URL consumes one inspection request; this is not a sitewide index census. |

## Quick start

1. Prepare a Typenode Workspace, a Google Cloud OAuth application and access to your reporting properties.
2. Enable the required Google APIs and connect Google in your chosen Typenode Environment with the read-only scope below.
3. Activate your copy of the hosted MCP template through Typenode: **[https://typenode.ai/templates/google-search-console-mcp](https://typenode.ai/templates/google-search-console-mcp)**. The [setup guide](docs/setup.md) documents prerequisites and connection checks.
4. Obtain your own Environment-specific MCP endpoint, add it to your AI client and complete Typenode consent.
5. Ask: **“List the Search Console properties I can access.”** Then select a returned property and make a dated report request.

## Requirements and permissions

| Requirement | Why it is needed |
|---|---|
| Typenode account | Hosts and executes your copy of the Workflows and MCP server; normal account/billing prerequisites apply. |
| Customer-owned Google Cloud project and OAuth client | The tested custom OAuth setup authenticates API reads. |
| Enabled APIs | Google Search Console API. |
| Google OAuth scope | `https://www.googleapis.com/auth/webmasters.readonly`. |
| Google property access | The consenting account must be authorised for the selected property and method; an OAuth scope does not grant property access. |
| Compatible AI client | Supports Typenode's authenticated remote MCP endpoint and can discover/invoke its tools. |

Credential values belong in secure Typenode configuration. Property identifiers and date ranges are call arguments, not hardcoded installation defaults. Google renewal and client-to-Typenode renewal are distinct authentication boundaries; [setup](docs/setup.md) explains both.

The MIT licence covers the files in this repository, not the hosted implementation or service access. Typenode hosting, AI-client subscriptions and Google's quotas are separate. Check [provider quota guidance](https://developers.google.com/webmaster-tools/limits) and current Typenode account terms; this package does not promise free runtime usage.

## Example request

Ask your AI client to retrieve a report for your selected property and dates. Underneath, it can call `get_gsc_performance_totals` with arguments like these:

```json
{
  "property": "sc-domain:example.com",
  "start_date": "2026-09-01",
  "end_date": "2026-09-30"
}
```

The property and dates above are invented examples. Replace them with your own selection. The result includes typed native evidence, effective request, coverage notes and request accounting. Report results expose continuation where supported; errors provide a documented correction.

Browse [requests for every tool](examples/tool-calls.json), a [complete representative request](examples/sample.request.json), its [synthetic response](examples/sample.response.json), and [example interpretation guidance](examples/README.md). These examples demonstrate interface shapes and do not claim observed results for a real business.

## How it works

Your AI client invokes a named MCP tool. Typenode validates the request, performs bounded official Google API reads using your connected Credential, and returns a structured result. Presets reduce repetitive request construction; bundles return independent datasets and their outcomes.

The server adds request validation, bounded output, pagination, explicit source/error evidence and retrieval presets. Format checks omitted from advertised input schemas still run in preflight; other schema constraints can reject at admission. It does not author business recommendations, join the sibling servers' datasets or reconstruct unavailable metrics. Query results can change as Google data changes; pagination is not a snapshot.

## Limitations

Search Console supplies search reporting, not what visitors did after arriving. Search Analytics may omit query detail and does not promise every row. Average position is an aggregate, not a fixed rank. Overlapping properties or appearance groups should not be added blindly.

URL inspection reports Google's indexed-version evidence for supplied URLs. It is not a live crawl or sitewide index census. Sitemap metadata is not a complete inventory of indexed pages.

Empty results do not prove absence of real-world activity. Preserve dates, filters, reporting populations, source metadata and unresolved evidence. A partially returned bundle is not an entirely successful report; continue a selected dataset through its documented primitive without reacquiring all siblings.

See [verification and pending release checks](docs/verification.md) for the distinction between live evidence, synthetic checks and unverified setup/authentication guarantees.

## Frequently asked questions

### Can I use this with Claude or ChatGPT?

The tools are designed for clients that support Typenode's authenticated remote MCP connection. Add your own endpoint and complete the client-to-Typenode consent flow. Check current client support and refresh discovery after catalog changes; a healthy connection badge alone does not prove tool access.

### Does it change my Google account or reporting configuration?

No. The tools perform read-only API operations using `https://www.googleapis.com/auth/webmasters.readonly`. Some reporting methods use HTTP POST to retrieve data; that does not make them configuration writes.

### Do I need a Google Cloud project?

Yes for the tested customer-owned custom OAuth setup. Enable the relevant APIs and register an OAuth application. You also need Google account permission on the properties you query. See [Google's access guidance](https://developers.google.com/webmaster-tools/v1/prereqs).

### Does cloning the GitHub repository start the MCP server?

No. These files document the interface of a hosted server. Obtain the template at [https://typenode.ai/templates/google-search-console-mcp](https://typenode.ai/templates/google-search-console-mcp) and connect your own account; the contracts are not executable Workflows. See [setup](docs/setup.md) for prerequisites and current activation status.

### Can I combine GSC and GA4?

Yes: connect both sibling servers and let the AI client orchestrate their reads. GSC describes search visibility and clicks; GA4 describes recorded traffic and outcomes. Align dates, property scope and URL identities explicitly. These aggregates do not establish query-to-person signup attribution. See [combined recipes](prompts/with-ga4.md).

### Where do the data and credentials go?

Credentials are configured in your Typenode Workspace/Environment. Retrieved reporting data passes through Typenode execution and to the connected AI client. Review both services' data-handling terms for your account. This repository contains no live credential values or private execution captures.

## What is in this repository?

- [manifest.json](manifest.json): reference metadata, requirements and links to the tool contracts.
- [tools/](tools/): names, descriptions, input/output schemas and reference safety annotations. Host propagation of annotations is not certified. No implementation code or Workflow graphs.
- [docs/setup.md](docs/setup.md): account/credential requirements, hosted activation status and first-read checks.
- [prompts/](prompts/): copy-paste task recipes, not protocol-registered prompt resources.
- [examples/](examples/): illustrative calls and source-shaped responses.

Use the contracts to inspect supported arguments, plan client integrations and understand response shapes. Editing a contract file does not change the hosted tool. Workflow customisation and publication, where supported, happen within Typenode.

## Related templates and support

The complementary **Google Analytics 4 MCP** covers the other side of search visibility and recorded on-site activity. Use the combined recipe linked above to understand which questions need both.

For an implementation issue, include the tool name, package version, sanitised arguments and error/coverage evidence in a repository issue. Keep tokens, OAuth client secrets, consent URLs and private datasets out of public reports.

Created by Typenode. This template is not affiliated with or endorsed by Google. The contracts and documentation in this repository are provided under the [MIT licence](LICENSE); the hosted implementation is excluded from this repository and licence grant. Third-party names and marks belong to their respective owners.
