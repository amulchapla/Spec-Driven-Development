# Appendix F — Facilitator Notes

[← Back to README](../README.md)

Suggested pacing for an instructor-led delivery. Self-paced learners can treat these as time budgets.

| Lab | Focus | Time |
|---|---|---|
| Lab 0 | Environment & Spec Kit setup | 30–45 min |
| Lab 1 | Constitution | 30–45 min |
| Lab 2 | Product specification | 45–60 min |
| Lab 3 | PostgreSQL component | 60–75 min |
| Lab 4 | Python API component | 75–90 min |
| Lab 5 | React front-end component | 75–90 min |
| Lab 6 | Integration & living spec | 60–90 min |

### Running the workshop

- **Pre-flight.** Verify every learner clears Lab 0 before the cohort begins — environment issues are the top time sink.
- **Azure PostgreSQL provisioning.** Before the workshop, provision an Azure Database for PostgreSQL Flexible Server and create the `claims_db` database. Either provide each learner with individual credentials or a shared read/write account. Ensure the server's firewall allows connections from learner IPs (or enable "Allow public access from any Azure service" for workshop convenience). Distribute connection details as a `db-config.env` template.
- **Checkpoints as gates.** Don't let learners advance past a lab's Checkpoint until it is green; SDD discipline depends on it.
- **Assessment idea.** Have learners submit their four artifacts (`constitution`, `spec`, `plan`, `tasks`) per component — the quality of the **specs**, not the code, is the real measure of mastery.
- **Stretch goal.** Ask advanced learners to implement the Lab 6 change request from spec edit to working code in under 30 minutes.

---

[← Back to README](../README.md)
