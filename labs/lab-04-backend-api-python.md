# Lab 4 — Build the Python Back-End API Component

[← Prev: Lab 3 — Database](lab-03-database-postgresql.md)  |  [Up: README](../README.md)  |  [Next: Lab 5 — Front-End →](lab-05-frontend-react.md)

**Estimated time:** 75–90 minutes  |  **Prerequisite:** Lab 3 complete (the database is running).

## Objectives

- Specify the API's behavior, contracts, and authorization rules per persona.
- Plan and generate a FastAPI service backed by the Lab 3 database.
- Run the API and exercise it through its interactive documentation.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> Specify the **contract** — what each endpoint accepts and returns, who may call it, and what business rules apply — before choosing how to implement it.
>
> Authorization is a first-class requirement: a customer may only touch their own claims; only an admin may approve or reject.

## Run the full SDD loop

1. **Specify.** Run `/speckit.specify` scoped to the API. Describe the endpoints each persona needs, the request/response contracts, and the rules governing status transitions and uploads.

   ```text
   /speckit.specify

   Specify the REST API for the Claims Management app, serving the two personas.
   Customer capabilities: create a draft claim with FNOL data; update an editable
   claim; submit a claim; upload photos to a claim; list and view their own claims.
   Administrator capabilities: list/filter claims by status; view any claim; approve,
   reject, or request more information; add internal notes.
   Rules: authentication is required; customers access only their own claims; only
   admins change status to Approved/Rejected/Info Requested; every status change is
   recorded in history; uploads are limited to image types and a max size.
   Define request/response shapes and error behavior. No framework details yet.
   ```

2. **Clarify.** Run `/speckit.clarify` and answer the agent's questions. Resolve auth mechanism expectations, pagination/filtering of the admin queue, allowed image types and size limit, and error response format.

3. **Plan.** Run `/speckit.plan` and lock in the Python implementation approach against the existing database.

   ```text
   /speckit.plan

   Implement the API with FastAPI on Python 3.11+.
   - Use SQLAlchemy models mapped to the Lab 3 schema; Pydantic for request/response.
   - JWT-based authentication; role-based authorization (customer vs admin) via
     dependencies; customers scoped to their own claims.
   - File uploads via python-multipart; store files on disk (or a /media volume) and
     persist metadata as Claim Documents.
   - Expose OpenAPI/Swagger docs at /docs.
   - Project layout: routers, services, models, schemas; dependency injection for DB.
   - Tests with pytest covering each endpoint and every status transition.
   Connect to the Azure PostgreSQL instance using the connection settings from
   `db-config.env`. Follow the Constitution.
   ```

4. **Tasks.** Run `/speckit.tasks`. The agent breaks the plan into small, testable units. Expect tasks such as: app skeleton and DB session, auth and authorization, claim CRUD endpoints, submit/transition endpoints, upload endpoint, admin queue and review endpoints, and pytest suites for each.

5. **Analyze.** Run `/speckit.analyze` to cross-check the spec, plan, and tasks for consistency, gaps, and Constitution violations. Resolve anything it flags before building.

6. **Implement.** Run `/speckit.implement`. The agent works task by task. Review focused diffs per endpoint. After each batch, run the tests the agent generated rather than waiting until the end.

## Verify the result

- Start the API: `uvicorn` via the command in the generated README.
- Open `http://localhost:8000/docs` and exercise endpoints interactively.
- As a **customer**: create a draft, upload a photo, submit, and list your claims.
- As an **admin**: list the queue, then approve or reject a claim and confirm history updates.
- Run `pytest` and confirm the endpoint and transition tests pass.

> [!NOTE]
> **Checkpoint — you're done when:**
> - The API starts and serves interactive docs at `/docs`.
> - Customer and admin flows work end to end against the Lab 3 database.
> - Authorization is enforced (a customer cannot see or change others' claims).
> - `pytest` passes for endpoints and status transitions.

> [!WARNING]
> **Watch out**
> - **CORS** will bite you in Lab 5 — if the plan didn't mention it, ask the agent to enable CORS for the front-end origin now.
> - If an endpoint lets a customer change status to *Approved*, the authorization rule was lost — re-anchor the agent to the spec and regenerate that task.

**What you learned:** how to specify a contract and authorization model first, then have the agent implement and test it against a real database.

> See [Appendix C](../reference/C-data-model-and-api-surface.md) for a reference API surface to compare against.

---

[← Prev: Lab 3](lab-03-database-postgresql.md)  |  [Up: README](../README.md)  |  [Next: Lab 5 →](lab-05-frontend-react.md)
