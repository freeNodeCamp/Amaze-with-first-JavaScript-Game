<!-- Never Repeat a Trick -->
<section
  id="never-repeat-a-trick"
  aria-labelledby="never-repeat-a-trick"
  data-item="Never Repeat a Trick?"
>
  <h2><a href="#never-repeat-a-trick">Never Repeat a Trick?</a></h2>
  
One rule of illusionists is never to repeat a trick. If the audience knows what is going to happen, they will watch more closely, and they might notice something the illusionist does not want them to see.

But the `slider.js` example allowed you to press the `Z` and the `X` keys multiple times. Each time, the `0` moved one step to the left or right. How did the code do that?

This is an important question, because, in your game, you are going to ask the player to hit the nail several times.

So now that you know what the <s>illusionist</s> code is going to do, you can watch more closely and see if you can notice the trick:

```javascript-
<i>var readlineSync = require('readline-sync'),
  MAX = 60, MIN = 0, value = 30, key;
console.log('\n\n' + (new Array(20)).join(' ') +
  '[Z] <- -> [X]  FIX: [SPACE]\n');
</i><b>while (true) {</b><i>
  console.log('\x1B[1A\x1B[K|' +
    (new Array(value + 1)).join('-') + 'O' +
    (new Array(MAX - value + 1)).join('-') + '| ' + value);
  key = readlineSync.keyIn('',
    {hideEchoBack: true, mask: '', limit: 'zx '});
  if (key === 'z') { if (value > MIN) { value--; } }
  else if (key === 'x') { if (value < MAX) { value++; } }
  else { </i><b>break</b><i>; }</i>
<b>}</b>
```

## A `while` loops
The slider example uses a [`while` loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while).

It loops around, checking if you have typed in one of the characters `Z`, `X` or `space`. If you typed `Z` or `X`, it updates the position of the `0` and the number on the right. If you pressed the `space` bar, it `breaks` out of the loop and stops.

## `while (true)`
A loop that is set up using `while (true)` will continue forever unless the command `break` is used somewhere inside the loop.

In your game, you want to stop the game when the nail has been fully hammered in. Here's how you could do that:

<details class="sandbox" open>
<summary>Leaving a `while` loop</summary>

1. Create a new file called `while.js`:

```tex-w
code while.js
```

2. Paste the following code into it:

```javascript
let length = 12
while (length) {
  console.log("Nail length: " + length)
  length = length - 1
}
console.log("length:", length)
```

3. In the Terminal window, run:

```tex-w
node while.js
```

This is what you should see in the Terminal:

![The `while` loop stops when `length` reaches `0`](images/whileLength.webp)

</details>

## Points to note

* The value of the variable `length` is going to change, so it has to be declared with `let`. If you use `const`, JavaScript will tell you that you made an error. (Try it.)
* When `length` has a value greater than 0, the `while` loop behaves as if `length` were `true`: `length` is _truthy_.
* `length = length - 1` subtracts `1` from `length`, each time that line of code is executed.
* When `length` reaches zero, the `while` loop stops looping.
* When you use the `+` operator between a string (`"Nail length "`) and a number (for example: `12`), JavaScript does not _add_ them. It _concatenates_ them, or strings them together.

</section>