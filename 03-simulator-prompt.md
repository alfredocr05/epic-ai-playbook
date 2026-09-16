# Prompt 2 · The simulation of the build

Paste this into your AI assistant and attach three things: your usage file, screenshots of the reference screen you want to resemble, and screenshots of the content you are allowed to reuse. Replace the bracketed parts.

---

You are building a single-file, offline HTML **simulation** of an Epic build so a working group can decide its content before anything is built in Epic. The build is `[what you are building]`. The result must look and behave like the reference screen in the attached screenshots `[reference_*.png]` (Epic Foundation, a sister department's build, or a mock-up): the same layout, the same kind of groups, the same controls.

**Inputs.**
- `[usage.csv]`: one row per real use, columns `[Item, Date, Context columns…]`, de-identified.
- `[reuse_*.png]`: screenshots of existing content we may reuse `[e.g. our current order sets, the approved SmartText library, the current flowsheet]`. Anything already there carries its review with it.
- Constraints: `[write yours as one paragraph, e.g. "reuse existing content wherever possible; stay close to the reference structure; three sections: before, during, after"]`.

**What to do.**
1. Read the reference screenshots and extract the structure: sections, groups, subgroups, controls, and the order they appear in. Read the reuse screenshots and extract every line item as text.
2. From the usage file, rank items by count within each context bucket. Match each ranked item to the reusable line items (fuzzy match; list uncertain matches separately). Record, for every candidate line: bucket, group, subgroup, display name, the matched existing record, the source (which existing build it came from; "reference only" if only in the reference; "new" if nowhere), the count, and the rank within its bucket.
3. Propose a tag per line: **Include** (high use and already in reusable content), **Consider** (low use), **Review** (ambiguous placement, duplicate records for the same thing, or new content that needs a review). State the thresholds you used.
4. Build the simulation: the reference layout; a control for each context bucket; every line shows its checkbox or control, its display name, and small chips for tag, count and rank; a **Collapse / Expand** toggle that hides Consider and Review lines so the group can see the clean screen versus the full draft; a search box; a summary panel with visible line counts.
5. Also produce the same content as a workbook: one sheet per bucket, the columns from step 2, plus an empty Decision column (Keep / Move / Drop).

**Rules.** No network dependencies. Embed the data as a JSON constant. Keep the look close to the reference; it is evidence, not a brand exercise. Give me the HTML file, the workbook, and a short list of the matches you were unsure about.

---

**How we used it.** The decision meeting was two people going line by line in this simulation. Every line had a number on it, so every decision had a weight. Collapsing the Consider lines showed the clean screen. When we finished, we regenerated the file with the decisions applied and sent that version to the build team as the spec.
