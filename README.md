# Ratelens MRP Mismatch Index

Open data on products where Amazon.in and Flipkart declare **different Maximum
Retail Prices for the same item**.

Under India's Legal Metrology (Packaged Commodities) Rules, MRP is a property of
the product, not of the shop: two retailers may charge different prices, but they
should not publish different MRPs for the same item. Where they do, the
advertised "% off" is calculated from a figure at least one of them has wrong —
so the discount badge can differ even when the selling price is identical.

In the August 2026 edition, **54 products**
carried a different declared MRP across the two platforms. In
**15** of them the selling price was effectively the
same, leaving the size of the discount badge as the only difference. The median
gap between the two declared MRPs was **13.5%**.

**Canonical source:** https://www.ratelens.in/reports/mrp-mismatch/
**Maintained by:** Ratelens (https://www.ratelens.in) — a price-comparison site for personal
grooming appliances in India.

## Editions

Each edition is frozen on the last day of its month and never rewritten, so a
figure cited from it stays true.

| Edition | Observed | Mismatches | Same selling price | Products matched | Listings observed | Data |
|---|---|---|---|---|---|---|
| [August 2026](https://www.ratelens.in/reports/mrp-mismatch/2026-08/) | 2026-08-31 | 54 | 15 | 197 | 6201 | [CSV](mrp-mismatch-2026-08.csv) |

## Columns

| Column | Type | Meaning |
|---|---|---|
| `brand` | string | Manufacturer brand as listed. |
| `model` | string | Manufacturer model code used to match the product across platforms. |
| `slug` | string | Ratelens page identifier; resolves to `https://www.ratelens.in/product/<slug>/` |
| `a_price` | number | Selling price observed on the Amazon.in listing, INR. |
| `a_mrp` | number | Maximum Retail Price declared by the Amazon.in listing, INR. |
| `a_off` | integer | Discount percentage advertised on the Amazon.in listing. |
| `f_price` | number | Selling price observed on the Flipkart listing, INR. |
| `f_mrp` | number | Maximum Retail Price declared by the Flipkart listing, INR. |
| `f_off` | integer | Discount percentage advertised on the Flipkart listing. |
| `gap` | integer | Percentage difference between the two declared MRPs. |
| `grade` | string | Confidence that the mismatch is real: High, Medium or Low. |
| `can_name` | boolean | True only when a third listing lets a majority identify which platform is the outlier. When false, the data shows the two declared MRPs cannot both be correct, but not which one is wrong. |

## Method

1. Products are matched across Amazon.in and Flipkart on **manufacturer model
   code**, not on title text, so the two rows are provably the same product.
2. Both platforms' declared MRP and selling price are recorded on the
   observation date.
3. A mismatch is recorded where the two declared MRPs differ. Listings that
   look like multipacks are excluded, since a bundle legitimately carries a
   multiple of the single-unit MRP.
4. Each mismatch is graded **High / Medium / Low** on three signals: whether a
   third listing can adjudicate, whether the match was on a model code, and the
   size of the gap.

## What this data does not show

- **It does not say which platform is wrong.** With only two sources declaring
  an MRP, the data shows both cannot be right, not which one errs. The
  `can_name` column is `false` in exactly those cases — which is most of them.
- **It does not establish intent.** A wrong MRP may be a stale catalogue entry,
  a pack revision, or a variant mismatch. Nothing here demonstrates otherwise.
- **It is a sample, not a census.** Coverage is personal grooming appliances on
  two platforms, not all of Indian e-commerce.
- Figures are observations on a date, not continuous monitoring.

## Licence

[CC BY 4.0](LICENSE). Free to reproduce, republish and analyse, including
commercially, with attribution.

## Citation

> Ratelens, "MRP Mismatch Index — August 2026", observed
> 2026-08-31. https://www.ratelens.in/reports/mrp-mismatch/2026-08/
