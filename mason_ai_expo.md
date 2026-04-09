# AI for Scarce Healthcare Resource Allocation

---

## Slide 1 — AI for Scarce Healthcare Resource Allocation

- Yikuan Li, Assistant Professor, College of Public Health
- George Mason University AI Expo
- April 29, 2026 — Fuse at Mason Square

---

## Slide 2 — The Crisis Moment

- During COVID-19, hospitals faced impossible choices: more patients needing ventilators than ventilators available
- Crisis Standards of Care activated across the U.S.
- The question shifted from *"How do we treat this patient?"* to *"Who gets treated at all?"*
- **News reference 1:** *New England Journal of Medicine* (March 2020) — U.S. hospitals reported shortages of ventilators needed to care for critically ill COVID-19 patients, with national estimates of only 60,000–160,000 devices available ([NEJM, Ranney et al. 2020](https://www.nejm.org/doi/full/10.1056/NEJMp2006141))
- **News reference 2:** CDC study of 625 hospitals across 29 states found that 63% reported at least one overcrowding alert, and 12% reported ventilator shortages during 2020–2021 ([Sandhu et al., *Public Health Reports* 2022](https://pmc.ncbi.nlm.nih.gov/articles/PMC9257510/))

---

## Slide 3 — How Allocation Works Across the U.S.

- No national standard — only **26 out of 50 states** had publicly available ventilator allocation guidelines, and they varied significantly ([Piscitello et al., *JAMA Network Open* 2020](https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2767383))
- Of those 26 states, **58% used SOFA scores**, **23% included comorbidity assessments**, and tiebreakers ranged from lotteries to age-based rules
- The same patient could receive a ventilator in one state but be denied in an adjacent state
- Examples — three major states, three very different rules:
  - **New York:** SOFA score only — prioritizes by organ failure severity, with lottery as tiebreaker. Does not consider age or comorbidities. (Developed in 2015, became the blueprint for several other states)
  - **Pennsylvania:** Multiprinciple — combines SOFA score with comorbidity burden, then uses age group as tiebreaker. Younger patients get priority when scores tie
  - **Michigan:** Prioritizes healthcare workers first — gives frontline medical staff explicit preference for ventilator access, then applies clinical criteria (Crafted in 2012, pre-pandemic)

---

## Slide 4 — The Key Question: Are These Protocols Optimal and Fair?

- With so much variation, a natural question arises: **Are any of these protocols actually saving the most lives? And are they fair?**
- **No — they are not optimal.** All existing protocols assign a static priority score at admission. They never adapt to the severity of scarcity or consider who else is competing for the same ventilator at the same time.
- **No — they are not fair.** Empirical evidence shows that Black patients were significantly less likely to receive ventilators under SOFA-based protocols, partly because SOFA scores may inadvertently assign higher severity to Black patients ([Ashana et al., 2021](https://doi.org/10.1164/rccm.202012-4383OC); [Bhavani et al., 2021](https://doi.org/10.1164/rccm.202106-1453LE)).
- Can we derive a new protocol that **saves more lives, and is more equitable?**

---

## Slide 5 — Method (Placeholder)

*[To be developed — Reinforcement Learning formulation, Transformer-based Q-network, fairness reward]*

---

## Slide 6 — Method (Placeholder)

*[To be developed — Simulator, training pipeline, real-world clinical data]*

---

## Slide 7 — Results: Saving More Lives

- At ~50% ventilator scarcity, our AI protocol (TxDDQN-fair) achieves **85.4% survival** compared to:
  - Multiprinciple (MD/PA): 82.0%
  - SOFA (NY): 80.9%
  - Youngest First: 77.2%
  - Lottery: 75.2%
- **Yes — AI saves more lives, at every level of scarcity**

---

## Slide 8 — Results: Achieving Fairness

- Our AI protocol achieves near-equal allocation rates across all racial groups (~80–83%), comparable to a coin flip (lottery)
- Existing protocols show clear biases:
  - **SOFA** favors White patients (79.1%) over Black patients (73.6%)
  - **Youngest First** favors Hispanic patients (84.4%) over White patients (72.9%)
  - **Multiprinciple** favors Hispanic patients (82.0%) over Black patients (74.3%)
- Our AI protocol is **as fair as a lottery, but saves 10% more lives**

---

## Slide 9 — Takeaways
- The framework generalizes beyond ventilators to any scarce healthcare resource
- AI can be a powerful tool for health policy making — not replacing clinicians, but informing better decisions

---

## Slide 10 — Acknowledgments & References

- Co-authors: Yikuan Li, Chengsheng Mao, Kaixuan Huang, Hanyin Wang, Zheng Yu, Mengdi Wang, Yuan Luo
- Institutions: George Mason Unviersity & Northwestern University & Princeton University
- Contact information
