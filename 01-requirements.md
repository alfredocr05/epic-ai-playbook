# Requirements

## Tools

An AI assistant that accepts file attachments and returns files. Claude (claude.ai or Claude Code) and OpenAI Codex were used; any assistant with equivalent capabilities is expected to work. A browser to open the generated HTML files. No Epic access is needed for steps 1 to 3.

## Input 1 · Usage table

One row per real use of an item, as a CSV file. Obtain it from a reporting analyst or Reporting Workbench; the query itself is outside this procedure.

| Column | Required | Content |
|---|---|---|
| `Item` | yes | the item as Epic names it: order display name, SmartText name, flowsheet row, event name, form field |
| `Date` | yes | date of use |
| context columns | optional | dimensions to split by: phase of care, department, note type, population, encounter type |

Aggregated counts (`Item`, `Count`, context columns) are acceptable in place of rows.

What counts as a use depends on the build: an order placed (order sets, Quick Lists, preference lists); a phrase inserted (SmartTexts); a row viewed or documented (Synopsis, flowsheets); a field completed (SmartForms); an event documented (event lists).

Cover a period long enough to include rare but real items; three to six months is typical.

## Input 2 · Reference screenshots

Screenshots of the screen the build should resemble: the Epic Foundation version, another department's build, or a mock-up. Capture every section and, where applicable, every tab or radio option.

## Input 3 · Reusable-content screenshots

Screenshots of existing, reviewed content the build is allowed to reuse (current order sets, an approved SmartText library, the current flowsheet). Lines matched to this content carry its prior review.

## Input 4 · Constraints

One paragraph, written before prompting. Examples: reuse existing content wherever possible; keep the reference structure; three sections; adult and pediatric versions.

## Data rules

- No patient, provider, or encounter identifiers in any file. Dates are sufficient.
- Verify one total independently before prompting, and compare it with the totals the assistant reports.
- Keep the generated files offline: they must not request fonts, scripts or data from the network.
