# Deep Dive Questions on Promises & Async/Await

A collection of advanced interview questions with detailed explanations and follow-ups.

---

## **1. Explain the internal states of a Promise. How does state transition work?**

**Answer:**
A Promise has **three states**:

* **Pending** – initial state
* **Fulfilled** – operation completed successfully
* **Rejected** – operation failed

Transition rules:

* A promise can only transition **once**.
* Pending → Fulfilled **or** Pending → Rejected
* After settling, the state is immutable.

**Follow-up Questions:**

1. What happens if you call `resolve()` and `reject()` inside the same executor?
2. What if a promise is resolved with another promise?

---

## **2. What is the Promise Resolution Procedure?**

**Answer:**
This is the algorithm defining how a promise resolves the value returned by `.then()` callbacks. If a callback returns:

* A primitive → wraps into a fulfilled promise.
* A promise → adopts its state.
* A thenable → attempts to call its `then()` method.

**Follow-up:**

* Why does returning `this` inside `.then()` create a TypeError? (Circular resolution)

---

## **3. Compare microtasks and macrotasks in context of promises.**

**Answer:**
Callbacks in `.then()` run in the **microtask queue**, which executes **before** macrotasks like `setTimeout`. This ensures deterministic promise behavior.

**Follow-up:**

* Where do async/await callbacks run?

---

## **4. What happens if you `await` a non-promise value?**

**Answer:**
The value is wrapped into `Promise.resolve(value)` and awaited.

**Follow-up:**

* How is this useful when designing APIs?

---

## **5. Explain error propagation in promises and async/await.**

**Answer:**
Errors behave like exceptions:

* In promises: rejected state → goes to `.catch()`
* In async/await: thrown errors behave like rejected promises

**Follow-up:**

* What happens when `.catch()` also throws?

---

## **6. Why doesn't try/catch work across async callbacks?**

**Answer:**
Because async callbacks run on a **future tick** of the event loop. `try/catch` only catches errors in the current call stack. Errors in async code must be captured via:

* `.catch()` on promises
* `try/catch` around `await`

---

## **7. How does promise chaining handle returned promises?**

**Answer:**
Returned promises are **adopted** by the next `.then()`. Execution pauses until the returned promise settles.

**Follow-up:**

* What if a `.then()` callback doesn't return anything?

---

## **8. What is the difference between: `await Promise.all()` and multiple await statements?**

**Answer:**

* `Promise.all()` runs operations **concurrently**.
* Multiple awaits run **sequentially**.

---

## **9. Explain how async/await is syntactic sugar over promises.**

**Answer:**
`async` wraps the return value in a promise.
`await` pauses execution until the awaited promise settles.

Under the hood, async/await compiles to promise chains.

---

## **10. Why is `await` inside loops dangerous?**

**Answer:**
It causes sequential execution unintentionally.
Better alternatives:

* `Promise.all()`
* `map()` → promise array → await all

---

## **11. What is a race condition in asynchronous JavaScript? How do you avoid it?**

**Answer:**
Occurs when multiple async operations depend on shared state. Avoid via:

* Mutex/locking
* Atomic operations
* Proper promise composition

---

## **12. Explain `Promise.race`, `Promise.any`, `Promise.allSettled`.**

**Answer:**

* **race** – resolves/rejects with first settled
* **any** – resolves with first fulfilled, ignores rejections
* **allSettled** – waits for all, returns status array

---

## **13. What is unhandled promise rejection?**

**Answer:**
Occurs when a promise rejects without a `.catch()` handler. Node may terminate the process if not handled.

---

## **14. How do you create a cancelable promise?**

**Answer:**
Promises cannot be canceled by default. Solutions:

* AbortController/AbortSignal
* Wrapper with flags
* Libraries like Bluebird

---

## **15. What is the Temporal Dead Zone equivalent for async/await?**

**Answer:**
Async functions create microtask boundaries—errors thrown inside async code propagate to the microtask queue rather than synchronously.

---

# End of Sheet
