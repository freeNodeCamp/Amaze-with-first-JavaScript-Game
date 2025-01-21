<!-- What is the Console -->
<section
  id="what-is-the-console"
  aria-labelledby="what-is-the-console"
  data-item="What is the Console?"
>
  <h2><a href="#what-is-the-console">What is the Console?</a></h2>
  
I can imagine a question in your mind: **How does this code in `main.js` ...**
```javascript
console.log("Hello World")
```
**... plus this command in the Terminal...**

```tex-w
node main.js
```
**... make this text appear in the Terminal?**

```tex-w
Hello World!
```

## The console and `console.log()`
In NodeJS, "[console](https://developer.mozilla.org/en-US/docs/Web/API/console)" is how JavaScript refers to the Terminal where the current script is running. (Later, you'll see that browsers also have a Console, which behaves very like the Terminal.)

## Objects and methods

`console` is a _global object_. This means that you can use it anywhere (globally), and that it can have `methods` and `properties`. As you will see, JavaScript is built with objects.

A method is something an object can do. A property is something it has. It doesn't have to have any methods or properties. If you think of a method like a human being:

* It can be like a new-born baby, who can cry but has no possessions yet. (It has methods but no properties)
* It can be like a reclusive miser, who has many possessions but does nothing with them. (It has properties, but no methods)
* It can be like a regular person, who has stuff and does stuff.


The `console` has several methods but no properties. (It's like a house elf. It doesn't need any possessions.)

In this project, you will use the following methods:

| method | action |
| ------ | ------ |
| `console.log()` | prints the parameters in the Terminal |
| `console.clear()` | removes all text from the Terminal |

## Parameters

The data inside the round parentheses (`( ... )`) is called a _parameter_. In this case `"Hello World!"` is the only parameter.

<details class="pivot" open>
<summary>Showing text in the Terminal</summary>
You'll be using `console.log()` several times in your project, to show text in the Terminal.

As you'll discover, it can also be used to _hide_ text, but not many people know this. (You don't have to keep it a secret.)

</details>

</section>