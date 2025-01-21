<!-- Dealing with errors -->
<section
  id="dealing-with-errors"
  aria-labelledby="dealing-with-errors"
  data-item="Dealing with errors"
>
  <h2><a href="#dealing-with-errors">Dealing with errors</a></h2>
  
I'm now going to make you break your code. When you run it and choose how hard your are plan to hit the nail, the Terminal will fill up with information about an error. Actually, I will create a series of errors for you, and you can discover how to fix them, one by one.

Error messages might look alarming, but they are designed to be helpful. They are written by experienced developers who want to understand what mistakes they themselves have made, so they can see how to fix them.

## Redraw the nail with a shorter length

The next step in your game is to show the nail with a shorter length because it has been hit by a virtual hammer.

The obvious way to do this would be to subtract the value returned by `keyInSelect()` from `length`. Or something like that.

1. Add a new line at the end of your script, as shown below.

```javascript-#39
<i>if (player) { // it's the human player's turn
  const index = keyInSelect(strength, question)
  console.log(
    "index:", index,
    "strength:", strength[index]
  )
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}</i>

<b>length = length - index</b>
```

2. Launch your game with `node main.js`
3. Press `Y`
4. Press `3`, to hit the nail hard.

<details class="trouble" open>
<summary>index is not defined</summary>
Here's the error that you will see:

```tex-w
<i>-===========| The nail is 12 units long.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
index: 2 strength: hard
</i><b>/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:51
length = length - index
                  ^

ReferenceError: index is not defined
    at Object.<anonymous> (/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:51:19)</b>
```

In fact, there will be more information printed in the Terminal, but the key information is shown above.

</details>

**"But..."** I hear you say, **"... `index` _is_ defined. Right there on line 40. Look!"**

```javascript-#39
<i>if (player) { // it's the human player's turn
  </i><b>const index = keyInSelect(strength, question)</b><i>
  console.log(
    "index:", index,
    "strength:", strength[index]
  )
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}

length = length - </i><b>index</b>
```

## Block scope

JavaScript sets up barriers between different blocks of code so that data in one block doesn't interfere with data from another. It uses curly braces (`{ ... }`) to do this. Humans do something similar with walls and fences and hedges.

![Fences and hedges to keep things safely in place](images/HausWildenrathGarten.jpg){data-title="File:HausWildenrathGarten.jpg" data-credits="[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/deed.en) by [Bodoklecksel](https://de.wikipedia.org/wiki/Benutzer:Bodoklecksel) | [source](https://commons.wikimedia.org/wiki/File:HausWildenrathGarten.jpg)"}

For JavaScript, the `index` that is _declared_ inside curly braces is _accessible_ only inside those curly braces. This is due to a concept called _scope_. Any time a variable is declared inside curly braces, the world outside those curly braces cannot touch it. See [MDN's documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block#block_scoping_rules_with_let_const_class_or_function_declaration_in_strict_mode) for more details.

```javascript-#39
<b>{</b><i> // it's the human player's turn
  const </i><b>index</b><i> = keyInSelect(strength, question)</i>
```
```js-s
// lines skipped //
```
```javascript-#45
<b>}</b>
```
```js-s
// lines skipped //
```
```javascript-#51
<i>length = length - </i><b>index</b>
```

It's like when you call your mother "Mum" (or whatever you call her) _within your family_, everyone knows who you are talking about. But if you hear a stranger on the street use the same word, you know that they are talking about someone else. Within the _scope_ of your family, "Mum" refers to a particular person. Outside the scope of your family, "Mum" means something different.

In the code above, the `index` on line 51 has not been declared using `const` or `let` or even `var`. So JavaScript gives you an error:

```tex-w
ReferenceError: index is not defined
```

## Fixing the problem
To tell the truth, `index` does not hold the right number. As you saw in section [17. Choosing a Number](#choosing-a-number), `index` refers to the position of the word `"hard"` inside the `strength` array, and positions in an array are counted starting from zero.

What you want is a number that is `index + 1`. Here's how you can create a variable called `force`, using `let`, and give it the value `index + 1`

```javascript-#33
<b>let force</b>

<i>console.log(rules)
let player = keyInYN(whoStarts)
console.log(clear.repeat(toDelete))
console.log(nail, prompt)

if (player) { // it's the human player's turn
  const index = keyInSelect(strength, question);
  console.log(
    "index:", index,
    "strength:", strength[index]
  )</i>
  <b>force = index + 1</b>
<i>
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}

length = length - </i><b>force</b>
```

Because you declare `force` using `let` _outside_ the curly braces:

* You can change its value
* It is also available _inside_ the curly braces

1. Edit your `main.js` script to add the references to `force`, as shown above.
2. Launch your game with `node main.js`
3. Press `Y`
4. Press `3`, to hit the nail hard.

<details class="trouble" open>
<summary>Assignment to constant variable</summary>
Now you get a new error:

```tex-w
<i>-===========| The nail is 12 units long.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
index: 2 strength: hard</i>
<b>/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:54
length = length - force
       ^

TypeError: Assignment to constant variable.
    at Object.<anonymous> (/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:54:8)</b>
```

This is my fault (but I did it on purpose). On line 22, I got you to declare `length` using `const`. This tells JavaScript that its value will never change.

```javascript-#22
const length    = 12
```

So, when on line 54, the script tries to set `length` to a different value...

```javascript-#54
length = length - force
```

... JavaScript complains.

</details>

<details class="challenge" open>
<summary>Can you solve "Assignment to constant variable" error?</summary>
What small change can you make to your script so that the "Assignment to constant variable" error no longer occurs?

<details class="solution">
<summary>Solution</summary>
You can simply declare the `length` variable using `let` instead of const.

```javascript-#22
let length    = 12
```

Now the output in the Terminal looks good. No errors.

```tex-w
-===========| The nail is 12 units long.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
index: 2 strength: hard
james@M1 Nail_It % 
```

Now it's time to redraw the nail.

</details>

</details>

</section>