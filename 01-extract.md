# Step 1 · The extract (SQL, no AI yet)

Everything downstream runs on one flat table. Pull it from Clarity, Caboodle or Reporting Workbench. Keep it **de-identified**: no patient, no provider, no encounter identifiers. Just the order, its phase, and a date.

## Columns (8)

| Column | Type | What it holds |
|---|---|---|
| `AnesthesiaStartDate` | date | Start date of the anesthesia record (used for the time window) |
| `OrderedDate` | date | Date the order was placed |
| `PatientAgeGroup` | text | `Adult` or `Pediatric` |
| `FirstAnesthesiaType` | text | e.g. `GENERAL`, `MAC`, `REGIONAL`, `GEN W REG` |
| `OrderCategory` | text | `Medication` or `Procedure` (labs, imaging, nursing orders count as Procedure) |
| `PhaseOfCare` | text | For medications: the documented phase (`OR - Preoperative`, `OR - Intraoperative`, `OR - Postop PACU/Recovery Only`) |
| `ProcedureTimingBucket` | text | For procedures: when the order was placed relative to the case (`Preprocedure`, `Intraprocedure`, `Postprocedure`) |
| `OrderName` | text | The order's display name exactly as Epic stores it |

One row per order placed. Our window was Jan 1 – Jun 23, 2026: 187,411 rows, 730 distinct order names.

## Query skeleton (adapt the table names to your build)

```sql
SELECT
  anes.AnesthesiaStartDate,
  ord.OrderedDate,
  CASE WHEN pat.AgeAtCase >= 18 THEN 'Adult' ELSE 'Pediatric' END AS PatientAgeGroup,
  anes.FirstAnesthesiaType,
  CASE WHEN ord.OrderType = 'Medication' THEN 'Medication' ELSE 'Procedure' END AS OrderCategory,
  med.PhaseOfCare,               -- medications: documented phase
  proc.ProcedureTimingBucket,    -- procedures: pre / intra / post relative to the case
  ord.OrderName
FROM AnesthesiaCases anes
JOIN Orders ord ON ord.CaseKey = anes.CaseKey
LEFT JOIN MedicationOrderPhase med ON med.OrderKey = ord.OrderKey
LEFT JOIN ProcedureOrderTiming proc ON proc.OrderKey = ord.OrderKey
JOIN PatientAgeAtCase pat ON pat.CaseKey = anes.CaseKey
WHERE anes.AnesthesiaStartDate BETWEEN '2026-01-01' AND '2026-06-23'
  AND ord.OrderingDepartmentGroup = 'Anesthesia';   -- the filter that defines "what anesthesia orders"
```

Export as CSV with a header row. That file is the only input the next two prompts need.

## Grouping (still SQL)

We also grouped the ranked orders by phase in SQL: for each `PatientAgeGroup × OrderCategory × Phase` bucket, rank order names by count. Thirty per bucket is enough for the dashboard. If you skip this, the dashboard prompt will do the ranking for you.
