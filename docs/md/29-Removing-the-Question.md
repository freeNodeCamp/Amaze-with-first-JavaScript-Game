<!-- Removing the Question -->
<section
  id="removing-the-question"
  aria-labelledby="removing-the-question"
  data-item="Removing the Question"
>
  <h2><a href="#removing-the-question">Removing the Question</a></h2>
  
<details class="challenge" open>
<summary>#3 Can you remove the question after it has been answered?</summary>

The Terminal would look better if the question were removed, and just the result of answering the question were shown.

```tex-w
-===========| The nail is 12 units long.

-==========| You hit the nail gently.
```

<details class="hint">
<summary>Hints</summary>
1. You originally set `const toDelete = 14`, so that you could use...

   ```javascript-#
   console.log(clear.repeat(toDelete))
   ```

   ... to remove the rules that are shown at the beginning.

2. How many lines do you need to delete for the question?
3. At what point should you delete the question lines?
4. Is `const` still a good way to declare `toDelete`?

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
const clear     = "\x1B[1A\x1B[K"
const strength  = [
  'gently',
  'firmly',
  'hard'
]
const question = 'How hard do you plan to hit?'
const hit      = "You hit the nail "

</i><b>let toDelete = 14</b><i>
let length   = 12
let nail     = "-" + "=".repeat(length - 1) + "|"
let prompt   = nailIs + length + long
let force

console.log(rules)
let player = keyInYN(whoStarts)
console.log(clear.repeat(toDelete))
console.log(nail, prompt)

if (player) { // it's the human player's turn
  const index = keyInSelect(strength, question)
  force = index + 1
  prompt = hit + strength[index] + "."
  </i><b>toDelete = 7</b><i>
} else { // it's the AI's turn to play
  console.log(`The AI is not ready yet.
You'll have to play solo.`)
  player = true
  force = 0
}

length = length - force
nail   = "-" + "=".repeat(length - 1) + "|"
</i><b>console.log(clear.repeat(toDelete))</b><i>
console.log(nail, prompt)</i>
```


</details>
</details>
</section>