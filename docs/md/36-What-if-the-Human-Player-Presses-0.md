<!-- What if the Human Player Presses 0 -->
<section
  id="what-if-the-human-player-presses-0"
  aria-labelledby="what-if-the-human-player-presses-0"
  data-item="What if the Human Player Presses 0?"
>
  <h2><a href="#what-if-the-human-player-presses-0">What if the Human Player Presses 0?</a></h2>
  
By default, `readline-sync.keyInSelect()` considers that pressing `0` means `CANCEL`. But your game doesn't cancel anything.

If you press the `0` key now, the game will behave a little strangely. It will not make the nail any shorter, and it will show the string `undefined` instead of `gently`, `firmly` or `hard`. And it will continue to ask you to play.

```tex-w
<i>-=============| The nail is 14 units long.

==============| You hit the nail </i><b>undefined</b><i>.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: </i>
```

<details class="sandbox" open>
<summary>Where does `undefined` come from?</summary>

Back in section [18. Arrays and index Zero](#arrays-and-index-zero), you saw that the first item in an array is at `index 0`. You saw that you could get the value at each entry in the array, by counting from `0` to the-number-of-items-in-the-array minus 1.

Here's how you can check this in the Node IDE in your Terminal:

```tex-w
<b>node</b>
Welcome to Node.js v23.1.0.
Type ".help" for more information.
> <b>s = [ 'gently', 'firmly', 'hard' ]</b>
[ 'gently', 'firmly', 'hard' ]
> <b>s[0]</b>
'gently'
> <b>s[1]</b>
'firmly'
> <b>s[2]</b>
'hard'
```

Now try using index values that are out of range: greater than 2 or less than 0. You will get the value [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined):

```tex-w
> <b>s[3]</b>
undefined
> <b>s[-1]</b>
undefined
```

JavaScript looks for a value at the given place in the array, but there's nothing there. In JavaScript-speak, this "nothing" is `undefined`. When you add this nothing to a string, it appears as the string `"undefined"`, but it's not a string.

You can create `undefined` in different ways

1. If you ask for an item in an array that doesn't exist (as you gave just don.)
2. If you don't give any value to a variable that you create with `let`, its value will be `undefined`

```tex-w
> <b>let empty</b>
undefined
```

3. If you ask an object for a property that it doesn't have:

```tex-w
> <b>r = require("readline-sync")</b>
{
  _DBG_set_useExt: [Function (anonymous)],
```
```tex-s
// lines skipped //
```
```tex-w
  question: [Function (anonymous)],
  prompt: [Function (anonymous)],
  keyIn: [Function (anonymous)],
```
```tex-s
// lines skipped //
```
```tex-w
}
> <b>r.unknownProperty</b>
undefined
```

4. If you call a method that does not return any value:

```tex-w
<b>console.log("This text will be followed by `undefined` because the method console.log() does not return a value")</b>
This text will be followed by `undefined` because the method console.log() does not return a value
undefined
```

</details>

<details class="note" open>
<summary>`undefined` is falsy</summary>
As mentioned earlier, JavaScript treats the value `undefined` as if it were `false`.

</details>

<details class="pivot" open>
<summary>Stopping the game when you press `0`</summary>
When the AI starts playing (and making mistakes), there will be times when you are testing the game that you will want to stop the game and make a change to the code. Right now, you are forced to play all the way through to the end.

As you have seen, when you press `0`, `keyInSelect()` returns the value `-1`.

In the next section, you'll see how to stop the game if the value return by `keyInSelect()` is less than 1.

</details>
</section>