## What are loops?
---------------
Loops are things made to make your life easier, at least, if you know how to use them.  
Loops can be powerfull when used right, but can also bring down any script.  
Loops come in handy when you need to go through a array, or when you need to do the same thing x times after eachother.  
The loops available in the Athena scripting language are **For**, **While** and **Do ... While**.  
All of those will be covered in this article, with their own examples.  
Also, the special loop commands break; and continue; will be covered.  
The intention of this page is that you will get to understand how loops work, and how to use them properly.

### For Loop
The for loop is probably the most seen loop used in rAthena scripting, this is usually used to loop through arrays and execute a series of commands for each array entry.  
But you can use it every time you need to execute a series of commands x times.  
For loops are build up of 3 or 4 parts, depending on how they are used.  
The general buildup for a For loop is as following:
```
for (initialization(1); condition(2); update(3)) {
   Code to execute(4);
}
```
If you don't know what all parts do, don't panic, since I'm going to explain that now ;)

-   **variable initialization:** This part of the for loop usually contains a 'set' command to initialise the counter variable. Most codes use @i, @j etc as those counter variables.
-   **condition:** This part is a logical expression, the same thing as the one you find inside a 'if'. For example, @i &lt; 10, will be true as long as the variable @i is smaller then 10.
-   **variable update:** This, together with the expression, is the loop part of the script. Each time the for loop restarts (that is, when the previous run has ended, and it jumped back to it) the expression is evaluated. If the result of the expression is true, then the action will be executed, that is why the action usually contains a increment on the counter variable. The action is not executed when the loop is initiated (the initialization part is used then).
-   **Code to execute:** This is, in theory, a optional part of the for loop. This part is usually used for any other commands then the counter increase done in action. Basically, all commands should be able to run in the action field. In the Athena Script Language, all of the code (with exception of the increment) is put into this part.

After all that explaining, it's time for a little example:
```
for (set @i,0; @i < 10; set @i,@i+1) {
   mes @i;
}
```
This is one of the most simple for loops you can think of, but it serves well as executable example. When this for loop is started, a message window will be created with the following context:
```
0
1
2
3
4
5
6
7
8
9
```

	**Note**: 
	The 10 is not there, since @i &lt; 10 is false when @i is 10.  
	What the loops does is the same as explained above.  
	Firstly, the initilization is done (set @i,0;) and the expression is evaluated.  
	Then, the code is executed (mes @i;) and the end of the loop is reached,  
	so it jumps back to the first part, and executes the action (set @i,@i+1) (See how this replaces the initialization part?).  
	Then it starts evaluating the expression (@i &lt; 10), which is true since @i is 1.  
	Because the expression is true, the code inside of the curlies is executed.  
	This keeps on going until the expression is false, which will happen once @i is 10.  
	As soon as that happens, it quits the loop and continues on the first line after the closing curly.

### While Loop

This loop is almost the same as a for loop, but less automated.  
With this loop, you'll have to initialize the variable yourself, and increase it yourself.  
In some situations, this is better then the for loop.  
The general format for a **while** loop only contains out of two parts:
```
while (expression(1)) {
   Code to execute(2);
}
```
Both of these parts are the same as in the for loop, and the way it works is also similar.  
When the code is reached, the while loop evaluates the expression.  
If that expression returns true, the code will be executed.  
A while loop will only stop when break; is used, or the expression returns false.  
A simple example, doing the same as in the for loop example above, is this:
```
    set @i,0;
    while (@i < 10) {
        mes @i;
        set @i,@i+1;
    }
```
The result will be exactly the same.  
As long as @i is smaller then 10, the code is executed. While loops can be used for a lot of things, including a (theoretically) never ending cycle:
```
    while (1) {
        mes "I won't go away!";
        next;
    }
```
	**Note:** 
	The above is a script that will need you to relog!

### Do ... While Loop
Ah... We've already reached the last loop type.  
Wow, I actually managed to write stuff about the for and while loop eh...  
Well then. This loop is basically the same as a while loop, only the way it is executed is slightly different (and the same goes for the coding).  
Since there isn't much I can explain on loops anymore, I'll just start with the general format:
```
    do {
        Code to execute(1)
    } while (expression(2));
```
See how the code and expression changed?  
Basically, this is a inverted while loop, and the do is only there to let the engine know there is a loop.  
Once this part of code is reached, the code will be executed first (!).  
Once the code is executed, the expression is evaluated. If the expression returns true, it loops back to the do, and runs the code again.  
If you noticed that this way, the code is always executed at least once, good job =).  
If you didn't, well, then you know it now :P.  
This is because the engine executes scripts from top to bottom (excluded goto's and such), that way, the engine will first find the do {, then the code, and then the while.  
Again, the simple example from before:
```
set @i,0;
do {
   mes @i;
   set @i,@i+1;
} while (@i < 10);
```
Again, the results will be the same. In terms of executing, the initialization is done before the do, then the code is executed and the counter is increased. Then the expression is evaluated, and when it returns true, jump back to the do. Also, this is a little more dangerous version of while. Because the expression is evaluated afterwords, using it incorrectly will cause a infinity loop. A BAD example is this:
```
set @i,0;
do {
   mes @i;
   set @i,@i+1;
} while (@i != 0);
```
	**Note:**  
	This easily happens when comparing two variables in the expression.

### Break and Continue

These two commands are really useful when executing loops, since they can skip parts of the loop, which decreases the execution time. break; completely exits a loop, while continue; will only skip the rest of the current run.

Once a break; is encountered, the script directly jumps to the line after the loop's body, and thus exiting the loop. For example:
```
    for (set @i,0; @i < 10; set @i,@i+1) {
        if (@i == 4) break;
        mes @i;
    }
```
This will break out of the loop once @i is equal to 4, meaning the the result of this loop is:

    0
    1
    2
    3

Continue also quits a part of the loop, but will jump to the last line (or the beginning) of the loop. That way, only that run of the loop is not executed. A simple example for continue:
```
    for (set @i,0; @i < 10; set @i,@i+1) {
        if (@i > 5 && @i <= 8) continue;
        mes @i;
    }
```
This will return:

    0
    1
    2
    3
    4
    5
    9
    10

The 'mes @i;' code is not executed when the if in front of the continue; is true, which is for @i &gt; 5 and @i &lt;= 8 (5,6,7,8) and thus, those will not be shown in the message window.

## Final Notes
-----------
I might add some more to this page once I think of things missing. Do not hesitate to add them yourself, or to contact me if you don't dare to edit this page ;P.  
Good luck with loops =)   
-- Yhn 15:51, 28 June 2007 (CDT)

One note by me: when your loop has only one line (aside from the command word/s), you can dispose of the { }. One line can be:
```
     if (@a != @b)
         getmapinfo @map$,@x,@y,0;
     else if (@a > @b)
          set @c,getcharid(3);
     else if (@a < @b)
          announce "Foo",bc_map|bc_yellow;
     else
          close;
```