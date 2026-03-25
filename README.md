# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Y Vignesh
**Student ID    :** 2310040087
**Date Submitted:** 2026-03-25

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
count_clashes() measures the number of clashes in the timetable, where a clash occurs when a student has two exams scheduled in the same time slot. A value of 0 means a perfect timetable.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
generate_neighbor() creates a new timetable by randomly selecting one exam and assigning it to a different time slot. The new timetable differs from the current one by only one exam’s slot.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept the new solution. If the new solution is better (delta < 0), it is always accepted. If it is worse, it may still be accepted with a probability based on temperature, which helps the algorithm escape local optima.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379 |
| Clashes at iteration 1 | 12 |
| Final best clashes | 3 |
| Did SA reach 0 clashes? (Yes / No) | No |

**Copy the printed timetable output here:**
```
  Final Timetable
------------------------------------------
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
------------------------------------------
  Total clashes : 3
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The biggest drop in clashes happens in the early iterations when the temperature is high. As the temperature decreases, the curve gradually flattens and improvements become less frequent.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        | 8             | 31                   | No                 |
| 0.95        | 3             | 135                  | No                 |
| 0.995       | 3             | 1379                 | No                 |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
With fast cooling (0.80), the temperature drops quickly and the algorithm converges early to a poor solution. With slower cooling (0.95 and 0.995), the algorithm explores more and finds better solutions with fewer clashes, although it takes more iterations.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
The cooling rate 0.95 gives the best result because it balances exploration and convergence, achieving a low number of clashes in fewer iterations compared to 0.995.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | Slower cooling rates allow the algorithm to efficiently minimize clashes but require more iterations. |
| 2 — Cooling rate | cooling_rate = 0.95 | 3 | A moderately slow cooling rate offers the best balance between fast execution and good solution quality. |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
The most important thing I learned is that the cooling rate controls the balance between exploration and convergence in simulated annealing. If cooling is too fast, the algorithm may get stuck in a local optimum. If it is too slow, it takes more time but finds better solutions.
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, timetable pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
