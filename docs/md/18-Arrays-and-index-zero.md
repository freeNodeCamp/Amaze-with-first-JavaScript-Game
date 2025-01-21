<!-- Arrays and index zero -->
<section
  id="arrays-and-index-zero"
  aria-labelledby="arrays-and-index-zero"
  data-item="Arrays and index Zero"
>
  <h2><a href="#arrays-and-index-zero">Arrays and index Zero</a></h2>
  
The animal names in the last example are stored in an [array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array). An array is identified by square brackets (`[ ... ]`) enclosing a number of items separated by commas.

Arrays allow you to store a list of items. Here the items are words, but they could be any type of data, including other arrays.

Any white space (such as space characters or new lines) between the items is ignored. Both these arrangements of text have exactly the same effect:

```js-w
animals = ['Lion', 'Elephant', 'Crocodile', 'Giraffe', 'Hippo']
```

```js-w
animals = [
  'Lion',
  'Elephant',
  'Crocodile',
  'Giraffe',
  'Hippo'
]
```

## The house metaphor

You can think of an array as a block of flats. For the computer, the array is located at a particular memory address, but the items within the array have their own addresses, just like each floor in a block of flats has its own floor number.

In the UK, Canada, Australia and some other countries, you walk into a block of flats on the ground floor. You have to go up one flight of stairs to get to "the first floor". The lift will show the number 0 for the ground floor. (In the USA, the first floor is at street level. The elevator will show the number 1 for this floor.)

![Counting from zero](images/UKLiftNumbers.jpg){data-title="Elevator button building. A close up of a metal elevator with numbers" data-credits="[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/deed.en) | [source](https://garystockbridge617.getarchive.net/media/elevator-button-building-architecture-buildings-035b05)"}

JavaScript, like the UK, counts from zero.

The "block of flats" metaphor breaks really quickly. In JavaScript, it is easy to add and remove items from an array. It's not at all easy to add or remove floors from a block of flats.

The important thing to note is that an array has its own address in memory, and that all the items within it can be found at that address. You will use a human-readable variable name to represent this memory address. The items in the array can change, just like people can move in and out of their flats, but the variable name will always refer to the space where the current items can be found.

## Counting from zero

To access a particular item in an array, you write the array name followed by square brackets which contain an integer. For example:

```javascript
animals[1]
```

For [practical and theoretical reasons](https://en.wikipedia.org/wiki/Zero-based_numbering), arrays in JavaScript start counting from zero, not from 1. There are zero items _before_ 'Lion', so `animals[0]` refers to 'Lion'.

## `animals[index]`

In the script that you have originally copied, the variable `index` receives an integer from `keyInSelect()`. When you _press_ the number `2` key on your keyboard (to select the Elephant), `keyInSelect()` _returns_ the number `1`, because JavaScript considers that `animals[1]` is 'Elephant'.

```javascript-#7
const index = keyInSelect(animals, question)
console.log(
  'Ok, ' + animals[index] + ' goes to your room.'
)
```
The adjusted value of `index` ensures that the output in the Terminal shows the correct animal name.

```tex-w
<i>[1] Lion  
</i><b>[2] Elephant</b><i>  
[3] Crocodile  
[4] Giraffe  
[5] Hippo  
[0] CANCEL  
 
Which animal? [1...5 / 0]: </i><b>2</b><i>  
Ok, </i><b>Elephant</b><i> goes to your room.</i>
```

<details class="sandbox" open>
<summary>A feature, not a bug</summary>
You can edit your `keyInSelect.js` file to show that the value of `index` corresponds to the expected item in the `strength` array:

```javascript-
<i>const { keyInSelect } = require('readline-sync')
const strength = [
  'gently',
  'firmly',
  'hard'
]
const question = 'How hard do you plan to hit?'
const index = keyInSelect(strength, question)
console.log(
  "index:", index</i><b>,
  "strength:", strength[index]</b><i>
)</i>
```

![When you log `strength[index]` you get the value you expect](images/strengthFirmly.webp)

</details>

## Adjusting for force

In the final version of your game, vhen you hit the nail "gently", the value returned by `keyInSelect()` will be `0`, but nail will get driven `1` unit into its support.

Conversely, when the AI hits the nail with a force of `3` (for example), the Terminal should show `"I hit the nail hard"`, where "hard" is found at `strength[2]`.

You are going to have to pay attention to this. The adjustment will be in a different direction for the player as for the AI.

<details class="pivot" open>
<summary>The power of arrays </summary>
This project uses arrays in a very limited way. In the future, you will be using the power of arrays in many different circumstances. I won't describe all the things that arrays can do, but you can check out the [documentation on the MDN website](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) any time you need to know more.

</details>

</section>