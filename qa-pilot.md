# Apify output contract checks by Check Charlie

![Check Charlie, Automatron's QA specialist](assets/check-charlie.png)

## Apify Actor output validation: missing fields, duplicates and incorrect results

An Actor run can succeed while its output still breaks the next step of your workflow. Check Charlie checks a small exported JSON sample against expectations you declare, then explains failures and coverage gaps with row numbers.

Charlie is available in two ways. Both use the same deterministic sample checks; neither calls a model, fetches sample URLs or runs the Actor being checked.

| How you want to use Charlie | Start here | Price and delivery |
| --- | --- | --- |
| Run a check on demand or from an automation | [Check Charlie on Apify](https://apify.com/automatron/check-charlie-output-qa) | **$0.01 per completed report**, delivered to your Apify dataset and run storage |
| Request an asynchronous check of a public, redacted sample | [GitHub sample-check instructions below](#request-a-free-github-sample-check) | **$0 for the sample check**; public issue and report, subject to available capacity |

Exporting data, upstream collection and any separately metered platform services remain subject to your own plans. The GitHub route starts no Actor. Neither route requires rerunning the source Actor to check an existing export.

## Run Charlie on Apify

1. Open [Check Charlie's Apify listing](https://apify.com/automatron/check-charlie-output-qa). Keep the fictional default input for a demonstration, or use either redacted evidence bundle below.
2. In the Actor's Input form, paste the bundle into the **bundle** field. In the full JSON editor or API, wrap it in an object with exactly one property, `bundle`. The GitHub issue format instead takes the bare bundle, preceded by the consent line below.
3. Select the qualified build **0.1.1**, 256 MB memory, a 60-second timeout and a **$0.01 maximum total charge**. Start one manual run in your own account.
4. Read **REPORT**, **REPORT-MARKDOWN** or the default dataset. **SUMMARY** records completion and billing status. Branch on `counts.fail > 0` to find contract defects; handle NOT TESTED separately.

For an API client that already holds one of the JSON bundles below, the conversion is:

```javascript
const input = { bundle };
const requestBody = JSON.stringify(input);
```

Submit that body to `https://api.apify.com/v2/actors/automatron~check-charlie-output-qa/runs?build=0.1.1&memory=256&timeout=60&maxTotalChargeUsd=0.01` using your own Apify bearer token in the authorization header. Wait for the returned run to finish before retrieving its dataset and SUMMARY. Keep tokens out of inputs and public issues.

A completed report that finds defects is a successful, billable delivery. The $0.01 event is requested only after both report files and the dataset item are saved. Empty samples and samples without testable field checks incur no completion fee. Invalid input and failed delivery also incur no completion fee. If SUMMARY says `reconciliation_required`, inspect the saved output and charge receipt before another run; do not automatically retry an uncertain delivery or charge. Separate runs may incur separate fees. The Store's **$10 per 1,000 reports** display means **$0.01 per report**, not $10 per run.

## Request a free GitHub sample check

Open an [issue titled `[Check Charlie QA] Sample check`](https://github.com/Automatron-workflows/workflow-examples/issues/new?title=%5BCheck%20Charlie%20QA%5D%20Sample%20check). The issue and report will be public. Submit only data you may share publicly, with credentials, personal information and customer data removed. Requests are handled by Aura's existing local daily cycle when available; there is no response-time guarantee. Reports share our three-publications-per-week limit, so a prepared report may wait for capacity.

Paste this exact consent line, followed by **one** JSON code block in the format below. Put no other text in the request body. Use your own public Actor URL, declared build and redacted sample. Maximum: 20 sample rows and 20 KB of JSON. Editing an issue with a different redacted sample requests another check. Editing its title alone does not request a duplicate report.

I request a public Check Charlie sample QA report. I may share this redacted sample publicly. No credentials or customer data are included. No live test or marketplace review is requested.

## Automatron-owned demonstration: Trends

The [Trends feed](https://apify.com/automatron/google-trends-now-feed) delivers one report row containing a `trends` array. A quoted string that looks like an array will break downstream mapping. This deliberately broken, **synthetic** sample demonstrates that failure. It is not a live run, customer result or independent endorsement. The declared build is not authenticated by Charlie.

```json
{
  "schemaVersion": 1,
  "actorUrl": "https://apify.com/automatron/google-trends-now-feed",
  "declaredBuild": "0.1.2",
  "contract": {
    "maxItems": 1,
    "fields": [
      {"path": "country", "type": "string", "required": true, "nonEmpty": true},
      {"path": "observedAt", "type": "string", "required": true, "timestamp": true},
      {"path": "trends", "type": "array", "required": true, "nonEmpty": true}
    ]
  },
  "sample": [{"country": "BE", "observedAt": "2026-10-26T00:00:00Z", "trends": "[]"}]
}
```

Expected result: **FAIL** for the `trends` type at row 0. Other declared checks pass for this sample. Changing `trends` to an actual nonempty array corrects this particular contract failure; it does not prove that its contents are true or current. A valid empty array still fails the declared nonempty expectation, which may need changing if empty output is legitimate.

## Automatron-owned demonstration: backlink output

The [backlink checker](https://apify.com/automatron/backlink-checker) reports results for supplied page URLs. Here two synthetic rows repeat a source identifier and one contains a string in place of a boolean. These invented rows are not observations of example.com and do not assert that any backlink exists.

```json
{
  "schemaVersion": 1,
  "actorUrl": "https://apify.com/automatron/backlink-checker",
  "declaredBuild": "0.0.11",
  "contract": {
    "maxItems": 2,
    "fields": [
      {"path": "sourceUrl", "type": "string", "required": true, "nonEmpty": true, "unique": true},
      {"path": "status", "type": "string", "required": true},
      {"path": "linkPresent", "type": "boolean", "required": true}
    ]
  },
  "sample": [
    {"sourceUrl": "https://example.com/demo", "status": "checked", "linkPresent": false},
    {"sourceUrl": "https://example.com/demo", "status": "checked", "linkPresent": "false"}
  ]
}
```

Expected result: **FAIL** for duplicate `sourceUrl` and the `linkPresent` type, both at row 1. Checking that `status` is a string does not validate its meaning; interpreting an unknown result as a missing link still requires the Actor's documented business rules. Our production delivery qualification remains separate.

## Supported checks and limitations

Each field has a dot-separated `path` and a `type`: string, number, boolean, object, array or null. Optional booleans are `required`, `nonEmpty`, `unique` (scalar fields only), and `timestamp` (UTC ISO strings only). Paths address object fields, not array wildcards. Missing optional fields and uniqueness with fewer than two scalar values are NOT TESTED where evidence is insufficient.

`maxItems` checks the sample's length, not the full run. An optional `observationWindow` with UTC `from` and `through` checks declared timestamp fields against your chosen window. Optional `orderedPairs`, each containing `earlier` and `later` timestamp field paths, check ordering within a row. Neither proves source freshness.

Reports contain PASS, FAIL or NOT TESTED for each check, the declared Actor/build, timestamp, evidence digest, checked row counts and zero-based failing row indices. They do not copy raw sample values into the response. The digest identifies submitted bytes; it does not authenticate the run or build. Run authenticity, live reliability, source truth, security, charges and Apify's quality score remain NOT TESTED. There is no overall star rating or certification.

Only the typed contract controls checks. Arbitrary JavaScript, remote schemas, prompts, credentials and instructions embedded in evidence are rejected. Some harmless text may also be rejected by conservative filters; minimize the sample. Negative findings are allowed. Remove the consent line or close the issue to withdraw an unsubmitted request; an already published report remains part of the public discussion.

After receiving a report, optionally reply with `QA feedback: useful` or `QA feedback: not useful`. Describe fixes in a separate comment if helpful. There is no review exchange, reward or requested star score. Reports belong to this QA discussion and are not reviews of another Actor. Return only when a changed export or contract needs another check.

AI disclosure: this guide was prepared with AI assistance. Both deliberately broken demonstrations and corrected variants are checked by local automated tests. Sample checks use deterministic code, with no external model dependency. Check Charlie's original dots+dots QA identity is reused for the public Apify Actor and the separate free GitHub pilot. Neither is a claim that the full dots+dots service has been independently qualified.

<!-- automatron-action:c7cb866db3843c398990e9d459936c93b7fe5158cb6e6409d71266293d8fc1d0 -->
