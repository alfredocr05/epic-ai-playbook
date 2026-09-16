# Procedure 1 · Generate the coverage dashboard

**Input.** The usage table (Input 1).
**Output.** One self-contained HTML file.
**Time.** One session.

## Prompt

Attach the usage table and paste the following. Replace the bracketed fields.

```prompt
Build a single-file, offline HTML dashboard for a working group deciding the content of an Epic build: [describe the build, e.g. "a pre-operative order set", "a SmartText library for discharge summaries", "the Synopsis layout for the cardiac ICU"]. Embed all fonts, scripts and data in the file; the page must open from disk with the network disabled.

Input: the attached file [usage.csv], one row per real use, columns [Item, Date, context columns]. It is de-identified. Treat Item as the candidate content line and each context column as a way to split the data.

Buckets: allow the user to split the data by each context column. For every bucket compute (a) the true total number of uses, counting all rows in the bucket, not only the top N; (b) the number of distinct items; (c) the top 30 items ranked by count.

Page:
1. Header: total uses, distinct items, date range, each with a plain-language label.
2. One segmented control per context column; default to the largest bucket.
3. The bucket's top 30 items as horizontal bars with counts.
4. A slider "Keep the top N" (1 to 30, default 10). Show N and the coverage in large type. Coverage = sum of the top-N counts divided by the bucket's true total. Draw a cut line under rank N and dim the rows below it.
5. A cumulative-coverage curve (rank on x, cumulative share on y) with the cut line marked.
6. A preview list of the top-N items as a plain checklist.

Rules: compute everything at build time and embed the result as a JSON constant. Use tabular numerals and one accent colour. Label every number. Return the HTML file and, separately, the total uses, distinct items, and the top-10 coverage for the default bucket, for verification.
```

## Expected output

An HTML file that opens from disk. Each segmented control changes the ranked list; the slider changes the coverage figure and the cut line; the curve flattens after the first ranks. The assistant's separate summary reports the totals for the default bucket.

## Check

1. The total uses equal the row count of the file (or the sum of `Count`).
2. For one bucket, the coverage at N = 10 equals the sum of the top-10 counts divided by the bucket total, computed by hand.
3. The file works with the network disabled.
4. The file contains only items, dates, counts and context values.

Assistants often divide by the sum of the top 30 instead of the bucket total, which inflates coverage; check 2 detects this.

## Refine

Paste follow-up prompts in the same conversation.

```prompt
Use the bucket's true total (all rows) as the coverage denominator instead of the sum of the top 30. Recompute and show the corrected default-bucket figures.
```

```prompt
Add [context column] as a third segmented control and recompute the buckets.
```

```prompt
Change the slider range to 1 to [N] and the default to [N].
```

```prompt
These items are the same thing under two names: [list the pairs]. Merge them before ranking and note the merges in a footnote.
```

```prompt
Print a table of every bucket with its total, distinct items, and coverage at N = 5, 10 and 15.
```

## Common problems

| Problem | Cause | Fix |
|---|---|---|
| Coverage too high | denominator is the top-30 sum | first follow-up prompt |
| Fonts change when offline | external font link | ask for system fonts or embedded fonts |
| Two rows for one item | duplicate records in Epic | merge in the data or with the fourth follow-up prompt |
| Bucket missing | context value spelled differently in the file | normalise the column before prompting |
