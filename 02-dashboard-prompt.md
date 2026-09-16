# Prompt 1 · The coverage dashboard

Paste this into your AI assistant (Claude, Codex or similar) and attach your usage file. Replace the bracketed parts.

---

You are building a single-file, offline HTML dashboard for a working group that must decide the content of an Epic build: `[what you are building, e.g. "a pre-op order set", "a SmartText library for discharge summaries", "the Synopsis layout for the cardiac ICU"]`. The audience is clinicians and analysts. Nothing may leave the file: no CDN, no network fonts, no analytics.

**Input.** The attached file `[usage.csv]` has one row per real use, with the columns `[Item, Date, Context columns…]`. It is de-identified. Treat `Item` as the candidate content line and the context columns as ways to split the data.

**Buckets.** Let the user split the data by each context column (for example `[phase of care × population]`). For every bucket compute: the true total number of uses (all rows in the bucket, not only the top N), the number of distinct items, and the top 30 items ranked by count.

**Page.**
1. A header stating the total number of uses, the number of distinct items, and the date range, each labelled in plain words.
2. One segmented control per context column. Default to the most common bucket.
3. A ranked list of the bucket's top 30 items as horizontal bars with the count at the right.
4. A slider "Keep the top N" (1–30, default 10). Above the list show, in large type, **N and the percentage of the bucket's real use covered by the top N**. Coverage = sum of the top-N counts ÷ the bucket's true total. Draw a cut line under rank N and dim the rows below it.
5. A small cumulative-coverage curve (rank on x, cumulative share on y) with the cut line marked.
6. A "What the build would contain" preview: the top-N items as a plain checklist.

**Rules.** Compute everything from the file at build time and embed the result as a JSON constant; the page must open from disk with no network. Use tabular numerals. One accent colour. Every number on screen must carry a label a viewer can understand without narration. Give me the finished HTML file and a five-line summary of the numbers for the default bucket so I can check them against a count I trust.

---

**How we used it.** In the room, we dragged the slider from 5 to 10 to 15 and read the coverage aloud. Ten items covered three quarters of real use. That ended the opinion phase.
