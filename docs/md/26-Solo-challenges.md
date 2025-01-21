<!-- Solo challenges -->
<section
  id="solo-challenges"
  aria-labelledby="solo-challenges"
  data-item="Solo challenges"
>
  <h2><a href="#solo-challenges">Solo challenges</a></h2>
  
If the AI is not ready to play yet, you can focus on creating an activity for a solo player. Below is a list of  challenges for you.

I'll treat each one in a separate section.
  
### 1. After the nail is hit, can you show it at its new length?
  
```tex-w
-===========| The nail is 12 units long.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 3
-========|
```

### 2. Can you show how hard the solo player chose to hit the nail?

```tex-w
-===========| The nail is 12 units long.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: 2
-=========| You hit the nail firmly.
```

### 3. Can you remove the question after it has been answered?

```tex-w
-===========| The nail is 12 units long.

-==========| You hit the nail gently.
```

### 4. Can you let the solo player hit the nail several times in a row?

```tex-w
-===========| The nail is 12 units long.

-========| You hit the nail hard.

-======| You hit the nail firmly.

-=====| You hit the nail gently.

-===| You hit the nail firmly.

-| You hit the nail hard.
```

### 5. Can you show the winning situation... even if the solo player hits the nail too hard the last time?

```tex-w
-===========|  The nail is 12 units long.

-==========|  You hit the nail gently.

-========|  You hit the nail firmly.

-=====|  You hit the nail hard.

-===|  You hit the nail firmly.

-==|  You hit the nail gently.

-|  You hit the nail firmly.

| You hit the nail hard.

You win!
```

### 6. Can you show the point of the nail only at the start of the game?

```tex-w
-===========|  The nail is 12 units long.

=========|  You hit the nail hard.

=======|  You hit the nail firmly.

====|  You hit the nail hard.

==|  You hit the nail firmly.

=|  You hit the nail gently.

| You hit the nail firmly.

You win!
```

### 7. Can you align all the text nicely?

```tex-w
-===========| The nail is 12 units long.

==========|   You hit the nail firmly.

=========|    You hit the nail gently.

=======|      You hit the nail firmly.

====|         You hit the nail hard.

==|           You hit the nail firmly.

=|            You hit the nail gently.

|             You hit the nail firmly.

You win!
```

### 8. Can you give the nail a different length each time?

For example: 

```tex-w
<i>-===========| The nail is </i><b>15</b><i> units long.</i>
```

### 9. Can you stop the game early, before there is a winner?

If the human player presses `0` when asked how hard to hit, can you make the game end gracefully?

```tex-w
<i>-==============| The nail is 15 units long.

============|    You hit the nail hard.

[1] gently
[2] firmly
[3] hard
[0] CANCEL

How hard do you plan to hit? [1, 2, 3, 0]: </i> <b>0

Thanks for playing!</b>
```

</section>