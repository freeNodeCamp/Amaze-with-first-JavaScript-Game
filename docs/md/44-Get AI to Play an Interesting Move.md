<!-- Get AI to Play an Interesting Move -->
<section
  id="get-ai-to-play-an-interesting-move"
  aria-labelledby="get-ai-to-play-an-interesting-move"
  data-item="Get AI to Play an Interesting Move"
>
  <h2><a href="#get-ai-to-play-an-interesting-move">Get AI to Play an Interesting Move</a></h2>



<details class="challenge" open>
<summary>#3.1 Can you make the AI play randomly when it is stuck?</summary>
If the AI always hits gently when it is in a losing position, the human player might learn that always hitting hard can sometimes lead to victory.

You can make your code a little bit smarter than a piece of plastic. You can make the AI choose a random value for `force` if it finds itself in a losing position. This means that even a human player who knows the winning strategy will have to pay attention on each turn.

<details class="hint">
<summary>Hints</summary>
1. If `force` is `0`, what will `!force` be? (Try it in the Node IDE).
2. Can you create an `if () { }` statement that will only run if `force` is `0`?
3. If `Math.floor(Math.random() * 4)` gives you a number between `0` and `3`, can you imagine how to create a number between `1` and `3`?
4. If `Math.floor()` reduces a number to the next lower integer, can you imagine that there might be a method to raise a number to the next higher integer?
5. `Math.ceiling()` is not the answer to the last question. Programmers don't like typing. Try this Google search: [js Math.ceiling](https://www.google.com/search?q=js+Math.ceiling)
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
const win      = `
You win!
`
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
    </i><b>force = length % 4
    if (!force) {
      force = Math.ceil(Math.random() * 3)
    }</b><i>
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
console.log(win)</i>
```

</details>
</details>
</section>