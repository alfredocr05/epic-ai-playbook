# Prompt 2 · The Quick List simulator (Foundation-shaped)

Paste this into Claude and attach three things: your extract CSV, screenshots of the Epic Foundation Quick List you want to resemble, and screenshots of the order sets you are allowed to reuse. Replace the bracketed parts.

---

You are building a single-file, offline HTML simulator of an Epic **Quick List** so a clinical working group can decide its content before anything is built in Epic. The result must look and feel like the Epic Foundation Quick List in the attached screenshots `[foundation_*.png]`: an Orders header, a "Quick List" tab, radio buttons for the phase (Preprocedure · Intraprocedure · Postprocedure/PACU), and two columns of groups, each group a titled box with checkbox lines.

**Inputs.**
- `[your_extract.csv]`: one row per order placed, columns `AnesthesiaStartDate, OrderedDate, PatientAgeGroup, FirstAnesthesiaType, OrderCategory, PhaseOfCare, ProcedureTimingBucket, OrderName` (de-identified).
- `[orderset_*.png]`: screenshots of our existing order sets. These define what we are allowed to reuse.
- Constraints: `[write yours as one paragraph — ours were: reuse only lines already in our order sets because they are pharmacy-validated and interaction-checked; stay close to Foundation's structure; three tabs: pre-op, intra-op, PACU]`.

**What to do.**
1. Read the order-set screenshots and extract every line item as text (drug, dose form, route). Read the Foundation screenshots and extract the group and subgroup structure per phase.
2. From the CSV, rank order names by count within each population × phase. Match each ranked order name to the order-set line items (fuzzy match on drug and form; list uncertain matches separately). Record, for every candidate line: population, phase, group, subgroup, display name, the matched Epic record name(s), the source (which order set it came from; "Foundation" if only there; "not in reviewed order sets" if nowhere), the count, and the rank within its phase bucket.
3. Propose a tag per line: **Include** (high volume and present in a reviewed order set), **Consider** (low volume), **Review** (phase ambiguity or duplicate records for the same drug). State the thresholds you used.
4. Build the simulator: Adult/Pediatric tabs; Preop/Intraop/PACU tabs; the Foundation-shaped two-column layout; each line shows its checkbox, display name, and small chips for tag, count and rank; a Collapse/Expand toggle that hides Consider and Review lines so the group can see the "clean" screen versus the full draft; a search box; a summary panel with visible line counts.
5. Also produce the same content as a workbook (one sheet per population × phase, columns as in step 2, plus an empty Decision column: Keep / Move / Drop).

**Rules.** No network dependencies. Embed the data as a JSON constant. Keep the tool's own look close to Epic (it is evidence, not a brand exercise). Give me the HTML file, the workbook, and a short list of the matches you were unsure about.

---

**How we used it.** Meeting 2 was two people going line by line in this simulator. Every line had a number on it, so every decision had a weight. Collapsing the Consider lines showed us the clean screen. When we finished, we regenerated the file with the decisions applied and sent that version to the pharmacy build team as the spec.
