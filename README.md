# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) SOFTWARE ENGINEERING IMMERSIVE

React and ES6 (also known as ECMAScript 6, ECMAScript 2015, or ECMAScript Harmony) are _closely_ intertwined, so let's take some time to review and to differentiate the two. Laying this groundwork will help us debug our code in the near future, while also granting us a better understanding of the React framework.

## What is ECMAScript?

ECMAScript is a scripting language _specification_- an international, technical standard- that was introduced by its maintainer organization, the European Computer Manufacturers Association (ECMA), to help standardize the JavaScript language.

_Fun Fact: [ECMA-262](https://tc39.es/ecma262/) specifically refers to ECMAScript, the JavaScript specification, but ECMA, the standards organization, is also responsible for standardizing FORTRAN (ECMA-9), C# (ECMA-334), C++ (ECMA-372), APIs (ECMA-402), JSON (ECMA-404), and many, many more._

> Learn More: [ECMA Standards](https://en.wikipedia.org/wiki/List_of_Ecma_standards)

## ES6 Features

ES6, the specification version that was updated and ratified in June 2015, added _significant_ features that have come to underpin modern JavaScript applications, which is why we'll be focusing on it this morning.

> Learn More: In June 2020, the 11th version– _ES2020_– was released, making it the most recent update. You will often see the upcoming version of ES referred to as _ES.Next_.

Some familiar features...

### Variables

Before ES6, variables were declared using the `var` keyword. ES6 introduced `let` and `const`, with some important differences about how these operate in a program.

### Template Literals

Before ES6, variables in strings had to be concatenated:

```js
"The sum of " + a + " and " + b + " is " + (a + b) + ".";
```

Thankfully, ES6 gave us template literals:

```js
`The sum of ${a} and ${b} is ${a + b}.`;
```

### Functions

Before ES6, to create a function, we had:

**Function Declarations:**

```js
function error(status) {
  console.error(status);
}
```

**Function Expressions:**

```js
const error = function (status) {
  console.error(status);
};
```

**Anonymous Functions:**

```js
function(status) {
  console.error(status)
}
```

...but then, ES6 introduced **Arrow Functions**:

```js
const error = (status) => {
  console.error(status);
};
```

You can go one step further:

```js
const error = (status) => console.error(status);
```

No parameters:

```js
const error = () => console.error("404");
```

Multiple Parameters:

```js
const error = (status, msg) => console.error(status, msg);
```

Multiple lines:

```js
const error = (status) => {
  let msg = "Error: ";
  console.error(msg, status);
};
```

### Array & Object Manipulation with the Spread Syntax

Before ES6, generating new Arrays and Objects from multiple data sources was a bit messy. ES6 introduced the _spread syntax_– `...`– for dealing with such cases in a clean, readable manner.

The basic idea behind the spread is that it "spreads out" or "unpacks" all of the values in an Array or Object.

```js
const evens = [2, 4, 6];
const odds = [1, 3, 5];

const moreEvens = [...evens, 8, 10];

console.log(moreEvens);
```

<details>

<summary>Output:</summary>

```bash
[ 2, 4, 6, 8, 10 ]
```

</details>

Without the `...` we would have gotten the following:

```js
const evens = [2, 4, 6];
const odds = [1, 3, 5];

const moreEvens = [evens, 8, 10];

console.log(moreEvens);
```

<details>

<summary>Output:</summary>

```bash
[ [ 2, 4, 6 ], 8, 10 ]
```

</details>

The spread syntax allows us to seamlessly integrate _nested_ values with other elements in a _single_ array. The order is still preserved when spreading out multiple arrays, and we can easily use more than one spread in a single line:

```js
const evens = [2, 4, 6];
const odds = [1, 3, 5];

const nums = [...evens, ...odds, 8, 9, 10];

console.log(nums);
```

<details>

<summary>Output:</summary>

```bash
[ 2, 4, 6, 1, 3, 5, 8, 9, 10 ]
```

</details>

Best of all, this isn't limited to Arrays. Similar operations are possible with Objects:

```js
const people = {
  JayZ: { shirt: "goldfish" },
  Ashley: { shirt: "Nine Inch Nails" },
  JohnMaster: { shirt: "button down" },
};

const otherPeople = {
  Jason: { shirt: "coffee" },
  Mimi: { shirt: "wonder woman" },
};

const allPeople = {
  ...people,
  ...otherPeople,
};

console.log(allPeople);
```

<details>

<summary>Output:</summary>

```bash
{ JayZ: { shirt: 'goldfish' },
  Ashley: { shirt: 'Nine InNailsch ' },
  JohnMaster: { shirt: 'button down' },
  Jason: { shirt: 'coffee' },
  Mimi: { shirt: 'wonder woman' } }
```

</details>

Do note, however, that latter values will "overwrite" former values:

```js
const letters = {
  a: 1,
  b: 2,
  c: 3,
};

const moreLetters = {
  d: 4,
  e: 5,
  a: 10,
};

const allLetters = {
  ...letters,
  ...moreLetters,
};

console.log(allLetters);
```

<details>
    <summary>Output:</summary>

```bash
{ a: 10, b: 2, c: 3, d: 4, e: 5 }
```

The value of `a` is 10 since that was the "last" value associated with the `a` key.

</details>

Just like Arrays, Objects can mix directly declared keys with `spread`ed values:

```javascript
const letters = {
  a: 1,
  b: 2,
  c: 3,
};

const moreLetters = {
  d: 4,
  e: 5,
  a: 10,
};

const allLetters = {
  ...letters,
  g: 20,
  u: 30,
  ...moreLetters,
};

console.log(allLetters);
```

<details>
    <summary>Output:</summary>
    
```
{ a: 10, b: 2, c: 3, g: 20, u: 30, d: 4, e: 5 }
```

</details>

#### Use Cases & Drawbacks

The spread operator is quickly becoming one of the key work horses of ES6. The flexible and clean syntax allows smooth merging of data from disparate sources as well as a safe way to handle state updates in frameworks like React.

There is still a problem. The spread operator only generates a new _shallow_ value of the data structure that is being unpacked. If an Array or Object has nested Arrays or Objects as elements, then the nested elements are not similarly `spread`ed.

Without nested compound data structures, everything is fine:

```javascript
const letters = {
  a: 1,
  b: 2,
  c: 3,
};

const allLetters = {
  ...letters,
  g: 20,
  u: 30,
};

allLetters.a = 20;

console.log("all letters: ", allLetters);
console.log("letters: ", letters);
```

<details>

<summary>Output:</summary>

```bash
all letters:  { a: 20, b: 2, c: 3, g: 20, u: 30 }
letters:  { a: 1, b: 2, c: 3 }
```

</details>

Notice how `a` is not mutated in the original `letters` Object, since a new copy is created when using the spread operator.

But what if that value is nested in another object?

```javascript
const letters = {
  vowels: { a: 1 },
  a: 1,
  b: 2,
  c: 3,
};

const allLetters = {
  ...letters,
  g: 20,
};

allLetters.vowels.a = 20;

console.log("all letters: ", allLetters);
console.log("letters: ", letters);
```

<details>

<summary>Output:</summary>

```bash
all letters:  { vowels: { a: 20 }, a: 1, b: 2, c: 3, g: 20 }
letters:  { vowels: { a: 20 }, a: 1, b: 2, c: 3 }
```

</details>

### Complex Variable Assignment with Destructuring

In addition to the spread syntax, ES6 also introduced a mechanism for extracting one or more key/value pairs from an object and assigning them to variables. The syntax resembles variable assignment, with a few tweaks.

Before ES6, extracting object properties for assignment would require:

```js
const person = {
  first_name: "Stefon",
  last_name: "Simmons",
  city: "New York City",
};

const first_name = person.first_name;
const last_name = person.last_name;
const city = person.city;

console.log(first_name);
console.log(last_name);
console.log(city);
```

But ES6 introduced the object destructuring assignment, which allowed for single line assignments:

```js
const person = {
  first_name: "Stefon",
  last_name: "Simmons",
  city: "New York City",
};

const { first_name, last_name, city } = person;

console.log(first_name);
```

The above will log the value of `first_name` to the console:

```bash
'Tara'
```

Under the hood, _variable names_ matching the _key names_ of the object are auto-initialized and assigned the value associated with that key, from the object. (If the key does not exist in the object, its value will be `undefined`.)

For what it's worth, this same effect works in "reverse". Key/value pairs can be inserted into an object literal if a matching variable is found in scope.

```js
const first = "Stefon";
const last = "Simmons";

const person = {
  first,
  last,
};
console.log(person);
```

The above will log the following to the console

```bash
{ first: 'Stefon', last: 'Simmons' }
```

Finally, the spread, used in these contexts, will grab everything in the destructure assignment that is not explicitly extracted into a variable.

```js
const person = { first_name: "Stefon", last_name: "Simmons", city: "New York" };

const { city, ...other } = person;

console.log(other);
console.log(city);
```

The console will log:

```bash
{ first: 'Stefon', last: 'Simmons' }
'New York City'
```

## Practice

### Destructuring

In a scratch.js file, define a javascript Object with three keys, `name`, `age`, and `hometown`. Use your own information to fill the object with key-values.

Try using the destructuring syntax to extract all three keys into variables. Log out each variable to the console using `node scratch.js` in the CLI.

Next, remove 2 of the destructured variables, then try using the spread syntax to extract the two removed keys, without extracting the third.

### Spread Out

Define two arrays, `evens` and `odds` filled with even and odd numbers.

Using the spread operator, make a new array `numbers` that contains all of the evens and odds.

### Merge Objects

Define an object, `faveFoods`, create keys– the names of your favorite foods– and the values– the restaurant or locale where that food is made.

Now make another object `friendFaveFoods`, and do the same thing, but this time ask your neighbor what their favorites are.

Using the `spread` operator, build a final object, `allFoods`, the result of merging the items from your `faveFoods` and your neighbor's `friendFaveFoods`.
