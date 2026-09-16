# Procedure 3 · Refine the simulation into the specification

**Input.** The simulation from Procedure 2 and the decisions from the meeting (the workbook with the Decision column filled in, a list, or annotated screenshots).
**Output.** A revised HTML file (version 2) and a one-page hand-off note.
**Time.** One session.

## Prompt

Attach the version 1 file and the decisions, then paste the following.

```prompt
Attached are the version 1 simulation [simulation_v1.html] and the decisions [decisions.xlsx or screenshots]. Produce simulation_v2.html with the decisions applied:

1. Remove every line marked Drop. Move every line marked Move to its target group. Add every line listed as added, with its source or "new".
2. Tag every remaining line Include in the decided buckets. Leave the undecided buckets exactly as in version 1 and label them "not yet decided".
3. Keep the group order and the line order as specified; this file is the build specification.
4. Print a table: for each bucket, lines in v1 and v2, groups in v1 and v2.
5. Write a one-page hand-off note for the build team: the final structure per bucket; each line's display name and matched existing record; every line that is new or traces only to the reference, listed separately for review.

Return the HTML file, the table and the note.
```

## Expected output

A version 2 file that shows only the decided content, a delta table, and a hand-off note listing every line with its existing record.

## Check

1. Count the lines in one decided bucket by hand and compare with the table.
2. Confirm that every dropped line is absent and every added line appears with a source.
3. Confirm that the undecided buckets match version 1.

## Refine

```prompt
Reorder the lines in [group] to: [list]. Keep everything else unchanged.
```

```prompt
Add [line] to [group] with source "[existing screen]" and tag Include.
```

```prompt
Produce the hand-off note as a table with columns: bucket, group, display name, existing record, source, note.
```

```prompt
Export the final content as a CSV with one row per line and the same columns as the hand-off table.
```

## Hand-off

Send the build team version 2 and the hand-off note. Keep version 1 for reference. The content owners review the lines listed as new or reference-only before the build.
