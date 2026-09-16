# Requirements

## Tools

An AI assistant that accepts file attachments and returns files. Claude (claude.ai, Claude Code) and OpenAI Codex meet this requirement; assistants with equivalent capabilities should perform similarly. A browser opens the generated HTML files. Steps 1 to 3 require only the assistant and a browser.

## Input 1 · Usage table

One row per real use of an item, as a CSV file. Obtain the table from a reporting analyst or from Reporting Workbench.

| Column | Required | Content |
|---|---|---|
| `Item` | yes | the item as Epic names it: order display name, SmartText name, flowsheet row, event name, form field |
| `Date` | yes | date of use |
| context columns | optional | dimensions to split by: phase of care, department, note type, population, encounter type |

Aggregated counts (`Item`, `Count`, context columns) also work.

The build determines what counts as a use: an order placed (order sets, Quick Lists, preference lists); a phrase inserted (SmartTexts); a row viewed or documented (Synopsis, flowsheets); a field completed (SmartForms); an event documented (event lists).

Cover a period long enough to include rare but real items; three to six months is typical.

## Input 2 · Reference screenshots

Screenshots of the screen the build should resemble: the Epic Foundation version, another department's build, or a mock-up. Capture every section and every tab or radio option.

## Input 3 · Reusable-content screenshots

Screenshots of existing, reviewed content available for reuse (current order sets, an approved SmartText library, the current flowsheet). Lines matched to this content carry its prior review.

## Input 4 · Constraints

Write one paragraph before prompting. Examples: reuse existing content wherever possible; keep the reference structure; three sections; adult and pediatric versions.

## Data rules

- Exclude patient, provider and encounter identifiers; dates suffice.
- Verify one total independently before prompting, then compare it with the totals the assistant reports.
- Keep the generated files self-contained: fonts, scripts and data embedded in the file.
