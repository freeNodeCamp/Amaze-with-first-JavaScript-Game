<!-- Showing the Winning Situation -->
<section
  id="showing-the-winning-situation"
  aria-labelledby="showing-the-winning-situation"
  data-item="Showing the Winning Situation"
>
  <h2><a href="#showing-the-winning-situation">Showing the Winning Situation</a></h2>
  
<details class="challenge" open>
<summary>#5 Can you show the winning situation?</summary>
In the last challenge, your code stopped working when `length` was reduced to `0` or less.

Now can you add some code after the end of the `while` loop that will show the final state and declare the human player the winner?

Below you can see how the Terminal might look when you have completed this challenge. Note that the final hit can be stronger than necessary.

```tex-w
<i>-===========|  The nail is 12 units long.

-==========|  You hit the nail gently.

-========|  You hit the nail firmly.

-=====|  You hit the nail hard.

-===|  You hit the nail firmly.

-==|  You hit the nail gently.

-|  You hit the nail firmly.</i>

<b>| You hit the nail hard.

You win!</b>
```

<details class="hint">
<summary>Hints</summary>

1. You will need to clear the question out of the Terminal
2. The value for `prompt` set in line 48 will be correct
3. You can create a new `const` variable to contain the text "You win!"
4. If you use backticks (`` ` ``) around your text, you can ensure that there is a blank line both before and after it.

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
</i><b>const win      = `
You win!
`</b><i>

let toDelete = 14
let length   = 12
let prompt   = nailIs + length + long
let force
let nail

console.log(rules)
let player = keyInYN(whoStarts)

while (length > 0) {
  nail   = "-" + "=".repeat(length - 1) + "|"
  console.log(clear.repeat(toDelete))
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

  length = length - force
}</i>

<b>console.log(clear.repeat(toDelete))
console.log("|", prompt)
console.log(win)</b>
```

</details>
</details>
</section>