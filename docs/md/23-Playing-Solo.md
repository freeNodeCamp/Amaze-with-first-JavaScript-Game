<!-- Playing Solo -->
<section
  id="playing-solo"
  aria-labelledby="playing-solo"
  data-item="Playing Solo"
>
  <h2><a href="#playing-solo">Playing Solo</a></h2>
  
Your game asks the human player if they want to start. But the AI is not ready to play yet, so, for the time being, you can get the human player to play solo.

Remember, back in section [16. A Few Words about `true` and `false`](#true-and-false), you saw this `if` statement with two branches?

```javascript-w
if (player) { // it's the human player's turn
  
} else { // it's the AI's turn to play
  // TODO: choose the number between 1 and 3 to ensure AI wins
  // (if possible)
}
```

You can add this at the end of your` main.js` file, with a placeholder action to the `else` branch (where the human player chose not to start):

```javascript-#28
if (player) { // it's the human player's turn
  // TODO: ask the human player for a number between 1 and 3

} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}
```

<details class="question" open>
<summary>Placeholder for AI</summary>
Question: What do you expect will happen if you run your script and press any key except `Y`?

Answer: The game will print the string in the Terminal. And stop.

```tex-w
<b>node main.js</b>

-===========| The nail is 12 units long.
The AI is not ready yet. You'll have to play solo.
james@M1 Nail_It % 
```

Note that, for now, the lines...

```javascript-#33
player = true
force = 0
```

... have no effect. (So why are they there? 🤔)

</details>

Until you have added real code for the AI, just remember to press `Y` each time you launch the game.

<details class="challenge" open>
<summary>Ask the human player how hard to hit</summary>
You already know how to ask the human player how hard they plan to hit the nail. Where have you done this before?

Can you copy and paste the code that you wrote earlier into the the first branch of the `if` statement?

<details class="hint">
<summary>Hint</summary>
You wrote a script called `keyInSelect.js`, which originally asked about Elephants.

</details>

<details class="solution">
<summary>A copy and paste solution</summary>
The simplest solution is to copy and paste the code from `keyInSelect.js` into the first branch of the `if` statement:

```javascript-#24
<i>let player = readlineSync.keyInYN(whoStarts)
console.log('\x1B[1A\x1B[K'.repeat(toDelete))
console.log(nail, prompt)

if (player) { // it's the human player's turn
  </i><b>const { keyInSelect } = require('readline-sync')
  const strength = [
    'gently',
    'firmly',
    'hard'
  ]
  const question = 'How hard do you plan to hit?'
  const index = keyInSelect(strength, question)
  console.log(
    "index:", index,
    "strength:", strength[index]
  )</b><i>
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}</i>
```
Now, if you run your script and press `Y`, you'll be asked how hard you plan to hit:

![The game logs your answer to the question, then stops](images/hitHowHard.webp)

The game now asks the question and logs your answer to it, but then stops.

<details class="question" open>
<summary>Do you really need to require('readline-sync') twice?</summary>
Because this solution used copy and paste, there is a _second_ instruction to `require('readline-sync')`

```javascript-#29
  const { keyInSelect } = require('readline-sync')
```

The Don't Repeat Yourself principle (DRY) recommends that you never repeat code if you can help it. Can you think of a better way to handle the way the `keyInSelect()` method is loaded?
</details>

</details>


<details class="solution">
<summary>A more elegant solution</summary>
This second solution has just the same effect, but it is more elegant:

* The `keyInYN` and `keyInSelect` methods of `readline-sync` are loaded explicitly at the beginning of the script.
* The strings used to display text in the Terminal have been placed together with all the other strings, so that it will be easy to find them if they need to be updated or translated.
* The string `"\x1B[1A\x1B[K"` has been assigned to its own variable

**You should adopt the solution below, which is why I have given the complete code listing.**

```javascript-
<b>const {
  keyInYN,
  keyInSelect
} = require('readline-sync')</b><i>

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
const length    = 12
const toDelete  = 14
const nail      = "-" + "=".repeat(length - 1) + "|"
const prompt    = nailIs + length + long</i><b>
const clear     = "\x1B[1A\x1B[K"
const strength  = [
  'gently',
  'firmly',
  'hard'
]
const question = 'How hard do you plan to hit?'</b><i>

console.log(rules)
let player = </i><b>keyInYN</b><i>(whoStarts)
console.log(</i><b>clear</b><i>.repeat(toDelete))
console.log(nail, prompt)

if (player) { // it's the human player's turn
  </i><b>const index = keyInSelect(strength, question)
  console.log(
    "index:", index,
    "strength:", strength[index]
  )</b><i>
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}</i>
```

</details>
</details>

</section>