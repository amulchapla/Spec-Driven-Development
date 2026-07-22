# Spec-Driven Development with VS Code & GitHub Copilot

### A Hands-On Workshop — Building the Claims Management Application

> Learn the discipline of **specifying before you build** — and let GenAI do the heavy lifting.

**Stack:** React · Python · PostgreSQL · GitHub Spec Kit

---

## About this workshop

This is a hands-on, self-paced workshop. Over a sequence of labs you will build a complete **Claims Management** application — a web front end, a back-end API, and a relational database — not by writing code line by line, but by writing clear specifications and directing **GitHub Copilot** to generate, test, and refine the implementation for you.

The application is the vehicle; the destination is a new way of working: **Spec-Driven Development (SDD)** — a discipline in which a reviewable *specification*, not the code, is the source of truth, and an AI coding agent turns that intent into working software while you steer and verify.

> [!IMPORTANT]
> **The spec-driven mindset**
>
> You are not here to type code. You are here to make intent explicit, then verify that what the agent produced matches it. Every lab reinforces the same loop:
> **Constitution → Specify → Clarify → Plan → Tasks → Analyze → Implement** — with a human checkpoint at every arrow.

---

## What is Spec-Driven Development?

In traditional "vibe coding," you describe a goal to an AI agent and hope the result matches what you had in mind. The code often compiles and looks right, yet quietly solves a slightly different problem — because a prompt captures what you *typed*, not what you *meant*.

Spec-Driven Development flips this. Instead of coding first and documenting later, you start with a **specification**: a clear, reviewable contract for how the software should behave. That spec becomes the shared source of truth that you, your team, and your AI agent all work from. The result is less guesswork, fewer surprises, and higher-quality code.

The key shift: specifications are no longer dusty documents written once and forgotten. They are **living, executable artifacts** that evolve with the project.

### Why it pays off with GenAI

- **Upfront clarity** — assumptions surface early, when changing direction costs a few keystrokes instead of entire sprints.
- **Fewer regressions** — the spec drives task breakdowns and checklists, so the agent validates its own work against documented intent.
- **Reviewable progress** — you review small, focused changes that each solve one specified piece, not thousand-line code dumps.
- **Easier maintenance** — the *why* behind technical decisions lives in version control alongside the code.
- **Cheap experimentation** — because the spec is detached from the code, you can ask the agent to produce multiple implementations from the same spec and compare them.

---

## The tooling: GitHub Spec Kit

This workshop uses **GitHub Spec Kit**, an open-source toolkit that brings SDD to life inside your editor. It has two parts:

- **The Specify CLI** — a small command-line tool that bootstraps a repository for SDD. It downloads the templates and helper scripts for your chosen coding agent (here, GitHub Copilot) and sets up the scaffolding the agent iterates on.
- **Repo-native prompt files** — once initialized, your repository gains Markdown prompt files that appear as **slash commands** in Copilot Chat. Your whole workflow becomes files-and-scripts in the repo, not clicks trapped in a tool UI.

After initialization your repository contains, at minimum:

- `.github/prompts/` — prompt files exposed as Copilot Chat slash commands (type `/` in chat).
- `.github/copilot-instructions.md` — repository-wide rules Copilot should always follow.
- `.specify/` — templates, helper scripts, and "memory," including your project constitution.

---

## The Spec Kit workflow

Spec Kit organizes work into seven phases, each with a Copilot Chat slash command. **The cardinal rule: do not advance to the next phase until the current one is validated.**

| Phase | Command | What you do | What the agent produces |
|---|---|---|---|
| Constitution | `/speckit.constitution` | State the project's non-negotiables — stack, architecture, security, testing. | `constitution.md` governing all later phases |
| Specify | `/speckit.specify` | Describe **what** you're building and **why** — personas, journeys, outcomes. No tech. | `spec.md` (a living requirements artifact) |
| Clarify | `/speckit.clarify` | Answer the agent's targeted questions to remove ambiguity. | A sharper `spec.md` |
| Plan | `/speckit.plan` | Now get technical — stack, architecture, constraints, integrations. | `plan.md` |
| Tasks | `/speckit.tasks` | Ask the agent to break the plan into small, testable units. | `tasks.md` |
| Analyze | `/speckit.analyze` | Cross-check spec, plan, and tasks for consistency and gaps. | A consistency report |
| Implement | `/speckit.implement` | Let the agent build the tasks; you review focused diffs. | Working code, task by task |

> [!TIP]
> **Specify** is about user experience and outcomes — deliberately free of technology choices. **Plan** is where technology enters. Keeping the two separate is what lets you re-plan or re-implement the same spec later without rewriting your intent.

---

## The application you will build

A **Claims Management** application for an insurance scenario, built around **First Notice of Loss (FNOL)**. It serves two personas and is composed of three components.

### Personas

- **Customer (policyholder)** — files a new claim by providing FNOL details and uploading photos; updates a claim while it is still editable; views the status and history of their claims.
- **Claims Administrator (adjuster)** — reviews submitted claims, requests additional information, adds internal notes, and approves or rejects claims.

### Components

1. **Front-end UI (ReactJS)** — a single-page app supporting both personas, including FNOL capture and photo upload for customers and a review queue with approve/reject actions for administrators.
2. **Back-end API (Python)** — a REST API that powers the UI: claim CRUD, file uploads, authentication, role-based authorization, and claim status transitions.
3. **PostgreSQL database** — the persistence layer storing customers, claims, uploaded documents, status history, and administrator notes.

### Claim lifecycle

```
Draft → Submitted → Under Review → Info Requested → Approved / Rejected → Closed
```

### High-level architecture

```
   [ Customer Browser ]          [ Administrator Browser ]
            \                            /
             \                          /
          React Front-End  (Vite single-page app)   <-- Component 1
                         |
                  HTTPS / REST + JWT
                         |
          Python Back-End API  (FastAPI)            <-- Component 2
                         |
                  SQLAlchemy / Alembic
                         |
          PostgreSQL Database  (Azure Flexible Server)  <-- Component 3
```

> [!TIP]
> The stack above (React + Vite, FastAPI, PostgreSQL) is the recommended default for this workshop and is what the sample prompts assume. You lock it into your **Constitution** in Lab 1 so the agent never drifts to a different stack.

---

## Learning objectives

By the end of this workshop you will be able to:

- Explain spec-driven development and why it improves AI-assisted software delivery.
- Set up GitHub Spec Kit with GitHub Copilot in VS Code.
- Encode engineering standards (stack, security, testing) into a project Constitution.
- Write specifications that capture intent without prescribing implementation.
- Drive the Specify → Clarify → Plan → Tasks → Analyze → Implement loop for each component.
- Build and integrate a three-tier full-stack application from specs.
- Treat specs as living artifacts — change a requirement and propagate it through the loop.

---

## Prerequisites

Before Lab 0, make sure you have:

- A **GitHub account with GitHub Copilot enabled** (a free plan is sufficient to learn).
- **Visual Studio Code** with the **GitHub Copilot** and **GitHub Copilot Chat** extensions installed and signed in.
- **Git**, **Python 3.11+**, and **Node.js 20+** installed.
- The **`uv`** package manager (from Astral) — Spec Kit's CLI is Python-based and `uv` makes installation clean and reproducible.
- An **Azure subscription** with an Azure Database for PostgreSQL Flexible Server provisioned (or connection credentials provided by the facilitator).

---

## How to use this repo

Work through the labs **in order** — each lab's output is the next lab's input. Each lab file follows the same shape: objectives & time, a spec-driven mindset callout, numbered steps (with exact slash commands and prompts), a checkpoint gate, common pitfalls, and a takeaway.

Labs 3, 4, and 5 each run the **full SDD loop** on one component, so you practice the same workflow three times — once per tier of the stack.

### Lab index

| # | Lab | Focus | Time |
|---|---|---|---|
| 0 | [Set Up Your Environment and Tooling](labs/lab-00-environment-setup.md) | Install & init Spec Kit | 30–45 min |
| 1 | [Establish the Project Constitution](labs/lab-01-constitution.md) | Non-negotiables & stack lock | 30–45 min |
| 2 | [Author the Product Specification](labs/lab-02-product-specification.md) | The *what* & *why* | 45–60 min |
| 3 | [Build the PostgreSQL Database Component](labs/lab-03-database-postgresql.md) | Full SDD loop · data tier | 60–75 min |
| 4 | [Build the Python Back-End API Component](labs/lab-04-backend-api-python.md) | Full SDD loop · API tier | 75–90 min |
| 5 | [Build the ReactJS Front-End Component](labs/lab-05-frontend-react.md) | Full SDD loop · UI tier | 75–90 min |
| 6 | [Integrate, Test, and Iterate End-to-End](labs/lab-06-integration-end-to-end.md) | Integration & living spec | 60–90 min |

### Reference material

- [A — Spec Kit Command Reference](reference/A-spec-kit-command-reference.md)
- [B — Prompt Library](reference/B-prompt-library.md)
- [C — Reference Data Model & API Surface](reference/C-data-model-and-api-surface.md)
- [D — Effective Prompting for SDD](reference/D-effective-prompting.md)
- [E — Troubleshooting & Common Gotchas](reference/E-troubleshooting.md)
- [F — Facilitator Notes](reference/F-facilitator-notes.md)

---

## The golden rules

1. **Spec before code.** If you're prompting for code before the spec and plan exist, stop and back up.
2. **One phase at a time.** Validate the current artifact before generating the next.
3. **Steer and verify.** Your job is judgment, not typing. Read every diff against the spec.
4. **Keep specs alive.** When requirements change, change the spec first — then regenerate.
5. **Small, reviewable changes.** If a task produces a huge diff, the task was too big. Split it.

---

## Repository structure

```
claims-management-workshop/
├── README.md                       ← you are here
├── labs/
│   ├── lab-00-environment-setup.md
│   ├── lab-01-constitution.md
│   ├── lab-02-product-specification.md
│   ├── lab-03-database-postgresql.md
│   ├── lab-04-backend-api-python.md
│   ├── lab-05-frontend-react.md
│   └── lab-06-integration-end-to-end.md
└── reference/
    ├── A-spec-kit-command-reference.md
    ├── B-prompt-library.md
    ├── C-data-model-and-api-surface.md
    ├── D-effective-prompting.md
    ├── E-troubleshooting.md
    └── F-facilitator-notes.md
```

**Start with [Lab 0 →](labs/lab-00-environment-setup.md)**
