# The Price of a Gigabyte: Residential Proxy Prices 2019–2026 (dataset)

Dated residential proxy prices per GB for 12 providers, read from their own pricing pages (live on 2 October 2026) and from Wayback Machine captures back to 2019, plus a monthly GB Price Index (July 2024 = 100).

- **Published by:** [ProxyPicker](https://proxypicker.com/), an independent data lab for the proxy and web-data industry
- **Site page (full write-up, charts, quotes):** https://proxypicker.com/price-of-a-gigabyte/
- **Version:** 2026-10-02 (data as of 2 October 2026 unless a file says otherwise)
- **Licence:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) for ProxyPicker’s data, see [LICENSE](LICENSE) and *Sources and licences* below
- **DOI:** not minted yet. A Zenodo DOI will be added when the first GitHub release is archived.
- **Contact:** info@proxypicker.com (corrections, press and data requests)

## Files

| File | Rows | Source CSV on the site |
|---|---:|---|
| `data/gb-price-index-2019-2026.csv` | 16 | `proxypicker-gb-price-index-2019-2026-v2.csv` |
| `data/gb-price-by-provider-2019-2026.csv` | 24 | `proxypicker-gb-price-by-provider-2019-2026.csv` |
| `data/gb-price-observations-2019-2026.csv` | 108 | `proxypicker-gb-price-observations-2019-2026.csv` (columns removed, see below) |
| `data/SHA256SUMS` | | SHA-256 checksums (`cd data && sha256sum -c SHA256SUMS`) |

All files are UTF-8, comma-separated, with a header row. Blank cells mean *no value*, not zero.

**Differences from the site CSVs.** `entry_quote` and `rate_100gb_quote` (verbatim page text) and `raw_file` (a path on our server) were removed from the observations file. Verbatim quotes from third-party pages are not included here (they remain the property of their publishers). Each row keeps the source URL so you can check it; the quote CSV is downloadable on the site page.

## Data dictionary

### `gb-price-index-2019-2026.csv`

| Column | Meaning |
|---|---|
| `period` | Half-year period (YYYY-MM, January or July) or `2026-10` for the live check on 2 October 2026 |
| `n_entry` | Number of providers with an entry price in the period |
| `median_entry_usd_per_gb` | Median entry price, USD per GB |
| `min_entry` | Lowest entry price, USD/GB |
| `max_entry` | Highest entry price, USD/GB |
| `n_100gb` | Number of providers with a 100 GB rate |
| `median_100gb_usd_per_gb` | Median rate at 100 GB, USD/GB |
| `min_100gb` | Lowest 100 GB rate, USD/GB |
| `max_100gb` | Highest 100 GB rate, USD/GB |
| `providers_entry` | Providers counted in the entry figures (semicolon-separated) |
| `providers_100gb` | Providers counted in the 100 GB figures |
| `n_priced_pages` | Pricing pages with readable prices in the period |
| `n_showing_discount_or_code` | Of those, pages showing a struck-through price or coupon code |
| `providers_showing_discount_or_code` | Which providers showed one |
| `index_100gb_jul2024_100` | GB Price Index at 100 GB (July 2024 = 100), same-provider chained |
| `index_n_100gb` | Providers in the 100 GB index for the period |
| `index_providers_100gb` | Which providers |
| `index_entry_jul2024_100` | GB Price Index on entry prices (July 2024 = 100) |
| `index_n_entry` | Providers in the entry index |
| `index_providers_entry` | Which providers |

### `gb-price-by-provider-2019-2026.csv`

| Column | Meaning |
|---|---|
| `metric` | `entry_usd_per_gb` or `rate_100gb_usd_per_gb` |
| `provider` | Provider name (current brand; former names in brackets in other files) |
| `2019-07` … `2026-10 (live)` | Value for that period, USD/GB. `not captured` = no readable capture; blank = page read but no comparable price (applies to every period column) |

### `gb-price-observations-2019-2026.csv`

| Column | Meaning |
|---|---|
| `provider` | Provider name (current brand; former names in brackets in other files) |
| `period` | Half-year period (YYYY-MM, January or July) or `2026-10` for the live check on 2 October 2026 |
| `capture_timestamp` | Wayback Machine capture timestamp (YYYYMMDDhhmmss, UTC), or live fetch time |
| `source_url` | Pricing page URL as captured |
| `wayback_url` | Raw Wayback capture URL (`id_` form) used |
| `entry_usd_per_gb` | Entry price, USD/GB: pay-as-you-go if shown, otherwise the smallest monthly plan |
| `entry_basis` | Which plan the entry price comes from |
| `regular_entry_usd_per_gb` | Struck-through “regular” entry price, if shown |
| `coupon_entry_usd_per_gb` | Entry price after a code shown on the page, if any |
| `rate_100gb_usd_per_gb` | Rate at about 100 GB, USD/GB: best plan ≤100 GB, or the band containing 100 GB |
| `rate_100gb_basis` | Which plan the 100 GB rate comes from |
| `regular_100gb_usd_per_gb` | Struck-through “regular” 100 GB rate, if shown |
| `coupon_100gb_usd_per_gb` | 100 GB rate after a code shown on the page |
| `promo_shown` | Discount or code shown on the page (free text) |
| `notes` | Reading notes |

## Methodology and limitations

The text below is copied from the methodology on the [site page](https://proxypicker.com/price-of-a-gigabyte/), which also has the charts and tables it refers to.

### What we couldn’t verify

- **IPRoyal**: the Wayback Machine has no captures of its residential pricing page, so it appears in today’s table only.
- **Pages built by JavaScript**: some archived captures contain no prices at all (Decodo in 2022, Rayobyte in mid-2026, NodeMaven before 2026, Proxy-Seller throughout, Bright Data’s residential tab before mid-2020). We left those periods blank rather than guess.
- **Bright Data before 2022**: the pay-as-you-go rate wasn’t captured; only the $1,000/month plan was.
- **“From” prices**: Proxy-Cheap stopped publishing a tier table in late 2023 and DataImpulse’s pre-2024 pages only say “from $1”. These periods are blank.

### Methodology (data pulled 2 October 2026)

- **Product**: rotating residential proxies, priced per GB, US dollars, monthly billing, excluding VAT. Annual-billing discounts are ignored.
- **Entry rate**: the price per GB on the cheapest way to start: pay-as-you-go if the page shows it, otherwise the smallest monthly plan.
- **100 GB rate**: the price per GB if you buy 100 GB in one month. For fixed-size plans we use the best rate among plans of 100 GB or less. For dollar-commitment plans we divide the plan price by the rate. For volume bands we use the band that contains 100 GB.
- **Discounts**: we use the price you pay without typing a code. On-page automatic sale prices count; coupon-code prices are recorded separately and excluded.
- **History**: for each provider we pulled every archived capture of its pricing page from the Wayback Machine CDX API (2018 onward), picked the capture closest to 1 January and 1 July of each year (within ±75 days), and saved the raw HTML. A period with no capture in that window, or with no readable price, is a gap.
- **Today**: each live pricing page was downloaded on 2026-10-02 and read the same way.
- **Verification**: every number in the dataset is stored with the exact text it was read from. A script checks that this text appears verbatim in the saved page before the number is used.
- **Index**: for each period, the geometric mean of each provider’s price divided by its own July 2024 price, over providers readable in both periods; July 2024 = 100. The number of providers behind each point is in the table and the CSV. Plain medians are shown alongside with their n.

#### Limitations

- Small sample, especially before 2023 (two or three readable providers per period). Treat early figures as indicative.
- List prices aren’t what big customers pay: enterprise contracts are negotiated and not public.
- Providers define a “GB” and their pools differently, and SOAX now prices by country tier (we use Tier 1: US/UK/AU/JP). This is a price index, not a quality comparison.
- Six-month spacing means short promotions between captures are missed.
- Live prices change often. Everything here is as of the date shown.

## Sources and licences

- **Provider pricing pages (live, 2 October 2026) and Internet Archive Wayback Machine captures.** Prices are facts read by ProxyPicker; no page text is redistributed.

ProxyPicker’s compilation, classifications, calculations and notes are licensed CC BY 4.0. Third-party material keeps its own licence as listed above. Provider and product names are trademarks of their owners; no provider endorses or sponsors this dataset.

## How to cite

> ProxyPicker. (2026). *The Price of a Gigabyte: Residential Proxy Prices 2019–2026* (Version 2026-10-02) [Data set]. https://github.com/jameyriley46-ux/proxypicker-price-of-a-gigabyte-dataset

Please also link to the site page: https://proxypicker.com/price-of-a-gigabyte/

```bibtex
@misc{proxypicker_price_of_a_gigabyte_2026,
  author = {{ProxyPicker}},
  title = {{The Price of a Gigabyte: Residential Proxy Prices 2019–2026}},
  year = {2026},
  version = {2026-10-02},
  howpublished = {\url{https://github.com/jameyriley46-ux/proxypicker-price-of-a-gigabyte-dataset}},
  note = {Data set. See https://proxypicker.com/price-of-a-gigabyte/}
}
```

A `CITATION.cff` file is included, so GitHub’s “Cite this repository” button gives the same citation.
