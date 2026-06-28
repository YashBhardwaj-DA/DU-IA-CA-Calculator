# DU IA/CA Calculator

A single-file, no-login tool for Delhi University NEP students to track their **Internal Assessment (IA)** and **Tutorial/Continuous Assessment** marks across the semester — because most colleges never show this breakdown to students until results are already out.

**Live tool:** _add your deployed URL here_

---

## Why this exists

Under DU's NEP 2022 structure, every paper's marks are split across components that colleges rarely explain clearly:

- Small papers (**AEC / SEC / VAC**, 2 credits) → IA out of **10**
- Big papers (**DSC / DSE / GE**, 4 credits) → IA out of **30**
- Each paper also carries a **Component**: `LT` (Lecture+Tutorial), `LP` (Lecture+Practical), or `P` (Practical only)
- Practical marks are **never released to students** by the university — only the Lecture-side IA and, for LT papers, the Tutorial marks are visible
- IA itself splits into **Assignment (40%) + Class Test (40%) + Attendance (20%)**
- Tutorial marks (out of 40, LT papers only) convert to a letter grade in bands of 5: `0–5 F · 5–10 D · 10–15 C · 15–20 B · 20–25 B+ · 25–30 A · 30–35 A+ · 35–40 O`

This tool walks through that exact structure — pick your semester, add your actual papers with their real type and component, enter the marks as your professors announce them, and get a running statement that mirrors a DU marksheet's format.

It does **not** predict your final grade or theory-paper score. It only tracks the IA/Tutorial portion that's visible to you during the semester. Practical-only papers are explicitly skipped, never guessed at.

---

## How it works (the wizard)

1. **Student Info** — name, roll number, enrolment number, college, and semester (only semester is required).
2. **Subjects** — add each paper with its Type (DSC/DSE/GE/AEC/SEC/VAC) and Component (LT/LP/P). The tool calculates credits and IA max automatically.
3. **Enter Marks** — for each non-practical paper, enter Assignment, Class Test, and Attendance marks against their real maximums. LT papers also get a Tutorial marks field with a live grade preview.
4. **Dashboard** — a DU-statement-style table of every paper, its IA breakdown, Tutorial marks and grade, and running totals. Printable straight to PDF.

Everything is editable at any time — go back a step, change a number, the dashboard updates instantly.

---

## Features

- **Manual entry only**, by design — many colleges don't expose this data to students at all, so the tool never tries to fetch or guess it.
- **Type-aware IA maximums** — 10 for AEC/SEC/VAC, 30 for DSC/DSE/GE, calculated automatically from what you select.
- **Component-aware skipping** — Practical-only (`P`) papers are excluded from entry entirely, since that data is genuinely not available to students.
- **Live Tutorial grading** — see the letter grade update as you type, using DU's standard 5-mark bands.
- **Local-only storage** — your data is saved to `localStorage` as you go, so refreshing or returning later doesn't lose your progress. Nothing is ever sent to a server.
- **Print/PDF export** of the final dashboard in a clean, marksheet-style layout.
- **Start Over** control to wipe everything and begin a new semester from scratch.

---

## Tech stack

Plain HTML, CSS, and vanilla JavaScript — **one single `index.html` file**, no build step, no dependencies beyond two Google Fonts. This was a deliberate choice to make deployment to Netlify (or any static host) a pure drag-and-drop with zero configuration.

---

## Running it locally

```bash
python3 -m http.server 8080
```
Then open `http://localhost:8080`. Or just double-click `index.html` — it works from `file://` too, since there's no routing or server dependency.

---

## Deployment (Netlify)

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the folder containing `index.html` onto the page.
3. Done — Netlify gives you a live URL immediately.

To connect it to a custom domain (e.g. `du-ia-calculator.netlify.app` or your own domain), use **Domain settings** in your Netlify site dashboard after the first deploy.

For GitHub-based deploys instead: push this repo to GitHub, then **Add new site → Import an existing project** in Netlify and point it at the repo. Build command: leave blank. Publish directory: `.` (root) — since it's a single file at the root, no build output folder is needed.

---

## Customizing the rules

All the grading logic lives in one place near the top of the `<script>` block in `index.html`:

- `SMALL_TYPES` / `BIG_TYPES` — which paper types count as 2-credit vs 4-credit
- `iaMaxFor()` — IA maximum per type
- `iaBreakdownMax()` — the 40/40/20 split of Assignment/Test/Attendance
- `gradeForTutorial()` — the 5-mark Tutorial grade bands

If your college uses a different split, these are the only functions you'd need to touch.

---

## Privacy

No analytics, no cookies, no accounts, no network requests besides loading the page itself and two font files. All marks data stays in your browser's `localStorage`, scoped to whichever domain hosts the site, and is never transmitted anywhere.

---

## Disclaimer

This is an independent, unofficial student tool. It is not affiliated with, endorsed by, or connected to the University of Delhi or any of its colleges. Always confirm your actual marks with your college's official portal or administration — this tool only helps you track and total what you've been told, in the format DU eventually uses.

---

## License

MIT — use it, fork it, adapt it for your own college's IA structure.
