# Lab 1 — Establish the Project Constitution

[← Prev: Lab 0 — Environment Setup](lab-00-environment-setup.md)  |  [Up: README](../README.md)  |  [Next: Lab 2 — Product Specification →](lab-02-product-specification.md)

**Estimated time:** 30–45 minutes  |  **Prerequisite:** Lab 0 complete.

## Objectives

- Encode the project's non-negotiable principles.
- Lock in the technology stack so the agent cannot drift.
- Add repository-wide Copilot instructions.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> The Constitution is the highest authority in your project. The agent consults it during Plan, Tasks, and Implement — so a good Constitution prevents whole classes of mistakes before they happen.
>
> Write principles, not paragraphs. Each rule should be something you could check a pull request against.

## Steps

1. **Run the constitution command.** In Copilot Chat, type `/speckit.constitution` and provide the project's non-negotiables. Use a prompt like the one below (also in [Appendix B](../reference/B-prompt-library.md)).

   ```text
   /speckit.constitution

   Establish the governing principles for a Claims Management full-stack app.
   Non-negotiables:
   - Architecture: three tiers - React front end, Python REST API, PostgreSQL DB.
     No business logic in the database; the front end never talks to the DB directly.
   - Stack is fixed: React + Vite (front end); FastAPI + SQLAlchemy (API);
     PostgreSQL 15+ (data). Do not introduce other frameworks without explicit approval.
   - API-contract-first: every endpoint has a documented request/response schema.
   - Security: authentication required; role-based authorization (customer vs admin);
     validate all input; never commit secrets; treat claim data as PII.
   - Testing: every API endpoint and every state transition has an automated test.
   - Delivery: prefer small, reviewable changes; keep specs as the source of truth.
   ```

2. **Review the generated Constitution.** Open the constitution file under `.specify/` (the agent will tell you the exact path). Read it critically: does it capture the stack, the layering rule, security, and testing expectations?

3. **Refine it.** Ask Copilot to tighten or add principles — for example, accessibility standards for the UI, or an audit-trail requirement for claim status changes. Re-read until each line is checkable.

4. **Add repository-wide Copilot rules.** Open `.github/copilot-instructions.md` and add house rules that apply to every prompt, such as:

   ```markdown
   # Copilot Instructions (repo-wide)
   - Prefer small, reviewable changes; explain trade-offs briefly.
   - Do not invent new frameworks or tools unless explicitly asked.
   - Keep edits consistent with existing patterns in this repo.
   - Follow the project Constitution in .specify/ at all times.
   ```

5. **Commit your foundation.** Commit the Constitution and instructions so your guardrails are versioned alongside the code that will follow.

> [!NOTE]
> **Checkpoint — you're done when:**
> - A constitution file exists and covers stack, architecture, security, and testing.
> - Every principle is concrete enough to check a change against.
> - `.github/copilot-instructions.md` contains your repo-wide rules.

> [!WARNING]
> **Watch out**
> - Vague principles ("write good code") give the agent nothing to enforce — be specific.
> - Do not put feature requirements here. The Constitution is about **how** you build, not **what** you build — that comes next.

**What you learned:** how to give the agent a durable set of guardrails that govern every later phase.

---

[← Prev: Lab 0](lab-00-environment-setup.md)  |  [Up: README](../README.md)  |  [Next: Lab 2 →](lab-02-product-specification.md)
