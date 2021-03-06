# Lecture 3: Conditionals and Loops

### Taq Karim
Senior Software Engineer, Intersection

---
## Objectives
* Use `if/else` conditionals for control flow
* Use Boolean logic to combine and manipulate conditional tests
* Use `switch/case` conditionals for control flow based on matching explicit values
* Differentiate between `true`, `false`, truthy, and falsy
* Review iteration using `for` and `forEach`, and introduce `while` and `do/while` loops

---
## Agenda
* Conditional Statements
* Comparison Operators
* Truthy and Falsy
* Logical Operators
* Switch Statements
* `while` & `do/while`
* Iteration

---
## Conditional Statements
Conditional statements enable us to decide which blocks of code to execute and which to skip, based on the results of a condition, *i.e.* a test.

-

JavaScript supports two conditional statements: `if/else` and `switch`. We'll start off with `if/else` which uses Boolean, `true` or `false`, tests.

---
## If / Else Statement

The block of code within the body of the `if` statement, *i.e.* between the `{ }` is run if `expr` evaluates to `true`.

-

`expr` can be any JavaScript expression.
```
if (expr) {
    //code block to run
}
```

---
### Block Statements
A block is delimited by a pair of curly braces, `{}`. We use block statements to group together statements, or lines of code.

-

Any statements intended to be executed after a conditional check will be grouped into a block statement.
```
// simple block
{
    console.log("Hello World!");
    console.log("Hi!");
}
```

Note that there is **no** semicolon at the end of the block.

---
### If Statement Example
```
if (1 > 0) {
  console.log("1 is greater than 0");
}
//=> "1 is greater than 0"
```

---
### Else Statement

If `expr` does not evaluate to `true`, *i.e.* it's `false`, we can add an optional `else` clause to run a block of code.
```
if (0 > 1) {
  console.log("0 is greater than 1");
} else {
  console.log("0 is less than 1");
}
//=> "0 is less than 1"
```

---
### Else if Statement
Use `else if` statements to test more than one case. JavaScript will stop checking conditionals once it hits one that evaluates to `true`.
```
const petType = "cat";
if (petType === "dog") {
  petType += "?";
} else if (petType === "cat") {
  petType += "!";
} else {
  petType = "*" + petType;
}
console.log(petType === "cat!")
//=> true
```

---
Do **not** assign values within a conditional. The conditional is dependent on what you're assigning rather than a comparison:

-

```
x = 5;

if (x = 3) {
    console.log("Will be printed.");
}

if (x = 0) {
    console.log("Will NOT be printed.");
}
```

---
## Ternary Operators
The ternary operator is a "concise" `if/else` statement that returns a value depending on whether the expression evaluates to `true` or `false`:

```
const variable = (expr) ? /* true value */ : /* false value */;
```

-

It's best practice  to have simple ternary operators. We're essentially doing this:
```
if (expr) {
    const variable = /* true value */
} else {
    const variable = /* false value */
}
```

-

Whenever I assign a value to a variable based on some condition, I almost always use a ternary operator. It's cleaner.

-

```
const age = 45;
const minAgeToVote = 18;

const allowedToVote = (age >= minAgeToVote) ? "yes" : "no";
console.log(allowedToVote);
//=> "yes"
```

---
## Comparison Operators
Comparisons in JavaScript can be made using equality comparison operators (`==`, `!=`, `===`, `!==`) and relational operators (`>`, `<`,`>=`, `<=`).

-

We can compare across types, *e.g.* strings against numbers, in JavaScript, but we won't.

-

We should only compare values of the same type. While there is an internal algorithm JavaScript uses for the conversions, we should **not** rely on it.

-

These comparisons are nonsensical, but JavaScript will still let us make them:

```
"A" > "a"
//=> false

"b" > "a"
//=> true

12 > "12"
//=> false

12 >= "12"
//=> true
```

---
## Equality Operator: ==
With the double-equals equality operator, `==`, JavaScript will perform type coercion in the background, if the operands have different types, to check if they are equal.
```
"dog" == "dog";
//=> true

"dog" == "cat";
//=> false

1 == "1";
//=> true

1 == "2";
//=> false
```

-

Basically, numbers and strings that contain numbers of the same value will be considered equal. We will **never** use double-equals.

---
## Identity Operator: ===
Also referred to as the strict equality operator. This operator compares both type and values.

```
1 === "1";
//=> false
```

It does **not** do type conversion. We will always use triple-equals rather than double-equals; it is more precise.

---
## Comparing Objects
Any object, *e.g.* an array, is only equal to itself. Objects are compared by reference, **not** value.

```
[] === []
//=> false

const a = [];
a === []
//=> false

a === a
//=> true
```

Primitives are compared by value whereas objects are compared via where they're stored in memory.

---
## Inequality Operators
We have `!=` and `!==`, with the latter as the strict inequality operator.

We'll always use the `!==` because it returns `true` if the operands are not equal and/or not of the same type.

-

```
1 != "1"
//=> false

1 !== "1"
//=> true

1 !== 2
//=> true
```

---
## Truthy and Falsy
The following values are considered falsy in JavaScript:
```
"" // empty string
NaN // not-a-number
null
undefined
```

-

Everything else is truthy, including empty array,`[]`, and object literals, `{}`.

-

The rules for truthy and falsy are coherent, and used for simplfying conditional expressions.

---
## Not Operator: !
`!` is the logical NOT operator. It returns `false` if the operand is `true`, vice-versa.
```
!true
//=> false

!false
//=> true
```

-

This operator takes one value, so it's an example of a unary operator. We can also wrap the operand in parentheses.

```
!("")
//=> true
```

-

We often use the `!` operator in guard statements in the beginning of a function.

```
function getFinalPrice(price) {
  // `price` is `undefined` when it's not passed in
  if (!price) { return 0; }
  const salesTax = 0.08875;
  return price * (1 + salesTax);
}
```

---
We can use `!!` to verify if a value is truthy or falsy by negating the negation.

```
!!0
//=> false

!!-1
//=> true

!![]
//=> true

!!{}
//=> true

!!null
//=> false

!!""
//=> false
```

---
## Logical Operators
We just saw the not operator, `!`, which is a unary operator. We also have two binary operators in JavaScript:
```
&& // AND
|| // OR
```

We'll use these operators to check multiple expressions or conditions at the same time.

---
## And Operator
The `&&` operator requires both left and right values to be `true` to return `true`. Otherwise, it returns `false`:
```
true && true
//=> true

true && false
//=> false

false && false
//=> false
```

The **AND** operator will only return true when both values are `true`.

-

Example:
```
const network = "GA-Guest";
const pw = "Yellowpencil";
if ((network === "GA-Guest") && (pw === "yellowpencil")) {
    console.log("wifi access granted");
} else {
    console.log("wifi access denied");
}

//which message will be shown in our console?
```

---
## Or Operator
The `||` operator requires either the left or right value to be `true` to return `true`. Otherwise, it returns `false`.
```
true || false
//=> true

false || true
//=> true

false || false
//=> false
```

The **OR** operator will only return `false` when both values are `false`.

-

Example:
```
const day = "Monday";

if ((day === "Monday") || (day === "Wednesday")) {
    console.log("We have class!");
}
```

---
## Short-Circuit Evaluation
Logical expressions are evaluated left to right, so we can use `||` and `&&` for short-circuit evaluation to return one of the operands.

```
false && (x) // short-circuit evaluated to false
true || (x) // short-circuit evaluated to true
```

Note that `x` is not evaluated.

---
## Using && Short-Circuit
We'll use `&&` to check for truthiness before working with a variable. For example, trying to read an a property of `null` or `undefined` will always cause an error

```
undefined.length
//=> Uncaught TypeError: Cannot read property 'length' of undefined
```

-

We can use `&&` to stop the evaluation because `null` and `undefined` are falsy.

```
//a variable not assigned a value is undefined
const x;
x && x.length
//=> undefined
```

* A JavaScript error at runtime can break the rest of your page.

---
## Using || Short-Circuit
We'll use `||` to set a value if the left operand is `false`. This is often used for default values, especially in functions.

```
function getFinalPrice(price) {
  // `price` is `undefined` when it's not passed in
  const price = price || 0;
  const salesTax = 0.08875;
  return price * (1 + salesTax);
}

getFinalPrice(); // 0
getFinalPrice(10); // 10.8875
```

-

**N.B.**: you can also solve the problem above using **default** parameters:
```
function getFinalPrice(price=0) {
  // `price` is `undefined` when it's not passed in
  const price = price;
  const salesTax = 0.08875;
  return price * (1 + salesTax);
}

getFinalPrice(); 
// ^^^ 0, since we set default to be 0 in arg list
getFinalPrice(10); // 10.8875
```

---

## Eligibility Check Exercise

---
Working in repl.it, write a function that outputs a message based on a user's age. Please **work in groups** of 2-3.

-

The program must **print out only the most recent item** a person can do, *e.g.* if a user's age is 46, the message is 'You can run for president':

* Under 16: 'You can go to school!'
* 16 or Older: 'You can drive!'
* 18 or Older: 'You can vote!'
* 35 or Older: 'You can run for president!'
* 62 or Older: 'You can collect social security!'

-

If a user doesn't provide a valid age, tell them to do so. For now, you can hardcode the age to test your code.

---
## Switch Statements
A switch statement first evaluates the `expr` and then matches the `expr`'s value to a `case` clause. If there's a match, it executes the statements for that case.

---

We need to use `break` to stop it from continuing to evaluate statements if there's a match. There's also an optional `default` clause.
```
switch (expr) {
    case value1:
        //statements
        //in documentation, anything with [] is optional
        [break;]
    ...
    case valueN:
        //statements
        [break;]
    default:
        //statements
        [break;]
}
```

**You will almost always want this behavior, so don't forget the `break`!**

-

Example:
```
const num = 1;
switch(num) {
    case "1":
        console.log("You entered the string '1'");
    case 1:
        console.log("You entered the number 1");
        // watch what happens without the `break`
    default:
        console.log("You did not enter 1");
}
// You entered the number 1
// You did not enter 1
```
Note that internally the comparison between the expression and the case value is done using `===`.

-
Example with break...
```
const num = 1;
switch(num) {
    case "1":
        console.log("You entered the string '1'");
        break;
    case 1:
        console.log("You entered the number 1");
        break;
    default:
        console.log("You did not enter 1");
}
// You entered the number 1
```

---

## Refactor via Switch Statement
If we're comparing against specific values in our `if/else` statements, we can almost always refactor to cleaner code using a `switch` statement.

-

Individually, using repl.it, refactor the following code to use a `switch` statement.
```
const grade = 'B';

if (grade === 'A') {
  console.log('Awesome job');
} else if (grade === 'B') {
  console.log('Good job');
} else if (grade === 'C') {
  console.log('Okay job');
} else if (grade === 'D') {
  console.log('Not so good job');
} else if (grade === 'F') {
  console.log('Poor job');
} else {
  console.log('Unexpected grade value entered');
}
```
-

## Solution

```
const grade = 'B'

switch (grade) {
  case 'A':
    console.log('Awesome job');
    break;
  case 'B':
    console.log('Good job');
    break;
  case 'C':
    console.log('Okay job');
    break;
  case 'D':
    console.log('Not so good job');
    break;
  case 'F':
    console.log('Poor job');
    break;
  default:
    console.log('Unexpected grade value entered');
}
```

---
## What if we removed break from the solution?
```
const grade = 'B'

switch (grade) {
  case 'A':
    console.log('Awesome job');
  case 'B':
    console.log('Good job');
  case 'C':
    console.log('Okay job');
  case 'D':
    console.log('Not so good job');
  case 'F':
    console.log('Poor job');
  default:
    console.log('Unexpected grade value entered');
}
//Good job
//Okay job
//Not so good job
//Poor job
//Unexpected grade value entered
```

---
## Fall-Through Technique
This is akin to using `||` in `if/else` statements. For example, what if we only cared about passing?
```
const grade = 'B'

switch (grade) {
  case 'A':
  case 'B':
  case 'C':
    console.log('You passed!')
    break;
  case 'D':
  case 'F':
    console.log('You failed')
    break;
  default:
    console.log('Unexpected grade value entered')
}
//You passed!
```

---
## Loops

Let's review some ways to make loops in JavaScript. We'll use them to evaluate some block of code multiple times.

---
## While Loop
We can use the `while` statement to run a code block as long as the condition is `true`. The condition is evaluated **before** executing the block.

```
while (condition) {
    //statements
}
```

-

Outside of interviews, I've rarely use a `while` loop. They're useful for rare problems where you're not iterating over an array, or you don't know when to stop outside of the loop.

---
## Infinite and Never-run While Loops
Remember, the condition is evaluated **before** executing the block.
```
while (true) {
  // infinite loop
}

while (false) {
  // never-run loop
}
```

-

Create an array containing the numbers 1-10 inclusive
```
const num = 1;
const numArray = [];
while (num < 11) {
    numArray.push(num);
    num++;
}
console.log(numArray);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
```

-

Alertnative approach:
```js
const numArray = [];
while (numArray.length < 10) {
    numArray.push(numArray.length+1);
}
console.log(numArray);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
```
^ what are the key differences between this example and the one above it?

-

ES6 approach:
```js
const numArray = Array.from(Array(11).keys()).slice(1)
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
```
Note that this approach, while terse may be considered a bit more confusing. (NB: I'm personally very fond of this technique)


---
## Do-While Loop
The `do...while` runs a block of code until the condition is `false`. The condition is evaluated **after** executing the statement once.

```
const num = 10;
const numArray = [];
do {
    numArray.push(num);
    num -= 1;
} while (num > 0);
// [ 10, 9, 8, 7, 6, 5, 4, 3, 2, 1 ]
```

---
## For Loop
We've see a `for` loop already. Let's take one more look:
```
const a = [1, 2, 3, 4, 5];
for (const i = 0; i < a.length; i++) {
  console.log(a[i]);
}
//what should we see?
```

-

If we absolutely need to use a `for` loop to iterate over an array, it's helpful to cache the array's length:

```
const a = [1, 2, 3, 4, 5];
const len = a.length;
for (const i = 0; i < len; i++) {
  console.log(a[i]);
}
```

-

Alternatively, here is a more terse approach
```
const a = [1, 2, 3, 4, 5];
for (const i = 0, len = a.length; i < len; i++) {
  console.log(a[i]);
}
```

---
## forEach Loop
As mentioned in the last class, we prefer the `forEach` loop:
```
["dog", "cat", "turtle"].forEach(
    function(currentValue, index, array) {
        console.log("I want a ", currentValue);
        console.log(currentValue);
    }
);
```
Using the `array` and `index` parameter, how else could we have logged each value?

-

Here's another way to write the above (NB: I strongly prefer this approach

```
["dog", "cat", "turtle"].forEach(
    (currentValue, index, array) => {
        console.log("I want a ", currentValue);
        console.log(currentValue);
    }
);
```

-

^ we call this an `arrow function`, it has subtle differences (I would say advantages) over using the `function` keyword. We will discuss these nuances when appropriate but for now strongly prefer to use arrow functions over function expressions when handling callbacks (ie: functions passed into other functions, like above)

---
## Fizz Buzz
Fizz Buzz is a math game designed to teach the concept of division. Take a few moments to read through the starter code, and then we'll get started.

(It's an infamous problem: https://blog.codinghorror.com/why-cant-programmers-program/ )
