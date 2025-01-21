<!-- Nails with Random Lengths -->
<section
  id="nails-with-random-lengths"
  aria-labelledby="nails-with-random-lengths"
  data-item="Nails with Random Lengths"
>
  <h2><a href="#nails-with-random-lengths">Nails with Random Lengths</a></h2>
  
<details class="challenge" open>
<summary>#8 Can you give the nail a different length each time?</summary>

Can you choose a nail length in the range 12 - 15 units, to make the game more interesting (when the AI starts to play)? For example:

```tex-w
<i>-===========| The nail is </i><b>15</b><i> units long.</i>
```
</details>

## Math.random()

If you search on Google for [js random number](https://www.google.com/search?q=js+random+number), you can find a link to [MDN's article on Math.random()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random). This includes a **Try it** demo

![Click on the Run button to see new random numbers each time](images/TryRandom.webp)

There are three things to note here:

1. `Math.random()` gives a number in the range between `0` and _almost_ `1`. It will never return the value `1`.
2. If you multiply this number-between-0-and-almost-1 by any number, you will get a number between `0` and _almost_ the number you multiplied by.
3. [`Math.floor()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) takes a number and returns the next lowest integer. So `1.999` becomes `1`, and so does `1.001`

Using these three ideas together, you can create an integer (whole number) which is in the range `0` to `n - 1`, where `n` is the number that you multiply `Math.random()` by.

<details class="sandbox" open>
<summary>Try in the Node IDE</summary>
To get a number between 12 and 15, you could use:

```javascript
12 + Math.floor(Math.random() * 4))
```

1. In a new Terminal window, open the Node Interactive Development Environment (IDE) by typing:

```tex-w
node
```

2. Enter the expression `12 + Math.floor(Math.random() * 4)` and press Enter

```tex-w
<b>node</b>
<i>Welcome to Node.js v23.1.0.
Type ".help" for more information.</i>
> <b>12 + Math.floor(Math.random() * 4)</b>
13
```

The IDE will give you an number between `12` and `15` (or `12 + (4-1)`).

3. Press the Up Arrow on your keyboard to show the expression again, and press Enter.
4. Repeat step 3 many times.

You should get a different value most times, but sometimes you'll get the same value twice. That's how random it is.

```tex-w
> <b>12 + Math.floor(Math.random() * 4)</b>
14
> <b>12 + Math.floor(Math.random() * 4)</b>
14
> <b>12 + Math.floor(Math.random() * 4)</b>
15
> <b>12 + Math.floor(Math.random() * 4)</b>
15
> <b>12 + Math.floor(Math.random() * 4)</b>
12
```

You can try other expressions with `Math.random()` and `Math.floor()`, to see how they work together and separately.

</details>

<details class="challenge" open>
<summary>Choose a random nail length</summary>
 
<details class="hint">
<summary>Hint</summary>
Instead of `initial = 12`, you can use the new trick that you have learnt with `Math.random()

</details>

<details class="solution">
<summary>Solution</summary>

You just need to change one line.

```javascript-
<i>const {
  keyInYN,
  keyInSelect
} = require('readline-sync')

const rules = `Let's knock a nail into this computer!

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
If you want me to start press any other key. `
const nailIs    = "The nail is "
const long      = " units long."
const clear     = "\x1B[1A\x1B[K"
const strength  = [
  'gently',
  'firmly',
  'hard'
]
const question = 'How hard do you plan to hit?'
const hit      = "You hit the nail "
const win      = `
You win!
`

const initial = 12 </i><b>+ Math.floor(Math.random() * 4)</b><i>
let length    = initial
let toDelete  = 14
let prompt    = nailIs + length + long
let started   = false
let force
let nail

console.log(rules)
let player = keyInYN(whoStarts)

while (length > 0) {
  if (!started) {
    nail = "-" + "=".repeat(length - 1) + "|"
  } else {
    nail = "=".repeat(length) + "|"
  }

  console.log(clear.repeat(toDelete))
  console.log(nail, prompt)

  if (player) { // it's the human player's turn
    const index = keyInSelect(strength, question)
    force = Math.min(index + 1, length)
    prompt = " ".repeat(initial - length + force)
           + hit + strength[index] + "."
    toDelete = 7
  } else { // it's the AI's turn to play
    console.log(`The AI is not ready yet.
  You'll have to play solo.`)
    player = true
    force = 0
  }

  length = length - force
  started = true
}

console.log(clear.repeat(toDelete))
console.log("|", prompt)
console.log(win)</i>
```
 
 
 </details>

</details>

</section>