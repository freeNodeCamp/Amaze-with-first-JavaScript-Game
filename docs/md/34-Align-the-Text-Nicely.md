<!-- Align the Text Nicely -->
<section
  id="align-the-text-nicely"
  aria-labelledby="align-the-text-nicely"
  data-item="Align the Text Nicely"
>
  <h2><a href="#align-the-text-nicely">Align the Text Nicely</a></h2>
  


<details class="challenge" open>
<summary>#7 Can you align all the text nicely?</summary>
Here's how the Terminal should look when you have completed this challenge:

```tex-w
<i>-===========| The nail is 12 units long.

==========|   </i><b>You hit the nail firmly.</b><i>

=========|    </i><b>You hit the nail gently.</b><i>

=======|      </i><b>You hit the nail firmly.</b><i>

====|         </i><b>You hit the nail hard.</b><i>

==|           </i><b>You hit the nail firmly.</b><i>

=|            </i><b>You hit the nail gently.</b><i>

|             </i><b>You hit the nail firmly.</b><i>

You win!</i>
```

<details class="hint">
<summary>Hints</summary>
1. Somehow, you are going to need to keep track of how much shorter the nail becomes each time it is hit.
2. One way to do this is to create a `const` variable which remembers the initial length of the nail.
3. Each time you hit the nail, you can calculate the difference between its initial length and its new length.
4. You can use `" ".repeat()` to create a string of space characters that is the same length as the difference between its initial length and the nail's new length
5. You can combine this string of `" "` space characters with the string `prompt`, before you use `console.log()` to show the `prompt`.
6. The very first time you show the nail (with its point), you won't need any extra spaces.

</details>

<details class="solution">
<summary>Almost a solution</summary>

The following solution works fine, unless you hit the nail too hard the last time. For example, if there is only one unit left, and you hit the nail hard, you apply a `force` of `3`, not `1`, and the text is pushed two extra spaces to the right.

```tex-w
<i>-===========| The nail is 12 units long.

=========|    You hit the nail hard.

======|       You hit the nail hard.

===|          You hit the nail hard.

=|            You hit the nail firmly.

|               </i><b>You hit the nail hard.</b><i>

You win!</i>
```

Here's the slightly buggy solution:

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
const win      = `
You win!
`

</i><b>const initial = 12
let length    = initial</b><i>
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
    force = index + 1
    </i><b>prompt = " ".repeat(initial - length + force)
           + hit + strength[index] + "."</b><i>
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

To fix the bug in the solution above, you're going to have to find a way to reduce the value of `force` to just the right amount to drive the nail home. Here's a Google query that might lead you in the right direction: [js find minimum](https://www.google.com/search?q=js+find+minimum). <<< Click on it to see where it leads you.

<details class="solution">
<summary>Fix the bug</summary>
To fix this glitch, you can use JavaScript's built-in global [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) library. This contains a [`.min()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min) that you can use to reduce `force` to just the right amount to drive the nail home.

You'll need to change just one line of your code.

```javascript-#57
    force = Math.min(index + 1, length)
```

</details>

</details>

<details class="note" open>
<summary>`js`, or searching online for "JavaScript"</summary>
In the Google search query I used above, I wrote `js` and not JavaScript. There are many many JavaScript programmers who work for search-engine companies, and they all like to type as little as possible. As a result, their algorithms understand that the extension `js` refers to JavaScript, and you don't have to type the full name each time you make a query.

</details>

</section>