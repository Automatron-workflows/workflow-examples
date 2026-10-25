# Check known backlink placements from a manual Clay workflow

SEO agencies often have a list of placement pages and need evidence of whether those pages still link to one exact destination. Automatron's [Backlink Checker](https://apify.com/automatron/backlink-checker) checks the supplied pages; it does not discover backlinks.

## Example

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

This is a manual setup guide. A copyable native Clay template and live Clay execution have not been verified. The example input is checked offline; it is not a fabricated customer success story. Use the [complete published walkthrough](https://apify.com/automatron/backlink-checker#check-backlink-placements-from-clay) for the current product contract.

## Support

Purchase through [Automatron on Apify](https://apify.com/automatron/backlink-checker). Ask questions in this repository's Issues or Apify Issues, without credentials, private URLs or customer information. After actual use, an honest review is welcome regardless of satisfaction; no incentive is offered.

AI disclosure: this tutorial was prepared with AI assistance and checked against the product's source and example tests.

<!-- automatron-action:4a12fb26383b43229fe3fbca9ece31139965aa5c7ca0799312b0c9addaff83d2 -->
