	

---

###  **Question: Implement a Promise Pool (Concurrency Limiter)**

You need to implement a function `promisePool(functions, n)` that executes **up to `n` promises in parallel**, and starts the next one as soon as any promise settles.  
Once all are complete, it should resolve.

Each function in `functions` returns a Promise.

---

###  **Example Usage:**

```js
const timeout = (t) => new Promise(res => setTimeout(res, t));

const functions = [
  () => timeout(300).then(() => console.log('Task 1 done')),
  () => timeout(200).then(() => console.log('Task 2 done')),
  () => timeout(500).then(() => console.log('Task 3 done')),
  () => timeout(100).then(() => console.log('Task 4 done')),
];

await promisePool(functions, 2);
console.log('All done!');
```

#### Expected Output (timing-based, order may vary slightly):

```
Task 2 done
Task 1 done
Task 4 done
Task 3 done
All done!
```

---

### **Requirements:**

- At most `n` promises should be running at any given time.
    
- Start the next promise immediately when one finishes.
    
- Must resolve once all promises finish.
    
- Must handle synchronous functions gracefully.
    
- Must preserve efficiency even for large input arrays.
    

---

### 💡 **Follow-up Questions:**

1. How would you modify it to handle **retry logic** per task?
    
2. What’s the **difference** between this and the earlier `Scheduler` class problem?
    
3. How can you ensure fairness (FIFO) if tasks are being added dynamically?
    
4. How would you make this **cancelable** mid-way?
    

---

### 🧠 **Expected Answer:**

```js
async function promisePool(functions, n) {
  let i = 0;

  async function worker() {
    while (i < functions.length) {
      const fn = functions[i++];
      await fn();
    }
  }

  const workers = Array(Math.min(n, functions.length))
    .fill(null)
    .map(() => worker());

  await Promise.all(workers);
}
```

---

### ⚙️ **Explanation:**

- Maintains a shared index `i` for the next task to execute.
    
- Spawns `n` async “workers”; each worker executes one function at a time until none remain.
    
- `Promise.all` ensures all workers finish before resolving.
    
- No external libraries, no mutation of the functions array.
    
- Handles hundreds of tasks efficiently.
    
- **Time complexity:** O(n + m) where m = number of tasks.
    
- **Space complexity:** O(n).
    

---

### 🔍 **Extension Challenge (for extra credit):**

Enhance it to support:

```js
promisePool(functions, n, { retry: 2, delay: 100 });
```

→ Each task should retry up to 2 times on failure, waiting 100ms between retries.

---

Would you like the **next one** to push toward:

- 🧩 **“System design in JS”** (e.g., async job queue with retry and priority), or
    
- ⚙️ **“Algorithmic design in JS”** (e.g., memoization, deep clone with circular refs, or diff patch engine)?