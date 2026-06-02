# Swim-coach-ai-agent

<img width="1075" height="618" alt="image" src="https://github.com/user-attachments/assets/ff0b6162-abb0-46cc-8986-7200862dba58" />

AI-powered swim program assistant built on Microsoft Copilot Studio. A coordinator agent routes coach requests to four specialist agents — Lineup, Communications, Practice, and Recruiting — eliminating administrative overhead so coaches can focus on the pool.

---

## The Problem

<img width="1137" height="649" alt="image" src="https://github.com/user-attachments/assets/b9e217a0-714f-4694-a0a1-8ee46e8e13b9" />

Collegiate and club swim coaches spend 2–3 hours per meet manually building lineups, writing practice plans from scratch, tracking recruits in spreadsheets, and sending communications one by one. Most programs run on 1–2 coaches doing everything — leaving almost no time for actual coaching.

- **900+** Collegiate swim programs in the US
- **2,740+** Registered clubs in the US
- **36,000+** Swim clubs worldwide
- **35M+** Registered competitive swimmers globally

> "2-3 hours per meet just for lineups"
> — Maggie Kroemer, Head Coach, Valparaiso University Swimming

*Sources: [SwimCloud](https://www.swimcloud.com), USA Swimming*

---

## The Solution

<img width="1152" height="647" alt="image" src="https://github.com/user-attachments/assets/3898d885-44cf-4e90-99ad-69289d9977c8" />

One coordinator agent understands natural language requests and routes them silently to the right specialist. The coach never thinks about which tool to use — they just describe what they need.

| Agent | Responsibilities |
|---|---|
| **Lineup Agent** | Meet lineup optimization, event assignments, swimmer swaps, injury replacements, conflict detection, HY-TEK meet sheet generation |
| **Communications Agent** | Drafting and sending emails via Outlook, notifying swimmers of lineup changes, contacting coaches and administrators |
| **Practice Agent** | Generating practice plans, building workouts, taper planning, adjusting training volume and coaching style preferences |
| **Recruiting Agent** | Finding prospects, filtering by event and time standard, organizing recruiting data, generating recruiting documents |

---

## Tools Used

<img width="1148" height="640" alt="image" src="https://github.com/user-attachments/assets/ec3b0980-4cef-43c8-8f47-8b07fc44fd0e" />

- **Microsoft Copilot Studio** — agent orchestration, coordinator + 4 child agents
- **SharePoint Online** — live roster, meet schedule, and recruiting data
- **Power Automate** — Lineup Creation Flow, Practice document generation
- **Microsoft Outlook** — email drafting, sending, and reading
- **Claude Sonnet 4.6** — reasoning model powering the coordinator
- **LaTeX** — HY-TEK Meet Manager formatted meet sheet output

---

## Architecture

```
Coach (natural language request)
        │
        ▼
Swimming Assistant Coach Agent  ← Coordinator (Claude Sonnet 4.6)
        │
        ├──▶ Lineup Agent
        │       ├── SharePoint (Meet Schedule + Team Roster)
        │       ├── Lineup Creation Flow (Power Automate)
        │       └── lineup_template.txt (LaTeX / HY-TEK format)
        │
        ├──▶ Communications Agent
        │       └── Outlook Connector (Draft, Send, Get emails)
        │
        ├──▶ Practice Agent
        │       └── Create and Share Practice Flow (Power Automate)
        │
        └──▶ Recruiting Agent
                ├── SharePoint (Recruiting list)
                ├── Outlook Connector (Get emails)
                └── Recruiting_guidelines.pdf (knowledge)
```

---

## Repository Structure

```
swim-coach-ai/
├── README.md
├── agents/
│   ├── coordinator_instructions.txt
│   ├── lineup_agent_instructions.txt
│   ├── communications_agent_instructions.txt
│   ├── practice_agent_instructions.txt
│   └── recruiting_agent_instructions.txt
├── templates/
│   └── lineup_template.txt
├── flows/
    └── README.md

```

---

## Setup Instructions

### Prerequisites
- Microsoft 365 tenant with Copilot Studio access
- SharePoint Online site with the following lists:
  - **Meet Schedule** (fields: Title, Date, Location, MaxEvents)
  - **Team Roster** (fields: Title, Email, Year, PrimaryEvent, SecondaryEvent, BestTimePrimary, BestTimeSecondary, Status, Notes)
  - **Recruiting** list
- Power Automate premium connectors enabled
- Outlook connector access

### Step-by-step

1. Clone the repo: `git clone https://github.com/SantiagoGuty/swim-coach-ai`
2. Open [Microsoft Copilot Studio](https://copilotstudio.microsoft.com)
3. Create a new agent — paste contents of `agents/coordinator_instructions.txt` into Instructions, set model to **Claude Sonnet 4.6**
4. Create four child agents using the corresponding files in `agents/`
5. Connect SharePoint connector to your Meet Schedule and Team Roster lists (Lineup Agent)
6. Connect Outlook connector to Communications and Recruiting agents
7. Import the two Power Automate flows from `flows/`
8. Upload `templates/lineup_template.txt` as knowledge to the Lineup Agent
9. Add all four specialist agents as **Child** agents under the coordinator
10. Test by typing: `"Build the optimal lineup for Saturday's meet"`



## Hackathon Submission

Built for the **Microsoft Agent Academy Live Hackathon 2026** — Recruit Track.

| Judging Criteria | How This Project Addresses It |
|---|---|
| Accuracy & Relevance | SharePoint-grounded data only — no hallucination possible |
| Technical Execution | Multi-agent orchestration with silent routing and tool chaining |
| Creativity & Originality | Purpose-built for an underserved sports operations use case |
| User Experience | Coach speaks naturally, agent handles all complexity invisibly |
| Reliability & Safety | Confirmation loops before every action, out-of-scope guardrails |
| Use Case Impact | 900+ collegiate programs, 36,000+ clubs, 35M+ swimmers worldwide |

---

## Author

**Santiago Gutiérrez Morales**
MCS Candidate — University of Illinois Urbana-Champaign (AI Track, Fall 2026)
Former NCAA Division I Swimmer — Valparaiso University

sg136@illinois.edu | [linkedin.com/in/santiagoguty](https://linkedin.com/in/santiagoguty)
