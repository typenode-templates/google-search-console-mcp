# Interface examples

All identifiers, dates, event labels and measurements in these examples are invented. These files are synthetic interface examples, not live results, pagination receipts or proof of available data.

- [tool-calls.json](tool-calls.json): one illustrative request for every exposed tool. Validate against the corresponding Workflow's input node, then substitute your discovered property and dates.
- [sample.request.json](sample.request.json): a request for `get_gsc_performance_totals`.
- [sample.response.json](sample.response.json): a full synthetic output shape for that tool. It illustrates its response contract; it is not a captured execution of the example request.

The public contracts live in [tools/](../tools/); examples are checked against their schemas rather than defining a second contract. Do not reuse fixture cursors against a live server. A real cursor must come from the previous result of the same recipe and connection.

When explaining a result, identify the source, dates and effective filters. Retain native metadata, numeric strings and coverage notes. Distinguish empty, partial and failed datasets; avoid inventing zero values or treating observed event counts as unique business outcomes.

Use [task prompts](../prompts/getting-started.md) for orchestration and [verification](../docs/verification.md) for actual evidence limits.
