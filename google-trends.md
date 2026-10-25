# Turn a current trends feed into separate n8n topic items

Content researchers often need a small list of current topics to inspect, rather than a promise that a topic will become popular. Automatron's [Trending now feed for Google Trends](https://apify.com/automatron/google-trends-now-feed) returns timestamped RSS topics and attributed news links.

## Example

Use this input in Apify Console:

```json
{"country":"US","maxItems":20}
```

Select build `latest`, 256 MB memory, a 60-second timeout and a $0.01 maximum total charge. Start one manual run using your own account. Read its `REPORT`, `REPORT-MARKDOWN` and `SUMMARY` output. A successful nonempty feed includes one dataset report row with a `trends` array; the dataset does not contain one row per topic.

In n8n, use a manual trigger while configuring the workflow. Fetch that completed run's dataset using your own Apify credentials, then use **Split Out** on `trends`. Keep `country`, `observedAt` and the source links with each item. Inspect the topics and their news sources before using them in an editorial plan. Enable any recurrence only after checking your own budget.

## Price and limitations

The Actor event fee is **$0.01 per completed nonempty country feed**, up to 20 topics. There is no model charge or separate source API key. Apify reads/storage and n8n hosting may have separate costs under your plans. Repeated runs are separate purchases. Empty and failed feeds do not incur the Actor event fee.

Supported countries are US, GB, BE, DE and FR. The source is the current Google Trends RSS feed; traffic values are approximate buckets, not exact search volumes. This tool provides no keyword history, related queries or prediction of virality. Source failures and stale feeds stop delivery; do not mistake missing data for no interest.

## Validation and support

The input and array mapping are checked offline against the released Actor contract. That does not verify your n8n installation or represent an independent customer result. The published Actor has separate delivery qualification; no customer data is included here.

Purchase and run through [Automatron on Apify](https://apify.com/automatron/google-trends-now-feed). Ask questions in this repository's Issues or the Actor's Apify Issues. Please omit tokens, private datasets and customer information. After using it, an honest Apify review is welcome whether your experience was positive or negative. No incentive is offered.

AI disclosure: this tutorial was prepared with AI assistance and checked against the product's source and example tests.

<!-- automatron-action:4b32ad7e9275174492d99dcb7d37ff0686e499938e49119ba4460e1cdfb3c5ea -->
