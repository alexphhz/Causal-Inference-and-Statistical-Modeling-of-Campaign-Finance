# Data 102 — Campaign Finance & Voter Support

> **TL;DR**: This project investigates how **state-level economic conditions** and **campaign finance** relate to **voter support and primary outcomes** in U.S. elections. We combine **official datasets** (Census, BEA, FHFA, SBA, FEC) with **third‑party sources** (OpenSecrets, Kaggle), and apply **econometric methods** including OLS, multiple‑hypothesis correction (FWER/FDR), and causal designs (IV & propensity‑score matching).

---

## 🎯 Research Questions
1. How are **economic indicators** (e.g., GDP growth, unemployment, mortgage index, small‑business loans) associated with **campaign spending** and **vote shares**?
2. Which **endorsements** or **spending categories** best predict **primary outcomes**?
3. After controlling for confounders, do these relationships remain robust under **multiple‑testing correction** and **causal** strategies?

---

## 🗂️ Repository Structure
```
.
├─ README.md
├─ requirements.txt
├─ data/
│  ├─ raw/          # original inputs (not committed in production)
│  ├─ processed/    # cleaned / engineered datasets
│  └─ README.md     # data source links & notes
├─ notebooks/
│  └─ analysis.ipynb (or your final .ipynb)
├─ src/
│  ├─ __init__.py
├─ reports/
│  └─ report.pdf        # final write‑up (this repository’s basis)
└─ docs/                # exported figures/tables
```

> In this course‑style repo, the **notebook** demonstrates end‑to‑end analysis.

---

## 🧭 Data Sources (as used in the report)
- **U.S. Census** — population & demographics (state level)
- **BEA** — GDP growth / personal income
- **FEC** — federal campaign finance filings
- **OpenSecrets** — spending categories / summaries
- **FHFA** — mortgage price index
- **SBA** — small‑business loans
- **Kaggle / other** — supplemental compiled datasets

> See `data/README.md` for concrete links, vintages, and any data‑use notes. Raw files live in `data/raw/` (typically excluded from git); cleaned artifacts go to `data/processed/`.

---

## 🧹 Data Preparation
1. **Standardize identifiers** (state names/abbreviations, election cycles).
2. **Clean & harmonize**: handle missing values, units, nominal→real adjustments if applicable.
3. **Join** economic indicators to election finance records at the **state‑cycle** level.
4. **Feature engineering**: per‑capita spend, log transforms, lagged indicators, binary treatment flags (e.g., key endorsements).
5. **Splits**: create analysis subsets for **primaries** vs **general**, or **party**‑specific models.

---

## 📐 Methods
- **Descriptive & EDA**: correlation heatmaps, distribution checks, outlier diagnostics.
- **OLS regressions** with robust SEs (HC1/HC3 or cluster by state), model comparison via AIC/BIC and adj. R².
- **Multiple hypothesis testing**: control **FWER** (Bonferroni/Holm) and **FDR** (Benjamini‑Hochberg) across families of regressors.
- **Causal strategies** *(if applicable in your report)*:
  - **Propensity‑score matching** (nearest‑neighbor/Caliper) to estimate ATT on outcomes.
  - **Instrumental variables** for suspected endogenous regressors (2SLS diagnostics, weak‑IV tests).
- **Robustness**: alternative specifications, excluding influential points, placebo checks.


---

## 🔁 Reproducibility

### Environment
```bash
python -m pip install -r requirements.txt
jupyter lab  # or: jupyter notebook
```

### Run
- Open `notebooks/analysis.ipynb` (or the provided final notebook).
- Execute cells top‑to‑bottom to reproduce tables & figures.
- If large raw data are not tracked, follow `data/README.md` to download and place files under `data/raw/`.


---

## 📊 Key Results (from the report)
- Associations between **economic conditions** (GDP growth, unemployment, mortgage index, SBA loans) and **spending / vote share**.
- Signals from **endorsements**/**spending categories** on **primary outcomes**.
- Findings that **survive multiple‑testing** corrections; sensitivity to **IV/matching**.

> For exact coefficients, CIs, and corrected p‑values, see **`reports/report.pdf`** and the final notebook outputs in `notebooks/`.

---

## ⚠️ Limitations
- Observational data: potential omitted‑variable bias / reverse causality.
- Data coverage/vintage mismatch across sources.
- State‑level aggregation may mask county/district heterogeneity.


