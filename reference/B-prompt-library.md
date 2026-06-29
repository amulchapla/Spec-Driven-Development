# Appendix B — Prompt Library

[← Back to README](../README.md)

Copy-paste starting points for each phase. Always adapt them to the spec and plan already in your repo — the agent works best when your prompt references existing artifacts.

## Constitution (Lab 1)

```text
/speckit.constitution
Establish governing principles for a three-tier Claims Management app:
fixed stack (React+Vite / FastAPI+SQLAlchemy / PostgreSQL), API-contract-first,
authn + role-based authz, input validation, no secrets in code, claim data is PII,
automated tests for every endpoint and state transition, small reviewable changes.
```

## Specify — product (Lab 2)

```text
/speckit.specify
Claims Management app for insurance FNOL. Two personas (Customer, Administrator)
with the journeys and claim lifecycle described in the workshop. Focus on user goals,
scenarios, and acceptance criteria. No implementation details.
```

## Plan — per component (Labs 3–5)

```text
/speckit.plan
Database: PostgreSQL 15 in Docker, normalized tables, Alembic migrations, seed script.
API: FastAPI + SQLAlchemy + Pydantic, JWT auth + role-based authz, multipart uploads,
    OpenAPI docs, pytest.
Web: React + Vite + React Router, typed API client from env var, JWT handling,
    reusable upload component, accessible responsive UI.
Each plan must follow the Constitution and target the artifacts already built.
```

## Re-anchoring a drifting agent

```text
Re-read spec.md and plan.md for this feature. The last change violated
<the rule>. Regenerate only the affected task to match the spec exactly.
```

> The component-scoped Specify and Plan prompts also live in their respective lab files
> ([Lab 3](../labs/lab-03-database-postgresql.md), [Lab 4](../labs/lab-04-backend-api-python.md), [Lab 5](../labs/lab-05-frontend-react.md)) in fuller form.

---

[← Back to README](../README.md)
