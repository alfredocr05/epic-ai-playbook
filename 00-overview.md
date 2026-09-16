# Overview

This page describes a procedure for deciding the content of an Epic build (an order set, a Quick List, a SmartText library, a Synopsis layout, a SmartForm, an event list) using usage data and AI-generated HTML artifacts. Epic build itself is unchanged; the procedure produces the specification that the build team receives.

The procedure has three AI steps and produces three artifacts:

| Step | Input | Artifact | Purpose |
|---|---|---|---|
| 1. Dashboard | usage table | one HTML file | shows what share of real use the top N items cover |
| 2. Simulation | usage table, reference screenshots, reusable-content screenshots, constraints | one HTML file and one workbook | shows the finished screen with every candidate line carrying its count, rank and a proposed tag |
| 3. Refinement | the simulation and the group's decisions | a revised HTML file and a hand-off note | the build specification |

Each step is a single prompt pasted into an AI assistant that can read attached files and write a self-contained HTML file. The prompts below were used as written; the bracketed fields are the only parts that change between projects.

Expected effort: one working session per artifact. The content decision itself is made by the people who own the workflow, in a meeting, using artifact 2.
