<!-- Using the Debugger -->
<section
  id="using-the-debugger"
  aria-labelledby="using-the-debugger"
  data-item="Using the Debugger"
>
  <h2><a href="#using-the-debugger">Using the Debugger</a></h2>
  
Wouldn't it be good if you could look inside the JavaScript engine, to see what JavaScript is doing? In the last section, you saw the _output_ of the `while` loop, but you couldn't see the `process`.

With VS Code's debugger, you can step through the code, line by line as it is executing, and watch which line is executed next, and how the variables change.

Running code in the debugger is like turning the pages of a flipbook. You can run through several steps automatically, and then stop at a point which interests you.

![Taking the time to study each pages of a flipbook](images/flipbook.webp){data-title="Daumenkino kol" data-credits="[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/deed.en) by [ de:Technische Sammlungen der Stadt Dresden](https://de.wikipedia.org/wiki/Technische_Sammlungen_der_Stadt_Dresden) | [source](https://commons.wikimedia.org/wiki/File:Daumenkino_kol.jpg)"}

So here goes:
 
1. Start by creating a _breakpoint_ on line 1 of your script. A breakpoint is a point in your code where you tell the debugger: "Stop here. I want to look at this bit closely." To do this, move your mouse just to the left of the column of line numbers. A dark red dot should appear. Click to make the red dot brighter, and to fix it in place.

![Add a breakpoint on line 1](images/AddBreakpoint.webp)

2. Select the menu item Run > Start Debugging. You'll see that there is a keyboard shortcut — `F5` — that you can use in the future.

![Choose Run > Start Debugging, or press F5](images/StartDebugging.webp)

<details class="tip" open>
<summary>Using keyboard shortcuts</summary>
Moving your hand from the keyboard to your mouse or your trackpad takes time. Pressing a keyboard shortcut is always faster. Time is the one thing that you can't get any more of. 

If a professional developer is watching you work, and you use your mouse to activate items in a menu or a contextual menu, the professional will see that you are still a beginner. This might not be the impression that you want to give.

**It is well worthwhile taking the time to learn (or [create](https://code.visualstudio.com/docs/getstarted/keybindings)) shortcuts for actions that you use regularly.**

</details>

<details class="trouble">
<summary>A Note about the F keys </summary>
It may be that when you press `F5`, instead of starting VS Code's debugger, you trigger a media action, like switching your microphone on or off, or making the screen darker or brighter. In this case, you may need to press the `fn` key at the same time.

The `fn` key is usually at the bottom left corner of your keyboard, but this is not always true.

![The `fn` key may be anywhere on your keyboard ](images/FNKey.webp){data-title="fn key" data-credits="[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.en) by [LucaCV](https://commons.wikimedia.org/wiki/File:%22Windows-Key%22,_Win8-Version.jpg) | [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) by [
Blake Patterson](https://www.flickr.com/photos/blakespot/2384302595)
"}

It is usually possible to toggle the function and media keys, so that you don't have to press `fn` each time. The technique for doing this depends on your computer and your operating system. You can [search on Google](https://www.google.com/search?q=toggle+fn+key+lock+YOUR_OPERATING_SYSTEM_HERE) for a technique that will work for you.

</details>

## Choosing the debugger language

3. The Command Palette will open and ask you what kind of script you want to debug. Because the extension of your file is `.js`, it will guess you want Node.js. Click the line `Node.js` to confirm.

![Select the debugger for Node.js](images/SelectNodeJS.webp)

4. The debugger will start running your script, but it will stop before it executes the first line, because you place a breakpoint there.

![The Control Palette lets you progress through your script](images/StepOver.webp)

You will see:

* In the centre, at the top, a Control Panel with buttons for controlling the debugger

![The control panel](images/ControlPanel.webp)

* On the left, a pane with sections for `VARIABLES`, `WATCH`, `CALL STACK` `LOADED SCRIPTS` and `BREAKPOINTS`. For now, this just contains some house-keeping information about which file you are debugging. You'll see a red dot and a checkbox at the bottom showing where your first breakpoint can be found. The checkbox indicates that it is active.

![The Debug Pane on the left](images/DebugPane.webp)

* In your script itself, the line with the breakpoint is highlighted, and there is a yellow pointer surrounding the breakpoint. This indicates that the debugger has stopped here, and has not yet executed this line.

![The debugger is paused at the next line to be executed](images/lineToBeExecuted.webp)

## Stepping through the script

1. Click on the Step Over button in the Control Panel, or press the shortcut key `F10`.

![The Step Over button in the Control Panel](images/StepOverButton.webp)

2. The first line of code will be executed. You will see that the variable `length` is now shown in the VARIABLES pane. The yellow pointer and highlight will move to the next line that is about to be executed.

![When the first line is executed, `length = 12` is shown in the VARIABLES pane](images/lengthSetTo12.webp)

3. Press the Step Over button again or press `F10`. The `while` loop will see that `length` is _truthy_ because it has a non-zero value, and it will move your code into its code block.

4. Press the Step Over button again (`F10`), and the line `console.log("Nail length: " + length)` will be executed. You can see this output in the Debug Console panel, which replaces the Terminal.

![`Nail length: 12` is logged to the Debug Console](images/lengthLogged.webp)

5. Press Step Over again. This time the line two things will happen:
   * `length = length - 1` will be executed and the value of the `length` variable in the VARIABLES pane will change
   * The debugger will reach the end of the loop (identified by the closing curly brace (`}`), and will jump back to the beginning of the loop again.
  
![`length` is updated, and the loop starts again](images/looping.webp)

Once again, the `while` statement finds that the value `11` is truthy, and the code inside the loop is visited again.

## A conditional breakpoint

You _can_ continue to press the Step Over button once for each line of code, but you can also tell the debugger to run through the loop until something is about to change. You can set a _conditional breakpoint_. A conditional breakpoint will pause the debugger only in certain conditions.

Here's how to set a conditional breakpoint that will only pause the debugger when `length` has the value `1`:

1. In your script, Right-Click just to the left of line number 4.
2. In the contextual menu that opens, choose `Add Conditional Breakpoint`

![Right-click to add a conditional breakpoint](images/ConditionalBreakpoint.webp)

3. An editable frame will open where you can type an expression. The debugger will pause at this breakpoint only if this expression is `true`. Type:

```tex-w
length === 1
```

This expression evaluates to `true` only if the value of the `length` variable is identical to the number `1`.

![Set the condition that will trigger the breakpoint](images/SetTheCondition.webp)

4. Click on the Continue button.

![The Continue button in the Control Panel](images/ContinueButton.webp)

This will make the debugger run through every step automatically until it finds itself on line `4` and the the value of the `length` variable is identical to the number `1`. Then it will pause.

![Press Continue to run your code until the next breakpoint](images/ContinueToNextBreakpoint.webp)

You should see `Nail length` logged many times in the Debug Console, and an entry for `length = 1` showing in the VARIABLES pane. The line `length = length - 1` is ready to be executed.

5. Use the `F10` shortcut to activate the Step Over button and execute just this one line.

![Activate Step Over to set `length` to `0`](images/lengthIsZero.webp)

The entry `length = 0` will appear in the VARIABLES pane, and the code will jump back to the beginning of the loop. This time, the `while` statement will see that `length` is `0`, and `0` is _falsy_, so it will _not_ move your code into its loop block. Instead, it will jump to the first line after the loop block.

![When `length === 0`, the `while` loop will stop](images/LeaveLoop.webp)

6. Use Step Over again, to execute the final line `console.log("length:", length)`. One last entry will be printed in the Debug Console.
 
7. Press the Step Over button again to execute the line after that... which doesn't exist. This will make the debugger close.

The Control Panel will disappear, and so will the VARIABLES pane.

![The end of the debugging session](images/DebuggerClosed.webp)

<details class="pivot" open>
<summary>Just a trial session</summary>
There are no problems in the code in your `while.js` script. This debugging session just allowed you to see how the debugger works.

Now you know how to:

* Set a breakpoint
* Step through code one line at a time
* Set a conditional breakpoint
* Run through your code until the next breakpoint becomes active
* Watch how the value of your variables change at each step
* Watch how the code travels along different paths, depending on whether an expression is `true` or `false`.

In the future, when your code is not doing what you think it should be doing, you will be able to use these techniques to troubleshoot the problem, and find what needs to be fixed.

</details>
</section>