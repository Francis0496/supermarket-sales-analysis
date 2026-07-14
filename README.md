# 🛒 Supermarket Sales — From Exploration to Data-Driven Decisions

An end-to-end retail analytics project that turns **one quarter of point-of-sale data** into a set of
**ranked, evidence-backed business decisions** — each supported by its data, stress-tested for
statistical significance, and framed in dollar terms.

> The guiding principle: don't stop at *"which branch sells the most?"* Climb the analytics ladder —
> **descriptive → diagnostic → segmentation → statistical proof → decision** — and only act on effects
> that are actually real.

---

## 🎯 Goals & Objectives

**Primary goal:** convert raw transaction data into decisions a retail operator can act on Monday morning.

**Objectives:**
1. **Establish trust in the data first** — quantify and repair quality issues (missing values, duplicate
   invoices) *before* drawing any conclusion, recovering data losslessly rather than discarding it.
2. **Map where value concentrates** — revenue and gross income across branches, product lines and time.
3. **Diagnose the "why" and "when"** — expose the operational levers (peak hours/days, payment mix,
   customer-experience signals) that management can actually pull.
4. **Segment the customer base** — identify which customer types are worth most and how to target them.
5. **Prove it before spending** — use significance testing (ANOVA, t-tests, χ²) to separate real
   effects from noise, so budget isn't wasted chasing phantom gaps.
6. **Deliver quantified recommendations** — translate every finding into a concrete action with an
   estimated financial impact.
7. **Communicate clearly** — package the analysis as a reproducible notebook, a static report, and an
   interactive executive dashboard.

---

## 📦 Dataset

`supermarket_sales.csv` — ~1,000 transactions from a **3-branch supermarket chain** in Myanmar.

| Attribute | Detail |
|---|---|
| **Period** | January – March 2019 (Q1) |
| **Branches** | A · Yangon &nbsp;/&nbsp; B · Mandalay &nbsp;/&nbsp; C · Naypyitaw |
| **Grain** | One row = one invoice (transaction) |
| **Columns (17)** | `Invoice ID`, `Branch`, `City`, `Customer type`, `Gender`, `Product line`, `Unit price`, `Quantity`, `Tax 5%`, `Total`, `Date`, `Time`, `Payment`, `cogs`, `gross margin percentage`, `gross income`, `Rating` |

**Data-quality issues found & fixed (Stage 0):** 3 duplicate invoices removed and **149 missing values**
handled. Missing `Quantity`/`Unit price` were **recovered losslessly** using the exact identity
`Total = Unit price × Quantity × 1.05`, retaining **99.7%** of rows (1,003 → 1,000) instead of dropping them.

---

## 🧭 Analytical Workflow

| Stage | Question it answers | Decision it unlocks |
|---|---|---|
| **0 · Integrity** | Can I trust the numbers? | A clean, recovered dataset |
| **1 · Descriptive** | Where does the money concentrate? | Where to focus attention |
| **2 · Diagnostic** | *When* / *why* does it happen? | Operational levers (staffing, stock) |
| **3 · Segmentation** | Who is worth more? | Targeting & loyalty strategy |
| **4 · Statistical** | Are the differences *real*? | Confidence to act (or not) |
| **5 · Decision** | What do we do, and what's it worth? | Dollar-sized actions |
| **6 · Deeper cuts** | Which customers & categories to target? | RFM- and basket-style targeting |

---

## 💡 Key Findings & Decisions

1. **Staff & stock to the peak, not the average.** Saturdays around **19:00** are busiest
   (~$39,700 flows through that single hour). Aligning shifts/checkout capacity here is the highest-ROI lever.
2. **Don't chase branch-vs-branch gaps.** Revenue is near-parity (~4% spread) and the differences are
   **not statistically significant** — there's no failing store to rescue.
3. **Route payment tactics per branch.** Branch C leans cash; A & B lean e-wallet → target fee
   negotiations and promos accordingly.
4. **Turn loyalty from discount into lift.** Members and non-members spend almost the same — the program
   recognizes customers without lifting basket size.
5. **Run a service program at Branch B** (lowest rating) — and treat rating as its **own KPI**, since it
   has ~zero correlation with spend.
6. **RFM adaptation → Segment Value Matrix.** *(True RFM isn't possible — no customer ID.)* **Member-Female**
   is the most valuable segment (~$80K); **Normal-Male** visits most but spends least → basket-building target.
7. **Market-basket adaptation → Category Affinity (lift).** *(True basket analysis isn't possible — one
   product line per invoice.)* Signals are mild but directional: men over-index on **Health & beauty**
   (1.14×), women on **Fashion accessories**.

> **The core insight (reframe):** with a **fixed ~4.76% margin** and a **statistically uniform chain**,
> profit is driven by **operational throughput at peak times and payment economics** — *not* by
> merchandising or "fixing" a weak store.

---

## 📁 Repository Structure

```
SUPERMARKET/
├── supermarket_sales.csv       # Raw dataset (input)
├── supermarket.ipynb           # Main analysis notebook (EDA + Stages 0–6)
├── supermarket_report.html     # Static, self-contained report (executed notebook)
├── supermarket_report.pdf      # Portable/printable version of the report
├── dashboard.html              # Interactive executive dashboard of the 7 decisions
├── requirements.txt            # Python dependencies
└── README.md                   # You are here
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+

### Setup & run
```bash
# 1) (optional) create a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 2) install dependencies
pip install -r requirements.txt

# 3) launch the notebook
jupyter notebook supermarket.ipynb
```

Prefer not to run anything? Just open **`supermarket_report.html`** (or the PDF) in any browser — it's
fully self-contained with all charts embedded. For the interactive view, open **`dashboard.html`**.

---

## 🔬 Methodology Notes & Honesty

- **Lossless recovery over row-dropping.** Missing numerics were rebuilt from a verified accounting
  identity, and all financial identities (`Total = cogs + gross income`, `Tax = 5% × cogs`) were validated.
- **Significance-gated conclusions.** Every headline gap was tested at α = 0.05. The honest result —
  *the chain is statistically uniform* — is itself a decision (don't fund phantom differences).
- **Textbook RFM and market-basket are not computable on this data**, and the project says so plainly:
  there is **no customer identifier** (so no recency/repeat-visit history) and **one product line per
  invoice** (so no co-purchases). Stages 6 delivers rigorous *adaptations* that answer the same business
  questions.
- **Scope caveat.** This is a single quarter (n = 1,000) — a strong operational read, but too short to
  establish seasonality. Weekday/hour patterns are current-state, not annualized.

---

## 🛠️ Tech Stack

`Python` · `pandas` · `NumPy` · `Matplotlib` · `seaborn` · `SciPy` · `Jupyter`
Charts use the colorblind-safe **Okabe–Ito** palette, shared across the notebook and dashboard so they
read as one visual system.

---

## 📌 Author

Analysis by **[your name]** · `sesay.f@northeastern.edu`

*Feel free to open an issue or PR with suggestions.*
