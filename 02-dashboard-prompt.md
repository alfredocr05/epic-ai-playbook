# Prompt 1 · The coverage dashboard

Paste this into Claude (claude.ai, Claude Code or the desktop app) and attach your extract CSV. Replace the bracketed parts.

---

You are building a single-file, offline HTML dashboard for a hospital order-set working group. The audience is clinicians deciding which orders belong on an Epic Quick List. Nothing may leave the file: no CDN, no fonts from the network, no analytics.

**Input.** The attached CSV `[your_extract.csv]` has one row per order placed by anesthesia, with columns: `AnesthesiaStartDate, OrderedDate, PatientAgeGroup, FirstAnesthesiaType, OrderCategory, PhaseOfCare, ProcedureTimingBucket, OrderName`. It is de-identified. Medications carry their phase in `PhaseOfCare`; procedures carry it in `ProcedureTimingBucket`. Map both to three phases: Preprocedure, Intraprocedure, Postprocedure.

**Buckets.** `PatientAgeGroup` (Adult, Pediatric) × `OrderCategory` (Medication, Procedure) × phase (3) = 12 buckets. For each bucket compute: the true total number of orders (all rows in the bucket, not just the top N), the number of distinct order names, and the top 30 order names ranked by count.

**Page.**
1. A header with the total number of orders analysed, the number of distinct order names, and the date window, each labelled in plain words.
2. Three segmented controls: population, order type, phase of care. Default: Adult · Medication · Intraprocedure.
3. A ranked list of the bucket's top 30 orders as horizontal bars with the count at the right.
4. A slider "Quick list shows top N" (1–30, default 10). Above the list show, in large type, **N and the percentage of the bucket's total order volume covered by the top N**. Coverage = sum of the top-N counts ÷ the bucket's true total. Draw a "cut line" in the list under rank N and dim the rows below it.
5. A small cumulative-coverage curve (rank 1–30 on x, cumulative share on y) with the cut line marked.
6. A "Resulting quick-list preview": the top-N names as checkboxes, styled like a plain Epic order list.

**Rules.** Compute everything from the CSV at build time and embed the result as a JSON constant in the file; the HTML must open from disk with no network. Use tabular numerals. Keep the palette calm (one accent colour). Every number on screen must carry a label a viewer can understand without narration. Give me the finished HTML file and a five-line summary of the numbers for the default bucket so I can check them against my own query.

---

**How we used it.** In the room, we dragged the slider from 5 to 10 to 15 and read the coverage aloud. Ten orders covered 76 % of adult intra-op medication volume and 87 % of PACU medication volume. That ended the opinion phase.
