# Verification and release status

Reconciled on 17 October 2026 against the current reviewed template artifact, all saved Templates installation interfaces and available client descriptions. This document distinguishes the built servers' evidence from the public documentation and activation flow. The repository contains contracts only, not their implementation.

| Area | Evidence and limit |
|---|---|
| Contracts | All 18 tool names/descriptions match the saved bindings; input/output schemas are extracted from the saved Workflow interfaces. Code, graph topology and Trigger definitions are excluded. |
| Original servers | The 7 October 2026 acceptance pass recorded successful live consumer reads for all 18 GSC and 19 GA4 tools, with representative client replies independently matched to execution outputs. |
| Audience questions | That shared pass exercised and reviewed 20 GSC, 20 GA4 and 10 combined questions. Two original adapter failures passed exact-request retests; interpretation caveats remain. |
| Interactions | Live checks covered selected continuation, recipe mismatch, presets and bundle behavior. GA4 also exercised funnel caps and unavailable native rates. These observations do not prove every provider field combination. |
| Synthetic/replay checks | The retained shared suite reported 867 passing runtime output cases. This is a combined suite count, not 18 tools multiplied by live calls. Quota and permission failures were simulated rather than deliberately forced live. |
| Current Templates installation | All 37 Google Workflows have live deployments with no unpublished drift. The regex amendment passed 181 local cases and 37 source validators; intended-client property/report reads succeeded for both servers, including a GA4 nested AND/NOT filter. Representative malformed requests returned actionable corrections without Google calls. This was not a fresh all-tool live rerun. |
| This reference package | Contract JSON, schemas, examples, local links, canonical interface agreement and absence of implementation fields are checked locally. These are documentation checks, not live execution evidence. |
| Public activation flow | The reviewed bundle was published to production on 17 October 2026 and its exact snapshot/tool inventory was read back through the catalog MCP. The landing page is available; independent customer installation remains unverified. The public contracts are not executable installation files. |
| Authentication | Post-expiry renewal and client discovery must be checked on the final public setup path. Do not infer lifecycle reliability from a connected badge. |

## Known limits

- The original acceptance observed an accepted invocation whose runtime status was unavailable and recovered by polling the same invocation. Recovery is evidence of that result, not proof the platform defect is fixed.
- A connected-health indicator versus CLI authentication discrepancy was observed; its cause was not established in that acceptance pass.
- Changing Google data can change subsequent pages. Continuation does not create a snapshot or guarantee exactly-once enumeration.
- Native empty, incomplete, withheld or restricted data remains evidence with limits; the wrapper does not invent missing measurements.
- The AI client's conclusions are separate from server retrieval correctness.
- Formatting regexes omitted from discovery remain enforced in preflight; other advertised schema constraints can reject at admission. Broader lean prototype schemas were not deployed.
- GA4's recursive schemas remain large. Successful intended-client reads do not certify every recursive/funnel combination or universal host compatibility.
- Search Analytics rows are not an exhaustive inventory of all queries; supplied-URL inspection is not a crawl or sitewide index census.

## Before public promotion

1. Align the reference manifest with final template-library metadata, preserving the separation between public contracts and private implementation.
2. Verify the Typenode activation flow in an independent Workspace/Environment with that installation's Google connection.
3. Discover the full catalog and make at least one successful real client call through each tool; retain interaction checks separately.
4. Verify Google renewal and client-to-Typenode renewal after known expiry, plus a supported reconnect path.
5. Reassess platform observations against current release evidence and record accepted limits.
6. Verify the landing page points to the intended published snapshot, and review licence scope and branding.

Private execution captures, account identifiers, grants and consent links are deliberately absent. The example files contain invented values and are not live proof. The detailed source evidence stays with the maintainers; request a shareable summary through the published repository's issue tracker when available.
