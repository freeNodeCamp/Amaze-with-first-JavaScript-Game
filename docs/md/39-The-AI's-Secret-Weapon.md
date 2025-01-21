<!-- The AI's Secret Weapon -->
<section
  id="the-ais-secret-weapon"
  aria-labelledby="the-ais-secret-weapon"
  data-item="The AI's Secret Weapon"
>
  <h2><a href="#the-ais-secret-weapon">The AI's Secret Weapon</a></h2>
  
Now it's time to make your AI player as smart as the piece of plastic in [Matt Parker's video](https://www.youtube.com/watch?v=9KABcmczPdg).

Both you and the AI can choose a force that reduces the length of the nail by between 1 and 3 units. If the number of units left is a multiple of 4, the player whose turn it is to play is in a losing position. If the current player takes `n` units, their opponent can take `(4 - n)` units, and the number of units left will still be a multiple of four.

In other words, the AI will have to:

* Look at the current length
* Divide it into groups of 4 units
* Check if there are any units left over

For example: If the nail is `11` units long, this is `(2 x 4 = 8) + 3`. There will be `3` units left after dividing into groups of `4`.

There are mathematical terms I could use like _modulo_ or _remainder_, but let's imagine that my schooldays are a long time ago, and that I have forgotten these words. Here's a Google query that uses words that I do know:

[js find number left over after divide](https://www.google.com/search?q=js+find+number+left+over+after+divide)

When I click on this link, the first result comes from the trusty MDN documentation: [Remainder (%)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder). To quote this page:

> The remainder (%) operator returns the remainder left over when one operand is divided by a second operand. It always takes the sign of the dividend.

There is also a **Try It** section, where you can edit the values given in the code, and then press the Run button to see the results.

![Calculating `% 4` (modulo four), for different lengths of nail](images/modulo4.webp)

<details class="sandbox" open>
<summary>Testing in the Node IDE</summary>

You can also run your own tests in the Node IDE in the Terminal.

1. Open a new Terminal and type `node` (or return to the Terminal where the Node IDE is already running)
2. Type expressions like `13 % 4` in the Terminal, and then press Enter

```tex-w
<b>node</b>
Welcome to Node.js v23.1.0.
Type ".help" for more information.
> <b>13 % 4</b>
1
> 
```

You don't need to type `console.log()`. The IDE will automatically print out the value of the expressions you type in. It may even not wait until you press Enter before showing you the value.

</details>

<details class="pivot" open>
<summary>Implementing the AI's strategy</summary>
So the modulo (`%`) operator is the AI's secret weapon. As with the solo player, building the AI's strategy is going to take several steps. Some of them are going to break the existing game.

</details>

</section>