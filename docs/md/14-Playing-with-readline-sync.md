<!-- Playing with readline sync -->
<section
  id="playing-with-readline-sync"
  aria-labelledby="playing-with-readline-sync"
  data-item="Playing with readline-sync"
>
  <h2><a href="#playing-with-readline-sync">Playing with `readline-sync`</a></h2>
   
You can find the documentation for the `readline-sync` package [here](https://www.npmjs.com/package/readline-sync). Take your time to read it. And as you are reading it, try the examples for yourself, as described below.

There is nothing that I can tell you about the `readline-sync` package that I did not find in this documentation page, so you can learn about it exactly the same way that I did.

<details class="sandbox" open>
<summary>Micro projects in a sandbox</summary>
When I am working on a big project and I need to learn a new technique, I:

* Stop working on the big project
* Create a separate micro project, where I can:
  * Build a proof-of-concept
  * Make experiments
  * Make mistakes
  * Test ideas
  * Develop my understanding
  * Build a working template that I can import into my big project
  * Write up comprehensive notes for future-me

Whenever you see a sand-coloured box like this, you'll get the chance to do something similar.

1. Open a new Terminal

![Use Terminal > New Terminal, or click the + button to create a new Terminal](images/newTerminal.webp)

2. Assuming that your Terminal is open on the parent directory (`My Learning Journey`), you can run:

```tex-w
code Nail_It/Tests/readline-sync/index.js
```
The `code` at the beginning of the command refers to VS Code. This line tells VS Code to create a file called `index.js` at the location given. You will see a new editor tab open, with the name `index.js •`. The big round dot means "this file has not been saved yet", so you need one more step to bring it into existence.

![The `code` command will open a new tab in the text editor](images/newFile.webp)

3. Save the empty file

VS Code will now create all the intervening folders and the `index.js` file itself.

![VS Code creates all the folders when it saves the `index.js` file](images/savedFile.webp)

4. Run the command:

```tex-w
cd Nail_It/Tests/readline-sync 
```

This will [`c`hange the `d`irectory](https://www.earthdatascience.org/courses/intro-to-earth-data-science/open-reproducible-science/bash/bash-commands-to-manage-directories-files/#change-current-working-directory-cd) so that this new Terminal window will now be active in the new `readline-sync` directory.

![Use `cd` to change directory](images/cdToNewDir.webp)

5. Visit the [readline-sync documentation page](https://www.npmjs.com/package/readline-sync)
6. Copy the code that is given for the first "Simple case" (slightly edited below):

```javascript
const readlineSync = require('readline-sync');
 
// Wait for user's response.
const userName = readlineSync.question ('What is your name? ');
console.log('Hi ' + userName + '!');
 
// Handle secret text (e.g. password).
const favFood = readlineSync.question (
  'What is your favorite food? ',
  { hideEchoBack: true } // shows `*` instead of typed text.
);
console.log('Oh, ' + userName + ' loves ' + favFood + '!');
```

<details class="note" open>
<summary>var</summary>
The original documentation uses `var` to declare a variable name.

The `const` and `let` keywords were added in 2016, and they do a much better job than `var`, which is now outdated. You will see `var` only in older projects, and in certain very specific cases where a variable may be re-declared.

You can learn more about `var`, `const` and `let` in [this freeCodeCamp article](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/).

</details>

7. Paste this code into your file at `Nail_It/Tests/readline-sync/index.js`
8. Run the command:

```tex-w
node index.js
```

9. Answer the questions that you are given. Notice that you have to press Enter at the end of each answer.

10. Now the playful part:
    * Edit the code in `index.js` so that you see different questions when you run `node index.js`.
    * After each change, and before you run `node index.js`, see if you can predict what will happen.
    * Pay attention to where spaces are needed.
    * See if you can understand how the `+` operator works when it is placed between two strings. (You'll see this in more detail later.)
    * See what happens (if anything) when you change single quotes (`'`) to double quotes (`"`). What happens if you use one of each for the same string?
    * What happens if you use `hideEchoBack: false`?
  
<details class="note" open>
<summary>The options object</summary>

Notice how `hideEchoBack` is written inside curly braces (`{ ... }`). This structure generates an _object_ which has key-value pairs. Here's another object to illustrate this:

```javascript-#
{ key: "value", anotherKey: "another value", "a third key": 3 }
```

There are rules about how the names of the keys can be formed. They are similar to the rules for variable names. However, you can create a key name with any character in it, if you enclosed the key name with quotation marks.

</details>

Take your time. Have fun. Move on to the next section when you are ready.

</details>

</section>