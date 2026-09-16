# Prompt 3 · Apply the decisions (v1 → v2)

After the decision meeting, paste this with the v1 simulation file and your decisions (a list, or screenshots of the marked-up screen).

---

Here is the v1 simulation `[simulation_v1.html]` and our decisions `[decisions.md or screenshots]`. Produce `simulation_v2.html` with the decisions applied:

1. Remove every line we dropped; move lines we moved; add lines we added (mark added lines with their source, or "new" if none).
2. Re-tag every remaining line **Include** and clear the Consider and Review tags for the buckets we decided.
3. Keep the buckets we did not decide exactly as in v1 and label them "not yet decided".
4. Keep group order and line order exactly as we specified; this file is the build spec.
5. Print a delta table: for each bucket, lines in v1 → lines in v2, and groups in v1 → groups in v2.
6. Give me a one-page hand-off note for the build team: the final structure per bucket, each line's display name and matched existing record, and any line that is new or traces only to the reference (those need a review before build).

---

**How we used it.** The lists went from 135 lines to 89 and from 22 groups to 14. The v2 file plus the hand-off note is what the build team received. Two months later the build was in the test environment with no line-by-line debate on the way.
