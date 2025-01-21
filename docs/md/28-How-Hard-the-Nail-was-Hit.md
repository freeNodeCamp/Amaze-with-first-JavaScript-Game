<!-- How Hard the Nail was Hit -->
<section
  id="how-hard-the-nail-was-hit"
  aria-labelledby="how-hard-the-nail-was-hit"
  data-item="How Hard the Nail was Hit"
>
  <h2><a href="#how-hard-the-nail-was-hit">How Hard the Nail was Hit</a></h2>
  
  <details class="challenge" open>
  <summary>#2 Can you show how hard the solo player chose to hit the nail?</summary>

Here's what the Terminal should show when you have finished this challenge:
  
```tex-w
<i>-===========| The nail is 12 units long

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 2
-=========|</i> <b>You hit the nail firmly</b>
```

<details class="hint">
<summary>Hints:</summary>
1. In the last challenge, `prompt` was declared using `let`. This means that you can give a new value to `prompt`.
2. You can declare a new `const` variable to hold the part of the prompt that will always be the same.
3. You can use two (or more) parameters in `console.log()`. They will be separated by a space.

</details>

<details class="solution">
<summary>Solution</summary>

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
</i><b>const hit      = "You hit the nail "</b><i>

let length = 12
let nail   = "-" + "=".repeat(length - 1) + "|"
let prompt = nailIs + length + long
let force

console.log(rules)
let player = keyInYN(whoStarts)
console.log(clear.repeat(toDelete))
console.log(nail, prompt)

if (player) { // it's the human player's turn
  const index = keyInSelect(strength, question)
  force = index + 1
  </i><b>prompt = hit + strength[index] + "."</b><i>
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}

length = length - force
nail   = "-" + "=".repeat(length - 1) + "|"
console.log(nail, </i><b>prompt</b><i>)</i>
```

Again, this solution violates the DRY principle. The line `console.log(nail, prompt)` appears in two places. Remember that this should be fixed later.

</details>
</details>

</section>