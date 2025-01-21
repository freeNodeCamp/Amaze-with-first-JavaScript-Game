<!-- Asking Questions -->
<section
  id="asking-questions"
  aria-labelledby="asking-questions"
  data-item="Asking Questions with readline-sync"
>
  <h2><a href="#asking-questions with readline-sync">Asking Questions</a></h2>
  
To be exact, there is another line of text that appears when the game starts:

![The last line of text is a question about who is going to play first](images/yesNoPrompt.webp)

## NodeJS Packages

NodeJS does not provide an out-of-the-box solution for asking questions.

You can think of NodeJS like a food mixer: a powerful engine to which you can attach different accessories for different purposes. Some accessories are sold separately. 

![A food mixer with extra accessories](images/Kenwood_Chef-01ASD.jpg){data-title="File:Kenwood Chef-01ASD.jpg" data-credits="[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.en) by [Asurnipal](https://commons.wikimedia.org/wiki/User:Asurnipal) | [source](https://commons.wikimedia.org/wiki/File:Kenwood_Chef-01ASD.jpg)"}

The "accessories" that you can add to NodeJS are called "modules" or "packages". The web site [`npm`](https://www.npmjs.com/) ([whose name _does not_ mean Node Package Manager](https://www.npmjs.com/package/npm/v/10.8.0#faq-on-branding)) provides thousands of open-source packages, many of which are used [millions of times every month](https://www.bairesdev.com/blog/most-popular-npm-packages/#most-popular-npm-packages).

A popular package that you can use to ask questions in the Terminal is [readline-sync](https://www.npmjs.com/package/readline-sync). (The "sync" is short for "synchronous". )

## Installing readline-sync

When you installed NodeJS, a program called `npm` was installed at the same time. You can use this program to fetch NodeJS packages from the `npmjs.com` website, and include them in your project. Here's how you can do this:

1. Make sure your computer is connected to the Internet
2. In the Terminal for your `Nail_It` directory, run:

```tex-w
npm install readline-sync
```

<details class="tip" open>
<summary>npm i</summary>
Like me, and most programmers, you can be lazy. You can use `i` as a shortcut for `install`.

This command will have exactly the same effect:

```tex-w
npm i readline-sync
```

</details>

![Installing readline-sync](images/installReadlineSync.webp)

You'll see several things happen:

1. There will be a burst of activity in your Terminal as `npm` requests and then receives the files that you need. 
2. A folder called `node_modules` will be created in your `Nail_It` folder
3. Two new files will be added to your `Nail_It` folder:
   * `package.json`
   * `package-lock.json`

## `package.json`

The contents of `package.json` should look something like this (the version number may be different):

```json
{
  "dependencies": {
    "readline-sync": "^1.4.10"
  }
}
```

<details class="tldr">
<summary>JSON and package.json</summary>
`JSON` stands for "JavaScript Object Notation". A `.json` file can be used to store hierarchical information. It has a very strict file structure. If there is a comma too few or a comma too many in `package.json`, `npm` won't be able to read it. If you use backticks or single-quotes (`'`) instead of double-quotes, `npm` won't be able to read it. Treat `package.json` nicely.

The file `package.json` contains information that ensures that your project will work even if it is copied to someone else's computer. In this particular case, it says: "This project needs the `readline-sync` Node package, and it was built using version "1.4.10", so it should work with that version or a more recent one."

Some Node packages require other Node packages in order to work correctly. The `package-lock.json` file contains details of every package that was installed, and every package that _each of those packages_ installed. If you send a copy of your project to a colleague, the `package-lock.json` file will ensure that your colleague is working with exactly the same Node packages as you. This eliminates many cases where "It works on my computer!" is an issue.

</details>

## Using readline-sync

Before you can use `readline-sync`, you need to load its code into your own script. You can use the JavaScript function `require`, as shown in the code below. 

<details class="pivot" open>
<summary>Get it working, then learn how</summary>
Try this out. 

1. Edit your script
2. In the Terminal, run

```tex-w
node main.js
```
3. In the Terminal, press the `y` key, in response to the question.

The expected output is shown in Figure 11 below.

I'll explain in the next section exactly what is happening, why `player: true` appears in the Terminal when you run your script, and how you can find out for yourself how to make all this happen.

</details>

```javascript-w
<i>const readlineSync = require('readline-sync')
const whoStarts = `If you want to start, type Y.
If you want me to start press any other key. `

console.log(`Let's knock a nail into this computer!

* Each player takes a turn to hit the nail once.
* A player can hit the nail in one of three ways:
  gently, firmly, hard.
* Depending on the force used, the nail will be
  driven more or less deeply into the Terminal.
* The player who knocks the nail all the way in
  is the winner.

Are you ready?
`)</i>

<b>let player = readlineSync.keyInYN(whoStarts)
console.log("player:", player)</b>
```

![Integrating `readline-sync` into your project](images/useReadlineSync.webp)

</section>