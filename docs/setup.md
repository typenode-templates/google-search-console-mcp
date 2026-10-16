# Set up Google Search Console MCP

This repository documents the interface of a Typenode-hosted MCP server: tool contracts, prerequisites and usage examples. Tool implementations run within Typenode and are not distributed in this repository. The template page is [available](https://typenode.ai/templates/google-search-console-mcp); an independent customer installation remains to be verified; these JSON contracts cannot be imported as executable tools.

## 1. Prepare your accounts

Use your own Typenode Workspace and access to this MCP template through Typenode. Normal account/billing rules apply. The repository explains the requirements; start from the [template page](https://typenode.ai/templates/google-search-console-mcp) and its current setup instructions.

Use a Google account with access to the Search Console properties you intend to query. Registering a Cloud project or granting an OAuth scope does not grant access to a reporting property. Check Google's [API access guidance](https://developers.google.com/webmaster-tools/v1/prereqs).

## 2. Configure a Google OAuth application

Create or select a Google Cloud project you control. Enable:

- **Google Search Console API** (`searchconsole.googleapis.com`).

Configure Google Auth Platform's consent screen/audience. If using an external app in testing, add the connecting Google identity as a test user. Review Google's current testing and production requirements before offering access to other people.

Create a Web application OAuth client. Register the exact callback URI supplied by Typenode for this OAuth application. Obtain the client ID and client secret; enter them only through Typenode's secure credential setup.

For a custom Google OAuth configuration, use the following provider endpoints and template scope:

| Setting | Value |
|---|---|
| Authorization endpoint | `https://accounts.google.com/o/oauth2/v2/auth` |
| Token endpoint | `https://oauth2.googleapis.com/token` |
| Scope | `https://www.googleapis.com/auth/webmasters.readonly` |
| Provider renewal | Request Google's `access_type=offline` where the custom OAuth configuration supports authorization parameters; confirm a refresh token is obtained. |

Follow [Google's Web server OAuth documentation](https://developers.google.com/identity/protocols/oauth2/web-server). Google offline access is an authorization parameter, not a Google scope named `offline_access`. Re-consent may be needed when an existing grant does not return a refresh token.

The tested setup uses a customer-owned custom OAuth app. Managed Google OAuth and service-account installation are not verified template setup paths. To share one Google connection between the sibling GSC and GA4 templates, enable all three APIs and request both read-only scopes; each template alone needs only its own scope and listed APIs.

## 3. Connect Google in Typenode

Use Typenode's secure setup for the Google OAuth-backed Credential in the Environment where the server runs. Complete Google consent yourself. Follow the template's Typenode setup instructions for assigning that connection to the server; credential wiring stays within Typenode.

The OAuth client ID and secret belong in secure application/credential configuration, not in a public repository or tool arguments. The setup must support provider renewal rather than relying on a pasted short-lived token.

## 4. Activate the hosted MCP template

Start from the linked template page and obtain your copy through Typenode's supported setup flow. The manifest in this repository is a reference inventory, not an executable installer or Workflow blueprint. Do not attempt to create Workflows from the tool contract JSON files.

The installing agent connects the Google Credential in the selected Environment, sets `GSC_CREDENTIAL_CONTEXT` to its stable Credential ID and uses the matching `GSC_ACCESS_TOKEN` symbolic Secret. It validates each Workflow, creates its synchronous authenticated webhook trigger before its binding, and observes each deployment until terminal success. These names contain no token values. Activation exposes the documented tools. A fresh independent installation of the latest published snapshot remains unverified; the existing built servers' live evidence is recorded separately in [verification](verification.md).

## 5. Connect your AI client

Get the MCP endpoint for **your** server in **your** Environment from Typenode. Add that remote endpoint to your client's supported MCP connection UI and complete the Typenode OAuth consent.

This is a second authentication boundary: the client authenticates to Typenode; Typenode separately authenticates to Google. For renewable client access, verify that the Typenode issuer grants refresh access (`offline_access` where required) and that renewal works after expiry. Google consent settings cannot repair an expired client-to-Typenode grant. Follow current client and Typenode UI instructions; these drafts do not assume a particular scope-selection screen is available.

Use a client that supports Typenode's authenticated remote MCP connection. Confirm fresh discovery contains all 18 domain tools. A connected badge alone is insufficient. After catalog updates, refresh tool discovery using the client's supported refresh/reconnect path.

## 6. Make the first reads

Ask: **“List the Search Console properties I can access.”**. Select an accessible property from the actual result, then ask the next question in [Getting started](../prompts/getting-started.md) using explicit dates. Never substitute the invented example property for a real discovered one.

Success means the actual tool exchange supplies a typed source result, the selected identifier is correct, and each page either ends explicitly or supplies its documented continuation. Empty data is a valid retrieval result. Later verify access after known token expiry; the final public activation flow has not yet passed a fresh independent installation.

## Troubleshooting

| Symptom | Check |
|---|---|
| Client returns UNAUTHORIZED before a workflow starts | Typenode client grant, expiry, refresh access and reconnect path. |
| Google authentication failure inside a result | OAuth-backed Google credential and provider refresh. |
| API disabled or access denied | Enabled API in the OAuth application's project, required scope, selected Google identity and property permission. |
| Empty report | Dates, filters, property, instrumentation and native coverage metadata. Do not assume no real-world activity. |
| Cursor mismatch | Repeat the same effective recipe/page size/connection, or restart without the cursor. |
| Google quota error | Inspect native quota/error evidence and retry later; do not advance the cursor or retry immediately. |
| Accepted invocation has unavailable runtime status | Preserve its identity and inspect/poll that invocation before starting another acquisition. |

## Costs

The licence for these contracts and documentation does not pay for hosting or AI-client access. Typenode account/execution costs and any AI-client subscription are separate. Google API quotas also apply; reported HTTP read counts are not prices or GA4 quota-token debits. Check [Google's quota documentation](https://developers.google.com/webmaster-tools/limits) and [current Typenode information](https://typenode.ai) for your situation.
