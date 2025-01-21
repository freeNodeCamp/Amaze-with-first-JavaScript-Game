<!-- process and process.exit() -->
<section
  id="process-and-process-exit"
  aria-labelledby="process-and-process-exit"
  data-item="process and process exit()"
>
  <h2><a href="#process-and-process-exit">process and process exit()</a></h2>
  
When you run a script using `node` in the Terminal, NodeJS creates an object called `process`, which contains all properties and methods that let it do its job.

One of these methods is `exit()`, which will allow you to stop the script from running. A property that you will probably use in future projects is `argv`, which is an array describing which version of `node` is running, which file it is running, and any more text you may have typed after `node main.js` in the Terminal.

<details class="tldr" open>
<summary>What `process` looks like</summary>

Here's how you can see what `process` looks like. (Your values for `version` and `argv` may be different.)

1. Add these two lines at the very beginning of your `main.js` script. (This is only temporary. You will remove them very soon.)

   ```javascript
   <b>console.log(process)
   process.exit()</b><i>
   
   const {
     keyInYN,
     keyInSelect
   } = require('readline-sync')
   
   const rules = `Let's knock a nail into this computer!</i>
   ```
   ```javascript-s
   // All the other lines skipped //
   ```

2. In the Terminal, run:

```tex-w
node main.js
```

3. In the Terminal, you should see over 800 lines of data printed. I have just given you the highlights below:

```bash
<i>process {
  version: 'v23.1.0',
  versions: {
    node: '23.1.0',
    acorn: '8.12.1',</i>
```
```bash-s
// many lines skipped //
```
```bash-#29
    <i>zlib: '1.2.12'
  },</i>
```
```bash-s
// many lines skipped //
```
```bash-#269
  <i>kill: [Function: kill],</i>
  <b>exit: [Function: exit],</b>
  <i>finalization: [Getter/Setter],</i>
```
```bash-s
// many lines skipped //
```
```bash-#384
  <i>title: 'node',</i>
  <b>argv: [
    '/opt/homebrew/Cellar/node/23.1.0_1/bin/node',
    '/Users/james/My Learning Journey/Nail_It/main.js'
  ],</b><i>
  execArgv: [],</i>
```
```bash-s
// many lines skipped //
```
```bash-#826
  <i>[Symbol(shapeMode)]: false,
  [Symbol(kCapture)]: false
}</i>
```

<details class="question" open>
<summary>process.exit() stops the script</summary>
Did you see how the line `process.exit()` prevented the rest of your script from running?

Can you imagine how you will use this to stop the game if the human player presses `0` for the force for hitting the nail?

</details>
OK? That was too much information?

4. You can delete these two lines from the beginning of your script, now that you know about `process.exit()`. 

```javascript-#
   <s>console.log(process)</s>
   <s>process.exit()</s>
```
```javascript-s
```
```javascript
   const {
     keyInYN,
     keyInSelect
   } = require('readline-sync')
   
   const rules = `Let's knock a nail into this computer!</i>
   ```
   ```javascript-s
   // And your script continues //
   ```
</details>
</section>