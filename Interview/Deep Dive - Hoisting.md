# JavaScript Hoisting – Interview Questions


---

## **Question 1: What will be the output of the following code and why?**



```javascript
console.log(a);
var a = 10;

--------------

foo();
function foo() {
  console.log("Hello");
}

--------------

bar();
var bar = function () {
  console.log("Test");
};
```


```javascript
console.log(a);
var a = 10;
```

### **Answer:**

The output will be:

```
undefined
```

### **Explanation:**

Due to **hoisting**, the variable `a` is moved to the top of its scope, but only the _declaration_ is hoisted, not the assignment.

This is how JavaScript interprets the code:

```javascript
var a; // hoisted
console.log(a); // undefined
a = 10;
```

### **Follow-up Questions:**

1. **What happens if `let` is used instead of `var`?**  
    Using `let` will throw a `ReferenceError` because `let` variables are hoisted but placed in the **Temporal Dead Zone (TDZ)**.
    
2. **Will replacing `var` with `const` change anything?**  
    Yes, it will also throw a `ReferenceError` because `const` is also in the TDZ and must be initialized at declaration.
    

---

## **Question 2: Predict the output of the following code involving function hoisting.**

```javascript
foo();

function foo() {
  console.log("Hello");
}
```

### **Answer:**

The output will be:

```
Hello
```

### **Explanation:**

**Function declarations** are fully hoisted — both their name and their implementation. So JavaScript treats the code as if the function is defined at the top.

---

## **Question 3: What will be logged and why?**

```javascript
bar();

var bar = function () {
  console.log("Test");
};
```

### **Answer:**

The output will be:

```
TypeError: bar is not a function
```

### **Explanation:**

Here, only the **variable declaration** `var bar` is hoisted, not the function expression.

The code becomes:

```javascript
var bar; // hoisted
bar();   // bar is undefined → TypeError
bar = function () {
  console.log("Test");
}
```

Function expressions are **not hoisted as functions**.

### **Follow-up Questions:**

1. **Does the same happen if we use `let bar = function()` instead?**  
    No — it results in a `ReferenceError` because `bar` would be in the TDZ.
    
2. **How does hoisting differ for arrow functions?**  
    Arrow functions behave like function expressions — only the variable is hoisted.
    

---

