---
title: Execution context in javascript
date: 2021-02-06
published: true
tags: ['js','execution context']
cover_image: ./images/let-const-script-scope.png
canonical_url: false
description: "What happens when a file is executed in js behind the scenes"
---

When a file is executed in javascript there are two phases of execution. One is the memory creation phase (phase one), another one is code execution phase (phase two). In the memory creation phase javascript engine skims through the program and allocates `undefined` to variables and assigns function definition as it is to its name.

consider the code snippet below, ill try to explain the way in which the javascript code is executed.

``` js
var num = 10;
function addOne(inNum) {
  var result = inNum + 1;
  return result;
}
var eleven = addOne(num);
var twelve = addOne(eleven);
```
![phaseone-memory-creation-phase](/images/posts/functionexecution1.svg)

In phase one, a Global execution context is created(which is represented by the outer square in the diagram) the variables are assigned undefined and the function definition is assigned to its name in the global scope. Now, if we use `const` or `let` this will create the variables in the `Script` scope and not in the `Global` scope as shown in the image below.

![let-const-Script-scope](/images/posts/let-const-script-scope.png)

Once that is done in the phase two, the code is executed line by line, and in line 1, the variable num is assigned 10 in the global scope. Next it sees the definition for `addOne`, since there is nothing to execute it jumps to line `var eleven = addOne(num)`.

Whenever a function is executed in javascript a new execution context is created. Remember when the program is run it has already created a `Global Execution Context`. Now when javascript engine encounters `addOne(num)` it creates a new local execution context, and passes the argument `num` to parameter `inNum` which has the value 10 in the memory local to it(global memory).

![phasetwo-code-execution-phase](/images/posts/functionexecution2.svg)

In the new local execution context the execution of the program happens in two phases, as soon as it creates the local execution context, it assignes `undefined` to the variables and assigns function definitions to its name if any is present. In the first phase(memory creation phase), the variable result is assigned `undefined`. Once the execution enters the code execution phase, the line `var result = inNum + 1` is executed and the value `11` is asssigned to the variable `result`.

Now when the javascript engine encounters the line `return result;` the value of `11` from the local memory is returned and assigned to the variable `eleven`. If there is no return statement in a function, javascript always returns `undefined`.

![phasetwo-code-execution-phase](/images/posts/functionexecution3.svg)

Once the code execution of the local execution context is complete, the execution context is deleted and is shown by the red cross mark over the local execution context.

Now the code execution is at line `var twelve = addOne(eleven);` and the value of `11` present in the global memory is assigned to the argument `eleven` and is assigned to the parameter `inNum`. Again when the javascript engine encouters a function execution in this line, a brand new local execution context is created. In phase one the variables are assigned `undefined` and function definition is assigned to their names if any exists in the function body.

In the second phase of code execution, the line `var result = inNum + 1` is encountered, the value of `inNum` which is `11` is added to `1` and the value `12` is stored in the variable `result` which earlier had the value of `undefined` in the memory creation phase. When the javascript engined encounters line `return result;` the value in the local memory 12 is returned and the execution context is deleted.

Javascript engined uses a data structure to keep track of the function to call at any time using a data structure called the 'CALL STACK' which we will be discussing next in another post.
