# Check known backlink placements from a manual Clay workflow

SEO agencies often have a list of placement pages and need evidence of whether those pages still link to one exact destination. Automatron's [Backlink Checker](https://apify.com/automatron/backlink-checker) checks the supplied pages; it does not discover backlinks.

## Example

Copy the [Aura · Backlink placement verification starter](https://app.clay.com/shared-table/share_0tnhdnt7vPYo7MMeMBP), or follow the steps below. Its public preview contains one IANA input, buyer setup instructions and clearly labelled synthetic examples. The copied table preserves Manual mode and its description but starts with zero rows: add one row and paste the input below. It contains no Apify connection or executable enrichment; add the native action using your own account. Copying does not run the checker.

Start with one public example, using your own Apify connection:

```json
{"urls":["https://www.iana.org/domains/reserved"],"targetUrl":"https://www.iana.org/go/rfc6761"}
```

This is valid input, not a claim about the page's current links. In Clay, disable automatic table and enrichment runs before adding **Run Apify Actor**. Choose `automatron/backlink-checker` and map a real URL array to `urls` and the exact destination string to `targetUrl`. Do not pass a quoted JSON array or put a token in a table cell. The buyer supplies their own connection.

For a batch, use 1–25 pages sharing the same exact destination. Run manually only after reviewing the resolved input and budget. If Clay's action cannot apply a hard charge cap, run in Apify Console with the maximum charge set there, then import that existing run into Clay. For 25 completed checks, the Actor event fees are $0.10. Do not invent an input field for the charge cap.

Join output by run/batch reference and `sourceUrl`, never row position alone. Display **Present** only for `status: checked` with `linkPresent: true`, and **Missing in HTML** only for `status: checked` with `linkPresent: false`. Any other result is **Unknown / review required**. Keep unknown rows. Anchors and link attributes are in `links[].anchor` and `links[].rel`.

To compare a later run, keep the same target and save the real completed digests by source URL as `baseline`. Use only keys belonging to the current batch. Preserve earlier usable evidence if a later observation is unknown. Changed evidence does not itself prove a removed link.

## Price and limitations

The fee is **$0.004 per completed page check**; unknown results are unbilled by the Actor. Clay usage, other platform charges and repeated runs may add costs under your own plans. This checks fetched HTML, not every possible browser-rendered state. It does not include notifications, automatic baseline rotation or backlink discovery.

The shared starter's public preview, copying and disabled automatic runs were checked on 25 October 2026. Live Clay-to-Apify execution and Clay marketplace acceptance remain unverified. The synthetic examples illustrate Present, Missing in HTML and Unknown; they are not observations of the IANA input or customer success stories. Use the [complete published walkthrough](https://apify.com/automatron/backlink-checker#check-backlink-placements-from-clay) for the current product contract.

## Support

Purchase through [Automatron on Apify](https://apify.com/automatron/backlink-checker). Ask questions in this repository's Issues or Apify Issues, without credentials, private URLs or customer information. After actual use, an honest review is welcome regardless of satisfaction; no incentive is offered.

AI disclosure: this tutorial was prepared with AI assistance and checked against the product's source and example tests.

<!-- automatron-action:f881f98e31ee66e36868430c922d9debd530c9bfb9f5987f8e6c0126a95d16dc -->
