# JavaScript Interview Preparation

This file contains a collection of JavaScript interview questions, examples, and explanations. Each section focuses on a specific topic or concept in JavaScript.

---

## 1. Event Handling: `addEventListener` vs `onclick`
### Question
Explain the difference between `addEventListener` and `onclick` in JavaScript, including how they behave inside a loop.

---

### `addEventListener` vs. `onclick`

| Feature              | `addEventListener`                               | `onclick`                                 |
|----------------------|--------------------------------------------------|-------------------------------------------|
| **Handler Count**    | Allows multiple handlers for the same event      | Only one handler can be set at a time     |
| **Overwriting**      | Does **not overwrite** other handlers            | **Overwrites** any previous handler       |
| **Use Case**         | When multiple actions need to respond to the event | When a single action is required        |
| **Syntax**           | `element.addEventListener("event", handler);`    | `element.onclick = handler;`              |

#### Explanation

### addEventListener: 
Each iteration of the loop adds a new handler, so when you click the button, all handlers fire sequentially. This is why you see all three addEventListener logs.

### onclick: 
Each assignment to onclick replaces the previous one. After the loop, only the last onclick handler (where i is 2) remains, so only "onclick handler 2" is logged.

### Key Takeaway
Use addEventListener for multiple handlers.

Use onclick if only one handler is needed, as it overwrites previous handlers.

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

---

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

---

### Implicit Global Variable

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
