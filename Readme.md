# Stay vs Switch Analyser

An AI-powered career decision tool for early-career professionals. Helps you decide whether to stay in your current job or start looking — with personalised reasoning, industry benchmarks, and a downloadable PDF report.

**Live demo:** `https://yourusername.github.io/stay-or-switch`

---

## What it does

Users answer ~20 questions across 6 dimensions of their current job:

- 💰 Compensation & Benefits
- 🚀 Growth & Learning
- 🎯 Role & Impact
- 🤝 Manager & Culture
- 📊 Market & Stability

The tool then produces:

- **A verdict** — Stay & Optimise, Start Looking, or It Depends
- **Dimension scores** (out of 10) adjusted by industry context
- **Benchmark comparison** — bar chart + percentile rankings vs industry peers
- **AI coaching narrative** — personalised 3-paragraph career coaching via Claude API
- **Key signals** — specific reasons driving the recommendation
- **Next moves** — 4 actionable steps tailored to their scores
- **Shareable URL** — results encoded in the link, no data stored
- **PDF report** — full downloadable report with all of the above

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/yourusername/stay-or-switch.git
cd stay-or-switch
```

### 2. Configure Formspree (lead notifications)

When a user downloads the PDF report, you receive an email with their:
- Name
- Industry
- WhatsApp number
- Email address
- Verdict and overall score

To set this up:
1. Create a free account at [formspree.io](https://formspree.io)
2. Create a new form — name it `Stay vs Switch Leads`
3. Copy your endpoint (e.g. `https://formspree.io/f/mykagdao`)
4. In `index.html`, find this line and replace with your endpoint:

```js
const FORMSPREE_ENDPOINT = "https://formspree.io/f/YOUR_FORM_ID";
```

> The current repo already has an endpoint configured. If you fork this, replace it with your own.

### 3. Rename the file

Rename `stay-switch-v3.html` to `index.html` so GitHub Pages serves it as the homepage:

```bash
mv stay-switch-v3.html index.html
```

### 4. Push to GitHub

```bash
git add .
git commit -m "Initial deploy"
git push origin main
```

### 5. Enable GitHub Pages

1. Go to your repo on GitHub
2. Click **Settings → Pages**
3. Under **Source**, select `Deploy from a branch`
4. Choose `main` branch, `/ (root)` folder
5. Click **Save**

Your tool will be live at `https://yourusername.github.io/stay-or-switch` within a minute.

---

## How the scoring works

Each dimension is a weighted composite of slider and pill answers:

| Dimension | Weight | Key drivers |
|---|---|---|
| Growth | 28% | Skill velocity, mentorship, promotion clarity |
| Culture | 22% | Manager quality, psychological safety, burnout |
| Compensation | 20% | Market rate, raise trajectory, benefits |
| Role | 18% | Impact, clarity, visibility |
| Market | 12% | Skills demand, company stability |

**Verdict thresholds:**
- ≥ 6.8 → Stay & Optimise
- ≤ 4.2 → Start Looking
- Between → It Depends

All scores are adjusted by **industry modifiers** — a 7/10 skill growth score means something different in a startup vs a government role.

---

## Industry benchmarks

Benchmark averages are currently simulated based on typical industry distributions. To make them data-driven over time, replace the `BENCHMARKS` object in `index.html` with aggregated real scores from your user base.

---

## Tech stack

- Pure HTML/CSS/JS — no framework, no build step
- [Chart.js](https://chartjs.org) — benchmark bar chart
- [jsPDF](https://github.com/parallax/jsPDF) — client-side PDF generation
- [Claude API](https://anthropic.com) — AI coaching narrative
- [Formspree](https://formspree.io) — lead notification emails

---

## Customisation

| What | Where in `index.html` |
|---|---|
| Industry list & modifiers | `const INDUSTRIES = [...]` |
| Benchmark averages | `const BENCHMARKS = {...}` |
| Scoring weights | Inside `computeScore()` |
| Verdict thresholds | Inside `getVerdict()` |
| Formspree endpoint | `const FORMSPREE_ENDPOINT` |
| Questions | `const STEPS = [...]` |

---

## License

MIT — free to use, fork, and modify.

---

*Built for early-career professionals navigating one of the most important decisions of their working life.*
