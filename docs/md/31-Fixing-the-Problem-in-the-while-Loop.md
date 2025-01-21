<!-- Fixing the Problem with the while Loop -->
<section
  id="fixing-the-problem-with-the-while-loop"
  aria-labelledby="fixing-the-problem-with-the-while-loop"
  data-item="Fixing the Problem with the while Loop"
>
  <h2><a href="#fixing-the-problem-with-the-while-loop">Fixing the Problem with the `while` Loop</a></h2>
  
When `length` reaches `0`, the expression `length - 1` takes on the value `-1`. And the [string method `.repeat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat) can't handle negative numbers. If you hit the nail too hard the last time, then `length` itself can become negative.

So you need to make sure that the calculation for `nail` never happens _after_ length has been reduced to `0` or less.

## `length` is tested at the beginning of each loop

In your current code, line 55 changes the value of `length` inside the `while` loop, and line 56 uses this new value.

```javascript-#55
length = length - force
nail   = "-" + "=".repeat(length - 1) + "|"
```

Before the `while` loop even starts, your code calculates and prints a value for `nail`:

```javascript-#33
<b>let nail     = "-" + "=".repeat(length - 1) + "|"</b>
<i>let prompt   = nailIs + length + long
let force

console.log(rules)
let player = keyInYN(whoStarts)
console.log(clear.repeat(toDelete))</i>
<b>console.log(nail, prompt)</b>
```

<details class="question" open>
<summary>What if you put these earlier lines inside the `while` loop?</summary>

If you move the earlier lines that clear the Terminal and draw the nail _inside_ the `while` loop, you don't need to repeat them at the _end_ of the loop.

If `length` gets set to `0` inside the `while` loop, it will just not run again. The value of `length - 1` can never become negative. (SPOILER: Or can it?)

```javascript-#31
<i>let toDelete = 14
let length   = 12
let prompt   = nailIs + length + long
</i><b>let nail</b><i>
let force

console.log(rules)
let player = keyInYN(whoStarts)

while (length) {
  </i><b>console.log(clear.repeat(toDelete))
  nail = "-" + "=".repeat(length - 1) + "|"
  console.log(nail, prompt)</b>
```
```js-s
// lines skipped //
```
```javascript-#55
  length = length - force
  <s>nail   = "-" + "=".repeat(length - 1) + "|"</s>
  <s>console.log(clear.repeat(toDelete))</s>
  <s>console.log(nail, prompt)</s>
}
```

</details>

## The fix: first attempt

1. Edit your `main.js` script to remove lines 56 - 58, and to adjust the code, as shown in the listing above.
2. Run

```bash-w
node main.js
```
3. Press `Y`
4. Press the `3` key on your keyboard every time you are asked how hard you want to hit. If all goes well, your Terminal should look like this:

```tex-w
-===========| The nail is 12 units long.

-========| You hit the nail hard.

-=====| You hit the nail hard.

-==| You hit the nail hard.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
james@M1 Nail_It % 
```

Your game stops when `length` becomes `0`, and the result of your last strike is not shown.

## Showing that the fix is broken

1. Repeat steps 1 - 3 above,
2. Press `2` the _first_ time you are asked how hard you want to hit
3. Press `3` every other time.

It seems that the `length - 1` error is still present.

<details class="trouble" open>
<summary>Invalid count value: -3</summary>
```tex-w
-===========| The nail is 12 units long.

-=========| You hit the nail firmly.

-======| You hit the nail hard.

-===| You hit the nail hard.

-| You hit the nail hard.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:41
  nail   = "-" + "=".repeat(length - 1) + "|"
                     ^

RangeError: Invalid count value: -3
    at String.repeat (&lt;anonymous&gt;)
    at Object.&lt;anonymous&gt; (/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:41:22)
```

</details>

## Troubleshooting with the debugger

1. In `main.js`, remove the existing breakpoint
2. Add a conditional breakpoint on line 41:

![Add a breakpoint on line 41](images/breakpoint41.webp)

3. Give it the condition `length < 0`. This will become `true` if `length` becomes `-1`, `-2` or any other negative value

4. Start the debugger.
5. In the Terminal, press `Y` when asked
6. As before, press `2` the _first_ time you are asked how hard you want to hit
7. Press `3` every other time.

![`length` can become negative](images/length-2.webp)

When `length` is reduced to `1`, and you press the `3` key, `length - force` evaluates to `-2`. 

<details class="warn" open>
<summary>Negative numbers are truthy</summary>
In section [16. A Few Words about `true` and `false`](#true-and-false), I wrote:

> JavaScript treats the number `0`, the empty string `""` and a few other empty values as `false`. These values are said to be _falsy_.
> 
> Conversely, JavaScript treats anything that is not `false` or `0` or empty as `true`... even the word `"false"`, because `"false"` contains letters, so it's not empty. **Anything that is not `false` or falsy is _truthy_.**

As you have just discovered, negative numbers are neither `0` nor `false`, so JavaScript treats them as _truthy_. If you want the `while` loop to stop when the value for `length` is `0` _or less_, you need to change the condition, to while (length > 0)`, which you can read as "while `length` is greater than zero".

</details>

<details class="solution" open>
<summary>Can you fix it yourself?</summary>
Can you fix this issue yourself?

Hint: You only need to add four characters to `main.js` (and two of them are optional spaces).


<details class="solution">
<summary>Solution</summary>
Here's the full script of `main.js` with the required changes.

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

let toDelete = 14
let length   = 12
let prompt   = nailIs + length + long
</i><b>let nail</b><i>
let force

console.log(rules)
let player = keyInYN(whoStarts)

while (</i><b>length > 0</b><i>) {
  </i><b>nail = "-" + "=".repeat(length - 1) + "|"
  console.log(clear.repeat(toDelete)) 
  console.log(nail, prompt)</b><i>

  if (player) { // it's the human player's turn
    const index = keyInSelect(strength, question);
    force = index + 1
    prompt = hit + strength[index]
    toDelete = 7

  } else { // it's the AI's turn to play
    console.log(`The AI is not ready yet.
  You'll have to play solo.`)
    player = true
    force = 0
  }

  length = length - force
}</i>
```

Now when you run your script, the output in the Terminal should look something like this, even if you hit too hard the last time:

```tex-w
-===========| The nail is 12 units long.

-=========| You hit the nail firmly.

-======| You hit the nail hard.

-===| You hit the nail hard.

-| You hit the nail hard.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
```

</details>
</details>



<details class="tip" open>
<summary>DRY code is good</summary>
This problem was created because the same lines of code were being executed in two different places. The original code broke the Don't Repeat Yourself principle.

The problem was solved by rethinking the code so that no repetition was necessary.

At the very end of this guide, you will discover _functions_, which are reusable blocks of code where you can create functionality that you write in one place, and can use from many different places.

</details>
</section>