# Lab 2 — Author the Product Specification

[← Prev: Lab 1 — Constitution](lab-01-constitution.md)  |  [Up: README](../README.md)  |  [Next: Lab 3 — Database →](lab-03-database-postgresql.md)

**Estimated time:** 45–60 minutes  |  **Prerequisite:** Lab 1 complete.

## Objectives

- Capture **what** the product does and **why** — personas, journeys, and outcomes.
- Use the Clarify phase to remove ambiguity.
- Produce a spec free of implementation detail.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> Resist the urge to mention React, FastAPI, or tables here. **Specify is about user experience and success criteria.** Technology is deliberately deferred to the Plan phase — that separation is what makes the spec reusable.
>
> Think like a product manager writing a PRD that the agent will implement: Who uses this? What problem does it solve? How do they interact? What outcomes matter?

## Steps

1. **Run the specify command.** In Copilot Chat, type `/speckit.specify` and describe the product at a high level. Focus on the two personas, their journeys, and acceptance criteria — not the stack.

   ```text
   /speckit.specify

   Build a Claims Management application for insurance First Notice of Loss (FNOL).

   Personas:
   - Customer (policyholder): create a claim by entering FNOL details and uploading
     photos; update a claim while it is still editable; view their claims and status.
   - Claims Administrator: review submitted claims, request more information,
     add internal notes, and approve or reject claims.

   Claim lifecycle: Draft -> Submitted -> Under Review -> Info Requested ->
   Approved/Rejected -> Closed.

   Focus on user goals, scenarios, and acceptance criteria. No implementation details.
   ```

2. **Clarify ambiguities.** Run `/speckit.clarify`. The agent will ask targeted questions — which FNOL fields are required, who can see which claims, what triggers "Info Requested," what file types are allowed for photos. Answer them; your answers sharpen the spec.

3. **Review the specification.** Open `spec.md`. Confirm it lists each persona's user stories with acceptance criteria, enumerates the claim states and who may trigger each transition, and defines what success looks like — with no mention of frameworks or schemas.

4. **Iterate.** If anything is missing or too implementation-flavored, prompt the agent to revise. The spec is a living document; getting it right now saves rework in every component lab.

> [!TIP]
> Spec Kit organizes work **by feature**, creating a numbered spec folder each time you run `/speckit.specify`. Treat this product spec as your north star. In Labs 3–5 you will run `/speckit.specify` again, scoped to one component at a time, each time referring back to this product intent.

> [!NOTE]
> **Checkpoint — you're done when:**
> - `spec.md` describes both personas with user stories and acceptance criteria.
> - The claim lifecycle and its transition rules are explicit.
> - There is no implementation detail (no frameworks, tables, or endpoints).

> [!WARNING]
> **Watch out**
> - Sneaking in tech ("store claims in a Postgres table") couples your intent to one design — keep it out.
> - Skipping Clarify leaves the agent guessing later. The questions it asks now are the bugs you avoid later.

**What you learned:** how to express intent the agent can build from — and why keeping technology out of the spec keeps your options open.

---

[← Prev: Lab 1](lab-01-constitution.md)  |  [Up: README](../README.md)  |  [Next: Lab 3 →](lab-03-database-postgresql.md)
