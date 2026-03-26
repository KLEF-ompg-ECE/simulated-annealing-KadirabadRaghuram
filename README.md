# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Raghuram Kadirabadar  
**Student ID    :** SA-2026-001  
**Date Submitted:** March 26, 2026  

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
count_clashes() counts the total number of clashes across all students, where a clash occurs when a single student has two exams scheduled in the same time slot. A value of 0 means a perfect timetable with no scheduling conflicts.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
generate_neighbor() creates a neighboring timetable by randomly selecting one exam and reassigning it to a different time slot. Only one exam's slot assignment changes, while all other exams remain in their current slots.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept the new neighbor solution. It always accepts improvements (delta < 0), but also accepts worse solutions with probability exp(-delta/T). SA accepts worse solutions occasionally to escape local optima and explore the solution space more thoroughly; this probability decreases as temperature drops.
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
The curve shows a steep initial drop in clashes from 12 down to around 3-5 within the first 200-300 iterations. After this initial improvement, the curve flattens out and remains relatively stable around 3 clashes for the remaining iterations, indicating that SA found a local optimum and is unable to improve further.
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
Fast cooling (0.80) causes the temperature to drop very quickly, allowing only 31 iterations before the algorithm terminates. This leaves insufficient time for exploration, resulting in a poor solution with 8 clashes. Moderate cooling (0.95) provides a better balance, achieving 3 clashes in 135 iterations. Slow cooling (0.995) maintains high temperature for longer, enabling thorough exploration across 1379 iterations, and achieves the same final result (3 clashes) as the moderate rate but is less efficient in computation.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
Both cooling_rate=0.95 and cooling_rate=0.995 gave equally good results (3 clashes). The 0.95 rate is more efficient, achieving the same quality in 135 iterations versus 1379 for 0.995. A moderate cooling rate provides the optimal balance: it's slow enough to allow sufficient exploration and avoid premature convergence, but fast enough to focus the search as better solutions are discovered. The 0.80 rate is too aggressive and traps the algorithm in poor local optima early on.
```


---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | Slow cooling allows thorough exploration and finds good local optima, but cannot guarantee perfect solutions within the iteration limit. |
| 2 — Cooling rate | cooling_rate = 0.95 | 3 | Moderate cooling rates balance exploration and convergence efficiency better than both very fast and very slow rates. |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
The most important learning is that cooling rate is critical to SA's performance and requires careful tuning. Fast cooling (0.80) causes premature convergence to poor solutions because the algorithm freezes too quickly before finding better regions. Slow cooling (0.995) ensures thorough exploration but wastes computational resources on redundant iterations. Moderate cooling (0.95) demonstrates the optimal balance: it maintains enough randomness early on to escape local traps, gradually focuses the search toward good solutions, and terminates efficiently. This illustrates the fundamental tradeoff in metaheuristics between exploration (trying diverse solutions) and exploitation (refining promising ones).
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, timetable pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
