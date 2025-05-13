---
title: JS Through the Years
layout: page
---


# 🚀 Modern JavaScript Features Since ES6 (2015–2024)

JavaScript has evolved dramatically since **ES6 (2015)**. Here's a quick reference of all the major additions to the language, broken down by year and usefulness.

---

## 📦 ES6 (2015) — The Big Upgrade

### ✅ Syntax & Variables
```js
let x = 10;
const y = 20;
const sum = (a = 1, b = 2) => a + b;
```

### ✅ Strings & Templates
```js
const name = 'World';
console.log(`Hello, ${name}!`);
```

### ✅ Destructuring
```js
const { name, age } = user;
const [first, second] = arr;
```

### ✅ Spread & Rest
```js
const copy = { ...original };
const sum = (...nums) => nums.reduce((a, b) => a + b);
```

### ✅ Objects
```js
const key = 'dynamic';
const obj = {
  name,
  [key]: 42,
};
```

### ✅ Classes
```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} speaks.`);
  }
}
```

### ✅ Promises
```js
fetch('/api')
  .then(res => res.json())
  .catch(console.error);
```

### ✅ Modules
```js
// utils.js
export function greet(name) {
  return `Hello, ${name}`;
}

// main.js
import { greet } from './utils.js';
```

---

## ✨ Post-ES6 Enhancements - Incremental Goodness

### 🔹 **ES7 (2016)**
- `Array.prototype.includes()`
- `**` exponentiation: `2 ** 3`

### 🔹 **ES8 (2017)**
- `async/await`
- `Object.entries()`, `Object.values()`
- `String.padStart()`, `padEnd()`

### 🔹 **ES9 (2018)**
- Spread in objects: `{ ...obj }`
- Rest in objects: `const { a, ...rest } = obj`
- `Promise.prototype.finally()`

### 🔹 **ES10 (2019)**
- `Array.prototype.flat()`, `flatMap()`
- `Object.fromEntries()`
- Optional `catch` binding: `catch {}`

### 🔹 **ES11 (2020)**
- **Optional chaining**: `user?.profile?.email`
- **Nullish coalescing**: `value ?? 'default'`
- `Promise.allSettled()`
- `globalThis`

### 🔹 **ES12 (2021)**
- Logical assignment: `a ||= 1`, `b &&= 2`, `c ??= 3`
- Numeric separators: `1_000_000`
- `String.prototype.replaceAll()`

### 🔹 **ES13 (2022)**
- `.at()` method: `array.at(-1)`
- Top-level `await` in modules

### 🔹 **ES14+ (2023–2024)**
- `Array.prototype.toSorted()`, `toReversed()`, `with()`
- Decorators (in TC39 Stage 3)
- Record & Tuple (proposals)
- Pattern matching (proposal)

---

## 🧠 Must-Know Modern JS Features

| Feature                      | Why It’s Useful                                  |
|------------------------------|--------------------------------------------------|
| `async/await`                | Simplifies async code                            |
| Optional chaining (`?.`)     | Safe access to deep properties                   |
| Nullish coalescing (`??`)    | Smart default values                             |
| Object & Array destructuring | Cleaner variable extraction                      |
| Spread/rest (`...`)          | Concise data manipulation                        |
| Modules (`import/export`)    | Better code organization                         |
| Promises & `Promise.all()`   | Parallel async operations                        |

---

## 🔧 Bonus: Decorators (Experimental)

```ts
function Log(target, key, descriptor) {
  const original = descriptor.value;
  descriptor.value = function (...args) {
    console.log(`Calling ${key} with`, args);
    return original.apply(this, args);
  };
}

class MyClass {
  @Log
  doThing(a, b) {
    return a + b;
  }
}
```

Decorators allow you to annotate and modify classes, methods, properties, and parameters. They're widely used in frameworks like **NestJS**, but also powerful for things like **logging**, **access control**, and **validation**.

> ⚠️ As of 2024, decorators are in [Stage 3 of TC39](https://github.com/tc39/proposal-decorators) and available in TypeScript.
