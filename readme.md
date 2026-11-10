# TankTrouble Multi-Account & Alt Stats Analyzer

A lightweight, responsive web aggregator deployed on GitHub Pages that computes, tracks, and analyzes real-time statistics across multiple TankTrouble accounts using the IronVault API.

**Author:** Invincible  
**Live Application:** [Launch Dashboard](https://benvilgaxhu-ui.github.io/Multiple-accounts-stats-Analyzer-/)

---

## ⚡ Overview

Monitoring performance across multiple accounts or alternate identities in TankTrouble usually demands manual lookups for every single profile on IronVault. 

This utility automates that process: simply paste a batch of usernames, and the dashboard queries the backend, resolves casing differences, works around strict rate limits, computes accurate game-mechanic metrics, and generates live cumulative totals.

---

## 🚀 Key Features

- **Bulk Alt Aggregation:** Analyze dozens of accounts in a single execution with real-time progress indicators.
- **Dynamic Sorting Options:**
  - Sort by **Kills (High → Low / Low → High)**.
  - Sort by **K/D Ratio**, **Win Rate %**, or **Level**.
  - Retain the **Original Order** as entered in the text box.
  - Clickable table headers for instant toggle sorting.
- **Single-Account Retry (↻):** If an account encounters a temporary network drop or rate limit resulting in `Not Found`, click the refresh icon next to the username to re-fetch that single account without rerunning the entire list.
- **Accurate Combat & XP Metrics:**
  - **Kills & Deaths:** Frags and total losses recorded.
  - **Kill/Death Ratio (K/D):** Individual combat efficiency and overall weighted group ratio.
  - **Defeats:** Calculated cleanly via $\text{Deaths} - \text{Suicides}$.
  - **Win Rate (%):** Normalized ratio derived from $\frac{\text{Victories}}{\text{Victories} + \text{Defeats}} \times 100$.
  - **Level Derivation:** Mapped directly against official XP thresholds ($0$ to $190{,}000\text{ XP}$) covering Levels 1 through 20.
- **Fault-Tolerant Engine:**
  - Multi-stage retry with exponential backoff for `HTTP 429` (Rate Limit) and `HTTP 500` server errors.
  - Automatic username casing, underscore, and space normalization.
  - Non-existent accounts are tagged with an isolated `Not Found` badge so cumulative statistics remain clean.
- **Data Export:** Export the parsed table into a standard `.csv` spreadsheet with one click.
- **Custom Visual Branding:** Embedded SVG Tank favicon for the browser tab and a clean dark-mode interface.

---

## 🌐 Live URL

You can access and run the hosted application directly:

```text
https://benvilgaxhu-ui.github.io/Multiple-accounts-stats-Analyzer-/
```

---

## 📖 How to Use

1. Navigate to the [Live Dashboard](https://benvilgaxhu-ui.github.io/Multiple-accounts-stats-Analyzer-/).
2. In the **Player Accounts** text area, paste your target account usernames (one name per line):
   ```text
   Invincible
   PlayerOne
   TankMaster99
   SpeedyTank
   GhostRider
   ```
3. Click **Calculate & Fetch All Stats**.
4. The dashboard will query each profile sequentially, populating cumulative cards and the sortable breakdown table.
5. If any account shows `Not Found` due to a server hiccup, click the **↻** button next to its name to retry.
6. Click **Export CSV** to download the aggregated results.

---

## 🧮 Calculation Logic

| Metric | Derivation Logic |
| :--- | :--- |
| **K/D Ratio** | $\frac{\text{Kills}}{\text{Deaths}}$ (or $\text{Kills}$ if $\text{Deaths} = 0$) |
| **Defeats** | $\text{Deaths} - \text{Suicides}$ (falls back to $\text{Deaths}$ if suicides exceed losses) |
| **Win Rate** | $\frac{\text{Victories}}{\text{Victories} + \text{Defeats}} \times 100$ |
| **Level** | Derived from `data.xp` mapped against the 20-tier XP threshold scale ($0$ to $190{,}000\text{ XP}$) |

---

## 🛠️ Tech Stack

- **Frontend:** HTML5, [Tailwind CSS](https://tailwindcss.com), [Font Awesome 6](https://fontawesome.com)
- **Engine:** Pure Vanilla JavaScript (Fetch API, Async/Await)
- **Data Provider:** [IronVault API](https://ironvault.vercel.app/)
- **Hosting:** GitHub Pages

---

## 👤 Credits & License

- Designed & Built by **Invincible**
- Released under the [MIT License](LICENSE).