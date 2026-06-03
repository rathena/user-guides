This article will go in-depth on various ways to script smartly and optimize your scripts. There is no real manual to use this article, besides reading it all, and trying to remember.

## Tips
### If-Statements
There are several ways to make your if-statements function better and faster, and make them more readable at the same time.

#### Use the switch statement:
Let's say we had the following code:
```
if(getarg(1) == 0) cutin "kafra_06",2;
if(getarg(1) == 1) cutin "kafra_05",2;
if(getarg(1) == 2) cutin "kafra_04",2;
if(getarg(1) == 3) cutin "kafra_03",2;
if(getarg(1) == 4) cutin "kafra_02",2;
if(getarg(1) == 5) cutin "kafra_01",2;
if(getarg(1) == 6) cutin "kafra_09",2;
if(getarg(1) == 7) cutin "kafra_08",2;
if(getarg(1) == 8) cutin "kafra_09",2;
```
We could replace that entire block by the switch command.  
This commands looks up the value that is provided, and jumps to the according case.  
Don't worry, if it isn't clear yet, let's go to the replacement code first:
```
switch(getarg(1)){`
   case 1: cutin "kafra_05",2; break;
   case 2: cutin "kafra_04",2; break;
   case 3: cutin "kafra_03",2; break;
   case 4: cutin "kafra_02",2; break;
   case 5: cutin "kafra_01",2; break;
   case 6: cutin "kafra_09",2; break;
   case 7: cutin "kafra_08",2; break;
   case 8: cutin "kafra_09",2; break;
   default: cutin "kafra_06",2; break;
}
```

As you can see, each if-line has been replaced by a case-line.  
The command switch looks up the value of getarg(1).  
If this would be 5, then it would jump to "case 5", do the cutin, and then break.  
Break makes it jump to after the right curly bracket ('}').  
If it finds getarg(1) to be 8, it jumps to "case 8", and does the same there.  
And the best part of the switch statement might be the default one.  
It kind of replaces the following really unoptimized line:

`if(getarg(1) != 1 && getarg(1) != 2 && getarg(1) != 3 .... && getarg(1) != 8) cutin "kafra_06",2;`

In English, this means, if the value of getarg(1) does not have an accompanied case, it will jump to the default label.

#### Use the brackets if you're executing more than 1 statement in 'if' statements.
If you have a piece of code, that needs to check for a condition, and do multiple things,  
then you can make it so, that you only have to use one if-line, instead of 4, 5, 1000 or something else.  
To do this, you will have to use the curly brackets.  
They tell the script engine that everything between the curly brackets belongs to the command before the left curly bracket.  

For example, take the following unoptimized code:
```
if(@var == 1) mes "haha";
if(@var == 1) mes "heha";
if(@var == 1) mes "hiha";
if(@var == 1) mes "hoha";
if(@var == 1) mes "huha";
```
This can be replaced by the following:
```
if(@var == 1){
   mes "haha";
   mes "heha";
   mes "hiha";
   mes "hoha";
   mes "huha";
}
```

What is so optimized about this?  
Well, in this case, you can easily see that each if-statement is completely the same, but keep in mind, that the script engine needs to do each if-statement each time it sees one.  
So, in the top part, it needs to do 5 checks. In the replacement, it only has to do one single check.  
Based on that check, it either executes the code between the { and } or skips to right after the }.  
Also, from a writer's point of view, this is exactly the same for you.  
You see in one glance that the entire part between the curly brackets belongs to the if(@var == 1) statement,  
so you do not have to check each if-statement individually to see that they are all the same.

#### Use if...else if you're not expecting more than 2 values.
When you evaluate if a variable meets a certain condition, and you need to do something when that condition is true,  
and something differently when the condition is false, then you really want to use the if...else combination.  
This does not only make it more clear for yourself, but also faster for the script engine, because it only needs to evaluate one if-statement instead of two.  

Take this unoptimized piece of code for example:
```
set @win, rand(2); // Generates 1 or 0
if(@win == 1){
   mes "You win!";
}
if(@win == 0){
   mes "You lose!";
}
```
This can be replaced by the following piece of code:
```
set @win, rand(2);
if(@win == 1){
   mes "You win!";
} else {
   mes "You lose!";
}
```

### Variable Use
A lot of people do not pay any attention when it comes to using variables.  
They randomly choose a type of variable and use it, or even use a variable when it isn't needed.  
You must keep in mind though, that rAthena has a limited amount of variables it can use, for (global) account and permanent player variables.  
Therefor, you want to minimize the use of it. This section will contain some examples of how to minimize that use.

#### Use binary methods to store large number of flags (1 and 0).
What a lot of people do not know, is that a single variable can store up to 32 different flags, or values. And with this, I do not mean the use of an array, but really a single variable. This comes in very handy when you are only using a 1 or 0, for example: "set @win, 1;". In a normal situation, you can only win or lose, so it can only be a 1 or 0.
But, let's see how this translates into normal code:

Bad code:
```
flag1 = 1;
flag2 = 1;
flag3 = 0;
flag4 = 1;
flag5 = 0;
if(flag1) mes "flag1 is checked";
```
Good code:
```
set flags, 26; // (equivalent to: 16|8|0|2|0 [binary 11010])
if(flags&16) mes "flag1 is checked"; // 11010 & 10000 > 0 (10000)
```

As you can see, only one variable used instead of 5, and it contains all the values of those five variables. (In this case, it is also a lot shorter, but that doesn't have to be the case.)
Note:  
Using binary methods to store variables require that you have at least some knowledge on how to use binary values.  
This is what you may call advanced scripting, so it is quite normal if you do not understand it right away.

### Infinite For Loops
By nature, the rAthena Scripting Engine has a limit on the amount of loops that can go through in a specific amount of time,  
thus halting the script to eliminate the ever dreadful 'Infinite Loop'. However, there is a way around this:

This script below, would actually halt around 682 give or take a few loops, due to preventions on infinite loops.
```
for (set .@a, 0; .@a < 10000; set .@a, .@a + 1) {
  debugmes .@a;
}
```

This method used below slows the processes down by a millisecond. This works because each time 'sleep' or 'sleep2' is used, the script's gotocount is reset.
```
// Supposing you have 10,000 entries... let .@b = Total Entries, .@a is your splicing filter every 500 entries
while (.@b < 10000) {
  for (set .@a, .@b; .@a < .@b + 500; set .@a, .@a + 1) {
    debugmes .@a;
  }
  set .@b, .@a;
  sleep 1;
}
```

### While (!getmapxy())

The standard getmapxy() returns 0 if the player is found, and 1 if the player is offline.  
By using the !getmapxy() feature, while the value does NOT have a value aka it's 0, loop (player still online and active).  
This can also be written `while (getmapxy() == 0) { }`:
```
while ( !getmapxy(.@map$, .@x, .@y, 0 ) ) {
  if ( .@map$ != "prontera" ) { // check the player has warped to other map or not
    dispbottom "gone"; 
    end; 
  }
  dispbottom .@x +" "+ .@y; // report the position every N second
  sleep2 1000; // pause the script
}
end; // when the player logout, the loops break
```
### Dynamic Menu
These menu's help in many different ways.  
Perhaps you have an unknown list of items and you want the user to select one.  
How do you know which item it was?  
What if you have a menu based on certain criteria?  
This menu can then change based on the information per player.  
This is where a dynamic menu can come into play.

The basis of a Dynamic menu is as follows:  
Knowing what option a player chooses, even though the option chosen may be random.

This is easily done with a small example of a simple (Item Required Warper)
```
prontera,158,174,4 script  MyDynWarper 88,{
// Take Locations
setarray .@maps$[0],"Prontera","Morocc","Geffen","Izlude";
setarray .@mapx[0],158,100,200,300;
setarray .@mapy[0],174,100,200,300;
// Set Items Needed
setarray .@items,501,502,503,504; 
// Generate Menu
for (set .@a, 0; .@a < getarraysize(.@maps$); set .@a, .@a + 1) {
  if (countitem(.@items[.@a])) {
    set .@menu_maps$[getarraysize(.@menu_maps$)], .@maps$[.@a];
    set .@menu_index[getarraysize(.@menu_index)], .@a;
  }
}  
// Generate the Menu String
set .@menu$, .@menu_maps$[0];
for (set .@a, 1; .@a < getarraysize(.@menu_maps$); set .@a, .@a + 1) {
  set .@menu$, .@menu$ + ":" + .@menu_maps$[.@a];
}
// Query Selection
set .@a, select(.@menu$) - 1; 
warp .@menu_maps$[.@a], .@mapx[.@a], .@mapy[.@a];
end;
}
```
### Compact IF Statement
While, it looks messy, it can help shorten and quicken simplified IF/ELSE statements.  
Example below includes a before and after:

Before:
```
if ( team == 1 )
    mes "You are team Red";
else
    mes "You are team Blue";
```
After:  
`mes "You are team "+( ( team == 1 )?"Red":"Blue" );`
