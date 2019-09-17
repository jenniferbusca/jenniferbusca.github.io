---
layout: post
title:      "Javascript Variables"
date:       2019-09-17 12:35:38 -0400
permalink:  javascript_variables
---


## Variable Types

### `var`
Var defines a variable globally, and can be accessed anywhere.

**When to use:** The use of `var` should be limited. Because it is not block scoped, there may be unexpected results due to hoisting. 
### `let`
The `let` keyword allows variables to be defined with block or function scope. The variable cannot be re-declared within the same scope, but it can be re-assigned. 

**When to use**: When the variable identifier will be re-assigned
### `const`
The `const` keyword allows variables to be defined with block or function scope similar to `let`, however, it cannot be re-assigned. Although `const` variables cannot be re-assigned, their properties can be changed. 
```
const food = "cheese"
food = "apple" // This will produce and error

const food = {name: "cheese, type: "dairy"}
food.name = "apple" // This will not produce an error

```

**When to use**: When the variable identifier does not need to be re-assigned

| Variable Type       | var      | let      | const
| --------            | -------- | -------- | -------- 
| Can be re-assigned? | Yes      | Yes      |  No
| Can be hoisted?     | Yes      | No       |  No
| Global Scope        | Yes      | Yes      |  Yes
| Function Scope      | Yes      | Yes      |  Yes 
| Block Scope         | No       | Yes      |  Yes

## Variable Scope

### Global Scope

When a variable is declared outside of a function, it becomes a global variable and can be referenced anywhere. `var`, `let` and `const` can all have global scope.

``` 
var foodName = "cheese"
let otherFoodName = "apple"
const lastFoodName = "pizza"

function faveFoods() {
    return `${foodName}, ${otherFoodName}, ${lastFoodName}`;
}

faveFoods()
\\"cheese, apple, pizza"
console.log(foodName)
\\"cheese"
console.log(otherFoodName)
\\"apple"
console.log(lastFoodName)
\\"pizza"
```

### Function Scope
Variables declared inside a function cannot be referenced from outside of the function. `var`, `let` and `const` can all have global scope.

```
function faveFoods() {
  var foodName = "cheese"
  let otherFoodName = "apple"
  const lastFoodName = "pizza" 
}
console.log(foodName)
//Uncaught ReferenceError: foodName is not defined
    at <anonymous>:1:1
console.log(otherFoodName)
//Uncaught ReferenceError: otherFoodName is not defined
    at <anonymous>:1:1
console.log(lastFoodName)
//Uncaught ReferenceError: lastFoodName is not defined
    at <anonymous>:1:1
```

### Block Scope
Blocks are used to group statements and are commonly used in if/else statements. `var` declarations do not have block scope, however `let` and `const` do. Since `var` does not have block scope, it can be re-declared inside the block. 
Even though `const` can not be declared more than once, it can be declared again here because it is being declared uniquely within the block.
```
var foodName = "cheese"
let otherFoodName = "apple"
const lastFoodName = "pizza"
{
  var foodName = "new cheese"
  let otherFoodName = "new apple"
  const lastFoodName = "new pizza"
}
console.log(foodName)
// "new cheese"
console.log(otherFoodName)
// "apple"
console.log(lastFoodName)
// "pizza"
```



