# Tutorial4Typescript
## Variable Declaration
* In typescript variable are decleared using `let` and `const` keyword.
* `const` is an augmentation of `let` in that it prevents re-assignment to a variable.
* **`const` declarations must be initialized**
* When a variable is declared using `let`, it uses what some call block-scoping.
* `var` declarations are accessible anywhere within their containing function, module, namespace, or global scope

```typescript=
let x = 10;
let x = 20;// error: can't re-declare 'x' in the same scope
const pi = 3.14;
```
