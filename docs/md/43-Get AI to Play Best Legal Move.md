<!-- Get AI to Play Best Legal Move -->
<section
  id="get-ai-to-play-best-legal-move"
  aria-labelledby="get-ai-to-play-best-legal-move"
  data-item="Get AI to Play the Best Legal Move"
>
  <h2><a href="#get-ai-to-play-best-legal-move">Get AI to Play the Best Legal Move</a></h2>

As [Matt Parker explains](https://www.youtube.com/watch?v=9KABcmczPdg&t=291s), the winning strategy is to leave a multiple of 4 units when you complete your turn.

It [will always play only one marble]((https://www.youtube.com/watch?v=9KABcmczPdg&t=531s)) if it is in a losing position. This is a good strategy when playing against a human who doesn't understand the system, because the human has more marbles to make a mistake with. It's certainly the easiest strategy for a piece of plastic to use.

<details class="challenge" open>
<summary>#3 Get the AI to play the best legal move</summary>
The AI must choose a value for `force` between `1` and `3`, but it can't always choose to play `length % 4`. If `length % 4` is 0, you can make the AI hit the nail gently, so that it only becomes one unit shorter.

Here the AI starts in a losing position, so it plays gently:

```tex-w
<i>-===========| The nail is 12 units long.

</i><b>===========|  I hit the nail gently.</b>
```

But if the human player makes a mistake, the AI seizes the opportunity to win.

```tex-w
</i>==========|    You hit the nail gently.

</i><b>========|     I hit the nail firmly.</b>
```

After the AI's turn, the number of units left is a multiple of four. Whatever the human player does, the AI can play to restore a multiple of four:

```tex-w
<i>=====|        You hit the nail hard.

</i><b>====|         I hit the nail gently.</b>
```

After any move the human player can make, the AI is going to win:

```tex-w
<i>[1] gently
[2] firmly
[3] hard
[0] CANCEL</i>

How hard do you plan to hit? [1, 2, 3, 0]: </i>
```

<details class="hint">
<summary>Hints</summary>
1. You've tested something like `length % 4` in the Node IDE. Would this be useful here?
2. How do you prevent the AI from using `0` for `force`?
3. You've already seen `Math.min()` in this line of code:

   ```javascript
   force = Math.min(index + 1, length)
   ```
   
   You used this to make sure that `force` never became more    than was necessary to win, so that the text for the last hit    was properly aligned.
   
   It won't be a surprise that JavaScript also gives you [Math.   max()](https://developer.mozilla.org/en-US/docs/Web/   JavaScript/Reference/Global_Objects/Math/max)

4. You want to make sure that the value of `force` used by the AI is always at least `1`
5. You'll need to set `index` to `force - 1`, so that the correct value from the `strengths` array is used for the AI

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
    </i><b>force = Math.max(1, length % 4)
    index = force - 1</b><i>
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