# MM Paid Monitoring — Spec

## Purpose
Automated Google Ads performance monitoring for MindMeister (MM) paid campaigns.
Single n8n workflow with three independent trigger paths.

## Slack Channel
- **Testing**: `C08NX15CMEJ`
- **Production**: TBD

## Paths

### 1. Daily — Anomaly Alert (Mon–Fri, 9 AM)
- **Data source**: Google Ads API (native n8n node)
  - Pulls yesterday's campaign data
  - Pulls last-7-days campaign data for rolling average baseline
- **Anomaly thresholds**:
  - CPC up >25% vs 7-day average → ⚠️ warning / 🚨 critical at >50%
  - CTR down >20% vs 7-day average → ⚠️ warning / 🚨 critical at -40%
  - ROAS down >30% vs 7-day average (if conversions > 0)
  - Daily spend >50% above 7-day daily average
  - Per-campaign checks for campaigns with ≥€20 spend
- **Output**: Always sends daily summary; anomaly section included when triggered
- **AI**: OpenAI GPT-4o writes the Slack message

### 2. Weekly — WoW Report (Tuesday, 10 AM)
- **Data source**: Google Sheets (`last_week` + `prev_week` tabs)
- **Sheet**: `MM Paid campaign overview` (ID: `1Uag5Qd7elO6R6S1VLXvWIATfK9MHHbNkr-sNM1BOaX0`)
- **Budget**: `Meister 2025 - Budget planning sheet - Paid Ads` — MM tab (current month)
- **Output**: WoW comparison, channel breakdown, top/bottom campaigns, 2 recommendations
- **AI**: OpenAI GPT-4o writes the Slack message

### 3. Monthly — MoM Report (1st of month, 10 AM)
- **Data source**: Google Sheets (`last_month` + `prev_month` tabs)
- **Budget**: MM budget tab (last month figures)
- **Output**: MoM comparison, full channel analysis, trend observation, 3 recommendations
- **AI**: OpenAI GPT-4o writes the Slack message

## n8n Credentials Required
| Purpose | Credential name |
|---------|----------------|
| Google Ads API | ⚙️ Needs to be configured (customer ID = MM Google Ads account) |
| Google Sheets | `Daan - Google sheet connection` |
| OpenAI | `Daan Open AI key` |
| Slack | `Campaign - Bot connection (Daan)` |

## Workflow Setup
1. Import `workflow.json` into n8n
2. Open each `Get MM Campaigns` node and set the MM Google Ads Customer ID + credential
3. Activate the workflow

## File Structure
```
meister-mm-monitoring/
├── SPEC.md           — this file
├── CLAUDE.md         — instructions for Claude
└── workflow.json     — n8n workflow export
```
