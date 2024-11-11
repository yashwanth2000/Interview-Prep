# JavaScript Interview Preparation

This file contains a collection of JavaScript interview questions, examples, and explanations. Each section focuses on a specific topic or concept in JavaScript.

---
## Table of Contents
1. [Event Handling: `addEventListener` vs `onclick`](#1-event-handling-addEventListener-vs-onclick)
2. [Arithmetic Operations](#2-arithmetic-operations)
3. [Implicit Global Variable](#3-implicit-global-variable)
4. [Comparing Objects](#4-comparing-objects)
5. [Function Properties](#5-function-properties)
6. [Spread Operator and Object Copy](#6-spread-operator-and-object-copy)
7. [Number Comparisons and Types](#7-number-comparisons-and-types)
8. [Object Comparison](#8-object-comparison)
9. [Type Coercion Operations](#9-type-coercion-operations)
10. [Object Key Conversion and Property Access](#10-object-key-conversion-and-property-access)
11. [Boolean Arithmetic](#11-boolean-arithmetic)
12. [Memoization in JavaScript](#12-memoization-in-javascript)
13. [Promises with Button Click Example](#13-promises-with-button-click-example)

---

## 1. Event Handling: `addEventListener` vs `onclick`

### Question
Explain the difference between `addEventListener` and `onclick` in JavaScript, including how they behave inside a loop.

### `addEventListener` vs. `onclick`

| Feature              | `addEventListener`                               | `onclick`                                 |
|----------------------|--------------------------------------------------|-------------------------------------------|
| **Handler Count**     | Allows multiple handlers for the same event     | Only one handler can be set at a time     |
| **Overwriting**       | Does **not overwrite** other handlers           | **Overwrites** any previous handler       |
| **Use Case**          | When multiple actions need to respond to the event | When a single action is required        |
| **Syntax**            | `element.addEventListener("event", handler);`    | `element.onclick = handler;`              |

#### Explanation

- **`addEventListener`:**  
  Each iteration of the loop adds a new handler, so when you click the button, all handlers fire sequentially. This is why you see all three `addEventListener` logs.

- **`onclick`:**  
  Each assignment to `onclick` replaces the previous one. After the loop, only the last `onclick` handler (where `i` is 2) remains, so only "onclick handler 2" is logged.

### Key Takeaway
- Use `addEventListener` for multiple handlers.
- Use `onclick` if only one handler is needed, as it overwrites previous handlers.

#### Example

```javascript
const btn = document.getElementById("btn");

for (let i = 0; i < 3; i++) {
  btn.addEventListener("click", () => {
    console.log("addEventListener handler", i);
  });

  btn.onclick = () => {
    console.log("onclick handler", i);
  };
}

// Output
addEventListener handler 0
addEventListener handler 1
addEventListener handler 2
onclick handler 2
```
---

## 2. Arithmetic Operations

### Question
Explain the difference between multiplication (`*`) and exponentiation (`**`) operators in JavaScript.


### Arithmetic Operations (`*` vs `**`)

| Operator         | Operation                                             | Example                  | Output |
|------------------|-------------------------------------------------------|--------------------------|--------|
| **Multiplication (`*`)** | Multiplies two values                              | `s * 2`                  | `4`    |
| **Exponentiation (`**`)** | Raises the first value to the power of the second | `s ** 3`                 | `8`    |

#### Explanation

- `s * 2`: Multiplies `s` (which is 2) by 2, resulting in 4.
- `s ** 3`: Raises `s` to the power of 3, so `2 ** 3` results in 8.

```javascript
let s = 2;
console.log(s * 2); // Output: 4
console.log(s ** 3); // Output: 8
```

---

## 3. Implicit Global Variable

### Question
Why do you see a global variable in the console when a variable is not explicitly declared inside a function?


| Concept                       | Description                                                         |
|-------------------------------|---------------------------------------------------------------------|
| **Implicit Global Variable**   | In non-strict mode, assigning a value to a variable without `let`, `var`, or `const` will create a global variable. |
| **Strict Mode**                | If `"use strict";` is added, JavaScript will throw a `ReferenceError` for undeclared variables. |

#### Explanation

- The function creates a global variable `salary` implicitly because no declaration (`let`, `var`, `const`) is used.
- In **non-strict mode**, JavaScript automatically creates global variables, which can cause unexpected behaviors.
- To avoid this, always use `"use strict";` to prevent implicit global variables.

#### Example

```javascript
function test() {
  salary = 10000;
  console.log(salary); // Output: 10000
}
test();
```
---

## 4. Comparing Objects

### Question
Why does {} == {} return false in JavaScript?


| Concept                       | Description                                                         |
|-------------------------------|---------------------------------------------------------------------|
| **Object Comparison**         | Objects are compared by reference, not by value. Different instances of objects will always return `false` when compared directly. |

#### Explanation
- JavaScript compares objects by their references in memory.
- Even if two objects have the same properties and values, they are considered different unless they point to the same reference.

  
#### Example

```javascript
console.log({} == {}); // false
console.log({} === {}); // false
```
---
## 5. Function Properties

### Question
What happens when you try to access and modify properties on a function, and why do you see different values in the console?


| Concept | Description |
|---------|-------------|
| **Function Properties** | Functions in JavaScript are objects and can have properties assigned to them |
| **Property Access** | Properties can be accessed using dot notation on the function name |
| **Undefined Properties** | Accessing a property before it's defined returns `undefined` |

#### Explanation
- Functions in JavaScript are special types of objects that can store properties
- When accessing `t1.abc` before assignment, it returns `undefined`
- Properties can be assigned and reassigned using the function name (t1.abc = 100)
- The property value changes reflect in subsequent function calls

#### Example
```javascript
function t1() {
  console.log(t1.abc);
}

t1();              // Output: undefined
t1.abc = 100;      // Assigning property
t1.abc = 200;      // Reassigning property
t1();              // Output: 200
```
---

## 6. Spread Operator and Object Copy

### Question
How does the spread operator create copies of objects and what happens when modifying the copied object?


| Concept | Description |
|---------|-------------|
| **Spread Operator** | Creates a shallow copy of object properties |
| **Object Copy** | New object gets its own reference in memory |
| **Property Modification** | Changes to copied object don't affect original |

#### Example
```javascript
let a = {
  name: "syc",
};

let b = { ...a };
b.name = "yash";
console.log(a.name, b.name); // syc yash
```

---

## 7. Number Comparisons and Types

### Question
How does JavaScript compare different number representations using strict equality?


| Concept | Description |
|---------|-------------|
| **Primitive Numbers** | Compared by value |
| **Number Objects** | Compared by reference |
| **Strict Equality** | Checks both value and type |

#### Example
```javascript
let x = 10;               // primitive
let y = new Number(10);   // object
let z = 10;               // primitive

console.log(x === y);     // false (different types)
console.log(y === z);     // false (different types)
console.log(x === z);     // true (same type and value)
```

---

## 8. Object Comparison

### Question
How does JavaScript compare objects and their properties?


| Concept | Description |
|---------|-------------|
| **Object Reference** | Objects are compared by reference, not content |
| **Property Comparison** | Individual properties should be compared directly |
| **Equality Operators** | Both == and === compare references for objects |

#### Example
```javascript
function test2(record) {
  if (record == { age: 28 }) {         // false
    console.log("adult");
  } else if (record.age == 28) {       // true
    console.log("still adult");
  } else if (record === { age: 28 }) { // false
    console.log("still adult");
  } else {
    console.log("no record");
  }
}
```
---

## 9. Type Coercion Operations

### Question
How do unary plus and logical NOT operators work with different types?


| Concept | Description |
|---------|-------------|
| **Unary Plus** | Converts operand to number |
| **Logical NOT** | Converts operand to boolean and negates it |

#### Example
```javascript
console.log(+true);   // 1 (true converted to number)
console.log(!"abc");  // false (non-empty string is truthy)
```
---

## 10. Object Key Conversion and Property Access

### Question
How are object properties accessed and what happens when objects are used as keys?


| Concept | Description |
|---------|-------------|
| **Object as Key** | Objects as keys are converted to string "[object Object]" |
| **Property Access** | Use dot notation or bracket notation |
| **Type Conversion** | Objects as keys are automatically toString() converted |
| **Accessing Object Properties**      | When using bracket notation to access properties, ensure the key is valid. Using a variable (like `r[key]`) will refer to a variable and not a property name, causing a `ReferenceError` if undefined. |

#### Explanation

1. **Object Conversion to String**:
    - When you assign an object (`q` or `r`) as a property key in another object (`p`), JavaScript automatically converts the object to a string. By default, all objects are represented as `"[object Object]"`, which means both `q` and `r` are converted to the same string key, leading to unexpected behavior.

2. **Accessing Object Properties**:
    - When you attempt to use `r[key]`, JavaScript expects `key` to be a variable. Since `key` is undefined in this context, a `ReferenceError` occurs. To access the property of `r`, use `r.key` or `r["key"]`.
  
#### Example
```javascript
var p = {};
var q = { key: "q" };
var r = { key: "r" };

// Objects q and r are converted to string "[object Object]" when used as keys
p[q] = 123;
q[r] = 456;

// Output object with string keys
console.log(p); // { '[object Object]': 123 }
console.log(q); // { key: 'q', '[object Object]': 456 }
console.log(r); // { key: 'r' }

// Accessing object keys with brackets
console.log(p[q]); // 123
console.log(q[r]); // 456

// Accessing a property incorrectly
console.log(r[key]); // Error: ReferenceError: key is not defined

// Accessing object properties correctly
console.log(r.key); // "r"
console.log(p[q]);    // 123
console.log(r.key);   // "r"
```
---

## 11. Boolean Arithmetic

### Question
How does JavaScript handle arithmetic operations with boolean values?


| Concept | Description |
|---------|-------------|
| **Boolean to Number** | true converts to 1, false to 0 |
| **Operator Precedence** | Multiplication has higher precedence than addition |

#### Example
```javascript
var aa = true + true + true * 3;
// Evaluates as: 1 + 1 + (1 * 3) = 5
console.log(aa); // 5
```
---
## 12. Memoization in JavaScript

### Question
Explain the concept of memoization in JavaScript with an example.

### Memoization

| Feature              | Description                                           |
|----------------------|-------------------------------------------------------|
| **Memoization**      | A technique to store the results of expensive function calls and return the cached result when the same inputs occur again. |
| **Cache**            | A data structure (like an object) used to store the results of function calls. |
| **Efficiency**       | Increases performance by reducing the number of redundant function executions. |

#### Explanation

- **Memoization** is used to optimize functions by caching the results of previous function calls.
- When a function is called with the same arguments again, it returns the cached result instead of re-executing the logic.
- The example demonstrates memoizing the `add` and `sub` functions.
- The first call to `memoizedAdd(5, 3)` will calculate the result and store it in the cache. The second call with the same arguments will fetch the result from the cache, improving performance.

#### Key Takeaway
Memoization is useful for optimizing functions that are called frequently with the same inputs.

#### Example

```javascript
function memoize(fn) {
  const cache = {};
  return function (...args) {
    const key = args.toString();
    if (cache[key]) {
      console.log("Fetching from cache", key);
      return cache[key];
    } else {
      console.log("Calculating using function", key);
      const result = fn(...args);
      cache[key] = result;
      return result;
    }
  };
}

function add(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

const memoizedAdd = memoize(add);
const memoizedSub = memoize(sub);

console.log(memoizedAdd(5, 3)); // Calculating using function 5,3
console.log(memoizedAdd(5, 3)); // Fetching from cache 5,3

console.log(memoizedSub(10, 4)); // Calculating using function 10,4
console.log(memoizedSub(10, 4)); // Fetching from cache 10,4
```
---
## 13. Promises with Button Click Example

### Question
Explain how a promise works with button click events in JavaScript and how `async/await` is used.


### Promises with Button Click

| Feature              | Description                                           |
|----------------------|-------------------------------------------------------|
| **Promise**          | Represents the eventual completion (or failure) of an asynchronous operation. |
| **resolve**          | A function used to fulfill the promise successfully. |
| **reject**           | A function used to reject the promise with an error. |
| **async/await**      | Makes handling promises more readable by allowing asynchronous code to be written in a synchronous style. |

#### Explanation

- **Promise**: A promise represents an asynchronous operation that can either resolve (success) or reject (failure). 
- **Event Listeners**: In the example, two buttons trigger the resolution and rejection of the promise based on click events.
  - The `resolveButton` resolves the promise when clicked, with a success message.
  - The `rejectButton` rejects the promise when clicked, with an error message.
- **async/await**: The `async` function allows you to use the `await` keyword to handle the result of the promise in a more readable and synchronous way.
- **Once Option**: `{ once: true }` ensures that the event listener is removed after it is triggered once, preventing multiple triggers.

#### Key Takeaway
Promises handle asynchronous operations and `async/await` improves readability. In this example, button clicks are used to resolve or reject the promise.

#### Example

```javascript
function createButtonClickPromise(resolveButtonId, rejectButtonId) {
  return new Promise((resolve, reject) => {
    const resolveButton = document.getElementById(resolveButtonId);
    const rejectButton = document.getElementById(rejectButtonId);

    resolveButton.addEventListener(
      "click",
      () => {
        resolve("Promise resolved: button clicked");
      },
      { once: true }
    );

    rejectButton.addEventListener(
      "click",
      () => {
        reject(new Error("Promise rejected: button clicked"));
      },
      { once: true }
    );
  });
}

window.addEventListener("load", async () => {
  console.log("File is loaded");

  const buttonClickPromise = createButtonClickPromise(
    "resolveBtn",
    "rejectBtn"
  );

  try {
    const result = await buttonClickPromise;
    console.log(result);
  } catch (error) {
    console.error(error.message);
  }
});
```
#### Output

- **If the `resolveBtn` is clicked first:**
  - File is loaded
  - Promise resolved: button clicked

- **If the `rejectBtn` is clicked first:**
  - File is loaded
  - Promise rejected: button clicked

---
