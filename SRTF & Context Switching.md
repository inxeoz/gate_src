
---

## 1) Key Terms (super short)

* **CPU burst time**: how long a process needs the CPU (if run without interruption).
* **Preemptive scheduling**: the OS **can stop** a running process and give the CPU to another one.
* **Non-preemptive scheduling**: once a process gets the CPU, it **keeps it** until it finishes or blocks (e.g., I/O).
* **SJF (Shortest Job First)**: pick the job with the **smallest total burst**. (Usually **non-preemptive**.)
* **SRTF (Shortest Remaining Time First)**: **preemptive** version of SJF — at **every arrival** or event, run the job with the **smallest remaining time** (can kick out the current one).
* **Context switch**: the CPU **changes from one process to another** (save/restore registers, etc.). We count **only switches between processes** (ignore “idle→first process” at time 0 and “last process→idle” at the end if the problem says so).

---

## 2) Memory Hook (real-world analogy)

**Chef in a restaurant (SRTF = “serve the dish that will finish soonest”)**

* The chef starts a **big curry (15 min)** at time 0.
* Later an order for **pasta (12 min)** comes at time **t**.
* At time 8, an order for **fries (5 min)** arrives.

With SRTF, the chef **re-evaluates whenever a new order arrives**:

> *“Which dish can be finished the soonest from **now**?”*
> If a new, quicker dish appears, the chef **puts the current pan aside** (preemption) and cooks the faster one first — more customers get served earlier.

This is exactly how SRTF works.

---

## 3) The Question (restated)

Three CPU-bound tasks:

* **T1**: burst **15**, arrival **0**
* **T2**: burst **12**, arrival **t**
* **T3**: burst **5**,  arrival **8**

Scheduling: **SRTF (preemptive)**.
We need the value(s) of **t** that give **exactly 4 context switches**.

> “Ignore context switches at **time 0** and **at the end**.”

**Exam convention we’ll use:**

* On a **tie**, the **newly arrived** process preempts (common in such questions).
* We’ll treat **t > 0** (the separate option “t = 0” is handled below in “edge notes”).

---

## 4) Solve it once with symbols, then lock it in with a concrete example

### Step A — What happens up to time *t*?

* From **0 to t**, only **T1** is present → CPU runs **T1**.
* At time **t**, **T2** arrives (12).

  * **T1 remaining** at time *t* = `15 − t`
  * **T2 remaining** = `12`

For **T2** to **preempt** T1 at arrival (i.e., cause a switch #1), we need:

* `12 < (15 − t)`  ⇒  `t < 3`, **or**
* `12 = (15 − t)`  ⇒  `t = 3` and (by our tie rule) **preempt**.

> ✅ So we need **0 < t ≤ 3** for the **first** switch (T1 → T2).
> (We’ll discuss **t = 0** in the edge notes.)

### Step B — From *t* to time 8 (T3 arrives)

* CPU is running **T2** during `(t, 8)`.
* At time **8**, **T3 (5)** arrives. Remaining times right then:

  * **T2 remaining** = `12 − (8 − t)` = `t + 4`
  * **T1 remaining** = `15 − t`
  * **T3** = `5`

Since **5** is the smallest, **T3** preempts.

> ✅ **Switch #2:** **T2 → T3** at time **8**.

### Step C — T3 runs to completion

* **T3** needs **5** units → runs from **8 to 13**.

At time **13**, remaining:

* **T1**: `15 − t`
* **T2**: `t + 4`

For **0 < t ≤ 3**, we have:

* `t + 4 ≤ 7` and `15 − t ≥ 12` ⇒ **T2** is shorter.

> ✅ **Switch #3:** **T3 → T2** at time **13**.

### Step D — Finish T2, then T1

* **T2** completes after `(t + 4)` more units (from 13 to `13 + t + 4`).
* Then only **T1** remains.

> ✅ **Switch #4:** **T2 → T1** (right when T2 finishes).

**Total switches (excluding time 0 and final end):** 4

**Therefore:** to get **exactly 4** switches we need
👉 **$0 < t ≤ 3$**.

> The option set in your screenshot marks **“t ≤ 3”** as correct — that matches the usual exam intent (they treat “t = 0” separately as another option). See “Edge notes” next.

---

## 5) Lock it in with a concrete, friendly example (pick $t = 2$)

* **0–2**: run **T1** (remaining becomes 13)
  **Switch #1 at t=2:** **T1 → T2** (12 < 13)
* **2–8**: run **T2** (used 6 units, remaining `t+4 = 6`)
* **8**: **T3** arrives with 5 < min(6, 13)
  **Switch #2 at 8:** **T2 → T3**
* **8–13**: run **T3** to completion
* **13**: compare remaining → **T2 = 6**, **T1 = 13**
  **Switch #3 at 13:** **T3 → T2**
* **13–19**: finish **T2**
* **19**: only **T1** left
  **Switch #4 at 19:** **T2 → T1**
* **19–32**: finish **T1** (end switch ignored)

### ASCII Gantt (t = 2)

```
time →   0      2           8     13          19                 32
         |------|-----------|-----|-----------|-------------------|
         T1     T2          T3    T2          T1
Switches:     (1)        (2)   (3)        (4)
```

---

## 6) Why **t > 3** doesn’t work (quick sanity check)

Take **t = 5** (so T2 arrives at 5):

* At 5, T1 has run 5 units → **T1 remaining = 10**, **T2 = 12** ⇒ no preemption.
* At 8, T3 (5) arrives ⇒ preempts **T1**. **Switch #1 at 8: T1 → T3**
* At 13, compare (**T1 = 7**, **T2 = 12**) ⇒ pick **T1**. **Switch #2 at 13: T3 → T1**
* At 20, **T1** finishes ⇒ go to **T2**. **Switch #3 at 20: T1 → T2**
* Done. Only **3 switches** (not 4).

---

## 7) Edge notes (so you never get tricked)

* **Tie at t = 3**: we assumed **preempt on tie** (new arrival wins), which is common in exam solutions. If your rule was “no preemption on tie,” then **t = 3** would **not** give 4 switches. (Exams usually expect the tie-preempt assumption for SRTF.)
* **t = 0** (arrive together): CPU would start **T2** (12) immediately (since 12 < 15). At time 8, **T2 remaining = 4**, **T3 = 5** ⇒ T2 keeps running (no switch). You end up with **only 2** counted switches.
  That’s why, practically, the range that really yields 4 is **$0 < t ≤ 3$**. In the given options, they separate **“t = 0”** as its own answer and accept **“t ≤ 3”** for the intended range.

---

## 8) Mini-cheatsheet (exam-ready)

* **SJF vs SRTF**

  * SJF: choose smallest **total** burst; usually **non-preemptive**.
  * SRTF: choose smallest **remaining** time; **preemptive** (re-decide at every arrival).

* **When do switches happen in SRTF?**

  * On a new arrival, if its **remaining time** is **less** (or **equal**, under tie-preempt rule) than the current job’s **remaining time** → **switch**.

* **Counting context switches**

  * Count only **process→process** switches.
  * Ignore **idle→first** (time 0) and **last→idle** (the end), if the problem tells you to.

* **This problem’s answer**

  * For **exactly 4** switches: **$0 < t ≤ 3$** (exam’s chosen option: **t ≤ 3**).
  * Use the **chef analogy** to remember: new faster dish arrives → chef swaps pans.

---

