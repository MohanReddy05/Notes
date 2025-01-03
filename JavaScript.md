```javascript
// variable is a symbolic name for a variable
//variable declared using let, const or var keyword
let x; //declared variable x  //undefined
x = 10; //variable initialized to 10

console.log(x); //console.log() is used to log varialbles of anytype
```

# <h1>variables</h1>

> Variables in JavaScript are used to store and manage data in a program. They serve as containers for values, which can be used and manipulated throughout your code. JavaScript offers several ways to declare variables, each with distinct behavior and use cases.

## Types Of Varibales

### 1. var

-   Variables declared with var are function-scoped, meaning they are only accessible within the function they are declared in.
-   Supports hoisting, so the declaration is moved to the top of the scope during compilation but initialized as undefined.

> var in JavaScript has largely fallen out of favor due to the introduction of let and const in ES6 (ECMAScript 2015).

**Reasons For Fall of var**

1. **Poor Scoping Rules (Function Scope)**

-   var is function-scoped, which means it is accessible throughout the entire function where it's declared, even outside the block where it's defined.
-   This can lead to unintentional errors
    Example :
    ```javascript
    function testVar() {
        if (true) {
            var x = 10;
        }
        console.log(x); // Works, output: 10
    }
    ```

2. **Lack of Temporal Dead Zone**

-   Variables declared with var are hoisted to the top of their scope and initialized as undefined. This can lead to bugs if you try to access them before the declaration.
    ```javascript
    console.log(x); // undefined
    var x = 10;
    ```

3. **No Block Scope**

-   Variables declared with var do not respect block scope, which makes it harder to manage them in complex applications.
    ```javascript
    {
        var x = 10;
    }
    console.log(x); // Accessible, output: 10
    ```

4. **No Constancy**

-   var does not support immutability, making it prone to accidental reassignments. const provides a way to declare variables that cannot be reassigned.
    ```javascript
    var name = 'Alice';
    name = 'Bob'; // Allowed
    ```

**how var executed**

When you use var in JavaScript, the JavaScript engine processes your code in two distinct phases: compilation phase and execution phase. During the compilation phase, the engine identifies all var declarations and hoists them to the top of their scope. This behavior is specific to var and does not apply to let or const.

1. Compilation Phase:

    In the compilation phase, the JavaScript engine scans the code and records variable declarations (and function declarations). For var, the variable is hoisted and initialized with a value of undefined. For let and const, they are also hoisted but are kept in a Temporal Dead Zone (TDZ) and not initialized until their declaration is executed.

    ```javascript
    console.log(x); // undefined
    var x = 10;
    ```

    _what happens in the compilation phase:_

    - The engine detects the var x declaration and hoists it to the top of its scope. The variable x is initialized with undefined.
    - the code becomes

    ```javascript
    var x; // Hoisted
    console.log(x); // undefined
    x = 10;
    ```

2. Execution Phase:

-   The console.log(x) statement runs, and the value of x (currently undefined) is logged.
-   The x = 10 assignment updates the value of x.

    > **Note:** let and const declarations are not initialized during the hoisting phase. They remain in the TDZ, and accessing them before their declaration results in a ReferenceError.

    ```javascript
    console.log(x); // ReferenceError: Cannot access 'x' before initialization
    let x = 10;
    ```

**How the Engine Differentiates var from let and const**

-   Scope: The engine determines the variable's scope during the compilation phase.
    -   var is scoped to the nearest function or global scope.
    -   let and const are block-scoped.
-   Initialization Timing:
    -   var is initialized to undefined during hoisting.
    -   let and const are uninitialized until their declaration is executed
-   Behavior in TDZ: Accessing let or const before declaration throws a ReferenceError.

### 2. let

-   Introduced in ES6 (2015).
-   Variables declared with let are block-scoped, meaning they are accessible only within the enclosing {} block.
-   Not initialized until the declaration is encountered. Attempting to access it before results in a ReferenceError (Temporal Dead Zone)
-   Suitable for variables that need to be reassigned

```javascript
if (true) {
    let y = 20;
    console.log(y); // 20
}
console.log(y); // ReferenceError: y is not defined
```

### 3. const

-   Similar to let in terms of block scoping but with the additional restriction that the variable's value cannot be reassigned.
-   The value can still be mutable if it's an object or array.

## summary

| Feature       | var      | let   | const |
| ------------- | -------- | ----- | ----- |
| Scope         | Function | Block | Block |
| Hoisting      | Yes      | Yes   | No    |
| Reassignment  | Yes      | Yes   | No    |
| Preffered Use | Avoid    | No    | No    |

# Data Types

1. _Primitive types_
2. _Non primitive types_

## primitive types

### 1. Numbers

Represents both integer and floating-point numbers.

```javascript
myNumber = 10;
```

-   js uses 64 bits to store single number.
-   for exponent use e. For example 2.98e6, that's 2.98 X 10^8

**Special numbers**

There are special vlaues in javaScript that are treated as numbers but don't behave as normal numbers

-   `NaN` stands for "not a number",
-   `Infinity`
-   `-Infinity`

### 2. Strings

Sting is used to present text. They are written by enclosing their content in quotes.

-   JavaScript’s representation uses 16 bits per string element, which can describe up to 216 different characters.

```
`mohan`
'mohan'
"mohan"
```

-   _Newlines_ (the characters you get when you press enter) can be included only when the string is quoted with backticks (`).
-   a backslash (\\) inside quoted text indicates that the character after it has a special meaning. This is called escaping the character. A quote that is preceded by a backslash will not end the string but be part of it

```javascript
'This is the first line \n And this is the second';
```

-   Strings cannot be divided, multiplied, or subtracted.
-   The + operator can be used on them, not to add, but to concatenate—to glue two strings together

```javascript
'con' + 'cat' + 'e' + 'nate';
```

-   Backtick-quoted strings, usually called _<ins>template literals</ins>_, can do a few more tricks. Apart from being able to span lines, they can also embed other values.

```javascript
`half of 100 is ${100 / 2}`;
```

> **Note:** When you write something inside ${} in a template literal, its result will be computed, converted to a string, and included at that position. This example produces the string "half of 100 is 50".

#### String Methods

JavaScript provides a variety of built-in string methods for manipulating and working with strings

1. <ins>charAt</ins>()

-   Returns the character at a specified index in a string.
-   Example:
    ```javascript
    let text = 'Hello';
    console.log(text.charAt(1)); // Outputs: 'e'
    ```

2. <ins>charCodeAt</ins>()

-   returns the character code at a specified index in a string
-   Example:

    ```javascript
    let text = 'Hello';
    console.log(text.charCodeAt(0)); // Outputs: 72 (Unicode of 'H')
    ```

3. <ins>concate</ins>()

-   combines two or more strings into one string
-   Example:

    ```javascript
    let str1 = 'Hello';
    let str2 = ' World';
    console.log(str1.concat(str2)); // Outputs: 'Hello World'
    ```

4. <ins>includes</ins>()

-   Description: Checks if a string contains a specified substring.
-   Syntax: str.includes(searchString, position)
-   Example:
    ```javascript
    let text = 'Hello, World!';
    console.log(text.includes('World')); // Outputs: true
    ```

5. indexOf()

-   Description: Returns the index of the first occurrence of a specified substring, or -1 if not found.
-   Syntax: str.indexOf(searchValue, fromIndex)
-   Example:
    ```javascript
    let text = 'Hello, World!';
    console.log(text.indexOf('World')); // Outputs: 7
    ```

6. lastIndexOf()

-   Description: Returns the index of the last occurrence of a specified substring.
-   Syntax: str.lastIndexOf(searchValue, fromIndex)
-   Example:
    ```javascript
    let text = 'Hello, World, World!';
    console.log(text.lastIndexOf('World')); //Outputs: 14
    ```

7. replace()

-   Description: Replaces a specified substring with another substring. Can be used with a regular expression.
-   Syntax: str.replace(searchValue, newValue)
-   Example:
    ```javascript
    let text = 'Hello, World!';
    console.log(text.replace('World', 'JavaScript')); // Outputs: 'Hello, JavaScript!'
    ```

8. split()

-   Description: Splits a string into an array of substrings based on a separator.
-   Syntax: str.split(separator, limit)
-   Example:
    ```javascript
    let text = 'apple,banana,orange';
    let fruits = text.split(',');
    console.log(fruits); // Outputs: ['apple', 'banana', 'orange']
    ```

9. slice()

-   Description: Extracts a section of a string and returns a new string.
-   Syntax: str.slice(startIndex, endIndex)
-   Example:
    ```javascript
    Copy code
    let text = "Hello, World!";
    console.log(text.slice(0, 5)); // Outputs: 'Hello'
    ```

10. substring()

-   Description: Similar to slice(), but does not accept negative indices.
-   Syntax: str.substring(startIndex, endIndex)
-   Example:
    ```javascript
    Copy code
    let text = "Hello, World!";
    console.log(text.substring(0, 5)); // Outputs: 'Hello'
    ```

11. toLowerCase()

-   Description: Converts all characters in a string to lowercase.
-   Syntax: str.toLowerCase()
-   Example:
    ```javascript
    Copy code
    let text = "Hello, World!";
    console.log(text.toLowerCase()); // Outputs: 'hello, world!'
    ```

12. toUpperCase()

-   Description: Converts all characters in a string to uppercase.
-   Syntax: str.toUpperCase()
-   Example:
    ```javascript
    let text = 'Hello, World!';
    console.log(text.toUpperCase()); // Outputs: 'HELLO, WORLD!'
    ```

13. trim()

-   Description: Removes whitespace from both ends of a string.
-   Syntax: str.trim()
-   Example:
    ```javascript
    let text = ' Hello, World! ';
    console.log(text.trim()); // Outputs: 'Hello, World!'
    ```

14. trimStart() / trimLeft()

-   Description: Removes whitespace from the beginning of a string.
-   Syntax: str.trimStart() or str.trimLeft()
-   Example:
    ```javascript
    let text = ' Hello, World!';
    console.log(text.trimStart()); // Outputs: 'Hello, World!'
    ```

15. trimEnd() / trimRight()

-   Description: Removes whitespace from the end of a string.
-   Syntax: str.trimEnd() or str.trimRight()
-   Example:
    ```javascript
    let text = 'Hello, World! ';
    console.log(text.trimEnd()); // Outputs: 'Hello, World!'
    ```

16. toString()

-   Description: Returns the string representation of an object.
-   Syntax: str.toString()
-   Example:
    ```javascript
    let num = 123;
    console.log(num.toString()); // Outputs: '123'
    ```

17. search()

-   Description: Executes a regular expression on a string and returns the index of the match or -1 if no match is found.
-   Syntax: str.search(regexp)
-   Example:
    ```javascript
    let text = 'Hello, World!';
    console.log(text.search('World')); // Outputs: 7
    ```

18. match()

-   Description: Retrieves the result of matching a string against a regular expression.
-   Syntax: str.match(regexp)
-   Example:
    ```javascript
    let text = 'Hello, World!';
    let result = text.match(/[a-z]+/g);
    console.log(result); // Outputs: ['ello', 'orld']
    ```

19. localeCompare()

-   Description: Compares two strings based on local language settings.
-   Syntax: str.localeCompare(compareString)
-   Example:
    ```javascript
    let text1 = 'apple';
    let text2 = 'banana';
    console.log(text1.localeCompare(text2)); // Outputs: -1 ('apple' comes before 'banana')
    ```

20. startsWith()

-   Description: Checks if a string starts with a specified substring.
-   Syntax: str.startsWith(searchString, position)
-   Example:
    ```javascript
    let text = 'Hello, World!';
    console.log(text.startsWith('Hello')); // Outputs: true
    ```

21. endsWith()

-   Description: Checks if a string ends with a specified substring.
-   Syntax: str.endsWith(searchString, length)
-   Example:
    ```javascript
    Copy code
    let text = "Hello, World!";
    console.log(text.endsWith("World!")); // Outputs: true
    ```

### 3. Boolean

It is often useful to have a value that distinguishes between only two possibilities, like “yes” and “no” or “on” and “off”. For this purpose, JavaScript has a Boolean type, which has just two values, true and false

### 4. Empty Values

There are two special values,null and undefined, that are used to denote absence of meaningful values.

-   They are themselves values but doesn't carry any information.

#### i. undefined

-   Represents a variable that has been declared but has not been assigned a value.

```javascript
let x; // x is declared but not initialized
let y = undefined; // Generally, avoid doing this explicitly
console.log(x); // Outputs: undefined
```

#### ii. null

Represents an explicitly empty or non-existent value.

```javascript
let user = null; // Indicates the absence of a user object

function findUser() {
    return null; // Indicates no user was found
}
```

<ins>why null</ins>

```javascript
let user = null; // Indicates no user is currently set
let count = 0; // Indicates there are zero items, not "no count"
```

## Non Primitive Types

### 1. Array

Arrays used for storing Sequences of values

```javascript
let listOfNumbers = [2, 3, 5, 7, 11];
```

-   The first index of an array is zero, not one, so the first element is retrieved with `listOfNumbers[0]`
-   The first index of an array is -1(minus one).

#### Array Methods

| Method           | Description                                                                                            | Example                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| concat()         | Joins two or more arrays                                                                               | [1, 2].concat([3, 4])                                |
| every()          | Tests whether all elements pass a test                                                                 | [1, 2, 3].every(x => x > 0)                          |
| filter()         | Creates a new array with elements that pass a test                                                     | [1, 2, 3].filter(x => x % 2 === 0)                   |
| find()           | Returns the first element that satisfies a condition                                                   | [1, 2, 3].find(x => x > 2)                           |
| findIndex()      | Returns the index of the first element that satisfies a condition                                      | [1, 2, 3].findIndex(x => x > 2)                      |
| forEach()        | Executes a function on each element                                                                    | [1, 2, 3].forEach(x => console.log(x))               |
| includes()       | Determines whether an array contains a specified value                                                 | [1, 2, 3].includes(2)                                |
| indexOf()        | Returns the index of the first occurrence of a specified value                                         | [1, 2, 3].indexOf(2)                                 |
| join()           | Joins all elements of an array into a string                                                           | [1, 2, 3].join(',')                                  |
| lastIndexOf()    | Returns the index of the last occurrence of a specified value                                          | [1, 2, 3, 2].lastIndexOf(2)                          |
| map()            | Creates a new array with the results of calling a function on every element                            | [1, 2, 3].map(x => x \* 2)                           |
| pop()            | Removes the last element from an array and returns it                                                  | [1, 2, 3].pop()                                      |
| push()           | Adds one or more elements to the end of an array                                                       | [1, 2].push(3, 4)                                    |
| reduce()         | Reduces an array to a single value                                                                     | [1, 2, 3].reduce((sum, current) => sum + current, 0) |
| reverse()        | Reverses the order of elements in an array                                                             | [1, 2, 3].reverse()                                  |
| shift()          | Removes the first element from an array and returns it                                                 | [1, 2, 3].shift()                                    |
| slice()          | Extracts a section of an array and returns it as a new array                                           | [1, 2, 3].slice(1, 2)                                |
| some()           | Tests whether at least one element passes a test                                                       | [1, 2, 3].some(x => x > 2)                           |
| sort()           | Sorts the elements of an array in place and returns the sorted array                                   | [3, 1, 2].sort((a, b) => a - b)                      |
| splice()         | Changes the contents of an array by removing or replacing existing elements and/or adding new elements | [1, 2, 3].splice(1, 1, 'new')                        |
| toLocaleString() | Returns a string with a locale-specific representation of each element                                 | [1, 2, 3].toLocaleString()                           |
| toString()       | Converts an array to a string                                                                          | [1, 2, 3].toString()                                 |

---

**Key Points to Consider**

1. Some methods mutate the original array (like `pop()`, `push()`, `reverse()`, `shift()`, `sort()`, `splice()`), while others return a new array without modifying the original (like `concat()`, `filter()`, `map()`, `slice()`).
2. Methods like `every()`, `some()`, `find()`, and `findIndex()` are great for searching arrays efficiently.
3. `reduce()` is particularly powerful for aggregating data or transforming arrays into different structures.
4. `forEach()` is useful when you want to iterate over an array and perform side effects, but it doesn't return anything.
5. Methods like `join()`, `toLocaleString()`, and `toString()` are helpful for converting arrays to string representations.

---

**Best Practices**

1. Choose the appropriate method based on your specific use case. For example, use `map()` for transforming elements, `filter()` for selecting elements, and `reduce()` for aggregating data.
2. Be aware of which methods mutate the original array and which create new ones. This is crucial for maintaining predictable behavior in your code.
3. When working with large datasets, consider performance implications. Some methods like `every()` and `some()` can short-circuit, potentially improving performance.
4. Use arrow functions with array methods for concise and readable code, especially when dealing with simple operations.
5. Remember that many array methods accept callback functions, which allow for powerful and flexible operations on arrays.

---

### 2. Objects

Objects in JavaScript are collections of key-value pairs. They are the fundamental building blocks of the language and serve as containers for storing and organizing data. In essence, objects represent real-world entities or concepts, encapsulating related data and functionality.

**Key Characteristics of JavaScript Objects**

-   Key-Value Pairs: Objects store data in the form of key-value pairs, also known as properties. Keys are strings (or symbols), and values can be any valid JavaScript data type, including functions.
-   Dynamic Nature: Unlike some other languages, JavaScript objects are dynamic. You can add, modify, or remove properties at runtime.
-   Prototypal Inheritance: JavaScript uses prototypal inheritance, meaning objects can inherit properties from parent objects.
-   First-Class Citizens: Objects in JavaScript are treated as first-class citizens, meaning they can be passed as arguments to functions, returned from functions, and stored in variables or data structures.

```JavaScript
// Using object literal syntax
const person = {
  name: "John Doe",
  age: 30,
  greet: function() { console.log("Hello!"); }
};

// Using the Object constructor
const animal = new Object();
animal.name = "Lion";
animal.sound = "Roar";

// Using object destructuring
const { name, age } = person;

// Using class syntax (ES6+)
class Car {
  constructor(make, model) {
    this.make = make;
    this.model = model;
  }

  startEngine() {
    console.log("Vroom!");
  }
}
```

#### Object Methods

| Method               | Description                                                                                  | Example                                  |
| -------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Object.assign()      | Copies properties from one or more source objects to a target object                         | Object.assign({}, obj1, obj2)            |
| Object.create()      | Creates a new object with the specified prototype object and properties                      | Object.create(null)                      |
| Object.entries()     | Returns an array of a given object's own enumerable string-keyed property [key, value] pairs | Object.entries({a: 1, b: 2})             |
| Object.freeze()      | Freezes an object: other code cannot delete or change its properties                         | Object.freeze({a: 1})                    |
| Object.fromEntries() | Returns a new object from an iterable of key-value pairs                                     | Object.fromEntries([['a', 1], ['b', 2]]) |
| Object.keys()        | Returns an array of a given object's own enumerable property names                           | Object.keys({a: 1, b: 2})                |
| Object.values()      | Returns an array of a given object's own enumerable property values                          | Object.values({a: 1, b: 2})              |
| Object.entries()     | Returns an array of a given object's own enumerable string-keyed property [key, value] pairs | Object.entries({a: 1, b: 2})             |
| JSON.parse()         | Parses a JSON string, constructing the JavaScript value or object described by the string    | JSON.parse('{"name":"John"}')            |
| JSON.stringify()     | Converts a JavaScript object or value to a JSON string                                       | JSON.stringify({name: 'John'})           |

---

**Best Practices**

-   Use `Object.assign()` for shallow cloning objects or merging multiple objects into one.
-   Utilize `Object.create()` when you need to set up inheritance patterns or create objects without a prototype chain.
-   `Object.entries()`, `Object.keys()`, and `Object.values()` are useful for iterating over object properties, especially when combined with array methods like `forEach()` or `reduce()`.
-   Use `Object.freeze()` to ensure immutability of objects, which is particularly useful in functional programming paradigms.
-   When working with JSON data, always use try/catch blocks around `JSON.parse()` to handle potential parsing errors.
-   Be aware of the differences between `==` and `===` when comparing objects. `===` checks for reference equality, while `==` performs type coercion before comparison.
-   When extending built-in objects, consider using `Object.defineProperty()` or `Object.defineProperties()` to add non-enumerable properties, preventing them from showing up in `for...in` loops or `Object.keys()` calls

### Mutability

**same object binding**

-   The `object1` and `object2` bindings grasp the same object, which is why changing object1 also changes the value of `object2`.They are said to have the same identity.
-   The binding `object3` points to a different object, which initially contains the same properties as `object1` but lives a separate life

    ```javascript
    let object1 = { value: 10 };
    let object2 = object1;
    let object3 = { value: 10 };

    console.log(object1 == object2);
    // → true
    console.log(object1 == object3);
    // → false

    object1.value = 15;
    console.log(object2.value);
    // → 15
    console.log(object3.value);
    // → 10
    ```

**Const Object**

-   Bindings can also be changeable or constant, but this is separate from the way their values behave. Even though number values don’t change, you can use a let binding to keep track of a changing number by changing the value at which the binding points. Similarly, though a const binding to an object can itself not be changed and will continue to point at the same object, the contents of that object might change.

    ```javascript
    const score = { visitors: 0, home: 0 };
    // This is okay
    score.visitors = 1;
    // This isn't allowed
    score = { visitors: 1, home: 1 };
    ```

    > **Note**
    > : When you compare objects with JavaScript’s == operator, it compares by identity: it will produce true only if both objects are precisely the same value. Comparing different objects will return false.

# Literals

In JavaScript, literals are fixed values directly written in the source code. They represent various types of data and can include numbers, strings, objects, arrays, and more.

Here’s a breakdown of different types of literals in JavaScript:

1. Numeric Literals
   : Represent fixed numerical values.
   Example:

    ```javascript
    let decimal = 42; // Decimal literal
    let hexadecimal = 0x2a; // Hexadecimal literal
    let binary = 0b101010; // Binary literal
    let octal = 0o52; // Octal literal
    let float = 3.14; // Floating-point literal
    ```

2. String Literals
   : Represent sequences of characters enclosed in single ('), double ("), or template (`) quotes.
   Example:

    ```javascript
    let singleQuote = 'Hello, world!';
    let doubleQuote = 'Hello, world!';
    let templateLiteral = `Hello, ${singleQuote}`; // Template literal with interpolation
    ```

3. Boolean Literals
   : Represent the true or false logical values.
   Example:

    ```javascript
    let isJavaScriptFun = true;
    let isBoring = false;
    ```

4. Object Literals
   : Represent key-value pairs inside curly braces {}.
   Example:

    ```javascript
    let person = {
        name: 'Alice',
        age: 25,
        greet: function () {
            console.log('Hello!');
        },
    };
    ```

5. Array Literals
   :Represent ordered collections of values inside square brackets [].
   Example:
    ```javascript
    let fruits = ['apple', 'banana', 'cherry'];
    ```
6. Function Literals
   : Functions can be declared inline as literals.
   Example:
    ```javascript
    let greet = function () {
        console.log('Hello, world!');
    };
    ```
7. Template Literals
   : Strings that allow embedded expressions and multi-line strings using backticks (`).
   Example:
    ```javascript
    let name = 'John';
    let message = `Hello, ${name}! Welcome to JavaScript.`;
    ```
8. RegExp Literals
   : Regular expressions enclosed between slashes /.
   Example:
    ```javascript
    let regex = /hello/i; // Case-insensitive match for "hello"
    ```
9. Null Literal
   : Represents the absence of any value.
   Example:
    ```javascript
    let noValue = null;
    ```
10. Undefined Literal
    : Although undefined is a value, it is not explicitly defined as a literal in JavaScript. It is the default value for uninitialized variables:
    ```javascript
    let notDefined; // Implicitly `undefined`
    ```
11. BigInt Literals
    : Represent integers larger than Number.MAX_SAFE_INTEGER, suffixed with n.
    Example:
    ```javascript
    let bigInt = 1234567890123456789012345678901234567890n;
    ```
12. Symbol Literals
    : Represents unique and immutable values.
    Example:
    ```javascript
    let uniqueKey = Symbol('description');
    ```

# <h1> Conditional Statements </h1>

Conditional statements in JavaScript allow your code to make decisions and execute specific blocks of code based on those decisions. They are essential for controlling program flow.

### 1. `if` Statement

The if statement evaluates a condition and executes the block of code inside if the condition is true.

```javascript
if (condition) {
    // Code to execute if condition is true
}
```

Example:

```javascript
let age = 18;
if (age >= 18) {
    console.log('You are an adult.');
}
```

### 2. `if...else` Statement

The if...else statement provides an alternative block of code to execute if the condition is false.

```javascript
if (condition) {
    // Code to execute if condition is true
} else {
    // Code to execute if condition is false
}
```

Example:

```javascript
let age = 16;
if (age >= 18) {
    console.log('You are an adult.');
} else {
    console.log('You are not an adult.');
}
```

### 3. `else if` Statement

This statement allows multiple conditions to be checked sequentially.

```javascript
Copy code
if (condition1) {
// Code if condition1 is true
} else if (condition2) {
// Code if condition2 is true
} else {
// Code if all conditions are false
}
```

Example:

```javascript
let score = 85;
if (score >= 90) {
    console.log('Grade: A');
} else if (score >= 80) {
    console.log('Grade: B');
} else {
    console.log('Grade: C');
}
```

### 4. `switch` Statement

The switch statement evaluates an expression and executes code based on matching case values.

```javascript
switch (expression) {
    case value1:
        // Code for case value1
        break;
    case value2:
        // Code for case value2
        break;
    default:
    // Code if no case matches
}
```

Example:

```javascript
let day = 3;
switch (day) {
    case 1:
        console.log('Monday');
        break;
    case 2:
        console.log('Tuesday');
        break;
    case 3:
        console.log('Wednesday');
        break;
    default:
        console.log('Invalid day');
}
```

---

# <h1> Break </h1>

The `break` statement is used to exit or terminate a loop prematurely. It is commonly used in loops like for, while, and do-while loops.
Example:

```javascript
for (let i = 1; i <= 10; i++) {
    if (i === 5) {
        break; // Exit the loop when i is 5
    }
    console.log(i);
}
// Output: 1, 2, 3, 4s
```

---

# <h1> Continue </h1>

The `continue` statement is used to skip the current iteration of a loop and move to the next iteration. It is commonly used in loops like for, while, and do-while loops.
Example:

    ```javascript
    for (let i = 1; i <= 10; i++) {

    if (i % 2 === 0) {
    continue; // Skip the rest of the loop for even numbers
    }
    console.log(i);
    }
    // Output: 1, 3, 5, 7, 9

    ```

---

<h1> Loops </h1>

Loops are used to repeatedly execute a block of code until a certain condition is met. JavaScript provides several types of loops, including `for`, `while`, and `do...while` loops.

## 1. `for` Loop

: The `for` loop is used to iterate over a block of code a fixed number of times.

Syntax:

```javascript
for (initialization; condition; update) {
    //statements
}
```

Example:

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
} // Output: 1, 2, 3, 4, 5
```

## 2. `while` Loop

The `while` loop is used to repeatedly execute a block of code as long as a specified condition is true.
Syntax:

```javascript
while (condition) {
    //Code to execute as long as condition is true
}
```

Example:

```javascript
// Print numbers from 1 to 5
let i = 1;
while (i <= 5) {
    console.log(i);
    i++;
}
// Output: 1, 2, 3, 4, 5
```

## 3. `do...while` Loop

The `do...while` loop is similar to the `while` loop, but it guarantees that the code block is executed at least once, even if the condition is initially false.

Syntax:

```javascript
do {
    //Code to execute
} while (condition);
```

Example:

```javascript
// Print numbers from 1 to 5
let i = 1;
do {
    console.log(i);
    i++;
} while (i <= 5);
// Output: 1, 2, 3, 4, 5
```

## 4. `for...in` Loop

The `for...in` loop is used to iterate over the properties of an object.

Syntax:

```javascript
for (variable in object) {
    //Code to execute for each property
}
```

Example:

```javascript
const person = {
    name: 'Alice',
    age: 25,
    city: 'New York',
};

for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}
// Output:
// name: Alice
// age: 25
// city: New York
```

## <h2> 5. `for...of` Loop </h2>

The `for...of` loop is used to iterate over iterable objects like arrays, strings, and more.

Syntax:

```javascript
for (variable of iterable) {
    //Code to execute for each element
}
```

Example:

```javascript
const numbers = [1, 2, 3, 4, 5]; // An array of numbers
for (let number of numbers) {
    console.log(number);
}
// Output: 1, 2, 3, 4, 5
```

---

# Functions

A function is a block of code designed to perform a specific task. It can take inputs (parameters), do something with those inputs, and optionally return an output.

**Declaring Functions**
: declaration of a function contains

-   function keyword
-   Function name
-   Parameters(optional)
-   Code block(anything written within `{ }`)

```javaScript
function functionName(parameter) {
// Code Here
}


const myFunction = function (parameter) {
// Code Here
}
```

> **Note**:
>
> -   Once function is declared, to execute that function you must call it.
> -   Functions can be assigned to variables.

**Calling a Function**
: To run a function, you use its name followed by parentheses

-   Arguments
    : Actual values passed when calling the function

```javascript
myFunction('parameter');
```

**Returning Values**
: A function can send back to callers using `return`

```javascript
function square(num) {
    return num * num;
}
console.log(square(6)); // Outputs: 36
```

**Default Parameters**
:We can set default values parameters

```javascript
function greet(name = 'Guest') {
    console.log('Hello, ' + name + '!');
}
greet(); // Outputs: Hello, Guest!
```

> deefault parameters can be replaced while calling the function with arguments

## 1. Arrow Functions

<p>Arrow functions in JavaScript are a concise way to write functions introduced in ES6 (ECMAScript 2015). They are especially useful for writing short, clean, and functional-style code.
</p>

```javascript
const functionName = (parameters) => {
    // Function body
};
```

**Arrow Function variations**

1. No Parameters

    ```javascript
    const greet = () => console.log('Hello, World!');
    greet(); // Outputs: Hello, World!
    ```

2. Single Parameter
   :Parentheses are optional for a single parameter

    ```javascript
    const square = (x) => x * x;
    console.log(square(4)); // Outputs: 16
    ```

3. Returning an Object Literal
   :Wrap the object literal in parentheses to avoid ambiguity with the function body

    ```javascript
    const createUser = (name, age) => ({ name, age });
    console.log(createUser('Alice', 25)); // Outputs: { name: 'Alice', age: 25 }
    ```

**Key Features**

1. **No `this` Binding**
   : Arrow functions do not have their own `this`. They inherit `this` from their enclosing lexical scope. This makes them especially useful in callbacks or methods where maintaining the correct `this` context is essential.

    ```javascript
    function Person() {
        this.age = 0;

        setInterval(() => {
            this.age++; // `this` refers to the Person object
            console.log(this.age);
        }, 1000);
    }

    const person = new Person();
    ```

    If a regular function were used in setInterval, this would refer to the global object (or undefined in strict mode)

2. **Cannot be Used as Constructors**
   : Arrow functions cannot be used with the `new` keyword. They lack a `prototype` property, which is necessary for constructing objects.

    ```javascript
    const MyFunc = () => {};
    new MyFunc(); // Throws TypeError
    ```

3. **No `arguments` Object**
   : Arrow functions do not have an arguments object. Use rest parameters instead.

    ```javascript
    const sum = (...args) => args.reduce((total, num) => total + num, 0);
    console.log(sum(1, 2, 3, 4)); // Outputs: 10
    ```

---

**Use Cases**

1. **Simplifying Callbacks**
   :Arrow functions are ideal for callbacks:

    ```javascript
    const numbers = [1, 2, 3, 4];
    const doubled = numbers.map(n => n \* 2);
    console.log(doubled); // Outputs: [2, 4, 6, 8]
    ```

2. **Event Listeners**
   :Use arrow functions for simple event handlers:

    ```javascript
    document.querySelector('#button').addEventListener('click', () => {
        console.log('Button clicked!');
    });
    ```

3. **Functional Programming**
   : Arrow functions enhance the readability of functional programming patterns:

    ```javascript
    const filterOdds = (numbers) => numbers.filter((n) => n % 2 === 0);
    console.log(filterOdds([1, 2, 3, 4])); // Outputs: [2, 4]
    ```

---

**When Not to Use Arrow Functions**

1.  **Methods in Objects**
    : Arrow functions do not have their own `this`, so they may cause issues in object methods

    ```javascript
    const obj = {
        name: 'Alice',
        greet: () => console.log(`Hello, ${this.name}!`), // `this` is undefined or the global object
    };
    obj.greet(); // Outputs: Hello, undefined!
    ```

    Use regular functions for methods:

    ```javascript
    const obj = {
        name: 'Alice',
        greet() {
            console.log(`Hello, ${this.name}!`);
        },
    };
    obj.greet(); // Outputs: Hello, Alice!
    ```

2.  **Dynamic Contexts**
    : Avoid arrow functions when the function’s `this` depends on how it is called.

### Summary

| Feature                | Arrow Function   | Regular Function   |
| ---------------------- | ---------------- | ------------------ |
| `this` context         | Lexically scoped | Dynamically scoped |
| `arguments` object     | Not available    | Available          |
| Used as a constructor? | No               | Yes                |
| Syntax                 | Concise          | Longer             |

---

## 2. Anonymous Function

An anonymous function is a function without a name. In JavaScript, these are commonly used when a function is not meant to be reused elsewhere and is defined inline for immediate use.

**Characteristics**

1. **No Name**
   : Unlike named functions, anonymous functions do not have an identifier (name).

    ```javascript

    function() {
    console.log("This is anonymous!");
    }
    ```

    However, this standalone example would cause an error because it is not assigned or invoked. Anonymous functions must be used in specific contexts, like assignments or callbacks.

2. **Usage Contexts**
   :

-   Assigned to variables
-   Passed as arguments to other functions
-   Used as an <a href='#h-26'>Immediately Invoked Function Expression</a> (IIFE)

---

**Syntax**
Anonymous Function Expression
You can assign an anonymous function to a variable:

```javascript
const greet = function (name) {
    return `Hello, ${name}!`;
};
console.log(greet('Alice')); // Outputs: Hello, Alice!
```

---

**Common Use Cases**

1. Inline Callback Functions
   :Anonymous functions are often passed as arguments to higher-order functions, like map, filter, and reduce.

    Example: Array Methods

    ```javascript
    const numbers = [1, 2, 3, 4];
    const doubled = numbers.map(function(n) {
    return n \* 2;
    });
    ```

    console.log(doubled); // Outputs: [2, 4, 6, 8]
    Example: Event Listeners

    ```javascript
    document.querySelector('#button').addEventListener('click', function () {
        console.log('Button clicked!');
    });
    ```

2. Immediately Invoked Function Expressions (IIFE)
   An IIFE is an anonymous function executed immediately after being defined. It is wrapped in parentheses to differentiate it from a function declaration.

    Example:

    ```javascript
    (function () {
        console.log('This is an IIFE!');
    })();
    ```

    Use Case:
    IIFEs are useful for creating a local scope to avoid polluting the global namespace.

3. Dynamic Function Definition
   Anonymous functions can be created dynamically, such as in loops or based on conditions.

    Example:

    ```javascript
    const actions = [
        function () {
            console.log('Action 1 executed');
        },
        function () {
            console.log('Action 2 executed');
        },
    ];
    actions.forEach((action) => action());
    ```

---

**Anonymous Functions vs Named Functions**
|Feature| Anonymous Function| Named Function|
|---|---|---|
|Name| None| Defined by an identifier|
|Reusability| Limited| Can be reused elsewhere|
|Debugging| Harder (no name in stack)| Easier (name appears in stack trace)|
|Scope| Typically local Can be local or global|

---

**When to Use Anonymous Functions**

-   Short-lived Functions: When the function is only needed in one place.
-   Callbacks: In event handlers, asynchronous code, or higher-order functions.
-   Encapsulation: To avoid polluting the global scope.
-   IIFE: For immediate execution.

---

**Best Practices**

1. Use Arrow Functions When Possible: They are a concise way to write anonymous functions.
2. Avoid Nesting Too Many Anonymous Functions: This can make the code hard to follow.
3. Add Comments When Necessary: For complex logic, even inside anonymous functions.

---

**Advantages**

-   Compact Syntax: Great for quick, one-time use.
-   Encapsulation: Prevents unnecessary global variables.
-   Dynamic: Easily defined and passed as arguments.

**Disadvantages**

-   Debugging Difficulty: Since they lack a name, stack traces and error messages can be harder to interpret.
-   Reusability: They can't be reused without redefinition.
-   Reduced Readability: Overusing anonymous functions can make code harder to read and understand.

---

## 3. Immediately Invoked Function Expressions

Immediately Invoked Function Expressions (IIFE) are a pattern in JavaScript where a function is executed immediately after it is defined. This is particularly useful for creating private scopes and avoiding pollution of the global namespace.

**Syntax**

-   Function Definition: An anonymous function is defined.
-   Invocation: The function is immediately invoked.

    ```javascript
    (function () {
        console.log('IIFE executed!');
    })();

    //(function () {
    //  console.log("IIFE executed!");
    //}());

    //Example:
    (function (a, b) {
        console.log(a + b);
    })(3, 7); // Outputs: 10
    ```

**Why Use IIFEs?**

1.  Avoid Global Namespace Pollution
    In JavaScript, variables declared globally can accidentally overwrite existing variables. IIFEs create a new execution context, avoiding this issue.

    Example:

    ```javascript
    (function () {
        var privateVar = 'I am private!';
        console.log(privateVar);
    })();

    console.log(typeof privateVar); // undefined
    ```

2.  Create Private Scope
    Variables inside an IIFE are not accessible outside, making them private and preventing interference with other code.

    Example:

    ```javascript
    (function () {
        var counter = 0;
        console.log('Counter:', counter);
    })();

    // counter is not accessible here.
    ```

3.  Avoid Conflicts in Modular Code
    In large projects, IIFEs are used to wrap code in a module-like structure to isolate functionality.

    Example:

    ```javascript
    var Module = (function () {
        var privateVar = 'hidden';

        return {
            getVar: function () {
                return privateVar;
            },
        };
    })();

    console.log(Module.getVar()); // "hidden"
    ```

4.  Execute Setup Code
    IIFEs are ideal for running setup code or initializing variables.

        Example:

        ```javascript
        (function () {
            console.log("App initialized!");
            // Other setup code here
        })();
        ```

## <h2 id='high-order-function'> 4. High Order Functions</h2>

Functions that operate on other functions, either by taking them as arguments or by returning them, are called higher-order functions.

# <h1 id='bunding'>Binding</h1>

<h1>Recursion</h1>
<h1> Binding</h1>

# <h1>Memory Allocation</h1>

javaScript uses both heap and stack memory allocation:

-   Stack: Used for primitive types and function calls.
-   Heap: Used for objects and complex data structures.

| Stack                               | Heap                       |
| ----------------------------------- | -------------------------- |
| Primitive data types and references | Objects and functions      |
| Size is known at compile time       | Size is known at run time  |
| Fixed memory allocated              | No limit for object memory |

![Memmory management](https://media.geeksforgeeks.org/wp-content/uploads/20230306152333/memory-management-in-js.png)

**Global Scope**
The global scope contains the window object and any globally declared variables. This is not strictly part of either heap or stack but is important for understanding overall memory management.

**How Memory Allocation Works**

1.  When you declare a variable, it's initially stored on the stack.
2.  If you assign an object to that variable, the object itself goes to the heap, while a reference to it stays on the stack.
3.  When a function is called, a new stack frame is created containing the function's parameters and local variables.
4.  As the function executes, it may allocate objects on the heap.
5.  When the function returns, its stack frame is removed, but objects on the heap remain until they're garbage collected.

    ```javascript
    function example() {
        let x = 10; // Stack allocation
        let obj = { a: 20 }; // Heap allocation, reference on stack

        function inner() {
            let y = 30; // New stack frame
            console.log(x); // Accesses outer scope variable
        }

        inner();
    }

    example();
    ```

    > **Note**
    >
    > -   Be mindful of closures, as they can prevent garbage collection.
    > -   Avoid creating unnecessary objects or functions inside loops.
    > -   Use null or undefined to release references when you're done with an object.
    > -   Consider using WeakMap and WeakSet for managing large collections without preventing garbage collection.

# <h1>Asynchronoues Programming</h1>

**What is Synchronous Programming?**

The code is executed in a linear, sequential manner, where each statement is executed one after the other.

**what is Asynchronous Programming?**

The code is executed in a non-linear, concurrent manner, where multiple statements can be executed simultaneously.

**Why Asynchronous Programming?**

-   JavaScript executes code on a single thread (the main thread), which means only one operation can run at a time.
-   To prevent the main thread from being blocked by long-running tasks, JavaScript uses asynchronous programming to offload these tasks.

**How Asynchronous Programming Works?**

**Benefits of Asynchronous Programming**

1. Non-Blocking Execution
   : Asynchronous programming allows the program to continue executing other tasks while waiting for certain operations to complete. This prevents the program from being blocked and improves the responsiveness of the application.
2. Improved Performance
   : By allowing multiple tasks to run concurrently, asynchronous programming can improve the overall performance of the application.
3. User Experience
   : In front-end development, asynchronous operations (e.g., fetching data from APIs) ensure that UI interactions (e.g., animations or form inputs) are not interrupted, providing a smoother user experience.
4. Scalability
   :Asynchronous programming enables efficient handling of high numbers of simultaneous connections or requests, making it well-suited for web servers and applications with heavy traffic.
5. Better Error handling
   : Modern asynchronous patterns like Promises and async/await simplify error handling with constructs like `.catch()` or `try...catch`, making the code more predictable and easier to debug compared to traditional callback-based methods.
6. Memory Efficiency
   : Because asynchronous programming doesn't require the application to maintain multiple threads (as with traditional multithreading), it is more memory-efficient and avoids context-switching overhead.
