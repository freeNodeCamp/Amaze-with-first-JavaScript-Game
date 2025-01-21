<!-- A First JavaScript File -->
<section
  id="a-first-javascript-file"
  aria-labelledby="a-first-javascript-file"
  data-item="A First JavaScript File"
>
  <h2><a href="#a-first-javascript-file">A First JavaScript File</a></h2>
  
A successful business has many employees, in many different offices on many different floors, often in many buildings in many cities. A successful development project has the same level of complexity. There will be many different files, in many different folders on many different computers...

## Organizing your files

This project is simple. It will only use one file. But you should be ready to grow big quickly, and plan accordingly. It's therefore important to structure your work properly.

1. From the File menu in VS Code, choose `Open Folder`
2. Use the dialog to create a new folder that will hold all your projects that you create from tutorials, like this one. Save it in your Documents folder, or in a place where you can quickly find it again.
3. You could call it `My Learning Journey` or something like that.
4. Inside this generic folder, create a folder specifically for this project. I'm going to assume that you call it `Nail_It`, and I will refer to it by that name from now on.

![Create a folder called Nail_It](images/09NewFolder.webp)

5. Inside the `Nail_It` folder, create a file called `main.js`

![Create a file in Nail_It called main.js](images/10NewFile.webp)

The `.js` extension stands for JavaScript. The file that is at the heart of a project is often called `main`.

## Your first script

The first thing on the [list of things that the game can do](#what-needs-to-be-done) is "The game uses text". So the first thing you should get your first JavaScript file to do is to use text.

[The convention since 1978](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program) is to get your very first program to say "Hello World!"

1. In your file at `Nail_it/main.js`, type the following text:

```javascript
console.log("Hello World")
```

2. Save your file.

<details class="tip" open>
<summary>Auto-save</summary>
Even better: use the menu item File > Auto Save to tell VS Code to save your file as soon as you have made a change in it. This means that every time you run your code, you can be sure that you are running the most recent version, and not a file that you have changed but forgotten to save.

![Set up Auto Save, so that your latest changes are always saved](images/05AutoSave.webp)

</details>

## Executing your script
To run this file as a program, you will need to open a Terminal.

1. Choose the menu item Terminal > New Terminal.

By default, a new Terminal will appear a the bottom of the VS Code window.

2. Check the name of the folder that is shown in the Terminal. If it is not `Nail_It`, then type `cd` (which means `change directory`) and drag the name of the Nail_It folder into the Terminal, then press Enter.

![`cd` into the Nail_It directory](images/08cdToNailit.webp)

3. When the Terminal is active in the Nail_It directory, type...

   ```tex-w
   node main.js
   ```
   ... as shown in the Figure 5 above.
   
You should see `Hello World!` printed into the Terminal.

<details class="tip" open>
<summary>Running any JavaScript file the Terminal</summary>
You'll be using `node` to run other little test scripts soon.

If you [downloaded the source files](https://github.com/MERNCraft/Nail-It/scripts.zip){download=""} earlier, you can open the folder that contains them in a new VS Code window, and use the Terminal in that window to run any of the files. For example, you could try something like this:

```tex-w
cd /path/to/downloaded/folder
node completed.js
```

The completed game also remembers your score against the computer.

(Remember that you type `cd ` (followed by a space) and then can drag the icon of any folder into the Terminal window to navigate to that folder.)

</details>

<details class="note" open>
<summary>semicolons: `;`</summary>
JavaScript considers that any block of code that is followed by a semicolon (`;`) is a complete instruction. But JavaScript is user-friendly. JavaScript also looks at any block of code that is followed by a new line character and thinks: "Hmm... is this a complete instruction?"

In most cases, JavaScript programmers write one instruction per line, so putting a semicolon at the end of each line is usually not necessary. There are, however, some cases where a single instruction may take several lines. There are cases where a semicolon is essential.

I prefer not to use semicolons except in these special cases.

Sometimes, though, I will write two instructions on the same line, separated by a semicolon. So don't be surprised if you see this.
</details>

</section>