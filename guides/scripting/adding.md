Scripts are usually kept in the *npc* folder for the sake of organization even though scripts can contain more than a mere NPC.  
All files are saved as text files.  
Scripts cannot be loaded on to the server unless their text file is activated in a **.conf** file.

### A New Script

New scripts must be saved as a text file first.  
The file may be located anywhere in the rAthena directory, but is in the **npc** folder by default.

### Configuration Files

Any text editor may be used to edit **.conf** files.  
The **.conf** files are used to determine which script text files should be loaded.  
There are about a dozen **.conf** that handle different groups of scripts for the purpose of organization.  
It does not matter which **.conf** holds your custom scripts as long as the path is correct.

Typical **.conf** entry layout:

```
npc: npc/path/to/yourscript1.txt
// npc: npc/path/to/yourscript2.txt
```

	Note:  
	See how the second line is preceded with a double slash.  
	Content on the same line after double slashes will not be parsed.  
	In other words, *script2.txt* will not be loaded.  
	The slashes can be used to write comments.

determines which of the **.conf** will be read by the server.

`    import: npc/path/to/configuration.conf`

### The NPC in Game

After adding the script, it must be loaded before the script contents take effect in game. There are a few ways to do this.

-   The map server can be rebooted. This is generally the safest route though not the most convenient for active servers.
-   The GM command **@reloadscript** maybe used in game, though this may cause monster spawn bugs.
-   If a script needs to be reloaded because it has been edited, the GM commands **@loadnpc** and **@unloadnpc** may be used. This method is not convenient for script texts that contain multiple NPCs.

Client Side
-----------

The NPC name used in examples is "Teddy".

### Lua

The two files you will need to open and edit are "jobname.lua" and "npcidentity.lua". Jobname.lua will look like:

`    [jobtbl.NPCNAME] = "NPCNAME",`

Example:

`    [jobtbl.TEDDY] = "TEDDY",`

npcidentity.lua will look like:

`    ["NPCNAME"] = NPCID,`

Example:

`    ["TEDDY"] = 587,`

If your NPC has spaces in its name, its best to either remove them or  
replace them with underscores.  
So if the NPC's name was Brown Teddy the sprite's name would be  
Brown_Teddy.spr or BrownTeddy.spr and the lua files  
would be BROWN_TEDDY or BROWNTEDDY.  
Whatever ID you choose for your sprite will be the one you use in the script,  
so since Teddy has the sprite ID of 587, the beginning of my script will look like:

`    xmas_in,111,107,3   script  Teddy   587,{`

### Sprite

The sprite part is straightforward, just Teddy.spr is fine,  
you don't need Teddy_m.spr or anything like that,  
but if you want to add m for male to the name you can do that,  
but it won't effect its functionality in-game.  
NPC sprites are located in data/sprite/npc.

Tips & Hints
------------

-   If you are copy/pasting a script from a forum, be sure to check that the tabs are still intact.
-   Remember that paths and file names are case sensitive.
-   Remember to save after editing.
-   Create your own NPC folder and \*.conf file. This will make it much easier to keep track of your own scripts and can reduce the hassle when merging new revisions of rA. Follow the basic layout of the other \*.conf files and remember to import the \*.conf in

