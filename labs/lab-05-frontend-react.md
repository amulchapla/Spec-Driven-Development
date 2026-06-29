# Lab 5 — Build the ReactJS Front-End Component

[← Prev: Lab 4 — Back-End API](lab-04-backend-api-python.md)  |  [Up: README](../README.md)  |  [Next: Lab 6 — Integration →](lab-06-integration-end-to-end.md)

**Estimated time:** 75–90 minutes  |  **Prerequisite:** Lab 4 complete (the API is running).

## Objectives

- Specify the screens and flows for both personas.
- Plan and generate a React single-page app that consumes the Lab 4 API.
- Run the UI and walk both personas through their journeys.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> Specify behavior and screens from the **user's** point of view — what they see, do, and are told — before choosing component structure or state libraries.
>
> The UI is a client of the contract you already specified. Reuse the spec's language so the agent wires the right endpoints.

## Run the full SDD loop

1. **Specify.** Run `/speckit.specify` scoped to the UI. Describe each persona's screens, the FNOL form and photo upload, validation messages, and the admin review experience.

   ```text
   /speckit.specify

   Specify the web front end for the Claims Management app (two personas).
   Customer screens: sign in; a dashboard listing their claims with status; a new-claim
   wizard that captures FNOL data and lets them upload photos; a claim detail view that
   shows status history and allows editing while the claim is still editable.
   Administrator screens: a review queue filterable by status; a claim review screen
   showing all FNOL data and photos with actions to approve, reject, or request info,
   plus an internal notes panel.
   Include validation messages, empty states, and accessibility expectations.
   Describe what the user sees and does - not component or state-management choices.
   ```

2. **Clarify.** Run `/speckit.clarify` and answer the agent's questions. Resolve navigation/role-based routing, how the upload UI behaves (progress, multiple files), and what feedback each action shows.

3. **Plan.** Run `/speckit.plan` and lock in the React implementation approach against the live API.

   ```text
   /speckit.plan

   Implement the front end as a React single-page app built with Vite.
   - Routing with React Router; role-based routes for customer vs admin.
   - A typed API client targeting the Lab 4 API base URL (from an env var).
   - JWT handling: store the token, attach it to requests, redirect on 401.
   - A reusable file-upload component for claim photos with progress and validation.
   - Component structure: pages, components, hooks, api; lightweight state (Context
     or a small store) - no heavy framework unless justified.
   - Clear loading, empty, and error states; basic accessible, responsive styling.
   Follow the Constitution; do not introduce frameworks beyond those listed.
   ```

4. **Tasks.** Run `/speckit.tasks`. The agent breaks the plan into small, testable units. Expect tasks such as: app shell and routing, auth/login and token handling, customer dashboard, new-claim wizard with upload, claim detail/edit, admin queue, and admin review screen.

5. **Analyze.** Run `/speckit.analyze` to cross-check the spec, plan, and tasks for consistency, gaps, and Constitution violations. Resolve anything it flags before building.

6. **Implement.** Run `/speckit.implement`. The agent works task by task. Review each screen as it lands and click through it against the running API before accepting the next task.

## Verify the result

- Start the dev server: `npm run dev` (or the command in the generated README).
- Sign in as a **customer**, file a claim with a photo, submit it, and watch the status.
- Sign in as an **admin**, open the queue, review the claim, and approve or reject it.
- Confirm the customer now sees the updated status — data flowed **UI → API → DB** and back.

> [!NOTE]
> **Checkpoint — you're done when:**
> - The UI runs and routes correctly for each role.
> - A customer can create, update, view, and upload to claims.
> - An admin can review and approve/reject, and changes persist via the API.

> [!WARNING]
> **Watch out**
> - Blank screen with console **CORS** errors? Fix it in the API (Lab 4), not the browser.
> - If the agent hardcodes the API URL, ask it to read the base URL from an environment variable instead.

**What you learned:** how to specify a user experience independently of its implementation, then have the agent build a UI that consumes a contract you defined two labs earlier.

---

[← Prev: Lab 4](lab-04-backend-api-python.md)  |  [Up: README](../README.md)  |  [Next: Lab 6 →](lab-06-integration-end-to-end.md)
