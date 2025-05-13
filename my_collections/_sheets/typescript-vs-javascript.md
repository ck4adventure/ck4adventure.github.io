---
title: TS vs JS
layout: page
---

# 🔷 TypeScript vs JavaScript: Key Differences

TypeScript is a **superset** of JavaScript. That means every valid JavaScript program is also a valid TypeScript program. However, TypeScript adds several powerful features on top of JavaScript to help catch errors early and improve developer experience.

---

## ✅ What TypeScript Adds

### 1. **Static Typing**
TypeScript adds optional types to JavaScript, allowing tools to catch type errors before runtime.

```ts
function greet(name: string): string {
  return `Hello, ${name}`;
}
```

---

### 2. **Type Inference**
You don’t always need to annotate types — TypeScript often infers them.

```ts
let count = 10; // inferred as number
```

---

### 3. **Interfaces & Types**
Create reusable type shapes.

```ts
interface User {
  id: number;
  name: string;
}
```

```ts
type Status = "success" | "error";
```

---

### 4. **Classes with Types**
Enhanced class support with typed properties and access modifiers.

```ts
class Animal {
  constructor(private name: string) {}
  speak(): void {
    console.log(`${this.name} makes a noise.`);
  }
}
```

---

### 5. **Enums**
Useful for fixed sets of values.

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}
```

---

### 6. **Generics**
Write reusable and type-safe functions and classes.

```ts
function identity<T>(arg: T): T {
  return arg;
}
```

---

### 7. **Type Guards & Narrowing**
TS refines types within conditions.

```ts
function pad(value: string | number) {
  if (typeof value === "string") {
    return value.padStart(5);
  }
  return value.toFixed(2);
}
```

---

### 8. **Advanced Types**
Includes union, intersection, mapped, conditional, template literal types.

```ts
type Admin = User & { role: string };
type Response<T> = { data: T; error?: string };
```

---

### 9. **Declaration Files (`.d.ts`)**
Describe the types of JS libraries without modifying them.

---

### 10. **Non-JS-Specific Features**
- **Namespaces** (mostly legacy now)
- **Decorators** (experimental but supported with `experimentalDecorators`)
- **`readonly` & `const`-like enforcement**
- **Literal types** (`'open' | 'closed'`)
- **Tuple types** (`[number, string]`)

---

## 🛑 What TypeScript *Restricts* or *Removes*

- **Type errors** are surfaced during development, blocking builds if configured strictly.
- **Strict null checks** prevent `null`/`undefined` bugs.
- **Implicit `any`** is disallowed in strict mode.
- **Runtime behavior stays the same** — TS does **not** change how code runs.

---

## ⚙️ Tooling & Ecosystem Benefits

- Rich autocompletion & IntelliSense in editors
- Compile-time checking
- Code refactoring and navigation tools
- Integrates with modern frameworks (React, NestJS, Angular, etc.)

---

## 🧪 TypeScript in Practice

- Used heavily in **large codebases**
- Supported natively by tools like **ts-node**, **Vite**, **Next.js**, **Bun**
- Compile target can be JS from ES3–ES2023

---

## ✅ When to Use TypeScript

| Use Case                            | TypeScript Helps With              |
|------------------------------------|------------------------------------|
| Large projects                     | Safer refactors & fewer bugs       |
| Team collaboration                 | Clear contracts via types          |
| API-heavy applications             | Validating input/output types      |
| Framework-heavy apps (React/Nest)  | Component/Service contracts        |

---

> 🧠 **Bottom Line:** TypeScript enhances JavaScript with types, improving code quality, maintainability, and tooling. But it compiles down to regular JavaScript — so you get the best of both worlds.
