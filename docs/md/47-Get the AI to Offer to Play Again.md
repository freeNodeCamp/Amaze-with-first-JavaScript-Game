<!-- Get the AI to Offer to Play Again -->
<section
  id="get-the-ai-to-offer-to-play-again"
  aria-labelledby="get-the-ai-to-offer-to-play-again"
  data-item="Get the AI to Offer to Play Again"
>
  <h2><a href="#get-the-ai-to-offer-to-play-again">Get the AI to Offer to Play Again</a></h2>
  
<details class="challenge" open>
<summary>#5 Get your friends to lose constantly against your game</summary>
If your friends play this game once and lose, they might just say "Cool game, bro!" and move on to something else. If the game offers them a chance for revenge, they might continue playing.

Here's how your Terminal should look after you complete this last challenge:

```tex-w
<i>=|            You hit the nail hard.

|             I hit the nail gently.

I win!</i>

<b>Do you want to play again?
(Type Y for Yes, N for No): </b>
```
</details>

## A more complicated challenge

This challenge is not so easy, so I won't hide the hints. I'll walk you through it step by step.

## `keyInYNStrict()`

You've already used `readline-sync`'s method `keyInYNS()`. This returns `true` if the player presses the `Y` key and falsy value if they press any other. This is fine for starting the game. The game will start whatever key the player chooses to press.

When you ask if the player wants to _end_ the game, you don't want the game to stop unexpectedly. You want to make sure that the player _explicitly_ presses the `N` key to bring the game to an end.

`readline-sync` provides another method, `keyInYNStrict()`, which does just this.

You'll have to `require` this new method explicitly at the beginning of your script:

```javascript-
<i>const {
  keyInYN,
  keyInSelect</i><b>,
  keyInYNStrict</b><i>
} = require('readline-sync')</i>

```

## The `options` object

Back in section [15. Working with keyInYN](#working-with-keyinyn), you did some tests with the `options` object.

The object looks like this:

```javascript-#
const options   = { guide: false }
```

If you use it with `keyInYN()` or `keyInYNStrict()`, it hides the default text ` [y/n]` that `readline-sync` wants to show. It makes your game look neater.

```javascript-#51
let player = keyInYN(whoStarts, options)
```

## A string invitation to play again
You'll need to create a variable to contain the string that you will print in the Terminal when the game is over. You could do something like this:

```javascript
const replay = `
Do you want to play again?
(Type Y for Yes, N for No): `
```

## Alternating players

If the same player starts each time, the game is not so interesting. When the game first begins, you can declare a variable with `let` which indicates who will start first next time:

```javascript-w
<i>let player = keyInYN(whoStarts, options)</i>
<b>let nextPlayer = !player</b>
```

## A second `while` loop

You'll need to wrap your current game inside a second `while` loop. If you create a variable called `playing`, you can keep looping in the outer loop so long as `playing` is true. Here's a simplified version of how this can work.

```javascript
let playing   = true

while (playing) {
  // Initialize a new game

  while (length > 0) {   
    // Your current game goes here
  }

  // Somebody won. Ask the player if they want to play again
  playing    = keyInYNStrict(replay, options)
```

## Initializing a new game

The code that you currently use to set up the game will need to be inside the `while (playing) { }` loop, so that a new game is created each time.

```javascript-#
<b>while (playing) {
  const initial = 12 + Math.floor(Math.random() * 4)
  let length    = initial
  let prompt    = nailIs + length + long
  let started   = false</b>

  <i>while (length > 0) {</i>
```
```javascript-s
// Your current code goes here //
```
```javascript-#
  }
```
```javascript-s
// Preparing to play again //
```
```javascript-#
<i>}</i>
```

## When someone wins

After the game declares the winner of the current game, you will need to:

1. Ensure that play alternates between the players
2. Prepare to clear the old game if a new game starts
3. Ask if the player if they want to play again
4. Print a farewell message if they decide to quit.

```javascript-#
  <i>console.log(clear.repeat(toDelete))
  console.log("|", prompt)
  console.log(winner[player + 0])</i>

  <b>// Get ready to play again, alternating between
  // player and AI
  player     = nextPlayer
  nextPlayer = !nextPlayer

  // Prepare to delete the previous game
  toDelete   = 23

  // Ask the player if they want to play again
  playing    = keyInYNStrict(replay, options)

  if (!playing) {
    console.clear()
    console.log(endGame)
  }</b>
}
```

<details class="note" open>
<summary>All the code... but where to put it?</summary>
I've given you all the code that you need to solve this challenge. Before you look at the complete solution below, do your best to find where these pieces of code should go.

</details>


<details class="solution">
<summary>Solution</summary>

```javascript-
<i>const {
  keyInYN,
  keyInSelect</i><b>,
  keyInYNStrict</b><i>
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
</i><b>const options   = { guide: false }</b><i>
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
const winner   = [`
You win!
`,
`
I win!
`]
</i><b>const replay = `
Do you want to play again?
(Type Y for Yes, N for No): `</b><i>
const endGame  = `Thanks for playing!
`
let toDelete  = 14
</i><b>let playing   = true</b><i>
let index
let force
let nail

console.log(rules)
let player = keyInYN(whoStarts</i><b>, options</b><i>)
</i><b>let nextPlayer = !player</b><i>

while (playing) {
  </i><b>const initial = 12 + Math.floor(Math.random() * 4)
  let length    = initial
  let prompt    = nailIs + length + long
  let started   = false</b><i>

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
  console.log(winner[player + 0])

  </i><b>// Get ready to play again, alternating between
  // player and AI
  player     = nextPlayer
  nextPlayer = !nextPlayer

  // Prepare to delete the previous game
  toDelete   = 23

  // Ask the player if they want to play again
  playing    = keyInYNStrict(replay, options)

  if (!playing) {
    console.clear()
    console.log(endGame)
  }</b><i>
}</i>
```

</details>
</details>
</section>