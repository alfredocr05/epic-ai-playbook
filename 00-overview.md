# Overview

This procedure decides the content of an Epic build (an order set, a Quick List, a SmartText library, a Synopsis layout, a SmartForm, an event list) from usage data and AI-generated HTML artifacts. The procedure produces the specification that the build team implements in Epic.

Three AI steps produce three artifacts:

| Step | Input | Artifact | Purpose |
|---|---|---|---|
| 1. Dashboard | usage table | one HTML file | shows the share of real use covered by the top N items |
| 2. Simulation | usage table, reference screenshots, reusable-content screenshots, constraints | one HTML file and one workbook | shows the finished screen with every candidate line carrying its count, rank and a proposed tag |
| 3. Refinement | the simulation and the group's decisions | a revised HTML file and a hand-off note | the build specification |

Each step consists of one prompt to an AI assistant that reads attached files and writes a self-contained HTML file. The prompts below are complete; only the bracketed fields change between projects.

Each artifact takes one working session. The people who own the workflow make the content decision in a meeting, using artifact 2.
