<!-- Hitting More Than Once -->
<section
  id="hitting-more-than-once"
  aria-labelledby="hitting-more-than-once"
  data-item="Hitting More Than Once"
>
  <h2><a href="#hitting-more-than-once">Hitting More Than Once</a></h2>
  
<details class="challenge" open>
<summary>#4 Can you let the solo player hit the nail several times in a row?</summary>
This challenge is more tricky. I expect that you will see a number of errors as you work on it, so I will walk you through it. Fixing these errors will also resolve the WET issue (We Enjoy Typing - the opposite of DRY).

Here's the display in the Terminal that you are aiming for:

```tex-w
<i>-===========| The nail is 12 units long.

-========| You hit the nail hard.</i>

<b>-======| You hit the nail firmly.

-=====| You hit the nail gently.

-===| You hit the nail firmly.

-| You hit the nail hard.</b>
```

</details>

## Repetition with `while`

In section [20: Never Repeat a Trick](#never-repeat-a-trick), you wrote a script called `while.js`, which logged `Nail length: ` from 12 down to 1.

```javascript
let length = 12
while (length) {
  console.log("Nail length: " + length)
  length = length - 1
}
console.log("length:", length)
```

You can use a similar technique here.

1. In `main.js`, you can wrap the `if` statement that checks if the player is human or AI in a `while` loop:

```javascript-#37
<i>console.log(rules)
let player = keyInYN(whoStarts)
console.log(clear.repeat(toDelete))
console.log(nail, prompt)</i>

<b>while (length) {</b>
  <i>if (player) { // it's the human player's turn
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
  nail   = "-" + "=".repeat(length - 1) + "|"
  console.log(clear.repeat(toDelete))
  console.log(nail, prompt)</i>
<b>}</b>
```

2. In the Terminal, run:

```tex-w
node main.js
```

3. Press `Y` to choose to start.
4. Press a number from `1` to `3` each time you are asked.

To begin with, all will be well, but finally you will get an error:

<details class="warn" open>
<summary>Invalid count value: -1</summary>
```tex-w
<i>-===========| The nail is 12 units long.

-========| You hit the nail hard.

-======| You hit the nail firmly.

-=====| You hit the nail gently.

-===| You hit the nail firmly.

-| You hit the nail hard.</i>

<b>/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:56
  nail      = "-" + "=".repeat(length - 1) + "|"
                        ^

RangeError: Invalid count value: -1
    at String.repeat (<anonymous>)
    at Object.<anonymous> (/Users/james/Tutorials/My Learning Journey/Nail_It/main.js:56:25)</b>
```

</details>

## The debugger to the rescue!

It might be helpful to use VS Code's debugger to see what the problem is.

1. Press the F5 shortcut (or use the menu item Run > Start Debugging if you have the time, and no-one's looking)
2. As before, select Node.js in the Command Palette when asked which language you want to debug.

![Select the debugger for Node.js](images/SelectNodeJS.webp)

3. Open the Debug Console.
4. Yikes!

![The current environment doesn't support interactive reading from TTY](images/unsupported.webp)

Here's an extract of the error message. It shows that the error occurred on line 38 of `main.js`.

<details class="trouble" open>
<summary>environment doesn't support interactive reading from TTY</summary>
```tex-w
opt/homebrew/bin/node ./main.js
Let's knock a nail into this computer!

* Each player takes a turn to hit the nail once.
* A player can hit the nail in one of three ways:
  gently, firmly, hard.
* Depending on the force used, the nail will be
  driven more or less deeply into the Terminal.
* The player who knocks the nail all the way in
  is the winner.

Are you ready?

Process exited with code 1
Uncaught Error Error: The current environment doesn't support interactive reading from TTY.
stty: /dev/tty: Device not configured
/Users/james/Tutorials/My Learning Journey/Nail_It/node_modules/readline-sync/lib/read.sh: line 49: /dev/tty: Device not configured
stty: /dev/tty: Device not configured
    at readlineExt (/Users/james/Tutorials/My Learning Journey/Nail_It/node_modules/readline-sync/lib/readline-sync.js:221:19)
```
```tex-s
  # lines skipped #
```
```tex-w
    at <anonymous> (/Users/james/Tutorials/My Learning Journey/Nail_It/<b>main.js:38:14)</b>
```

</details>

Here is line 38 of `main.js`:

```javascript-#38
let player = keyInYN(whoStarts)
```

This is the line where `readline-sync` is used for the first time.

**In other words, the error occurred because VS Code's debugger doesn't work with `readline-sync`.**

The debugger is designed to work with Node.js and JavaScript. `readline-sync` interacts with the Terminal. Out of the box, they are incompatible.

But you can guess that if I suggested that you use the debugger, there will be a solution. The question is: How to find the solution.

Google is your friend. The problem you have just met is due to the interaction between three things: VS Code, `readline-sync` and the debugger. Here's a Google query for exactly these three things:

[vs code readline-sync debugger](https://www.google.com/search?q=vs+code+readline-sync+debugger)

1. Click on the link above.

![Using Google to search for solutions](images/askingGoogle.webp)

In my browser, the first link that Google gives is to a question on [stackoverflow.com](https://stackoverflow.com/).

<details class="note" open>
<summary>stackoverflow.com</summary>
[stackoverflow.com](https://stackoverflow.com/) is a site where developers of all levels, using every imaginable coding language can ask questions and get answers.

Most questions that you may have will already have been asked and answered, so you should search for existing answers before you ask a question of your own.

The site is gamified. You earn points for asking good questions, you earn points for giving good answers. But you can also lose points if your question is badly written, or shows that you haven't even tried to find a solution for yourself, or if it has already been asked many times.

Good answers get upvoted. You can see how many points the person who answered the question has earned. You can easily see which answers you can trust.

</details>

If I visit this stackoverflow link, I find that the question does not exactly match my problem. But I'm interested in answers.

1. Scroll down until you find [Muneeb's answer](https://stackoverflow.com/a/66850526/1927589)

![Muneeb's answer](images/MuneebAnswer.webp)

**"Well that's very nice. An answer with 10 reputation poinst,"** you think. **"But what's a `launch.json` file? And where do I put this line `"console": "integratedTerminal"`?"**

3. Look at the VS Code window where your error is showing.
4. Make sure the Run panel is showing (menu View > Run, Shift-Ctrl-D (for _Debug_), or click on the Run and Debug icon).

![The 'create a launch.json file' link](images/createLaunchJSON.webp)

5. Look for the link to `create a launch.json file`, and click on it.

![Composite image: creating the `launch.json` file](images/launchJSON.webp)

VS Code will create a new file at `Nail_It/.vscode/launch.json`. This will tell VS Code that, in the future, when you run the debugger, you want `node` to `launch` the file at `"${workspaceFolder}/main.js"` and not to bother you with any code written in `node_internals`.

This is the file where you can add the line `"console": "integratedTerminal"`:

```json
<i>{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "program": "${workspaceFolder}/main.js"</i><b>,
      "console": "integratedTerminal"</b><i>
    }
  ]
}</i>
```
1. Add the line suggested by Muneeb to your new `launch.json` file.
2. Be sure to place a comma (`,`) at the end of the previous line.
3. Press `F5` again, to start the debugger.

![The debugger doesn't complain now](images/debuggingWithReadlineSync.webp)

This time everything works fine. The Terminal explains to you how helpful it is being, and then it runs your script.

## Add a breakpoint

The debugger might not want to let you add a breakpoint while it is running.

1. Stop the debugger by pressing `Shift-F5`, or clicking on the little red square in the Control Panel.

![The Stop button in the Control Panel](images/stopButton.webp)

2. Check the first error you got, before you ran the debugger, to see where the error occurred:

```tex-w
RangeError: Invalid count value: -1
    at String.repeat (<anonymous>)
    at Object.<anonymous> (/Users/james/Tutorials/My Learning Journey/Nail_It/<b>main.js:56:25</b>)
```

3. Put a debug breakpoint on line 56 of your `main.js` script:

![Add a breakpoint to line 56](images/breakpoint56.png)

4. Press the `F5` key to start debugging.

Your game will ask you to press `Y` and then choose a number from 1 - 3.

5. Press `3` on your keyboard.

The debugger will stop on line 56, before it executes that line.

![Going through first pass off the `while` loop with the debugger](images/debugFirstPass.webp)

You can see that the value of `force` has been set to `3`, and that `length` has been updated to `9`. The value of `nail` is still exactly what you code calculated on line 33. The nail is still 12 units long.

6. Click on the Step Over button in the Command Palette, or press the `F10` shortcut.

![The value for `nail` is updated when you activate Step Over](images/updateNail.webp)

JavaScript has no problem creating a new string for `nail`.

7. Activate Step Over two more times.

![The question is cleared and the nail is redrawn](images/redrawTheNail.webp)

Three things will happen:

* The question will be cleared from the Terminal
* A new, shorter version of the nail will be drawn
* The debugger will jump back to the beginning of the `while` loop

8. Activate Step Over three more times. The debugger will step back into the `while` loop, because `length` is `9` and non-zero numbers are truthy. But on the third step, the debugger will stop showing which line is about to be executed and it will stop showing any variables.

![The debugger takes a break while readline-sync is active](images/readlineSyncIsActive.webp)

This is because the `keyInSelect()` method of `readline-sync` has taken control. It's busy listening for your input in the Terminal.

9. Click on the Terminal to activate it
10. On your keyboard, press a number from 1 - 3.

![The debugger becomes active again after `keyInSelect()` returns a value](images/debuggerActiveAgain.webp)

The debugger becomes active again.

Note that there is an entry for `index` in the `Block` section of the VARIABLES pane. (The value `this` is there for house-keeping reasons.)

11. Press the Continue button in the Control Panel, or press the shortcut key `F5`.
    
The debugger will jump directly to line 56, executing all the code on the way. 

12. In the WATCH panel, click on the `+` button and enter the expression `length - 1`.

![Using the WATCH panel to watch the value of an expression](images/watchLength-1.webp)

You should see that its value is `5`. Again, JavaScript will have no problem creating a new string for `nail`.

13. Press `F5` to make your script continue running.
14. Activate the Terminal, and press the `3` key on your keyboard
15. Repeat steps 13 and 14 again.

Now you can see the problem. In the WATCH panel, you can see that `length - 1 = -1`. The [string method `.repeat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat) can't handle negative numbers.

![Debugging the `while` loop](images/DebuggingTheLoop.webp)

<details class="question" open>
<summary>Where has `index` gone?</summary>
In the VARIABLES pane of the debugger, there is no entry for `index`. Why not?

The debugger is paused on line 56, which is outside the curly-bracket code block where `index` is declared. At this point in the code JavaScript and the debugger have forgotten that `index` ever existed.

</details>

16. Just for closure, activate Step Over one last time.

![Your game exits with an error](images/debuggerDisconnect.webp)

<details class="pivot" open>
<summary>How to fix this?</summary>
The debugger disconnects and JavaScript shows the same error it gave you before:

```bash-w
Invalid count value: -1 ... /Nail_It/main.js:56:25
```

This is the problem that you are going to have to fix, but the debugger has shown you how and where the error occurs.

Remember how I pointed out that there were problems with repeated lines of code? In the next section, you'll see how to make your code work without them.

</details>

</section>