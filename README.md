# Automatron workflow examples

Practical examples for turning Automatron's Apify outputs into useful automation steps. Start with the current trends feed if you need a small, attributed set of topics for an editorial research queue.

## Start here: current topics for an n8n workflow

Open [Trending now feed for Google Trends](https://apify.com/automatron/google-trends-now-feed) in Apify and use this input:

```json
{"country":"US","maxItems":20}
```

For one manual test in your own account, select build `latest`, 256 MB memory, a 60-second timeout and a $0.01 maximum total charge. A completed nonempty run produces `REPORT`, `REPORT-MARKDOWN` and `SUMMARY`, plus one dataset report row containing a `trends` array.

Follow the [n8n walkthrough](google-trends.md) to fetch that completed dataset and use **Split Out** on `trends`. Preserve the country, observation time and source links. Review the linked news before choosing topics. Configure and check the manual workflow before adding a schedule in your own account.

## Price and limitations

The Actor event fee is **$0.01 per completed nonempty country feed**, up to 20 topics. Empty or failed feeds do not incur that event fee. There is no model charge or separate source API key. Apify reads/storage and n8n hosting may carry separate costs under your plans; recurring runs are separate purchases.

Countries: US, GB, BE, DE and FR. Traffic buckets are approximate. The feed covers current Google Trends RSS topics; it provides no historical keyword series, exact search volume or prediction of popularity. Source failures and stale feeds stop delivery.

## Support and feedback

Use this repository's [Issues](https://github.com/Automatron-workflows/workflow-examples/issues) for questions about these examples, or the Actor's Apify Issues for a run problem. Include the failing step and a sanitized error. Keep credentials, private URLs, customer data and private datasets out of public issues. Support may use clearly labelled AI-assisted replies.

After actual use, an honest review on the [Apify listing](https://apify.com/automatron/google-trends-now-feed) is welcome regardless of whether the experience was positive or negative. No incentive is offered.

The JSON input and dataset mapping are checked against the released Actor contract. Your n8n installation still needs its own test. These examples contain no independent customer results.

AI disclosure: these examples were prepared with AI assistance and checked against the product's source and example tests.

<!-- automatron-action:6c8faef67f1c6edbf9fe7cc7f3b3ce1ac1a20adbfb97a5b8a815f7ee7b863b0e -->
