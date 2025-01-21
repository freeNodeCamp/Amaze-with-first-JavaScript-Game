<!-- Quotes or Backticks -->
<section
  id="quotes-or-backticks"
  aria-labelledby="quotes-or-backticks"
  data-item="Quotes or Backticks?"
>
  <h2><a href="#quotes-or-backticks">Quotes or Backticks?</a></h2>
  
The game that you are about to create shows several lines of text, right at the beginning:

```tex-w
Let's knock a nail into this computer!

* Each player takes a turn to hit the nail once.
* A player can use one of three levels of strength: gently, firmly, hard.
* Depending on the strength used, the nail will be driven more or less deeply into the Terminal.
* The player who knocks the nail all the way in is the winner.

Are you ready?
```

You might have noticed that the text in `"Hello World!"` was surrounded by _double quote_ characters (`"`). You might think that all you need to do is paste the multiline text that you want to show inside double quotes. But if you do, VS Code shows you lots of wavy red lines, and tells you that you have 52 problems, on for each word that is not in the first line.

![VS Code tells you that you have problems with your text](images/multilineStringFail.webp)

## Using backticks

If you want to create a block of text with more than one line, in JavaScript, you need to use backticks (`` ` ``).

Backticks can make you feel like a real programmer, if only because you've probably never used them before. And also, because you might have to spend some time looking at your keyboard to find where the backtick key is hiding.

Every keyboard manufacturer has their own idea of [where to hide the backtick character on your keyboard](https://www.google.com/search?q=backtick+keyboard&udm=2).

## Fix your code

When you have found the backtick key:

1. In `main.js`, replace the double-quote characters with single backticks, one at the beginning, and one at the end of the text.
2. In the Terminal, run:

```tex-w
node main.js
```

You should see your multiline block of text appear, as shown in Figure 7 below.

![Replace the " double-quotes with ` backticks](images/backtickSuccess.webp)

<details class="note" open>
<summary>Strings</summary>
From the early days of computing, sequences of characters have been referred to as _strings_. This is because they are treated as continuous groups, just like beads on a string.

From now on, the word "string" will mean:

A sequence of characters enclosed either by:

* single quote marks (`'`) or by
* double quote marks (`"`) or by
* back-ticks (`` ` ``)

In section [XX. Working with strings](), you'll see how to join strings together to create sentences dynamically.

</details>

<details class="tldr">
<summary>All about backticks and template literals</summary>
Backticks are very powerful. They can be used to do much more than just contain multiple lines of text. You won't need to use any of their other powers in this project, but it's good to know that they can help in many ways.

For more details, see [MDN's article on Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

</details>

<details class="tip" open>
<summary>Multiple Cursors</summary>
If you look carefully at Figure 7, or less carefully at the images below, you will see that there are _two_ text insertion cursors: one just after each backtick.

![VS Code allows you to use multiple text insertion cursors](images/multipleCursors.webp)

Programmers type a lot. VS Code provides many techniques for allowing programmers to type less.

For more details, see [the official Multicursor documentation](https://code.visualstudio.com/docs/editor/codebasics). Try the following:

1. Press `Alt` and Click wherever you want to add a cursor
2. Press `Alt` and Click on a cursor if you want to delete it
3. Press `Shift-Alt` and Click on a different line to select a rectangular block
4. Press `Alt` and Double-Click on a word to select the entire word

</details>

</section>