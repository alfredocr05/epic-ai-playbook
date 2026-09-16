# Verification and limitations

## Before showing an artifact to a group

- [ ] The totals reported by the assistant match an independent count.
- [ ] Coverage at N = 10 for one bucket, recomputed by hand, matches the dashboard.
- [ ] Every line in the simulation shows a count and a rank.
- [ ] The file opens with the network disabled and shows the same content.
- [ ] A search of the file for MRN, CSN and names returns nothing.
- [ ] The uncertain-match list has a reviewer's initials.

## Limitations

- Usage data reflects current practice, including practice the build intends to change. Low counts identify what the data leaves open; the group settles those lines.
- Fuzzy matching between usage items and existing content produces errors. Review the uncertain matches and spot-check the confident ones.
- The simulation supports the decision; the build team reproduces structure and wording in Epic from the hand-off note.
- Assistants differ in the amount of output they return in one file. Very large builds may need the data split by population or supplied as a separate file.

## Provenance

The procedure originates from a Quick List project at UI Health Care in 2026 (Alfredo Camargo Rodrigues, MD, Anesthesia). The prompts above reproduce that project's prompts with project values replaced by bracketed fields.
