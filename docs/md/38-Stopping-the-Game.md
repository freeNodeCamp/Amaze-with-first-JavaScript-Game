<!-- Stopping the Game -->
<section
  id="stopping-the-game"
  aria-labelledby="stopping-the-game"
  data-item="Stopping the Game"
>
  <h2><a href="#stopping-the-game">Stopping the Game</a></h2>
  
<details class="challenge" open>
<summary>#9 Can you stop the game early, before there is a winner?</summary>

If the human player presses `0` when asked how hard to hit, can you make the game end gracefully?

```tex-w
<i>-==============| The nail is 15 units long.

============|    You hit the nail hard.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: </i> <b>0

Thanks for playing!</b>
```

<details class="hint">
<summary>Hints</summary>
1. You can add a `const` variable called `endGame` with the text that you want to show when the game ends.
2. You can check if `index < 0` in the `if` statement for the player.
3. If so, you can `console.log(endGame)` and then call `process.exit()`
4. It might be tidier to remove the question that the player just decided not to answer.

</details>

<details class="solution">
<summary>Solution</summary>

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
</i><b>const endGame  = `Thanks for playing!
`</b><i>

const initial = 12 + Math.floor(Math.random() * 4)
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
    </i><b>if (index < 0) {
      console.log(clear.repeat(toDelete))
      console.log(endGame)
      process.exit()
    }</b><i>

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