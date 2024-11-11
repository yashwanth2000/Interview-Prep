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

---
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
## 3. Function Properties

### Question
What happens when you try to access and modify properties on a function, and why do you see different values in the console?

---

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

## 5. Spread Operator and Object Copy

### Question
How does the spread operator create copies of objects and what happens when modifying the copied object?

---
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

## 6. Number Comparisons and Types

### Question
How does JavaScript compare different number representations using strict equality?

---
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

## 7. Object Comparison

### Question
How does JavaScript compare objects and their properties?

---
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

## 8. Type Coercion Operations

### Question
How do unary plus and logical NOT operators work with different types?

---
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

## 9. Object Property Access

### Question
How are object properties accessed and what happens when objects are used as keys?

---
| Concept | Description |
|---------|-------------|
| **Object as Key** | Objects as keys are converted to string "[object Object]" |
| **Property Access** | Use dot notation or bracket notation |
| **Type Conversion** | Objects as keys are automatically toString() converted |

#### Example
```javascript
var p = {};
var q = { key: "q" };
var r = { key: "r" };

p[q] = 123;
q[r] = 456;

console.log(p[q]);    // 123
console.log(r.key);   // "r"
```
---

## 10. Boolean Arithmetic

### Question
How does JavaScript handle arithmetic operations with boolean values?

---
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

