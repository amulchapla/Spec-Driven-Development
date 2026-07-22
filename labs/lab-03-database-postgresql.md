# Lab 3 — Build the PostgreSQL Database Component

[← Prev: Lab 2 — Product Specification](lab-02-product-specification.md)  |  [Up: README](../README.md)  |  [Next: Lab 4 — Back-End API →](lab-04-backend-api-python.md)

**Estimated time:** 60–75 minutes  |  **Prerequisite:** Lab 2 complete.

## Objectives

- Specify the data the application must persist and the rules around it.
- Plan and generate a PostgreSQL schema with migrations and seed data.
- Connect to the Azure PostgreSQL database and verify the schema.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> Even though this is the data tier, the Specify step still describes **what** must be stored and the rules that govern it — not column types. Save the DDL decisions for Plan.
>
> Build the database first: it is the foundation the API and UI depend on.

## Run the full SDD loop

1. **Specify.** Run `/speckit.specify` scoped to the persistence layer. Describe the entities, their relationships, the data the FNOL captures, and the rules (required fields, allowed status values, audit trail).

   ```text
   /speckit.specify

   Specify the data persistence layer for the Claims Management app.
   Entities and relationships:
   - Customer: identity and contact details; a customer has many claims.
   - Claim: belongs to a customer; carries FNOL data (policy number, loss type,
     incident date, location, description, amount claimed) and a status.
   - Claim Document: a photo/file attached to a claim; a claim has many documents.
   - Claim Status History: an audit record of each status change, who made it, when,
     and an optional note.
   - User/Administrator: staff who review claims; has a role (customer or admin).
   Rules: a claim must always have a valid status from the defined lifecycle; status
   history is append-only; deleting a customer must not silently orphan claims.
   Focus on the data and its rules - not on column types or indexes yet.
   ```

2. **Clarify.** Run `/speckit.clarify` and answer the agent's questions. Resolve cardinality, which fields are mandatory, the exact status enumeration, and data-retention/PII expectations.

3. **Plan.** Now get technical. Run `/speckit.plan` and specify the database technology and design approach.

   ```text
   /speckit.plan

   Implement the persistence layer on PostgreSQL 15+ hosted on Azure Database for
   PostgreSQL Flexible Server. Connection details are read from a `db-config.env`
   file at the project root.
   - Use normalized tables with surrogate primary keys and foreign keys.
   - Model the status lifecycle as a constrained enum or lookup table.
   - Manage schema with Alembic migrations (versioned, reversible).
   - Provide a seed script with a few customers, claims, documents, and one admin.
   - Add indexes on foreign keys and on claim status for the admin queue.
   Follow the project Constitution.
   ```

4. **Tasks.** Run `/speckit.tasks`. The agent breaks the plan into small, testable units. Expect tasks like: write the docker-compose service, define the schema, create the initial migration, write the seed script, and add verification queries.

5. **Analyze.** Run `/speckit.analyze` to cross-check the spec, plan, and tasks for consistency, gaps, and Constitution violations. Resolve anything it flags before building.

6. **Implement.** Run `/speckit.implement`. The agent works task by task. Review each migration and script as it lands. Keep diffs small and aligned to the schema you specified.

## Verify the result

- Connect to the Azure PostgreSQL instance using the credentials in `db-config.env` (e.g., via `psql` or a database client).
- Apply migrations: run the Alembic upgrade command from the generated README.
- Run the seed script, then confirm the tables and sample rows exist.
- Query the admin queue index: list claims by status to confirm it returns seeded data.

> [!NOTE]
> **Checkpoint — you're done when:**
> - The Azure PostgreSQL instance is reachable using `db-config.env` credentials.
> - Migrations apply cleanly and create all specified tables and constraints.
> - Seed data is present and queryable; status values are constrained to the lifecycle.

> [!WARNING]
> **Watch out**
> - If the agent embeds business logic in triggers/stored procedures, push back — the Constitution keeps logic in the API tier.
> - No reversible migration? Ask for one. Reversibility is part of the plan, not a nice-to-have.

**What you learned:** how to run the complete Specify → Implement loop on a single tier, and how a constrained, migration-managed schema becomes the stable foundation for the API.

> See [Appendix C](../reference/C-data-model-and-api-surface.md) for a reference data model to sanity-check your design against.

---

[← Prev: Lab 2](lab-02-product-specification.md)  |  [Up: README](../README.md)  |  [Next: Lab 4 →](lab-04-backend-api-python.md)
