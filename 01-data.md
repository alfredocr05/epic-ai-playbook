# Your data

One flat file, one row per real use. That is all the prompts need. Ask your analyst or reporting team for it; describe it in these words.

## The shape

| Column | Required | What it holds |
|---|---|---|
| `Item` | yes | The thing that was used, named exactly as Epic names it (order display name, SmartText name, flowsheet row, event name, form field) |
| `Date` | yes | When it was used |
| `Context 1`, `Context 2` … | optional | Whatever you will want to split by: phase of care, department, note type, patient population, encounter type, user role |

If you can only get counts instead of rows, that works too: `Item`, `Count`, and the context columns.

## What "use" means, by build

| Build | One row per |
|---|---|
| Order set, Quick List, preference list | an order placed |
| SmartText, SmartPhrase library | a phrase inserted into a note |
| Synopsis, flowsheet layout | a row viewed or documented |
| SmartForm | a field completed |
| Anesthesia or procedure events | an event documented |
| Navigator, activity tab | an activity opened |

## Rules

- **No identifiers.** No MRN, CSN, name, user ID. Dates are enough.
- **Long enough to be honest.** Three to six months usually covers seasonal cases and rare-but-real items.
- **Count something you trust.** Before you paste, check one total by hand, and ask the assistant to print its totals so you can compare.
