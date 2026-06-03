Scripts control all NPCs, warps, mob spawns, shops, and quests you will find in the game and nearly everything else!  
Clearly they play a large part in customizing a server, but learning isn't very hard.

Scripts are built up of predefined script commands, all of which can be found in (for explanations, see [Script Commands](https://github.com/rathena/rathena/blob/master/doc/script_commands.txt).  
Every line should begin with a command and the argument it takes, and must end in a semicolon (or you'll get mapserver errors!).  
Arguments are usually separated by commas, and are sometimes contained in parentheses () or curly brackets {}.  
Tabs and proper indentation are standard scripting measures.

Scripts are saved as text (\*.txt) files, so all code can be written in Notepad.  
There are also a lot of scripting programs to use:  
the most recent and comprehensive one is [Vince's eNPC](http://rathena.org/board/topic/56484-enpc-script-editor/).  
All defined functions are highlighted, with an autocomplete feature included, and pressing "F1" will display the corresponding explanation for any command.

## Structure

### NPC

A **Script NPC** will look something like the following:

`prontera,156,145,4 `<tab>` script `<tab>` Test NPC `<tab>` 58,{`

The first section is the map location of the NPC, followed by its coordinates in x,y and the direction the NPC will face.  
Direction numbers are counted counterclockwise in 45º increments, with 0 being the center:
```
[1][8][7]
[2][0][6]
[3][4][5]
```
After the first tab, the type of script is defined.  
For our purposes, it'll stay "script" for now, but can also be function, shop, or cashshop, for starters.  
The name of the NPC is next. You can use up to 24 characters, so make it unique!  
Any duplicates will cause warnings or errors, and the NPC will just be automatically renamed anyway.
The last number is for the sprite (Ai4rei's sprite list can be found [here](https://nn.ai4rei.net/dev/npclist/?qq=8).  
It's followed by a comma and open curly bracket, marking the beginning of the script contents.  
Of course, the script must also end in a curly bracket.

#### Function

A **Function script** will look almost identical to:

`function `<tab>` script `<tab>` Function Name `<tab>` {`

The words "function" and "script" won't change; the name must also be unique. All functions can be called using the "callfunc" command.

#### Shop

A **Shop** starts like a normal script:

`prontera,156,145,4 `<tab>` shop `<tab>` Fruit Store `<tab>` 58,512:-1,513:1000`

The first section defines the map, coordinates, and direction. The word "shop" replaces "script" (alternately, "cashshop" will use Cashpoints instead of Zeny). The name and sprite ID follow, then a comma.
Items in the shop are defined in an ID:Price format. A price of -1 uses the default price in item_db.txt. Be sure the price is not too low, or a you will open a Zeny exploit in your server!

### Fundamentals

You can always look up commands that you need--even the best scripters don't have everything memorized. There are a few fundamentals that you should know by heart, though, since they are so commonly used.

#### Message

`*mes "`<string>`";`

This is the most basic command.  
Start the line with the word mes, then enter the message in quotes (don't forget the semicolon at the end!).  
To add color, simply add ^ and the hex code anywhere in the message.  
A list can be found [here](http://www.immigration-usa.com/html_colors.html).

*As an example:*

`mes "[^FF0000Test NPC^000000]";`
`mes "Hello!";`

*Will display:*

`[`<span style="color:#FF0000;">`Test NPC`</span>`]`
`Hello!`

#### Labels, Goto, and End

To create a label, type a label name and a colon at the start of a line.  
If the label does not end with an "end;" command, everything following the label will be read, so don't forget it between labels!  
To go to a label, use the simple "goto" command:

`*goto `<label>`;`

	Note:
	There are "special" labels that trigger whenever a specific event occurs. 
	The name usually makes it obvious, but you can find explanations in script_commands.txt.  
	Here is a brief sampling:

```
OnClock<hour><minute>:
OnInit:
OnAgitStart:
OnAgitEnd:
OnTouch:
OnPCLoginEvent:
OnPCLogoutEvent:
OnPCBaseLvUpEvent:
OnPCJobLvUpEvent:
OnPCDieEvent:
OnPCKillEvent:
OnNPCKillEvent:
OnPCLoadMapEvent:
```
#### Menus, Close, and Next
```
*menu "<option_text>",<target_label>{,"<option_text>",<target_label>,...};
*close;
*next;
```

Menus create a set of options, which trigger labels when selected.  
The text in quotes is what will be displayed, followed by its respective label.  
Enter as many choices as you want, and end the last one with a semicolon instead of a comma.  
"Close" will close any message window that is open (from "mes" commands).  
"Next" will clear the message window, bringing up a fresh screen.

*For example:*
```
mes "[Test NPC]";
mes "How are you doing today?";
menu "I am doing okay!",doingokay,"Not doing too well",bad;
doingokay:
mes "Glad to hear it!";
close;
end;
bad:
mes "Aww, I'm sorry about that.";
close;
end;
```
#### Conditions, Variables, and Set
```
*if(condition) {
<script>
}
*else {
<script>
}
```
Conditional statements "if" and "else" are the same as anywhere else. Multiple conditions can be specified: || means *or*, while && means *and*. == is *equal*, != is *not equal*. Inequalities can be used as well (&lt;, &gt;, &lt;=, &gt;=).
The "else" can be omitted, and the brackets aren't necessary unless multiple commands follow a conditional statement.
The type of variable used is defined in the name. There are permanent and temporary variables, as well as scope (temporary NPC), character, global, and global account. The default type is an integer, and adding $ as a suffix creates a string.
Here are some example types, taken from script_commands.txt:
```
name  - permanent character integer variable
name$ - permanent character string variable
@name  - temporary character integer variable
@name$ - temporary character string variable
$name  - permanent global integer variable
$name$ - permanent global string variable
$@name  - temporary global integer variable
$@name$ - temporary global string variable
.name  - NPC integer variable
.name$ - NPC string variable
.@name  - scope integer variable
.@name$ - scope string variable
#name  - permanent local account integer variable
#name$ - permanent local account string variable
##name  - permanent global account integer variable
##name$ - permanent global account string variable
```
The **set** command is used to give a value (or string) to a variable:

`*set <variable>,<expression>;`

The following script will pick a random number, store it as the temporary scope variable **.@random** and display two different messages depending on the result:
```
set .@random, rand(1,2);
if (.@random == 1) { mes "I like you! :D"; }
else { mes "I don't like you.  Get out of here!"; }
close;
```

#### Duplicating
It would be a huge waste of time and space to code the same NPC over and over again. By duplication, an NPC can be created in multiple locations.
Take a look at our old Test NPC:

`prontera,156,145,4 `<tab>` script `<tab>` Test NPC `<tab>` 58,{`

To be able to duplicate this, we will change the heading to this:

`- `<tab>` script `<tab>` Test NPC#01::testnpc `<tab>` 58,{`

The location doesn't need to be defined in the NPC, since it will be in the duplicates.  
The displayed name remains "Test NPC".  
But since NPC names must be unique, adding **#01** separates this one from the rest, which will be **#02**, **#03**, etc.  
Lastly, **::testnpc** is the reference name used for duplicating NPCs; this part is not displayed on the screen.  

After creating the base NPC, duplicates can be added anywhere to any file, so long as you use the same NPC name:

`spl_fild03,150,150,7 `<tab>` duplicate(testnpc) `<tab>` Test NPC `<tab>` 58`
`niflheim,50,50,2 `<tab>` duplicate(testnpc) `<tab>` Test NPC `<tab>` 58`
`tha_scene01,140,190,4 `<tab>` duplicate(testnpc) `<tab>` Test NPC `<tab>` 58`

The first part is **map,x,y,direction**, as you're probably used to by now.  
To define a duplicate, the word "duplicate" followed by the NPC, in parentheses, is needed.  
The last two parameters are the display name and sprite ID (yes, you can change these, too!).

## Finished Product

Here is an example using the features explained above:
```
    prontera,156,145,4 script  Test NPC::test  589,{
        mes "Hello, how are you?";
        mes "I am fine, how are you?";
        menu "I am doing okay!",-,"Not doing too good",L_Bad;
        mes "That's good, I'm glad to hear that";
        close;
    
    L_Bad:
        mes "Awww, that makes me a bit ^FF0000sad^000000. Sorry to hear that.";
        next;
        mes "Would you like some Zeny to help yourself feel better?";
        next;
        menu "Sure, give it to me!",L_Zeny,"Naw, No Zeny for me",-;
        close;
    
    L_Zeny:
        mes "I can only give you Zeny if you have 10,000 or less.";
        if (Zeny > 10000) goto L_Toomuch;
        mes "You have 10,000 Zeny or less, I see.";
        Zeny+=10000;
        next;
        mes "Hope you feel better!";
        close;
    
    L_Toomuch:
        mes "You have over 10,000 Zeny, you must feel really good about yourself!";
        close;
    }
    
    lhz_dun01,157,285,4    duplicate(test) Test NPC    859
    hu_fild05,186,210,4    duplicate(test) Test NPC    859
    yuno_fild07,221,179,4  duplicate(test) Test NPC    859
    tha_scene01,139,194,1  duplicate(test) Test NPC    859
```
### Adding Scripts
For an NPC to be loaded, refer to this [page](adding.md).
## External Links
### Sprite lists
* <http://nn.ai4rei.net/dev/npclist/>

### Color Charts
* <http://www.immigration-usa.com/html_colors.html>
* <http://www.december.com/html/spec/colorcodes.html>
* <http://www.colorschemer.com/online.html>

### Support, Request and Release
* [Scripting support on rA forums](https://rathena.org/board/forum/30-scripting-support/)