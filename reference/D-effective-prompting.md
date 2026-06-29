# Appendix D — Effective Prompting for Spec-Driven Development

[← Back to README](../README.md)

- **Separate WHAT from HOW.** Keep technology out of Specify; put it all in Plan. This keeps your spec reusable across implementations.
- **Reference existing artifacts.** Tell the agent to read the constitution, spec, and plan for the feature before generating — it grounds the output.
- **Validate every phase.** Read each artifact and fix it before generating the next. An error in the spec multiplies downstream.
- **Prefer small tasks.** If Implement produces a giant diff, the task was too big — ask the agent to split it.
- **Re-anchor on drift.** If output strays, point the agent back at the spec rather than patching the code by hand.
- **Use Clarify generously.** The questions the agent asks now are the defects you avoid later.

---

[← Back to README](../README.md)
