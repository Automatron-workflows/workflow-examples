# Turn a current trends feed into separate n8n topic items

Content researchers often need a small list of current topics to inspect, rather than a promise that a topic will become popular. Automatron's [Trending now feed for Google Trends](https://apify.com/automatron/google-trends-now-feed) returns timestamped RSS topics and attributed news links.

## Example

### Try the mapping with no Apify run

Download [the manual n8n demo](google-trends-demo.json), then use n8n's **Import from File**. Click **Execute workflow** once. The fictional report becomes two items, each with a `topic` object plus `country`, `observedAt` and a demonstration label. The workflow has no credentials, HTTP requests or schedule. It causes no Apify event charge; your own n8n hosting terms still apply.

The topics, traffic buckets and timestamp in this demo are invented for an output-mapping test. They are not current trends, customer results or evidence that the Actor was run. Keep that label on demonstration output.

### Get current source data

Use this input in Apify Console:

```json
{"country":"US","maxItems":20}
```

Select build `latest`, 256 MB memory, a 60-second timeout and a $0.01 maximum total charge. Start one manual run using your own account. Read its `REPORT`, `REPORT-MARKDOWN` and `SUMMARY` output. A successful nonempty feed includes one dataset report row with a `trends` array; the dataset does not contain one row per topic.

In n8n, use a manual trigger while configuring the workflow. Fetch that completed run's dataset using your own Apify credentials, then use **Split Out** on `trends`. Keep `country`, `observedAt` and the source links with each item. Inspect the topics and their news sources before using them in an editorial plan. Enable any recurrence only after checking your own budget.

To adapt the demo, replace its fictional-report node with your completed run's `REPORT`, or the single report row from its dataset. Keep **One item per topic** configured to split `trends` into the destination field `topic`. The live topic fields include `topic.topic`, `topic.approximateTraffic`, `topic.sourcePublishedAt` and `topic.news`. Keep credentials in n8n's credential store, never in exported workflow JSON.

For example, one demonstration output item is:

```json
{"topic":{"topic":"Fictional topic: city garden","approximateTraffic":"200+","news":[{"title":"Fictional source reference","url":"https://example.com/garden","publisher":"Example publisher"}]},"country":"US","observedAt":"2026-10-25T00:00:00.000Z","demonstration":"Fictional example; not an Actor run."}
```

## Price and limitations

The Actor event fee is **$0.01 per completed nonempty country feed**, up to 20 topics. There is no model charge or separate source API key. Apify reads/storage and n8n hosting may have separate costs under your plans. Repeated runs are separate purchases. Empty and failed feeds do not incur the Actor event fee.

Apify's [Free plan](https://apify.com/pricing) currently includes $5 monthly usage credit (checked 25 October 2026). Eligible users with sufficient remaining credit can use their own allowance for a first run. Check your plan and remaining balance before starting; this is not unlimited free use. Free-plan PPE activity provides no developer revenue under [Apify's current economics](https://docs.apify.com/actors/monetize/pricing-and-costs).

Supported countries are US, GB, BE, DE and FR. The source is the current Google Trends RSS feed; traffic values are approximate buckets, not exact search volumes. This tool provides no keyword history, related queries or prediction of virality. Source failures and stale feeds stop delivery; do not mistake missing data for no interest.

## Validation and support

The input and array mapping are checked offline against the released Actor contract. That does not verify your n8n installation or represent an independent customer result. The published Actor has separate delivery qualification; no customer data is included here.

Purchase and run through [Automatron on Apify](https://apify.com/automatron/google-trends-now-feed). Ask questions in this repository's Issues or the Actor's Apify Issues. Please omit tokens, private datasets and customer information. After using it, an honest Apify review is welcome whether your experience was positive or negative. No incentive is offered.

If this could help a future workflow, optionally **bookmark the Actor**. After actual use, separately consider an **honest review** describing what worked and what needs improvement. No star score is requested. Run it again when you actually need fresh topics.

AI disclosure: this tutorial was prepared with AI assistance and checked against the product's source and example tests.

<!-- automatron-action:c91d68bb7557c669aedef8f8772cfc330dfb28720615c9f6485e8ac485d63290 -->
