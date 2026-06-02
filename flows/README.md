# Power Automate Flows

This project uses two Power Automate flows. Documented here for replication.

---

## Flow 1 — Lineup Creation Flow

**Trigger:** When an agent calls the flow
**Available to:** Lineup Agent

**What it does:**
Receives the full LaTeX meet sheet as text, creates a .txt file in OneDrive,
generates a shareable link, and returns the URL to the agent so the coach
can download and compile it in Overleaf.

**Input parameter:**
- `lineup_text` (string) — the complete compilable LaTeX document

**Steps to replicate:**
1. Create a new flow — trigger: "When an agent calls the flow"
2. Add input: Text → `lineup_text`
3. Add "Create file" action (OneDrive)
   - Folder Path: /Documents
   - File Name: Lineup_[formatDateTime].txt
   - File Content: Text (lineup_text from trigger)
4. Add "Create share link" action (OneDrive)
   - File: Id (from Create file step)
   - Link type: Edit
   - Link scope: Anonymous
5. Add "Respond to the agent"
   - Output name: document_link
   - Value: Web URL (from Create share link step)
   - Description: Web URL of the LaTeX code for the lineup

---

## Flow 2 — Create and Share Practice Document

**Trigger:** When an agent calls the flow
**Available to:** Practice Agent

**What it does:**
Receives the practice plan as text, creates a .txt file in OneDrive,
generates a shareable link, and returns the URL to the agent so the
coach can access the practice document immediately.

**Input parameter:**
- `practice_plan_text` (string) — the full practice plan including warm-up, main set, and cool-down

**Steps to replicate:**
1. Create a new flow — trigger: "When an agent calls the flow"
2. Add input: Text → `practice_plan_text`
3. Add "Create file" action (OneDrive)
   - Folder Path: /Documents
   - File Name: Practice_plan_[formatDateTime].txt
   - File Content: Text (practice_plan_text from trigger)
4. Add "Create share link" action (OneDrive)
   - File: Id (from Create file step)
   - Link type: Edit
   - Link scope: Anonymous
5. Add "Respond to the agent"
   - Output name: document_link
   - Value: Web URL (from Create share link step)
   - Description: Shareable link to the practice plan document in OneDrive

---

## Important Notes

- Both flows must be connected before the agents can generate any file output
- Use the same Microsoft 365 account for the flows and the Copilot Studio agent
- Both flows are triggered by the agent — no manual trigger needed
- No API keys or secrets are stored — all connections use OAuth via Microsoft 365