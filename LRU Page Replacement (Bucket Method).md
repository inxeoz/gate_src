
---

# 📘 LRU Page Replacement (Bucket Method)

---

## 🔹 Question

**What are the minimum number of frames required to get a single page fault for the following sequence, assuming LRU replacement strategy?**

Reference string:
`1 2 3 4 2 1 5 6 2 1 2 3 7 6 3 2 1 2 3 6`

---

## 🔹 Step-by-step Filling the Buckets (Frames = 6)

We start with **6 empty buckets**.

1. **1 comes** → bucket empty → put 1. (**Fault**)
   Buckets = {1, -, -, -, -, -}

2. **2 comes** → put 2. (**Fault**)
   Buckets = {1,2,-,-,-,-}

3. **3 comes** → put 3. (**Fault**)
   Buckets = {1,2,3,-,-,-}

4. **4 comes** → put 4. (**Fault**)
   Buckets = {1,2,3,4,-,-}

5. **2 comes** → already there → (**Hit**)

6. **1 comes** → already there → (**Hit**)

7. **5 comes** → new → put 5. (**Fault**)
   Buckets = {1,2,3,4,5,-}

8. **6 comes** → new → put 6. (**Fault**)
   Buckets = {1,2,3,4,5,6}

---

👉 Now all 6 buckets are **full**. From now on, if a new page comes, LRU replacement will be used.

---

9. **2 comes** → hit
10. **1 comes** → hit
11. **2 comes** → hit
12. **3 comes** → hit

👉 Recently used = {2,1,2,3}
👉 Page **4** hasn’t been touched → it is **LRU**.

---

13. **7 comes** → not in memory → (**Fault**)

* Evict **4** (LRU)
* Insert **7**
  Buckets = {1,2,3,5,6,7}

---

14–20: All remaining pages are **hits** (no further faults).

---

## 🔹 Final Observation

* Total **compulsory faults** = 6 (to fill all frames first time)
* **One replacement fault** = when page 7 replaced page 4
* After that, no new faults (since page 4 never appears again)

✅ So, with **6 frames**, we get **exactly one page fault due to replacement**.

---

## 🔹 Answer

**The minimum number of frames required = 6** ✅

---

## 🔹 Easy Recall Trick

* Count distinct pages = **7**
* Frames = 7 → no replacement faults
* Frames = 6 (i.e., D−1) → usually gives exactly **1 replacement fault** (if the evicted page never comes back)
* Here, page 4 was removed and never returned → so only one replacement happened.

