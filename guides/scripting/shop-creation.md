Shops are very similar to [Basic Scripting](basics.md), although since there is only one line to find errors on, it's recommended to understand basic scripts first.
There are five parts to any shop script, tab separated to handle spaces in the name

`prontera,153,194,4`<TAB>`shop`<TAB>`Card Seller Uno`<TAB>`93,4001:-1,4002:-1,4003:10575,4004:-1`
`-      A       --B-     - C-     -     D      -    -E- - F_1 - - F_2 - -   F_3  - - F_4 -`

* A: Location  
  This is the map and coordinates (".gat" is not necessary)
* B: Direction  
  Face your Shop any direction from this chart:
  ```
	[1][8][7]
	[2][0][6]
	[3][4][5]
  ```
* C: NPC Type, shop in this case
* D: NPC Name, same as other NPCs
* E: NPC sprite number, a list for which can be found in [External Links](#external-links)
* F: Items being sold!  
  Notice there are no curly brackets like normal scripts.  
  Don't add them, it will error out and skip your shop  
  * F_1~4: Item format is ```<ItemID>:<price>,<ItemID>,<price>...```  
    The limit for items per shop is 100. You can add more, it will just stop at 100  
    The prices are a bit odd: -1 means 'read from item_db' and any other amount is an absolute price.  
    If you use absolute prices you open yourself to money exploits, it's best to just make sure all your item_db (SQL or YAML) items are priced!

## Shop Duplicating
----------------

Guess what! It's exactly the same as NPC duplicating! Except for the NPC type and primary contents

`-`<TAB>`shop`<TAB>`Card Seller#01::cardtwin`<TAB>`93,4001:-1,...`

And to run a duplicate, identical

`prontera,154,193,3`<TAB>`duplicate(cardtwin)`<TAB>`Card Seller Deus`<TAB>`93`
`prontera,150,193,5`<TAB>`duplicate(cardtwin)`<TAB>`Card Seller Deus`<TAB>`93`

## External Links
--------------

**Reference Manuals for scriping commands**

-   [Original Documentation](https://github.com/rathena/rathena/blob/master/doc/script_commands.txt)

**Sprite lists**

-   <https://nn.ai4rei.net/dev/npclist/>

**Color Charts**

-   <http://www.immigration-usa.com/html_colors.html>
-   <http://www.december.com/html/spec/colorcodes.html>
-   <http://www.colorschemer.com/online.html>

**Support, Request and Release**

-   [Scripting Support on rAthena Forum](http://rathena.org/board/forum/30-scripting-support/)