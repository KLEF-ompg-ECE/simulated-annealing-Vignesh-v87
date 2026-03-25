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

```text
`count_clashes()` measures the total number of times a student has two exams scheduled in the same time slot across all students. A value of 0 means a perfect timetable with zero clashes.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```text
`generate_neighbor()` creates a neighboring timetable by randomly selecting one exam and moving it to a different, randomly chosen time slot. The new timetable is identical to the current one except for this single exam's new slot assignment.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```text
This line decides whether to accept the newly generated timetable. It always accepts a better solution (where `delta < 0`), but also accepts a worse solution with a probability based on the current temperature to avoid getting trapped in local optima.
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
```text
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
```text
The biggest drop in clashes happens very early in the iterations while the temperature is still high. After the initial rapid drop, the curve flattens out and only makes minor, occasional improvements until the temperature gets too low.
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
```text
Fast cooling (0.80) drops the temperature so rapidly that the algorithm only completes 31 iterations and gets stuck in a poor local minimum with 8 clashes. Slower cooling rates (0.95 and 0.995) give the algorithm more time to explore the search space, allowing it to escape local optima and reach a much better final state of 3 clashes. However, the slowest cooling rate (0.995) takes significantly more iterations.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```text
Both 0.95 and 0.995 achieved the best result of 3 clashes, but 0.95 is more efficient because it required far fewer iterations (135 vs 1379) to reach the same quality of solution. The 0.80 rate decayed too fast to search effectively.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | Slower cooling rates allow the algorithm to efficiently minimize clashes but require more iterations. |
| 2 — Cooling rate | cooling_rate = 0.95 | 3 | A moderately slow cooling rate offers the best balance between fast execution and good solution quality. |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```text
The most important thing I learned is that the cooling schedule heavily dictates the performance of the Simulated Annealing algorithm. If the temperature drops too quickly, the algorithm will prematurely converge on a poor solution because it stops exploring. However, finding the right "sweet spot" (like 0.95) can dramatically reduce computational time while maintaining solution quality compared to excessively slow options.
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, timetable pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
