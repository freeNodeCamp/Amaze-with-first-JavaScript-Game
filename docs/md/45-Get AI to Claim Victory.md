<!-- Get AI to Claim Victory -->
<section
  id="get-ai-to-claim-victory"
  aria-labelledby="get-ai-to-claim-victory"
  data-item="Get AI to Claim Victory"
>
  <h2><a href="#get-ai-to-claim-victory">Get AI to Claim Victory</a></h2>
  
<details class="challenge" open>
<summary>#4 Can you make the AI claim victory when it wins?</summary>

Currently, when the game is over, the last line that is printed in the Terminal is "You win!", even if the AI was the real winner.

Your challenge here is to get the AI to print "I win!" when it beats you:

```tex-w
====|            I hit the nail hard.

===|             You hit the nail gently.

|                I hit the nail hard.</i>

<b>I win!</b>
```

<details class="hint">
<summary>Hints</summary>
1. You created an array called `players` with the value `[ "I", "You" ]`. Can you use that here?
2. Or would it be better to create a new array with the exact texts for the winners?
3. The last line inside the `while` loop is 
   ```javascript-#86
     player = !player
   ```
   This means that when your script exits the `while` loop, if the AI is the winner, `player` will be `true`. If the human player is the winner, `player` will be `false`. This is the opposite to what happens inside the `while` loop.
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
const players  = [ "I", "You" ]
const hit      = " hit the nail "
</i><b>const winner   = [`
You win!
`,
`
I win!
`]</b><i>
const endGame  = `Thanks for playing!
`

const initial = 12 + Math.floor(Math.random() * 4)
let length    = initial
let toDelete  = 14
let prompt    = nailIs + length + long
let started   = false
let index
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
    index = keyInSelect(strength, question)
    if (index < 0) {
      console.log(clear.repeat(toDelete))
      console.log(endGame)
      process.exit()
    }

    force = Math.min(index + 1, length)
    toDelete = 7
  } else { // it's the AI's turn to play
    toDelete = 0
    force = length % 4
    if (!force) {
      force = Math.ceil(Math.random() * 3)
    }
    index = force - 1
  }

  prompt = " ".repeat(initial - length + force)
         + players[player + 0] + hit + strength[index] + "."

  length = length - force
  started = true
  player = !player
}

console.log(clear.repeat(toDelete))
console.log("|", prompt)
</i><b>console.log(winner[player + 0])</b>
```

</details>
</details>
</section>