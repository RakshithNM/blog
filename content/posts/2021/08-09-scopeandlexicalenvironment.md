---
title: Scope/Lexical environment in javascript
date: 2021-08-09
published: true
tags: ['Javascript', 'Scope', 'LexicalEnvironment']
description: "What is scope in javascript?"
---

Scope is directly depended on the lexical environment of a variable.

Lexical means presence in hierarchy. Lexical environment is created everytime a execution context is created.

Lexical environment is the local memory environment and the lexical environment of the parent.

```js
  function a()  {
    console.log(b); // prints 10
  }
  var b = 10;
  a();
```

```js
  function a()  {
    var b = 10;
    c();
    function c() {
      console.log(b) // prints 10
    }
  }
  a();
```
