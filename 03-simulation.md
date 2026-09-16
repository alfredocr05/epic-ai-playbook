# Procedure 2 · Generate the simulation of the build

**Input.** The usage table (Input 1), reference screenshots (Input 2), reusable-content screenshots (Input 3), constraints (Input 4).
**Output.** One self-contained HTML file and one workbook.
**Time.** One session, plus a review of the uncertain matches.

## Prompt

Attach the usage table and all screenshots, then paste the following. Replace the bracketed fields.

```prompt
Build a single-file, offline HTML simulation of an Epic build so that a working group can decide its content before the build. The build is [describe the build]. Reproduce the layout of the reference screen in the attached screenshots [reference_*.png]: the same header, the same sections and groups, the same controls (tabs, radio options), in the same order.

Inputs:
- [usage.csv]: one row per real use, columns [Item, Date, context columns], de-identified.
- [reuse_*.png]: screenshots of existing reviewed content available for reuse: [name them].
- Constraints: [paste the constraints paragraph].

Steps:
1. From the reference screenshots, extract the structure: sections, groups, subgroups, controls, order.
2. From the reuse screenshots, extract every line item as text (name, form, route or equivalent).
3. From the usage table, rank items by count within each context bucket. Match each ranked item to the reusable line items by fuzzy matching; list uncertain matches separately. Record for every candidate line: bucket, group, subgroup, display name, matched existing record, source ("reused from [screen]", "reference only", or "new"), count, rank within bucket.
4. Assign a tag to every line and state the thresholds: Include (count at or above [threshold] and matched to reusable content), Consider (count below [threshold]), Review (ambiguous placement, two records for one item, or new content).
5. Build the simulation: the reference layout; one control per context bucket; every line with its checkbox, display name, and chips for tag, count and rank; a Collapse/Expand toggle that hides Consider and Review lines; a search box; a summary panel with visible line counts per section.
6. Produce the same content as a workbook: one sheet per bucket, the columns from step 3, plus an empty Decision column (Keep / Move / Drop).

Rules: embed all fonts, scripts and data in the file; keep the visual style close to the reference. Return the HTML file, the workbook, the thresholds used, and the list of uncertain matches.
```

## Expected output

An HTML file that resembles the reference screen, with every candidate line showing its count and rank, tags in three colours, and a toggle that removes the Consider and Review lines. A workbook with one sheet per bucket. A list of uncertain matches.

## Check

1. Pick five lines at random and compare their counts with the dashboard from Procedure 1.
2. Read the uncertain matches and correct wrong matches with a follow-up prompt.
3. Confirm that every group in the reference screen appears in the simulation.
4. Confirm that Collapse hides exactly the Consider and Review lines.

## Refine

```prompt
Move [line] from [group] to [group]. Rename the group [old] to [new]. Keep everything else unchanged.
```

```prompt
The matches [list] are wrong; the correct existing records are [list]. Update the source, the tags and the workbook.
```

```prompt
Change the Include threshold to [count] and re-tag. Report how many lines changed tag.
```

```prompt
These items are duplicates of one another: [pairs]. Keep [record], drop the other, and tag the kept line Include.
```

```prompt
Add a [population or phase] version as another tab with the same structure; rank from the same file filtered by [context value].
```

```prompt
The reference screen uses [term] for the section named [term] in the simulation. Use the reference wording everywhere.
```

## Use in the decision meeting

Open the simulation on a shared screen. Go through each section line by line and record Keep, Move or Drop for each line in the workbook or on a screenshot. Use Collapse to show the resulting screen. Lines tagged Consider are the ones the data leaves open; expect most discussion there.

## Common problems

| Problem | Cause | Fix |
|---|---|---|
| Layout differs from the reference | screenshots incomplete | capture every section and tab; re-prompt with the full set |
| Item matched to the wrong record | fuzzy match on similar names | second follow-up prompt |
| High-count item tagged Consider | absent from the reuse screenshots | confirm whether it exists; if yes, third follow-up prompt with the record |
| Simulation slow or blank | file exceeds the assistant's output limit | ask for the data as a separate JSON file loaded at build time, or split by population |
