<!-- Deleting text from the Terminal -->
<section
  id="deleting-text-from-the-terminal"
  aria-labelledby="deleting-text-from-the-terminal"
  data-item="Deleting Text from the Terminal"
>
  <h2><a href="#deleting-text-from-the-terminal">Deleting Text from the Terminal</a></h2>
  
So far, you have prepared code that can:

1. Display text in the Terminal
2. Ask the player a Yes-or-No question
3. Ask the player to press a number key.

That's good progress. 

Before moving on to drawing the nail, there are still two more trick that you can learn from the [`readline-sync` documentation](https://www.npmjs.com/package/readline-sync).

Here's the code from the next example in the [`readline-sync` documentation](https://www.npmjs.com/package/readline-sync). I haven't made any changes to it, because I plan to change it quite radically.

> * An UI like the Range Slider:
>     (Press Z or X key to change a value, and Space Bar to exit)
> 
> ```javascript-w
> var readlineSync = require('readline-sync'),
>   MAX = 60, MIN = 0, value = 30, key;
> console.log('\n\n' + (new Array(20)).join(' ') +
>   '[Z] <- -> [X]  FIX: [SPACE]\n');
> while (true) {
>   <b>console.log('\x1B[1A\x1B[K|'</b> +
>     (new Array(value + 1)).join('-') + 'O' +
>     (new Array(MAX - value + 1)).join('-') + '| ' + value);
>   key = readlineSync.keyIn('',
>     {hideEchoBack: true, mask: '', limit: 'zx '});
>   if (key === 'z') { if (value > MIN) { value--; } }
>   else if (key === 'x') { if (value < MAX) { value++; } }
>   else { break; }
> }
> ```

This code creates an interactive slider. Here's how you can test it:

1. Create a new file in your `Tests/readline-sync/` folder:

```tex-w
code slider.js
```

2. Paste the code shown above into the new file.
3. Save your changes.
4. In the Terminal, execute the command:

```tex-w
node slider.js
```

5. Press the `Z` and the `X` keys to make the `0` move left and right, and to update the number shown on the right
6. Press the space bar to stop the interaction.

<details class="question" open>
<summary>The first trick makes something vanish</summary>
Did you find it surprising that display of the slider bar changed _after_ it was first displayed? Somehow, the code in your `slider.js` script is rewriting the same line in the Terminal, with a different value each time.

Look at the code. Is there a chunk of code that looks really strange?

Or to put it another way: Can you guess what this code does?

```js-w
console.log('\x1B[1A\x1B[K')
```

Do you think it might be connected with the way the slider bar updates itself?

</details>

<details class="sandbox" open>
<summary>Exploring something new</summary>
Here's how you could test what it does.

1. Create a new file in a new subfolder of your `Nail_It/Tests/` folder:
```tex-w
code ../strings/deleteLines.js
```

This line says:

```tex-w
* <b>code</b>             Hey VS Code!
* <b>..</b>               Move to the parent folder of this
                   `readline-sync/` folder (that is: move
                   to the `Nail_It/Tests/` folder)
* <b>/string</b>          Create a new folder there called `string`
* <b>/deleteLines.js</b>  Create a JavaScript file there called
                   `deleteLines.js`
```

2. Paste the following code into your new file:

```javascript
console.log(10)
console.log(9)
console.log(8)
console.log(7)
console.log(6)
console.log(5)
console.log(4)
console.log(3)
console.log(2)
console.log(1)
console.log('\x1B[1A\x1B[K')
```

3. Save the new `deleteLines.js` file.
4. Tell the Terminal that you want to change directories, to work in the new `Nail_It/Tests/strings/` folder:

```tex-w
cd ../strings
```

5. Run the script that you have just created:

```tex-w
node deleteLines.js
```

![`console.log('\\x1B\[1A\\x1B\[K')` deletes the last line](images/deleteLine.webp)

You are used to seeing `console.log()` printing text in the Terminal, but the result of `console.log(1)` does not appear. In fact it _was_ printed, and then the line `console.log('\x1B[1A\x1B[K')` deleted it again.

</details>


<details class="challenge" open>
<summary>Can you delete more than one line?</summary>
Can you change `deleteLines.js` so that the last `console.log()` line deletes more than one line?

OK. I'll help you with this one. JavaScript has a method called [`repeat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat) that you can use with a string. Here's how it works:

```tex-w
<b>node</b>
Welcome to Node.js v23.1.0.
Type ".help" for more information.
> <b>"blah ".repeat(3)</b>
'blah blah blah '
```

<details class="solution">
<summary>Solution</summary>

You can make this change to your script:

```javascript
<i>console.log(10)
console.log(9)
console.log(8)
console.log(7)
console.log(6)
console.log(5)
console.log(4)
console.log(3)
console.log(2)
console.log(1)
console.log('\x1B[1A\x1B[K'</i><b>.repeat(9)</b><i>)</i>
```

![Use the `.repeat()` method to delete 9 lines](images/delete9.webp)

</details>
</details>

</section>