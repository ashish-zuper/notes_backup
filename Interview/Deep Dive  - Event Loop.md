
# JavaScript Event Loop – Interview Questions


---

## **Question 1 — Event Loop Execution Order**

### **What is the output of the following code? Explain in detail.**

```javascript
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => console.log("C"));

console.log("D");
```

### **Answer:**

The output will be:

```
A
D
C
B
```

### **Explanation:**

1. **Synchronous code executes first** → prints `A`, then `D`.
    
2. **Microtasks (Promises, async/await) run next** → prints `C`.
    
3. **Macrotasks (setTimeout, setInterval, I/O)** run last → prints `B`.
    

### **Follow-up Questions:**

1. **What happens if the timeout is set to 100ms instead of 0ms?**  
    The order remains the same (`A D C ...`) but `B` is delayed by ~100ms.
    
2. **Do async/await callbacks run as microtasks or macrotasks?**  
    They run as **microtasks**, same as Promise callbacks.
    

---

## **Question 2 — Event Loop + Heavy Blocking Code**

### **What will this code print and why?**

```javascript
console.log("start");

setTimeout(() => console.log("timeout"), 0);

for (let i = 0; i < 3_000_000_000; i++) {}

console.log("end");
```

### **Answer:**

The output will be:

```
start
end
timeout
```

### **Explanation:**

- `start` prints immediately.
    
- The `setTimeout` callback is added to the **macrotask queue**.
    
- The long `for` loop **blocks the main thread** for several seconds.
    
- After the loop finishes, `end` is logged.
    
- Only when the call stack is empty can the event loop execute queued macrotasks → prints `timeout`.
    

### **Follow-up Questions:**

1. **How can you avoid blocking the event loop for heavy computations?**
    
    - Use **Web Workers** or **Node.js Worker Threads**.
        
    - Break computation using `setTimeout`, `queueMicrotask`, or `requestIdleCallback`.
        
    - Use streaming or chunked processing.
        
2. **If the loop took 10 seconds, when would the setTimeout fire?**  
    After **10 seconds**, because the timer callback cannot run until the stack is free.
    

---