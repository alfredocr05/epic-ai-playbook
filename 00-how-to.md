# How to use this playbook

You need three things: a de-identified extract, screenshots of the screens you want to resemble and reuse, and an AI coding assistant that can read files and write HTML (we used Claude and Codex).

1. **Run the extract** (Step 1). SQL only. Check the totals yourself before anything else.
2. **Paste Prompt 1** with the CSV. Open the dashboard. Drag the slider. Now the group is looking at coverage, not opinions.
3. **Paste Prompt 2** with the CSV, the Foundation screenshots and your order-set screenshots. Open the simulator. Meet, decide line by line.
4. **Paste Prompt 3** with the decisions. Send v2 to the build team as the spec.
5. **Paste Prompt 4** after each meeting.

## Ground rules

- **No PHI, ever.** The extract carries no patient, provider or encounter identifiers. The screenshots are of build screens, not charts. If in doubt, leave it out.
- **AI helps you see. You decide.** Every clinical decision in our project was made by clinicians in a meeting, with a number next to each line.
- **Reuse what is validated.** Lines that already live in a reviewed order set carry their pharmacy review with them.
- **Check the numbers.** Ask the assistant to print the totals it computed and compare them with your query. We caught a denominator bug this way.

## Expect

The dashboard and the first simulator took an afternoon each. The decision meeting took 36 minutes. The Quick List reached the build environment two months later, with no line-by-line debate on the way.
