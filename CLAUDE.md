# KDC Impact360 — Development Impact & Performance Management System · CLAUDE.md

Last updated: 2026-10-06 (demonstration build 1.0)

A demonstration of **Eval360 configured for Kenya Development Corporation (KDC)**, a state
development finance institution. It connects strategy → capital deployment → investment →
implementation → development results → additionality → ESG → risk → evidence → evaluation →
learning → management decision. The centrepiece is the relationship between **financial
performance** and **development impact** (the development-finance matrix).

Architecture and rules follow the CIC demonstration (`../cic-eval360`), which follows FPC
(`../fpbc-eval360`). Same single-file pattern, same conventions.

---

## Two kinds of data — never mixed silently

This is the rule that matters most in this project (brief §2, §107–§110, §131–§133).

| Provenance | What | How it is shown |
|---|---|---|
| `PUBLIC_KDC` | Figures published by KDC or the World Bank — strategic targets, the 18 performance standards, SAFER first-year results, DRIVE targets and milestones, product parameters, the Strategic Plan's KRAs and objectives | Green **Public KDC Data** badge (`pubBadge(key)`); click opens the source |
| `DEMO_SYNTHETIC` | Every investee, PFI, county record, balance, score, rating, risk, action, ESAP, evaluation rating | Dashed **Illustrative Demo Data** badge (`demoBadge()`) |
| `CALCULATED` | Derived from either (e.g. SAFER disbursement rate 2.3 ÷ 3.5 = 65.7%) | `calcBadge()` |
| `USER_ENTERED` | Anything changed during a session | Activity log, `source_type` on the record |

- Every public figure lives in `PUBLIC` and names a source in `SOURCES` (section 7 of the file).
  **All were checked against the source on 6 October 2026** and are `CONFIRMED`; a consistency
  check fails if any public figure lacks a source or a confirmed status.
- Public and synthetic figures sit in visibly separate zones (`.zone pub` / `.zone demo`).
- **No invented history for a public point-in-time figure.** SAFER's results are a snapshot as at
  10 May 2025 — they get no trend line.
- Synthetic records reconcile to the public totals where they sit underneath them (the five
  SAFER PFIs sum to KES 2.3B disbursed, 3.225B committed, 33,000 MSMEs, 17,000 jobs, 35% women-led).

### Source register (verified 6 Oct 2026)

| Source | Supports |
|---|---|
| KDC Strategic Plan 2024/25–2028/29 ("KDC 2.0") | 118,714 jobs (annual 21,593 · 37,047 · 15,223 · 18,637 · 26,214), KES 16.3B GDP, 2.5M trees, Table 8.2.1 standards, 3 KRAs, 14 objectives, 4 goals |
| KDC press release, 10 May 2025 — SAFER first year | KES 3.5B / 2.3B / 3.225B, 33,000+, ~17,000 jobs, 19 regions, 12 products, 35% women-led, KES 3.15B+ pipeline |
| World Bank P175017 (SAFER) | IDA, USD 100M, effective 9 May 2022; KDC apex for Component 1 |
| World Bank press release 23 Jun 2022; DRIVE ISR P176517 (Apr 2025); ZEP-RE | DRIVE regional targets (1.6M, 2,500, 80%, USD 72M) and Kenya targets (800,000, 1,200, USD 40M, USD 115M, 37%; 60% reported Dec 2024; 150,000+ / 125,000) |
| KDC press releases (13 May 2025; Feb 2026) | KES 519M+ livestock value-chain financing; KES 70M West Pokot (Eco Pillar Sacco) |
| KDC products pages | Project, asset and green finance parameters |
| KDC job openings (2 Oct / 24 Sep 2026) | M&E Officer and Sustainability Officer requirements |

URLs are recorded in `SOURCES` and on the Master Data & Sources screen.

---

## Where this build departs from the brief, and why

| Brief | Built | Why |
|---|---|---|
| DRIVE "Component 2" figures (USD 40M, 1,200 groups, 800,000, USD 115M, 37%) | Labelled **Kenya targets**; 800,000 filed under Component 1 | That is how the World Bank results report labels them |
| DRIVE USD 72M "Component 1" | Regional, Component 2 de-risking facility | Source labelling |
| 1.6M people, 2,500 groups, 80% | Labelled **Regional (four countries)** | They are not Kenya-only targets |
| KES 519M milestone "March 2025" | 13 May 2025 | Release date on the PDF (KDC listing page shows 13 March) |
| Product list of 7 | 7, with a note that KDC also lists Digi-Finance and Special Projects | Source |
| Jobs trend Q1 FY2025/26 → **Q2 FY2026/27** = 74,320 | Shifted one quarter: ends **Q1 FY2026/27** | On 6 Oct 2026, Q2 FY2026/27 has not happened; Q1 has just closed. Same shift for the §106 impact trend |
| Portfolio health 78 / 24 / 12 / 6 + 6 exited, "126 active" | **84** / 24 / 12 / 6 active (= 126) + 6 exited | The brief's numbers sum to 120 active |
| "ESG actions overdue: 17" (§92) vs "5 ESAP overdue" (§80) vs "3" (§95) | **17 outstanding, 5 overdue** everywhere | One derived set of figures |
| "2 investments moved to High Risk" (§95) vs 3 (§80) | **3** everywhere | Same |
| Rift Agro development impact 76% (§36) and scorecard 79.8% (§40) | Both, as two measures | 76% = weighted impact dimensions (§102); 79.8% = six-dimension scorecard incl. additionality and ESG (§40) |
| KRA / objective structure | Verbatim from the plan | Found in the source; KPI-to-objective mapping is this demo's |
| "Strategic performance" (§91, no definition) | **KPI performance index** = share of the 21 KPIs on track, needs-attention counting ½ | An average of capped achievements read ~96% while 10 of 21 KPIs miss their standard |

All other quoted figures are derived from the records and asserted by 40 consistency checks —
including 74,320 jobs (= portfolio 42,600 + SAFER 17,000 + other programmes 14,720), KES 31.8B /
23.4B, 89 / 25 / 12, 42,600 jobs, 19,300 women/youth, KES 8.3B private capital, 74% impact,
86% collections, the data-quality figures 126 / 119 / 110 / 9 / 7 / 4, 48 actions (28/13/5/2),
and every Rift Agro figure.

---

## Layout, rules, testing

Same as `../cic-eval360/CLAUDE.md` — read it. In short:

- `kdc_eval360_demo.html` is the source of truth; edit it directly. No build step, no framework.
- Fixed clock **6 Oct 2026**; Kenya FY (Q1 Jul–Sep). Reporting period Q1 FY2026/27, closes 12 Oct.
- Every figure derived (section 18); quotas exact (`quota()` + residual calibration); generators
  order-dependent — run the self-test after any change to section 17.
- All date arithmetic in UTC (`addDays`, `daysBetween`).
- No inline `onclick`; `data-action` + `ACTIONS` / `CHANGES` / `SUBMITS`.
- Roles, not people: the brief asks that no individual's name be invented. Twelve role accounts.
- Verification chain (§59): Investment Officer submits → Portfolio Manager reviews (`canReview`)
  → M&E Officer validates (`canValidate`). Only Verified / Locked results reach dashboards.
- Programme-level access: SAFER and DRIVE officers see only their programme.

```bash
bash scripts/selftest.sh     # 67 screens × 12 roles + 40 data checks; exit 1 on failure
```

Open any screen directly: `kdc_eval360_demo.html#investment-detail/INV-2024-014/dg`.

## Working agreement

1. Self-test before every commit.
2. A new public figure needs a `SOURCES` entry and a check against the source before it gets the
   Public badge. Until then it is synthetic.
3. If KDC supplies real portfolio data, it replaces the synthetic records — and the provenance
   changes with it.
