# 🏒 NHL Expected Goals (xG) Model

**Predicting the probability that an NHL shot becomes a goal, using shot location, angle, and game context.**

Not every shot is equal. A one-timer from the slot is far more dangerous than a wrist shot from the blue line. An **expected goals (xG)** model puts a number on that: for each shot, it estimates the probability (0–1) that it becomes a goal. Teams and analysts use xG to judge whether a player or team is creating real chances or just getting lucky.

This project builds an xG model from scratch with **logistic regression**, starting simple and adding features one at a time to measure what actually matters.

> 🚧 **Status:** In progress, currently on Phase 1 (data exploration). See the [roadmap](#-roadmap).

---

## ❓ Questions this project answers
1. How much does **shot distance** alone explain whether a shot scores?
2. How much do **angle, shot type, rebounds, and rush chances** add on top of distance?
3. How close can a simple, explainable model get to a public xG model like MoneyPuck's?

## 📊 Data
- **Source:** [MoneyPuck.com](https://moneypuck.com/data.htm) shot-level data (free for non-commercial use, with credit to MoneyPuck)
- **Scope:** One recent NHL regular season to start (~100k+ shots)
- **Target:** `goal` (1 = goal, 0 = no goal)
- Raw data isn't committed to this repo because the files are large. See [`data/README.md`](data/README.md) to download it.

## 🛠️ Approach
| Step | What I do |
|---|---|
| **Clean** | Remove empty-net shots and missing coordinates |
| **Engineer** | Compute shot **distance** and **angle** to the net from (x, y) coordinates myself, then check them against MoneyPuck's values |
| **Baseline** | Logistic regression using **distance only** |
| **Improve** | Add angle → shot type → rebound → rush, measuring the gain from each |
| **Evaluate** | Log loss, ROC AUC, and a **calibration plot** (when the model says 20%, do ~20% of those shots actually score?) |

**Tools:** Python · pandas · scikit-learn · matplotlib

## 📈 Results
*Coming soon. This section will show model performance, the most important features, and a shot-danger map of the rink.*

| Model | Features | Log loss | ROC AUC |
|---|---|---|---|
| Baseline | distance | – | – |
| v2 | + angle | – | – |
| v3 | + shot type, rebound, rush | – | – |

## 🗺️ Roadmap
- [x] Set up repo and README
- [ ] **Phase 1: Explore.** Load one season, check goal rate, plot shot locations
- [ ] **Phase 2: Features.** Compute distance and angle, plot goal rate vs. distance
- [ ] **Phase 3: Baseline.** Train distance-only logistic regression and evaluate
- [ ] **Phase 4: Improve.** Add features one at a time, compare, check calibration
- [ ] **Phase 5: Visualize.** Shot-danger heatmap on a rink diagram
- [ ] **Stretch:** Compare my xG to MoneyPuck's xG, and rank players by goals scored above expected

## 🚀 How to run
```bash
git clone https://github.com/matt-dalk/nhl-expected-goals.git
cd nhl-expected-goals
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```
Then download the data (see `data/README.md`) and open `notebooks/01_explore.ipynb`.

## 💡 What I'm learning
*Updated as I go: what surprised me, what didn't work, and why.*

---
*Built by [Matt Dalkiewicz](https://github.com/matt-dalk), AI Engineering @ Penn State and club hockey player. Data courtesy of [MoneyPuck.com](https://moneypuck.com).*
