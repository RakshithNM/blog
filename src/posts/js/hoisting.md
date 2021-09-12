---
title: Hoisting in javascript
date: 2021-08-17
published: true
tags: ['js','hoisting']
description: "what is hoisting in javascriipt"
---

Hoisting means to be able to access variables and call a function that is declared down below without any error.

When javascript program is executed a execution context is created. There are two components in execution context, the variable environment and thread of execution.

The function execution happens in two phases,
  1. Memory creation phase.
  2. Code execution phase.

In the memory creation phase as soon as it encounters the varialbe assignment "undefined" is assigned to the variable. When the javascript engine encounters the function declaration, it literally assigns the function code to it. This happens even before the code execution phase and it explains hoisting.

``` js
console.log(abc); // undefined
var abc = 10;
```

``` js
console.log(def); // undefined
var def = function() {
  alert("def");
}
```

``` js
console.log(ghi); // f ghi() { console.log("ghi") }
function ghi() {
  console.log("ghi");
}
```
In the first and second code examples, variables `abc` and `def` are assigned `undefined` in the memory creation phase, which is why it logs undefined in the code execution phase and doesn't error out. In the third code example `ghi` is assigned the literal function code in the memory creation phase, which is why during the code execution phase the literal function code is logged to the console.

`const` and `let` declarations are also hoisted but they are not hoisted like `var` declarations. `const` and `let` declarations are hoisted but they are in the temporal dead zone. `const` and `let` are also allocated memory in the memory creation phase  but they are present in different memory space.

Temporal Dead Zone is the time between the let and const declarations being assined undefined and being assigned a value.

Accessing let and const before initialization is a Reference error
``` js
console.log(a); //  Reference error
let a;
a = 10;
```

Redeclaration is a syntax error
``` js
let a = 10;
let a = 100;
```
