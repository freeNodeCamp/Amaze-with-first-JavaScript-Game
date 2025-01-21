<!-- Working with keyInYN -->
<section
  id="working-with-keyinyn"
  aria-labelledby="working-with-keyinyn"
  data-item="Working with keyInYN"
>
  <h2><a href="#working-with-keyinyn">Working with `keyInYN`</a></h2>
  
  In the [documentation for the `readline-sync` package](https://www.npmjs.com/package/readline-sync), the next example is:

> * Get the user's response by a single key without the Enter key:
> 
> ```javascript-w
> const readlineSync = require('readline-sync');
> if (readlineSync.keyInYN('Do you want this module?')) {
>   // 'Y' key was pressed.
>   console.log('Installing now...');
>   // Do something...
> } else {
>   // Another key was pressed.
>   console.log('Searching for another...');
>   // Do something...
> }
> ```

1. Create a new file in your `Tests/` folder and call it `keyInYN.js`
2. Look at the code above. Predict what you will see in the Terminal when you run it.
3. Run:

```tex-w
node keyInYN.js
```

4. Press the `Y` key
5. Look at the output. Was your prediction correct?
6. Repeat steps 3 - 5 again, but press the `N` key.
7. Repeat steps 3 - 5 again, but press a completely different key.

When you press `Y`, you should see `Installing now...` in the Terminal.
When you press `N` _or any other key_ you should see `Searching for another...` in the Terminal.

<details class="challenge" open>
<summary>Yes, No or ...?</summary>
Here's a challenge.

Can you rewrite the code so that it shows exactly the value that the `keyInYN()` method returns, instead of a string like 'Installing now...' or 'Searching for another...'?

It should show `true` if `Y` is pressed, `false` if `N` is pressed or nothing if another key is pressed.

Hint: the file you created at `Nail_It/main.js` already does this. You can copy ideas from there.

<details class="solution">
<summary>Solution</summary>
```javascript
const readlineSync = require("readline-sync");
const question = "Do you want this module?"
const yesOrNo = readlineSync.keyInYN(question) 
console.log("yesOrNo: *", yesOrNo, "*")
```

I've added asterisk (`*`) characters around the value of `yesOrNo`, so that you can see when `yesOrNo` contains neither `true` nor `false`.

Note that there will be a space added between each item that `console.log()` prints, so when `yesOrNo` contains an empty string, `console.log()` prints `*  *`, with two spaces between the asterisks.

![Showing the output of keyInYN](images/yesOrNo.webp)

</details>

<details class="challenge">
<summary>Bonus question</summary>
Search the documentation for more places where it talks about `keyInYN`, until you find this:

> ### keyInYN
>
> ```javascript-w
> boolYesOrEmpty = readlineSync.keyInYN([query[, options]])
> ```

<details class="question" open>
<summary>Optional parameters</summary>
The square brackets in `keyInYN([query[, options]])` mean "The data inside these square brackets is optional." This means that `readlineSync.keyInYN()` (with no parameters at all) should work.

Why don't you try it?  
What does it do?  
Where in the documentation can you find a description of what to expect?

</details>

And later, you should find this:

> ... the following additional option is available.  
> **guide**
> 
> _Type_: boolean  
> _Default_: true
> 
> If true is specified, a string '[y/n]' as guide for the user is added to query. 

Can you create an options object like `{ guide: false }` and add it as the second parameter of the `keyInYN()` method? What do you expect will happen if you do?

</details>

<details class="solution">
<summary>Bonus Solution</summary>
```javascript
const readlineSync = require("readline-sync")
const question = "Do you want this module?"
const options = { guide: false }
const yesOrNo = readlineSync.keyInYN(question, options) 
console.log("yesOrNo: *", yesOrNo, "*")
```

![With `{ guide: false }`, the string `[y\n]` is not shown](images/bonus.webp)

</details>
</details>

</section>