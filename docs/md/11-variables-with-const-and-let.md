<!-- variables with const and let -->
<section
  id="const-and-let"
  aria-labelledby="const-and-let"
  data-item="Declaring Variables with const and let"
>
  <h2><a href="#const-and-let">Declaring Variables with `const` and `let`</a></h2>

Here are the new lines of code again:

```javascript-w
const readlineSync = require("readline-sync")
const whoStarts = "If you want to start, type Y. If you want me to start, press any other key. "
```
```javascript-s
// lines skipped //
```
```js-w
let player = readlineSync.keyInYN(whoStarts)
console.log("player:", player)
```

## What's new

Below is a list of things that you have not seen before, in the order in which they appear. I'll explain items 1 - 3 and item 5 in this section, and deal with the others in the following sections.

1. `const`
2. variables
3. assignment with `=`
4. `require()`
5. `let`
6. `readlineSync.keyInYN()`
7. `console.log()` with two parameters


## Thinking like a computer

Here's a new metaphor. You can think of NodeJS as being a long line of identical houses, each with its own specific address.

![Terraced Houses, each with its own address](images/terracedHouses.jpg){data-title="Terraced Houses in Lower Park Street" data-credits="[cc-by-sa/2.0 ](http://creativecommons.org/licenses/by-sa/2.0/) - © [Rob Noble](https://www.geograph.org.uk/profile/4178) - [geograph.org.uk/p/1870300](https://www.geograph.org.uk/photo/1870300)"}

People like to give their houses a name, but for the postal delivery worker, the house number is required and is the only official designation for the house.

 ![Sign showning a house number and the house's name](images/Tucson-John_Dillinger_House_-_1925-2.jpg){data-credits="[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.en) by [Tony Santiago](https://commons.wikimedia.org/wiki/User:Marine_69-71) | [original](https://commons.wikimedia.org/wiki/File:Tucson-John_Dillinger_House_-_1925-2.jpg)"}

When you write JavaScript, you talk about _variables_, not houses, and the space defined by each address is actually a block of Random Access Memory (RAM). However, the principle is the same. You, the human, create a name for a block of memory, and the NodeJS associates that name with a number in its index of available blocks, so it knows which memory block you are talking about.

In my metaphor, you _put_ an _agent, or just some stuff_, in each named _house_, then the agents work together with the stuff that you have given them to build a display on the street (the end-user's screen) that the end-user can interact with.

In the world of JavaScript, your code _assigns_ a _value_ to each named _variable_. When you use a variable name later, JavaScript looks up the number of the memory block in its index, and uses the _contents_ of the block instead of its _name_.

## `const` vs `let`

`const` and `let` are two ways of telling JavaScript to create a named space in its RAM.

`const` tells JavaScript: "Here is some data, it will be _constant_, it will never change." As a result, JavaScript can optimize the space for the data. This is like when you buy a house. You become the permanent owner, and once the initial paperwork is done, everything is simple. You live there: that's it.

Because the value in a variable created `const` has a fixed value, you must give a value as soon as you declare the variable.

`let` tells NodeJS: "You know, I need some space, but I can't be sure how much or what I'll use it for, and I might change my mind. Can you create a space that can get bigger or smaller and that can hold a string of text or a number or an object with many functions... or just about anything?"

When you use `let`, JavaScript has to be prepared for changes. This is like when you let out your house. You don't know what the new tenants are going to do to it, so you need to make an inventory, prepare a lease, ask for a deposit, ... all sort of extra things. And this has to be renewed each time the tenant changes.

Because the value in a variable created `let` can change, you can declare the variable without giving it a value. This is perfectly good code:

```javascript-#
let variableWithNoInitialValue
```

This will cause an error:

```javascript-#
const constantsMustBeAssignedAValue
```

![You must give a `const` variable a value when you create it](images/missingInitializer.webp)

<details class="tip" open>
<summary>Use `const` when possible</summary>
Your code will work faster (and your end-users will be happier) if you declare your variables `const` every time you can.

</details>

## Variable names

I've used the variable names `readlineSync`, `whoStarts` and `player`. The name of the Node Package that you installed was `readline-sync`. Why didn't I use `readline-sync` for the name of the variable?

Computing is all about speed. If JavaScript allowed me to use any name, then it would have to spend more time looking at each name to be sure that it was a name and not some other kind of data. So JavaScript has rules:

* A variable name can begin with a letter, a dollar sign (`$`) or an underscore (`_`)
* A variable name can contain letters, dollar signs, underscores and numbers (but it can't start with a number)
* A variable name _cannot_ contain a space (` `) or a dash (`-`) (so `readline-sync` is not possible)

### Variable naming conventions

By convention, when a variable is created from more than one word (like `whoStarts`), the first letter in each word is written in uppercase letters. This is called _camelCase_.

<details class="tldr">
<summary>Other variable formats</summary>
In HTML and CSS, you will use _kebab-case_ for `id` and `class` names.

In JavaScript, you might also find some constants written in _SCREAMING_SNAKE_CASE_ (but not in this project). These will be global constants that are set when the program first starts, and which can be used in many different places.

NodeJS also provides some special variables, like `__dirname` and `__filename`, which start with a double underscore. Again, you won't see these in this project. 

There are many different formats that can be used for variable names. The most comprehensive list I've found is [here](https://stackoverflow.com/a/64293621/1927589).

</details>

<details class="tip" open>
<summary>Variables should have descriptive names</summary>
You _can_ call a variable anything. The [script `minified.js`](https://MERNCraft.github.io/Nail-It/scripts.zip){download=""} uses single letter names for each variable. Here's are a couple of extracts:

```js-w
const t="If you want to start, type Y. If you want me to start, press any other key. ";const n="The nail is ";const l=" units long."
```
```js-s
// more obfuscated code //
```
```js-w
let M=e.keyInYN(t,O);let T=!M
```

This code works, but it is very hard to read.

You should always choose meaningful names for your variables, even if they are quite long. Each variable name should describe the data it contains. When future-you or a colleague reads your code, a good choice of names will save you a lot of time in understanding what the code does.

</details>

## Equals signs

In JavaScript, a single equals sign (`=`) is used to assign a value to a variable (or to use the house metaphor, to tell JavaScript to move a given piece of data into a named address). So...

```tex-w
const whoStarts = "If you want to start..."
```
... tells JavaScript:

* Select a block of memory at an address that I will call `whoStarts`.
* The contents of this memory block are not going to change. They will be constant.
* Assign the string "If you want to start..." to this memory block.
* In the future, when I refer to `whoStarts`, use the contents of the memory block instead.


<details class="note" open>
<summary>===</summary>
As you will see shortly, three equals signs together (`===`) means "is identical to". This creates an expression which can be either true or false. For example: `2 + 2 === 4` is `true`, but `2 + 2 === "four"` is `false`. But more about this later.

</details>

</section>