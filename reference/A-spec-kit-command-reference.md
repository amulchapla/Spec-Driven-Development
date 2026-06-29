# Appendix A — Spec Kit Command Reference

[← Back to README](../README.md)

| Command | Phase | Purpose | Artifact |
|---|---|---|---|
| `specify check` | Setup | Verify your environment is ready for Spec Kit. | — |
| `specify init . --ai copilot` | Setup | Scaffold SDD files for Copilot in the current repo. | `.github/`, `.specify/` |
| `/speckit.constitution` | Constitution | Define project-wide non-negotiables. | `constitution.md` |
| `/speckit.specify` | Specify | Describe **what** and **why** — no technology. | `spec.md` |
| `/speckit.clarify` | Clarify | Answer targeted questions to remove ambiguity. | Updated `spec.md` |
| `/speckit.plan` | Plan | Define stack, architecture, and constraints. | `plan.md` |
| `/speckit.tasks` | Tasks | Break the plan into small, testable units. | `tasks.md` |
| `/speckit.analyze` | Analyze | Cross-check spec, plan, and tasks for drift. | Consistency report |
| `/speckit.implement` | Implement | Build the tasks; review focused diffs. | Working code |

### Installation & upgrade

```bash
# Install the Specify CLI
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Verify environment
specify check

# Initialize in an existing repo (add --script ps on Windows for PowerShell helpers)
specify init . --ai copilot

# Upgrade later
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

> **Remember:** do not advance to the next phase until the current artifact is validated.

---

[← Back to README](../README.md)
