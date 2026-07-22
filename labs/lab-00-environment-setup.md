# Lab 0 — Set Up Your Environment and Tooling

[← Back to README](../README.md)  |  [Next: Lab 1 — Constitution →](lab-01-constitution.md)

**Estimated time:** 30–45 minutes  |  **Prerequisite:** A GitHub account with Copilot enabled.

## Objectives

- Install and verify all prerequisites.
- Create the project repository.
- Initialize GitHub Spec Kit and confirm the Copilot slash commands appear.

> [!IMPORTANT]
> **Spec-driven mindset**
>
> Tooling is plumbing, not the point — but a clean setup is what lets the rest of the workshop feel like magic instead of friction. Verify each step before moving on.

## Steps

1. **Confirm your editor and extensions.** Open VS Code, open the Extensions view, and confirm **GitHub Copilot** and **GitHub Copilot Chat** are installed. Open Copilot Chat and make sure you are signed in.

2. **Confirm the runtimes.** In a terminal, verify each tool is present:

   ```bash
   git --version
   python --version      # expect 3.11 or later
   node --version        # expect 20 or later
   uv --version          # the Astral package manager
   ```

3. **Create the project repository.** Create a new repository named `claims-management` on GitHub, then clone it locally and open it in VS Code:

   ```bash
   git clone https://github.com/<your-account>/claims-management.git
   cd claims-management
   code .
   ```

4. **Install the Specify CLI.** Install Spec Kit's CLI globally with `uv`, then run its health check:

   ```bash
   uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
   specify check

   # To upgrade later:
   uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
   ```

5. **Initialize Spec Kit in the repository.** From the repository root, scaffold the SDD files for the GitHub Copilot agent:

   ```bash
   # Initialize inside the existing repo folder:
   specify init . --ai copilot

   # On Windows, add PowerShell helper scripts:
   specify init . --ai copilot --script ps

   # (Greenfield alternative — create a new folder instead:)
   #   specify init claims-management --ai copilot
   ```

6. **Open the project folder in VS Code.** This matters: open the **project folder itself**, not its parent. If you open the parent directory, the slash commands will not appear.

7. **Confirm the slash commands.** Open Copilot Chat, click into the input box, and type `/`. You should see the Spec Kit commands:

   ```
   /speckit.constitution     /speckit.specify     /speckit.clarify
   /speckit.plan             /speckit.tasks       /speckit.analyze
   /speckit.implement
   ```

8. **Tour the scaffold.** In the Explorer, open `.github/prompts/`, `.github/copilot-instructions.md`, and `.specify/`. These are the files that drive everything that follows.

9. **Set up the database configuration file.** Create a `db-config.env` file at the project root with your Azure PostgreSQL connection details (provided by the facilitator, or from your own Azure subscription):

   ```bash
   # db-config.env — DO NOT commit this file
   DB_HOST=<your-server>.postgres.database.azure.com
   DB_PORT=5432
   DB_NAME=claims_db
   DB_USER=<your-username>
   DB_PASSWORD=<your-password>
   DB_SSLMODE=require
   ```

   Add `db-config.env` to `.gitignore` to avoid committing credentials:

   ```bash
   echo "db-config.env" >> .gitignore
   ```

10. **Verify Azure PostgreSQL connectivity.** Confirm you can reach the database:

    ```bash
    psql "host=<your-server>.postgres.database.azure.com port=5432 dbname=claims_db user=<your-username> sslmode=require"
    ```

    If `psql` is not installed, you can verify connectivity with Python:

    ```bash
    python -c "import psycopg2; conn = psycopg2.connect(host='<your-server>.postgres.database.azure.com', port=5432, dbname='claims_db', user='<your-username>', password='<your-password>', sslmode='require'); print('Connected!'); conn.close()"
    ```

> [!NOTE]
> **Checkpoint — you're done when:**
> - `specify check` reports your environment is ready.
> - Typing `/` in Copilot Chat lists the `/speckit.*` commands.
> - The `.github/prompts/` and `.specify/` folders exist in your repository.
> - The `db-config.env` file exists and you can connect to the Azure PostgreSQL instance.

> [!WARNING]
> **Watch out**
> - **Slash commands missing?** You almost certainly opened the wrong folder — open the project root in VS Code and reload the window.
> - **`specify: command not found`?** Your `uv` tool path isn't on `PATH` — restart the terminal, or follow the path hint `uv` prints on install.
> - **Copilot not responding in chat?** Confirm you are signed in and your Copilot subscription is active.

**What you learned:** how Spec Kit turns an ordinary repository into an SDD-ready workspace, with the agent's commands living as files in the repo.

---

[← Back to README](../README.md)  |  [Next: Lab 1 — Constitution →](lab-01-constitution.md)
