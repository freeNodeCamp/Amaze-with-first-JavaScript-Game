<!-- Drawing the Nail -->
<section
  id="drawing-the-nail"
  aria-labelledby="drawing-the-nail"
  data-item="Drawing the Nail"
>
  <h2><a href="#drawing-the-nail">Drawing the Nail</a></h2>
  
So far, your `main.js` script simply prints out the rules and asks the human player if they want to start.

![Your game so far](images/useReadlineSync.webp)

Now you have seen enough JavaScript to know how to draw a nail in the Terminal and indicate how long it is. Yes. You have. You even know how to delete the rules of the game and the question about who is going to start.

As [Matt Parker explains](https://www.youtube.com/watch?v=9KABcmczPdg&t=291s), in a game with 12 tokens, the player who starts cannot win against someone (or something) that understands the logic of the game. So you can start by drawing a nail 12 units long, plus a flat head.

<details class="challenge" open>
<summary>Can you draw a nail?</summary>
Can you edit your `main.js` script so that it draws a nail after the human player answers the question about who is going to start?

Here's what you need to print to the Terminal, using `console.log()`

![A nail drawn in ASCII art](images/nailLength12.webp)

1. Reopen the Terminal which is active on your `Nail_It` directory.

<details class="trouble">
<summary>Need to change directory?</summary>
If you have only the `strings` directory open, run...

```tex-w
strings % <b>cd ../../</b>
james@M1 Nail_It % 
```

... to change directory to the grandparent of the `Nail_It/Tests/strings` directory.

</details>

2. Open `main.js` in VS Code's text editor.
3. Edit `main.js`.
4. To test if your edits are working as you expect, in a Terminal open on your `Nail_It` directory, run:

   ```tex-w
   node main.js
   ```

<details class="hint">
<summary>Hints</summary>
* You can use the [string concatenator operator `+`](https://www.freecodecamp.org/news/how-js-string-concatenation-works/) to join two strings together.
* You can use the string method `.repeat()` to generate a long string by repeating a shorter string.
* You can use `'\x1B[1A\x1B[K'` with `console.log()` to delete a line of text from the Terminal.
* If you use `console.log()` with two parameters, a space will automatically be added between the paramaters in the output.
* Remember to save your file before you run `node main.js`.

</details>

<details class="solution" open>
<summary>A simple solution</summary>
The simplest solution is just to replace the line `console.log("player:", player)` with the two lines highlighted below:

```javascript-w
<i>const readlineSync = require('readline-sync')
const whoStarts = `If you want to start, type Y.
If you want me to start press any other key. `

console.log(`Let's knock a nail into this computer!

* Each player takes a turn to hit the nail once.
* A player can hit the nail in one of three ways:
  gently, firmly, hard.
* Depending on the force used, the nail will be
  driven more or less deeply into the Terminal.
* The player who knocks the nail all the way in
  is the winner.

Are you ready?
`)

let player = readlineSync.keyInYN(whoStarts)</i>

<b>console.log('\x1B[1A\x1B[K'.repeat(14))
console.log("-" + "=".repeat(11) + "| The nail is 12 units long.")</b>
```

</details>

<details class="solution" open>
<summary>A better solution, using variables</summary>
The solution below allows you to change the value of the `length` variable. Not only will the length of the nail change, but the text given its length in units will change at the same time.

All the strings are defined at together at the beginning of the script, and the interactive commands are placed together at the end.

```javascript
<i>const readlineSync = require('readline-sync')
</i><b>const rules = </b><i>`Let's knock a nail into this computer!

* Each player takes a turn to hit the nail once.
* A player can hit the nail in one of three ways:
  gently, firmly, hard.
* Depending on the force used, the nail will be
  driven more or less deeply into the Terminal.
* The player who knocks the nail all the way in
  is the winner.

Are you ready?
`
const whoStarts = `If you want to start, type Y.
If you want me to start press any other key. `</i>
<b>const nailIs    = "The nail is "
const long      = " units long."
const length    = 15
const toDelete  = 14
const nail      = "-" + "=".repeat(length - 1) + "|"
const prompt    = nailIs + length + long

console.log(rules)</b>
<i>let player = readlineSync.keyInYN(whoStarts)</i><b>
console.log('\x1B[1A\x1B[K'.repeat(toDelete))
console.log(nail, prompt)</b>
```

Try setting `const length = 15` and run `node main.js` again. Do you see the advantage of using a variable to store the length?

Note that if you set `const toDelete = 13` then not all of the rules will be deleted:

```tex-w
<b>node main.js</b>
Let's knock a nail into this computer!

-==============| The nail is 15 units long.
```

</details>
</details>

</section>