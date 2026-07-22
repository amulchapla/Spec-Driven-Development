# Appendix E — Troubleshooting and Common Gotchas

[← Back to README](../README.md)

| Symptom | Likely cause & fix |
|---|---|
| Slash commands don't appear | You opened the parent folder. Open the **project root** in VS Code and reload. |
| `specify: command not found` | The `uv` tool path isn't on `PATH`. Restart the terminal or add the path `uv` printed. |
| Copilot ignores your rules | Confirm the Constitution and `.github/copilot-instructions.md` exist and are committed; reference them in prompts. |
| Agent drifts from the spec | Re-anchor: ask it to re-read `spec.md`/`plan.md` and regenerate only the affected task. |
| Implement diff is huge | The task was too large. Ask the agent to break it into smaller tasks. |
| UI shows CORS errors | Enable CORS in the **API** for the front-end origin (a Lab 4 fix, not a browser one). |
| API can't reach the database | Check `db-config.env` for correct Azure hostname (`<server>.postgres.database.azure.com`), ensure your client IP is added to the Azure firewall rules, and confirm `DB_SSLMODE=require`. |

---

[← Back to README](../README.md)
