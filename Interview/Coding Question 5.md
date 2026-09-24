
* Closures
* Scopes
* Callbacks
* Promises & async/await
* Higher-order functions
* Prototypes / classes
* Objects & arrays
* Recursion
* Event loop & microtasks
* Error handling
* Functional programming
* This binding


---

# ⚡ Problem Statement: **Build a Mini In-Memory Task Runner Engine**

Implement a **TaskRunner** class that runs tasks in order and supports multiple task types:

Each task is an object:

```ts
{
  type: "sync" | "async" | "delay" | "nested",
  run: Function, 
  delay?: number,            // only for type="delay"
  tasks?: Task[]             // only for type="nested"
}
```

---

# **Your Task**

Implement a class:

```ts
class TaskRunner {
  constructor(tasks: Task[]);
  run(): Promise<void>;
}
```

The runner must support:

---

## ✅ **1. Sync Tasks**

Run immediately:

```js
{ type: "sync", run: () => console.log("A") }
```

---

## ✅ **2. Async Tasks (returning Promises)**

Wait for the promise:

```js
{ type: "async", run: () => fetchData() }
```

---

## ✅ **3. Delay Tasks**

Wait for `delay` ms:

```js
{ type: "delay", delay: 300, run: () => console.log("Waiting...") }
```

---

## ✅ **4. Nested Tasks**

A task that contains other tasks:

```js
{ type: "nested", tasks: [ ...subTasks ] }
```

These must run recursively using the **same TaskRunner logic** (closure + recursion expected).

---

# **Input Example**

```js
const tasks = [
  { type: "sync", run: () => console.log("1. Sync A") },

  { type: "async", run: () => Promise.resolve(console.log("2. Async B")) },

  { type: "delay", delay: 200, run: () => console.log("3. Delay C") },

  { 
    type: "nested", 
    tasks: [
      { type: "sync", run: () => console.log("4.1 Nested Sync") },
      { type: "delay", delay: 100, run: () => console.log("4.2 Nested Delay") },
    ]
  },

  { type: "sync", run: () => console.log("5. Sync D") }
];
```

---

# **Expected Output Order**

```
1. Sync A
2. Async B
3. Delay C
4.1 Nested Sync
4.2 Nested Delay
4. Sync D
```

---

# **Constraints**

* `1 ≤ tasks.length ≤ 10^5`
* Must NOT block the event loop incorrectly
* Must use **async/await**, closures, recursion, prototypes/classes
* Must handle invalid task types (throw error)
* Runner must preserve order
* Code must be efficient

---

# 🧠 **What this tests**

This merges **every major JS concept**:

| Concept                | Tested? | How                             |
| ---------------------- | ------- | ------------------------------- |
| Closures               | ✔       | Recursive nested runner         |
| Promises               | ✔       | async tasks                     |
| async/await            | ✔       | sequencing                      |
| Scoping                | ✔       | inner functions capturing state |
| Prototypes / Classes   | ✔       | TaskRunner class                |
| Event Loop             | ✔       | setTimeout delays               |
| Callbacks              | ✔       | run() may be sync or async      |
| Higher-order functions | ✔       | tasks containing functions      |
| Objects/Arrays         | ✔       | tasks structure                 |
| Recursion              | ✔       | nested type                     |
| Error handling         | ✔       | unknown types                   |

Perfect for SDE2–SDE3.

---

# ⭐ **Solution (Interview-Ready, Clean, Uses All JS Concepts)**

```js
class TaskRunner {
  constructor(tasks) {
    this.tasks = tasks;
  }

  async run() {
    await this.#executeTasks(this.tasks);
  }

  // private method using closure + recursion
  async #executeTasks(tasks) {
    for (const task of tasks) {
      switch (task.type) {

        case "sync":
          task.run();
          break;

        case "async":
          await task.run();
          break;

        case "delay":
          await new Promise((res) => setTimeout(res, task.delay));
          task.run();
          break;

        case "nested":
          if (!Array.isArray(task.tasks)) 
            throw new Error("nested task requires a tasks array");

          // recursive call (closure + async)
          await this.#executeTasks(task.tasks);
          break;

        default:
          throw new Error(`Unknown task type: ${task.type}`);
      }
    }
  }
}
```

---

# 🧪 Test

```js
const runner = new TaskRunner(tasks);
runner.run();
```

---

# 🔥 Follow-Up Questions (SDE3)

### 1️⃣ Add support for concurrency:

Run up to `k` tasks at a time.

### 2️⃣ Add cancellation using `AbortController`.

### 3️⃣ Add event hooks:

`beforeTask`, `afterTask`, `error`.

### 4️⃣ Add retry logic for async tasks.

### 5️⃣ Persist state and resume after failure.

---

If you want, I can generate:
✔ Another algorithmic JS question
✔ Another real-world backend JS question
✔ A deeply conceptual JS question (event loop, hoisting, closures, prototypes, async)
✔ A DP/graph problem framed in JS context
