
---

# Problem Statement: **Event Duration Normalization — Merge Overlapping Sessions**

A system receives **time-logged events** from multiple services.
Each event has a **start time** and an **end time**, but events can overlap.

You are asked to calculate the **total active duration** from these events **without double-counting overlapping periods**.


---

# **Input**

* An integer `n` — number of events
* A list of `n` **intervals**, where each interval is `[startTime, endTime]`

### Example:

```txt
n = 5
events = [
  [1, 4],
  [2, 5],
  [7, 9],
  [8, 10],
  [12, 15]
]
```

---

# **Output**

Return the **total active duration** (integer)
after merging all overlapping intervals.

### For the example above:

Merged intervals:

* [1, 5] → duration = 4
* [7, 10] → duration = 3
* [12, 15] → duration = 3

**Total = 4 + 3 + 3 = 10**

---

# **Expected Output**

```txt
10
```

---

# **Constraints**

* `1 ≤ n ≤ 10^5`
* `0 ≤ start < end ≤ 10^9`
* Large input sizes → time complexity must be **O(n log n)**
* Should handle highly overlapping intervals
* Return integer only — no printing required

---

# 🧠 What the interviewer is evaluating

* Ability to work with interval merging
* Sorting logic
* Edge cases handling
* Efficient time complexity
* Data structures
* Real-world mapping to backend scenarios

---

# ✅ **Solution (Clean, Interview-Ready)**

### **Approach**

1. Sort intervals by start time
2. Merge overlapping intervals
3. Sum the merged durations

---

## **Code (JavaScript / Node.js)**

```js
function totalActiveDuration(events) {
  if (events.length === 0) return 0;

  // 1. Sort events by start time
  events.sort((a, b) => a[0] - b[0]);

  let mergedStart = events[0][0];
  let mergedEnd   = events[0][1];
  let total = 0;

  for (let i = 1; i < events.length; i++) {
    const [s, e] = events[i];

    if (s <= mergedEnd) {
      // Overlapping → merge
      mergedEnd = Math.max(mergedEnd, e);
    } else {
      // No overlap → accumulate previous and reset
      total += mergedEnd - mergedStart;
      mergedStart = s;
      mergedEnd = e;
    }
  }

  // Add last interval
  total += mergedEnd - mergedStart;

  return total;
}
```

---

# 🧪 Example Test

```js
console.log(totalActiveDuration([
  [1,4],
  [2,5],
  [7,9],
  [8,10],
  [12,15]
])); 
// Output: 10
```

---

# 🔥 **Follow-up Questions (SDE2 → SDE3 Level)**

### 1. If intervals arrive as a stream (one by one),

how do you maintain the merged duration online?

### 2. Modify the solution to return **actual merged intervals** instead of only duration.

### 3. What if start and end times may be out-of-order (end < start)?

(Add input validation.)

### 4. How to handle **millions of intervals** that cannot fit in memory?

(Think external sorting, chunk processing.)

---

