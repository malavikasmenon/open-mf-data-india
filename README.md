# open-mf-data-india

The published dataset behind [Open Indian Fund Data](https://github.com/malavikasmenon/india-mf-explorer-web)
— Indian mutual fund scheme and NAV data, updated daily by that repo's
pipeline, served here as plain Parquet files.


## Structure

```
data/
  schemes/schemes.parquet   — scheme dimension, rebuilt daily
  nav/year=YYYY/month=MM/*.parquet — NAV fact table, partitioned by month
  manifest.json              — catalog the frontend reads to discover tables
  *.ingest.json               — provenance (source, retrieval time) per table
  nav_backfill_failures.json — scheme codes the last backfill couldn't fetch
```

Updated daily by [`update-data.yml`](.github/workflows/update-data.yml).
`nav_backfill_failures.json`'s absence means the last run had no failures.



## Disclaimer

This data is provided **as-is, with no guarantee of accuracy, completeness,
or timeliness**. It is compiled from AMFI's public disclosures and from
mfapi.in (a mirror of AMFI's scheme data), and while the pipeline tries to
catch and record fetch failures rather than silently dropping data, errors,
gaps, and upstream mistakes can and do happen — see `data/nav_backfill_failures.json`
for scheme codes the pipeline knows it couldn't fetch.

**We are not responsible for any loss, damage, or decision made based on this
data.** This is not financial advice, and this dataset should not be the sole
basis for any investment decision. If accuracy matters for your use case,
verify against AMFI's own published data before relying on it.
