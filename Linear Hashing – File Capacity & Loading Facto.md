
---

# 📘 Notes on Linear Hashing – File Capacity & Loading Factor

---

## 🔹 Key Definitions

### 1. **Blocking Factor (bfr)**

* Maximum number of records that can fit into **one block/bucket**.
* Example: If each block stores 4 records → `bfr = 4`.

---

### 2. **Number of Buckets (N)**

* Total number of **buckets (blocks)** in the file.

---

### 3. **Loading Factor (i)**

* Represents how much of the file capacity is currently used.
* **Range:** $0 \leq i \leq 1$

  * $i = 0$: file is empty.
  * $i = 1$: file is completely full.
  * $0 < i < 1$: file is partially filled.

---

## 🔹 Formula

$$
i = \frac{r}{bfr \times N}
$$

Where:

* $r$ = actual number of records in the file
* $bfr \times N$ = maximum number of records that can be stored

👉 Rearranging:

$$
r = i \times bfr \times N
$$

---

## 🔹 Example

Suppose:

* $bfr = 4$ (each bucket stores 4 records)
* $N = 10$ (10 buckets)
* $i = 0.75$ (75% filled)

👉 Maximum capacity = $bfr \times N = 4 \times 10 = 40$
👉 Actual records = $r = 0.75 \times 40 = 30$

✅ So, the file currently has **30 records**.

---

## 🔹 Why Not Keep $i = 1$ Always?

* In practice, $i$ is kept **less than 1** (e.g., 0.7–0.8).
* Reason: If a bucket is completely full, **new insertions cause overflow**.
* Keeping some free space ensures **efficient insertions** and reduces overflow chains.

---

## 🔹 Easy Way to Remember

Think of it like a **water bottle**:

* `bfr × N` = **bottle capacity**
* `r` = **amount of water actually filled**
* `i` = **how full the bottle is (0 to 1 scale)**

Formula is just:

$$
\text{fullness (i)} = \frac{\text{filled amount (r)}}{\text{capacity (bfr × N)}}
$$

Or equivalently:

$$
\text{filled amount (r)} = \text{fullness (i)} \times \text{capacity}
$$

---

✅ **Key Takeaway:**

* $i$ = percentage of file occupancy.
* $r = i \times bfr \times N$.
* Keep $i < 1$ to avoid overflow problems.

---
