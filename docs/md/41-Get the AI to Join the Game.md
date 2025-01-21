<!-- Get the AI to Join the Game -->
<section
  id="get-the-ai-to-join-the-game"
  aria-labelledby="get-the-ai-to-join-the-game"
  data-item="Get the AI to Join the Game"
>
  <h2><a href="#get-the-ai-to-join-the-game">Get the AI to Join the Game</a></h2>
  
<details class="challenge" open>
<summary>#1 Can you get the AI to join the game at all?</summary>

For now, the AI just lets you play. Can you make it print something into the Terminal to show that it exists? The simplest solution is to simply jump back to the beginning of the `while` loop after the AI's turn, which means that these lines will be executed a second time:

```javascript-#54
  console.log(clear.repeat(toDelete))
  console.log(nail, prompt)
```

The output you are looking for could be something like this:

```tex-w

-=============| The nail is 14 units long.

============|   You hit the nail firmly.
Say that again? I won't play yet.

============|   You hit the nail firmly.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 
```


<details class="hint">
<summary>Hints</summary>
1. Currently, the variable `player` is always set to `true`, to mean that it is the human player's turn to play. If the AI is to play you will need to set `player` to false.
2. The [logical not operator (`!`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT) can flip a truthy value to `false`.
3. Where is the best place to flip the value of `player`?
4. If the AI is not going to play, you'll need to make it choose `force = 0`, otherwise the nail will get shorter by itself. (Remember that I already set this for you earlier?)
5. The AI doesn't have to answer a question, so there will be no question lines to delete from the Terminal.
6. You should make the AI print something to the Terminal, just to show that it noticed that it had a turn.

</details>


<details class="solution">
<summary>Solution</summary>

You can achieve the result I show above with just three changes, as shown below.

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
const endGame  = `Thanks for playing!
`

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
    if (index < 0) {
      console.log(clear.repeat(toDelete))
      console.log(endGame)
      process.exit()
    }

    force = Math.min(index + 1, length)
    prompt = " ".repeat(initial - length + force)
           + hit + strength[index] + "."
    toDelete = 7
  } else { // it's the AI's turn to play
    </i><b>console.log("Say that again? I won't play yet.")
    toDelete = 0</b><i>
    force = 0
  }

  length = length - force
  started = true
  </i><b>player = !player</b><i>
}

console.log(clear.repeat(toDelete))
console.log("|", prompt)
console.log(win)</i>
```

</details>
</details>
</section>