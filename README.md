# Google Trends RSS, n8n and backlink verification examples

Practical Automatron examples for two jobs: finding current topics for an editorial research queue and checking whether known placement pages still link to your site.

## Choose your workflow

| Your task | Start here | What is ready |
| --- | --- | --- |
| Try topic-to-item mapping without credentials | [Import the n8n demo](google-trends-demo.json) and follow the [walkthrough](google-trends.md) | Tested manual workflow with two explicitly fictional topics; no network requests or automatic runs |
| Get current Belgian topics and news sources | [Copy the Belgian editorial research example on Apify](https://apify.com/automatron/google-trends-now-feed/examples/belgium-trending-topics-editorial-research) | Preset for BE and up to 20 topics; run in your own account |
| Check existing backlink placements from Clay | [Backlink/Clay walkthrough and copyable starter](backlink-clay.md) | Manual buyer setup and synthetic examples; live Clay-to-Apify execution remains unverified |

The [Trends Actor](https://apify.com/automatron/google-trends-now-feed) costs **$0.01 per completed nonempty feed**. The [Backlink Checker](https://apify.com/automatron/backlink-checker) costs **$0.004 per completed page check**. The checker verifies supplied URLs against one exact destination; it does not discover backlinks. Other platform costs depend on your own plans. Use your own remaining eligible Apify allowance for a trial; there is no publisher-funded trial or unlimited-free promise.

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

## Make a useful return visit

For an editorial queue, save a task in your own Apify account after a useful first run. Revisit it when you next need fresh topics, and keep the observation time and source news links with your shortlist. Review news sources before publishing. Run manually until you have checked value and cost; any schedule belongs in your own account and creates separately charged runs.

For link retention, save the real completed per-page digests from the first check and follow the [baseline instructions](backlink-clay.md) when you actually need another audit. Keep unknown results separate from confirmed missing links. This example does not add alerts or rotate baselines automatically.

Optionally bookmark the relevant Actor to find it again. After actual use, share an honest review of what worked and what needs improvement, regardless of satisfaction. No requested star score or reward.

## Support and feedback

Use this repository's [Issues](https://github.com/Automatron-workflows/workflow-examples/issues) for questions about these examples, or the Actor's Apify Issues for a run problem. Include the failing step and a sanitized error. Keep credentials, private URLs, customer data and private datasets out of public issues. Support may use clearly labelled AI-assisted replies.

After actual use, an honest review on the [Apify listing](https://apify.com/automatron/google-trends-now-feed) is welcome regardless of whether the experience was positive or negative. No incentive is offered.

The JSON input and dataset mapping are checked against the released Actor contract. Your n8n installation still needs its own test. These examples contain no independent customer results.

AI disclosure: these examples were prepared with AI assistance and checked against the product's source and example tests.

<!-- automatron-action:ed32e3e8a9abd51891f2e6bc56a59a966b29a35f562737bff4a6c26c52a07304 -->
