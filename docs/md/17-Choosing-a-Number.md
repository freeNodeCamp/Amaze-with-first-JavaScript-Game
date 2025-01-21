<!-- Choosing a Number -->
<section
  id="choosing-a-number"
  aria-labelledby="choosing-a-number"
  data-item="Choosing a Number"
>
  <h2><a href="#choosing-a-number">Choosing a Number</a></h2>
  
The third example in [documentation for the `readline-sync` package](https://www.npmjs.com/package/readline-sync), is something like the code that follows. 

<details class="note" open>
<summary>Edited for clarity</summary>
I've edited a bit for clarity. Can you spot the differences?

In particular, the first line selects `keyInSelect` directly from the `readline-sync` code, using a technique known as [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment).

</details>

> * Let the user choose an item from a list:
>
> ```javascript
> const { keyInSelect } = require('readline-sync')
> const animals = [
>   'Lion',
>   'Elephant',
>   'Crocodile',
>   'Giraffe',
>   'Hippo'
> ]
> const question = 'Which animal?'
> const index = keyInSelect(animals, question)
> console.log(
>   'Ok, ' + animals[index] + ' goes to your room.'
> )
> ```
> In the Terminal:
> ```tex-w
> [1] Lion  
> [2] Elephant  
> [3] Crocodile  
> [4] Giraffe  
> [5] Hippo  
> [0] CANCEL  
>  
> Which animal? [1...5 / 0]: 2  
> Ok, Elephant goes to your room.
> ```

To test this example:

1. Using your Terminal, create a new file:

```tex-w
code keyInSelect.js
```

1. Paste the code above into your new script file.
2. In the Terminal, run:

```tex-w
node keyInSelect.js
```

![Testing keyInSelect() in a new script](images/keyInSelect.webp)

It works exactly as advertised. But for your game, you want a number, not an animal. You are going to have to change this code, and see exactly what is going on inside it.

<details class="sandbox" open>
<summary>Adapting for the Nail It! game</summary>
You can edit the code in your new `keyInSelect.js` file so that it asks the question that you will need for the Nail It! game:

```javascript-
<i>const { keyInSelect } = require('readline-sync')
const </i><b>strength</b><i> = [
  </i><b>'gently',
  'firmly',
  'hard'</b><i>
]
const question = '</i><b>How hard do you plan to hit?</b><i>'
const index = keyInSelect(</i><b>strength</b><i>, question)
console.log(</i>
  <b>"index:", index</b>
<i>)</i>
```

Notice that instead of using `console.log()` to show the name of the item that is chosen, the code above logs the value of the `index` returned by `keyInSelect()`, directly. The result may surprise you.

![The value of `index` is 1 less than the number you press](images/howHard.webp)

You can try it several times. The value of `index` that is logged will always be 1 less than the number you press.

```tex-#
<i>How hard do you plan to hit? [1, 2, 3, 0]: </i><b>0</b><i>
index: </i><b>-1</b><i>

How hard do you plan to hit? [1, 2, 3, 0]: </i><b>1</b><i>
index: </i><b>0</b><i>

How hard do you plan to hit? [1, 2, 3, 0]: </i><b>2</b><i>
index: </i><b>1</b><i>

How hard do you plan to hit? [1, 2, 3, 0]: </i><b>3</b><i>
index: </i><b>2</b><i></i>
```

Is this a bug or a feature?
</details>

</section>