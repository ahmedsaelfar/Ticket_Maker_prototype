# 🎫 Ticket Maker — Validation Prototype

A single-file, browser-based assistant for call-center agents. It walks the agent through a troubleshooting SOP step by step, validates their choices **live** against known quality mistakes, and generates a clean ticket / ticket update at the end. It also tracks time per step and gives team leaders an AHT (Average Handling Time) dashboard.

> **Status:** Prototype `v0.1`. Only the **Data Down** flow is fully built. The other case types in the dropdown currently reuse the Data Down flow so the reporting can be previewed.

![Home screen](docs/screenshots/01-home.png)

---

## ✨ Features

### 1. Guided step-by-step case flow
The form reveals each step only when it becomes relevant: customer & CPE → initial checks → data status → phone set → SELT → connection type → right/wrong wiring → escalation checks → final result. If the data is already **UP**, the app tells the agent the case can be closed and hides the rest.

![Data UP closes the case](docs/screenshots/02-data-up-close.png)
![SELT step](docs/screenshots/03-selt-flow.png)

### 2. Live flowchart
A flowchart of the whole Data Down SOP lights up as the agent progresses: path taken, current step, escalation, resolved, and instability branches. A badge shows the current direction (in progress / heading to escalation / resolved).

![Wall outlet path](docs/screenshots/04-wall-outlet-path.png)
![Main wire path](docs/screenshots/05-main-wire-full.png)

### 3. Live Validation + Error Knowledge Base
Every choice is checked immediately.

- **Critical** issues block ticket generation (for example, a SELT reading that doesn't match the chosen threshold, a missing CPE type, or a phone-set contradiction).
- **Learned** advisories come from a built-in knowledge base of 22 recurring mistakes (mobile number checks, duplicate tickets, IR Rework/Acceleration, TTS in parallel, FTTH routing, and more).
- Messages are bilingual (English / Arabic).

![Error knowledge base](docs/screenshots/09-error-knowledge-base.png)

### 4. Voice Verification sub-flow
A dedicated modal covers the voice-verification SOP (same ADSL number, BSS FV status, package/barring checks, credit limit, subscription type, physical instability). If the case is resolved or stopped there, the Data Down steps are skipped and a ticket can be generated straight away.

![Voice verification](docs/screenshots/08-voice-verification.png)

### 5. Escalation pack & ticket generation
Before escalating, the agent gets a ready script and a checklist (told the customer the ticket number, asked for all mobile numbers, was it returned from IU Maintenance). **Create SR** stays disabled until every blocker is cleared. **Generate Ticket** produces a formatted summary, or refuses with a clear reason if critical issues remain.

![Escalation pack](docs/screenshots/06-escalation-pack.png)
![Generated ticket](docs/screenshots/07-generated-ticket.png)

### 6. Quick ticket update
Choose the outcome (Resolved / Waiting for customer callback / Escalated), add what should happen on callback, and get a copy-ready update, including outbound time when relevant.

![Quick update](docs/screenshots/11-quick-ticket-update.png)

### 7. Step timeline & outbound tracking
A timer records how long the agent spends on each step. A **Went outbound** button marks when the agent started an outbound call, with undo for accidental clicks.

![Timeline](docs/screenshots/10-step-timeline.png)

### 8. AHT analysis — Agent view
Click the profile badge to see today's summary, contribution by case type, outbound analysis, and the list of cases handled in the session.

![Agent view](docs/screenshots/12-agent-view.png)

### 9. AHT analysis — Team Leader view
- Team roster (add / remove agents)
- Team overview: agents, cases, average AHT, escalation rate, outbound share
- Highest-AHT steps across the team, agent ranking, and a per-agent drill-down
- **Coaching mode:** shows how often each error occurred. It is off by default so agents are not distracted mid-call
- **Load demo data** to preview the dashboards

![Team leader view](docs/screenshots/13-team-leader-view.png)
![Ranking and drill-down](docs/screenshots/14-team-ranking-drilldown.png)

---

## 🚀 Run it

No build step, no dependencies, no server.

```bash
git clone https://github.com/<your-username>/ticket-maker.git
cd ticket-maker
# just open the file in a browser
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

Or host it for free with **GitHub Pages**: *Settings → Pages → Deploy from branch → `main` / root*.

> The only external request is Google Fonts (Hanken Grotesk, JetBrains Mono). Without internet the app still works with fallback fonts.

## 🧱 Tech

- Plain **HTML + CSS + vanilla JavaScript** in one file (`index.html`)
- Inline SVG for icons and the live flowchart
- No framework, no backend, no build tooling

## 💾 Data & privacy

All data lives in the browser session only. **Nothing is sent to a server and nothing is persisted**, so closing the tab clears everything. Shared storage (sheet/database) is planned for the next phase.

## 🗺️ Roadmap

- [ ] Build the real flows for the remaining case types (Physical Instability, BLQ, WCAP, Browsing, Unable to Obtain IP, Logical Instability, Wireless)
- [ ] Persist cases to a shared sheet/database
- [ ] Close the open items flagged inside the Voice Verification modal
- [ ] Authentication / real agent profiles

## 📁 Structure

```
ticket-maker/
├── index.html            # the whole app
├── README.md
├── .gitignore
└── docs/
    └── screenshots/      # images used in this README
```

---
