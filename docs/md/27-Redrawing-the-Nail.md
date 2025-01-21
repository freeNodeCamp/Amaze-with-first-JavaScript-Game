<!-- Redrawing the Nail -->
<section
  id="redrawing-the-nail"
  aria-labelledby="redrawing-the-nail"
  data-item="Redrawing the Nail"
>
  <h2><a href="#redrawing-the-nail">Redrawing the Nail</a></h2>
  

  
<details class="challenge" open>
<summary>#1 <After the nail is hit, can you show it at its new length?</summary>
Here's what you need to print in the Terminal:

```tex-w
<i>-===========| The nail is 12 units long

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3</i>
<b>-========|</b>
```

<details class="hint">
<summary>Hints</summary>
1. Line 24 creates a `const` variable called `nail`. 

```javascript-#24
const nail      = "-" + "=".repeat(length - 1) + "|"
```

Can you declare `nail` in a different way, so that you can give it a new value?

2. Line 55 calculates a new value for `length`

```javascript-#55
length = length - force
```

Can you calculate a new value for `nail` based on the new `length`?

3. How will you show this new `nail` in the Terminal?

</details>

<details class="solution">
<summary>Solution</summary>
The solution below contains some refactoring.

1. I've moved all the `let` variable declarations together
2. I've  moved the declaration of the `prompt` variable after the declaration of `length`, because `prompt` uses `length`.
3. I've also declared `prompt` with `let`. This might be a clue for challenge N° 2.
4. I've removed the `console.log()` statement from the first branch of the `if` statement, because it's not needed anymore.

```javascript
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
const toDelete  = 14
const clear     = "\x1B[1A\x1B[K"
const strength  = [
  'gently',
  'firmly',
  'hard'
]
const question = 'How hard do you plan to hit?'

</i><b>let length = 12
let nail   = "-" + "=".repeat(length - 1) + "|"
let prompt = nailIs + length + long
let force</b><i>

console.log(rules)
let player = keyInYN(whoStarts)
console.log(clear.repeat(toDelete))
console.log(nail, prompt)

if (player) { // it's the human player's turn
  const index = keyInSelect(strength, question)
  force = index + 1
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}

length = length - force
</i><b>nail   = "-" + "=".repeat(length - 1) + "|"
console.log(nail)</b>
```

Notice that this code does not follow the DRY (Don't Repeat Yourself) principle. The line `nail = "-" + "=".repeat(length - 1) + "|"` occurs in two different places. You'll fix this in one of the future challenges.

</details>

</details>


</section>