<!-- Don't Show the Point of the Nail -->
<section
  id="dont-show-the-point-of-the-nail"
  aria-labelledby="dont-show-the-point-of-the-nail"
  data-item="Don't Show the Point of the Nail"
>
  <h2><a href="#dont-show-the-point-of-the-nail">Don't Show the Point of the Nail</a></h2>

<details class="challenge" open>
<summary>#6. Can you show the point of the nail only at the start?</summary>
```tex-w
<i>-===========|  The nail is 12 units long.

</i><b>=========|</b><i>  You hit the nail hard.

</i><b>=======|</b><i>  You hit the nail firmly.

</i><b>====|</b><i>  You hit the nail hard.

</i><b>==|</b><i>  You hit the nail firmly.

</i><b>=|</b><i>  You hit the nail gently.

| You hit the nail firmly.

You win!</i>
```

<details class="hint">
<summary>Hints</summary>
1. To solve this problem, you will need to tell JavaScript if a player has already chosen a value for `force`
2. You can create a new variable with `let` to hold this information
3. You could call your variable `started`, and give it the value `false` before the game begins
4. You can set `started` to `true` after the `if () {...} else {...}` statement, when you can be sure that one of the players will have chosen a value for `force`
5. You can create your own `if () {...} else {...}` statement to draw the nail with a point (`-`) if the game is not started, or without a point (only `=` characters) if the game has started.
6. You can use the logical not operator (`!`) to check if the game is not started.

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

let toDelete = 14
let length   = 12
let prompt   = nailIs + length + long</i>
<b>let started  = false</b>
<i>let force
let nail

console.log(rules)
let player = keyInYN(whoStarts)

while (length > 0) {</i>
  <b>if (!started) {</b>
    <i>nail = "-" + "=".repeat(length - 1) + "|"</i>
  <b>} else {
    nail = "=".repeat(length) + "|"
  }</b>

  <i>console.log(clear.repeat(toDelete))
  console.log(nail, prompt)

  if (player) { // it's the human player's turn
    const index = keyInSelect(strength, question)
    force = index + 1
    prompt = hit + strength[index] + "."
    toDelete = 7
  } else { // it's the AI's turn to play
    console.log(`The AI is not ready yet.
  You'll have to play solo.`)
    player = true
    force = 0
  }

  length = length - force</i>
  <b>started = true</b>
<i>}</i>

console.log(clear.repeat(toDelete))
console.log("|", prompt)
console.log(win)
```

</details>
</details>
</section>