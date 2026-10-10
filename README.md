> Written manually, without AI assistance.

# Snowflake_Youtube_Trending_dataset

## What this does

Builds a data lakehouse in Snowflake from YouTube trending data (11
countries) plus category metadata â€” then answers which content category a
new channel should target. Verdict: People & Blogs (after excluding Music
and Entertainment).

## Business process

Trending CSVs and category JSONs land in Azure Blob Storage, are staged and
merged into `table_youtube_final`, deduplicated, then queried: sum of views
per category first, then top-2-category appearances per country to remove
regional bias. `Report.pdf` is the full write-up and `output/` holds the
result CSVs.

## Technical flow

Blob container â†’ Snowflake external tables â†’ `TABLE_YOUTUBE_TRENDING` â¨
`TABLE_YOUTUBE_CATEGORY` on country + category_id â†’ dedupe into
`TABLE_YOUTUBE_FINAL` â†’ the 17 analysis queries in `code/` (`part_1`,
`part_2_q1`â€“`q9`, `part_3`, `part_4`), including a `RANK()` window query for
the top category per country.

## Repository structure

- [`code/`](code/) â€” the 17 analysis SQL queries
- [`output/`](output/) â€” result CSVs
- [`Report.pdf`](Report.pdf) â€” full write-up
