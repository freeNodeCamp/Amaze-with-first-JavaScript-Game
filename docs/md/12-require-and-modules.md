<!-- require and modules -->
<section
  id="require-and-modules"
  aria-labelledby="require-and-modules"
  data-item="require() and Modules"
>
  <h2><a href="#require-and-modules">`require()` and Modules</a></h2>

Here's an edited version of the first few lines of code:

```javascript
const readlineSync = require("readline-sync")
const whoStarts = "If you want to start, type Y..." // shortened
```
```javascript-s
// lines skipped //
```
```js-#14
let player = readlineSync.keyInYN(whoStarts)
console.log("player:", player)
```

You've seen that `readlineSync` somehow allows you to type a letter in the Terminal, and then JavaScript knows if that letter was a `Y` or not. But where does `readlineSync` get all this power from? And how could you have guessed to use `.keyInYN()` to make this happen?

## `require()` - a global function

The function `require()` is a native part of JavaScript. You can use it anywhere. It expects the name the parameter to be either...

* The name of a module
  
... or:

* The path to a file which contains a module script.

It then loads the module script that it finds at the designated place, and makes it available to your script.

## Finding `readline-sync`

When NodeJS reads `require("readline-sync")`, it understands that `"readline-sync"` is not the path to a file, so it looks:

* Inside the `node_modules` folder for a folder with the same name
* Inside that folder for a `package.json` file
* Inside the `package.json` file for an entry for "main"
* For the file named by "main".

Here's what it finds:

```json-#21
  "main": "./lib/readline-sync.js",
```

![How require finds the node_modules file to load](images/requiring.webp)

JavaScript now reads all the code that it finds in the file at `node_modules/readline-sync/lib/readline-sync.js`, and executes it.

<details class="tldr" open>
<summary>TL;DR</summary>
**Don't worry. I don't expect the code below to mean anything to you. I'm just showing you that all the code in a Node Module package is openly available. There's no hidden magic.** 

The code in `readline-sync.js` includes the following (minor edit for clarity):

```javascript-#1220
<i>function _keyInYN(query, options, limit) {
  var res;
  if (query == null) { query = 'Are you sure? '; }
  if ((!options || options.guide !== false) &amp;&amp; (query += '')) {
    query = query.replace(/\s*:?\s*$/, '') + ' [y/n]: ';
  }
  /* eslint-disable key-spacing */
  res = exports.keyIn(query, margeOptions(options, {
    // -------- forced
    hideEchoBack:       false,
    limit:              limit,
    trueValue:          'y',
    falseValue:         'n',
    caseSensitive:      false
    // mask doesn't work.
  }));
  // added:     guide
  /* eslint-enable key-spacing */
  return typeof res === 'boolean' ? res : '';
}</i>
<b>exports.keyInYN = function(query, options) {
  return _keyInYN(query, options);
};</b>
```

There, on line 1240 in `node_modules/readline-sync/lib/readline-sync.js`, is the function `keyInYN`, which your JavaScript can now use, thanks to the `require()` function.

</details>

## A black box

You can consider the contents of `node_modules` to be a black box. You don't need to understand how it works, just like you don't need to understand how your phone works. All you need to know is that, if you give the right input, you will get the output that you need.

I've just shown you how to look inside this black box, so that you can see the sort of content that it contains, but you may never need to do this again. It's enough to know that it works.



</section>