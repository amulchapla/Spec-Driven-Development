# Appendix C — Reference Data Model and API Surface

[← Back to README](../README.md)

> This is a **reference target, not a script to paste.** Let the agent derive the design from your spec and plan, then compare against this to sanity-check coverage.

## Entities (suggested)

| Entity | Key fields | Relationships |
|---|---|---|
| **Customer** | `id`, `name`, `email`, `phone` | has many Claims |
| **User / Administrator** | `id`, `name`, `email`, `role` | reviews Claims |
| **Claim** | `id`, `claim_number`, `customer_id`, `status`, `policy_number`, `loss_type`, `incident_date`, `location`, `description`, `amount_claimed`, timestamps | belongs to Customer; has many Documents and History |
| **Claim Document** | `id`, `claim_id`, `file_name`, `content_type`, `storage_path`, `uploaded_at` | belongs to Claim |
| **Claim Status History** | `id`, `claim_id`, `changed_by`, `from_status`, `to_status`, `note`, `changed_at` | belongs to Claim (append-only) |

## API surface (suggested)

| Method & path | Persona | Purpose |
|---|---|---|
| `POST /auth/login` | Both | Authenticate and receive a token |
| `POST /claims` | Customer | Create a draft claim (FNOL) |
| `PUT /claims/{id}` | Customer | Update an editable claim |
| `POST /claims/{id}/submit` | Customer | Submit a claim for review |
| `POST /claims/{id}/documents` | Customer | Upload a photo/document |
| `GET /claims` · `GET /claims/{id}` | Customer | List / view own claims |
| `GET /admin/claims?status=` | Admin | List / filter the review queue |
| `POST /admin/claims/{id}/approve` | Admin | Approve a claim |
| `POST /admin/claims/{id}/reject` | Admin | Reject a claim |
| `POST /admin/claims/{id}/request-info` | Admin | Request more information |
| `POST /admin/claims/{id}/notes` | Admin | Add an internal note |

## Claim lifecycle

```
Draft → Submitted → Under Review → Info Requested → Approved / Rejected → Closed
```

- A claim always has a valid status from this lifecycle.
- Status history is **append-only** — every transition records who changed it, when, and an optional note.
- Only an administrator may move a claim to *Approved*, *Rejected*, or *Info Requested*.

---

[← Back to README](../README.md)
