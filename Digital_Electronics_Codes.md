
---

# 📝 Codes in Digital Electronics

---

## 🔹 1. BCD (Binary Coded Decimal)

**Definition:**

* Each decimal digit (0–9) is represented in **4-bit binary**.
* Called **8421 BCD** because the weights of the 4 bits are **8, 4, 2, 1**.

**Why used?**

* Easy conversion between decimal and binary.
* Used in **calculators, digital clocks, digital displays**.

**Example:**

* Decimal 59 → 5 = `0101`, 9 = `1001` → BCD = `0101 1001`.

---

## 🔹 2. Gray Code

**Definition:**

* A **binary code** in which **two consecutive numbers differ by only 1 bit**.

**Why used?**

* Reduces **errors in digital circuits** (important in **position encoders, Karnaugh Maps**).

**Example (3-bit):**

| Decimal | Binary | Gray Code |
| ------- | ------ | --------- |
| 0       | 000    | 000       |
| 1       | 001    | 001       |
| 2       | 010    | 011       |
| 3       | 011    | 010       |
| 4       | 100    | 110       |
| 5       | 101    | 111       |
| 6       | 110    | 101       |
| 7       | 111    | 100       |

---

## 🔹 3. 8421 Code (Weighted BCD)

**Definition:**

* A **weighted code** with bit weights **8, 4, 2, 1**.
* This is the **standard BCD representation**.

**Why used?**

* Directly represents decimal digits in binary.

**Example:**

* Decimal 7 → `0111` (4+2+1 = 7).
* Decimal 9 → `1001`.

---

## 🔹 4. Excess-3 Code

**Definition:**

* A **non-weighted code** obtained by adding **3 (0011)** to each decimal digit in BCD.

**Why used?**

* Provides **self-complementing property** (useful in error detection and subtraction).

**Example:**

| Decimal | BCD (8421) | Add 3 | Excess-3 |
| ------- | ---------- | ----- | -------- |
| 0       | 0000       | +0011 | 0011     |
| 1       | 0001       | +0011 | 0100     |
| 2       | 0010       | +0011 | 0101     |
| 9       | 1001       | +0011 | 1100     |

---

# ✅ Quick Recap

* **BCD (8421)** → Decimal digits in 4-bit binary.
* **Gray Code** → Only 1 bit changes between consecutive numbers (minimizes error).
* **8421 Code** → Standard weighted code (8,4,2,1).
* **Excess-3** → BCD + 3, self-complementing.

---
