

###  **Question: Implement a Custom `compose()` Function**

Implement a function `compose(...fns)` that takes multiple functions and returns a new function which applies them **from right to left** (just like function composition in functional programming).

#### Example:

```js
const add = x => x + 2;
const multiply = x => x * 3;
const square = x => x * x;

const composed = compose(add, multiply, square);
// equivalent to: add(multiply(square(x)))

console.log(composed(2)); // ?
```

#### Expected Output:

```js
add(multiply(square(2))) = add(multiply(4)) = add(12) = 14
```

So the result should be:

```js
14
```

---

###  **Requirements:**

- Must accept any number of functions.
    
- Must execute them **right to left**.
    
- Must handle edge cases:
    
    - No functions → returns the input as is.
        
    - One function → returns it directly.
        

---

### 💡 **Follow-up Questions:**

1. How would you modify this to create a `pipe()` function that executes **left to right**?
    
2. Why might this pattern be preferred in functional programming?
    
3. How would you handle **asynchronous functions** (where functions return promises)?
    

---

### 🧠 **Expected Answer:**

```js
function compose(...fns) {
  return function (value) {
    return fns.reduceRight((acc, fn) => fn(acc), value);
  };
}

// Example usage:
const add = x => x + 2;
const multiply = x => x * 3;
const square = x => x * x;

const composed = compose(add, multiply, square);
console.log(composed(2)); // 14
```

---

### ⚙️ **Explanation:**

- Uses `reduceRight` to apply functions in reverse order.
    
- Each iteration passes the accumulated result to the next function.
    
- **Functional programming concept:** composition lets you build complex logic by combining smaller pure functions.
    
- **Time Complexity:** O(n), where n = number of functions.
    
- **Space Complexity:** O(1).
    

---

Would you like the next one to stay in this “medium-hard” range, or should I step it up to a **senior-level async or design-style question** (e.g., custom promise, event emitter, or scheduler)?