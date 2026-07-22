# Lab 6 — Integrate, Test, and Iterate End-to-End

[← Prev: Lab 5 — Front-End](lab-05-frontend-react.md)  |  [Up: README](../README.md)

**Estimated time:** 60–90 minutes  |  **Prerequisite:** Labs 3–5 complete.

## Objectives

- Run all three components together.
- Validate complete journeys for both personas.
- Experience the payoff of living specs: change a requirement and propagate it.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> This is where SDD proves its worth. Because intent lives in specs, a requirement change is a **spec edit followed by a regenerate** — not a frantic hand-edit across three codebases.

## Steps

1. **Orchestrate the stack.** Ask Copilot to create a script that starts all services locally, wiring the API's database connection (from `db-config.env`) and the front end's API base URL via environment variables.

   ```text
   # In Copilot Chat:
   Create a run script (e.g., run-all.ps1 / run-all.sh) that starts both the API
   (uvicorn) and the React dev server (npm run dev) locally. The API should read its
   database connection from db-config.env at the project root and be available on
   port 8000. The React app should read the API base URL from an env var and be
   available on port 5173. Include a stop/cleanup mechanism.
   ```

2. **Run end-to-end scenarios.** Turn your spec's acceptance criteria into a manual test pass. Walk the full customer journey (file → upload → submit → see status) and the full admin journey (review → request info or approve/reject → history updates). Confirm both personas see consistent state.

3. **Check for drift.** Run `/speckit.analyze` across the repository to surface inconsistencies between the specs and what was built. Address anything it flags.

4. **Experience the living spec.** Introduce a change request — for example, capture an *estimated repair cost* on a claim, or add a *Reopened* status. Do it the SDD way:
   1. Update `spec.md` with the new requirement (Specify), then `/speckit.clarify` if needed.
   2. Re-run `/speckit.plan` and `/speckit.tasks` for the delta only.
   3. Run `/speckit.implement` and review the small, focused diffs across the DB, API, and UI.

5. **Reflect.** Notice how the change rippled from a single edited specification into coordinated changes across all three tiers — with you reviewing diffs, not writing them.

## Optional extensions

- Add automated end-to-end tests and wire them into a CI workflow.
- Ask the agent to produce a **second plan variation** for one component and compare approaches.
- Add observability (structured logging) or a deployment plan as new specs.

> [!NOTE]
> **Checkpoint — you're done when:**
> - The API and front-end are running locally and connected to Azure PostgreSQL.
> - Both personas' complete journeys work across all three tiers.
> - `/speckit.analyze` reports no significant drift.
> - A spec change propagated through Plan → Tasks → Implement into working code.

> [!WARNING]
> **Watch out**
> - API can't reach the database? Check that `db-config.env` has the correct Azure hostname, your IP is allowed in the Azure firewall rules, and SSL mode is set to `require`.
> - Tempted to hand-edit code to make the change "faster"? That breaks the discipline and desyncs the spec. Edit the spec and regenerate.

**What you learned:** how the three components integrate into one application — and, most importantly, why a living specification turns change from a risk into a routine, reviewable operation.

---

🎉 **You've completed the workshop.** You built a three-tier full-stack application by specifying intent and directing an AI agent — and you proved the spec is the source of truth by changing it and watching the change flow into code.

[← Prev: Lab 5](lab-05-frontend-react.md)  |  [Up: README](../README.md)
