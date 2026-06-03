The **War of Emperium** is a battle between guilds for castles (5 castles in each of 4 towns, for a total of 20). Guilds fight against each other and the guild that owns the castle at the end of WoE has access to dungeons and treasures that are not accessible to people who are not in the residing guild.

## agit_controller.txt
--------------------
The body of the script should look similar to the following:
```
-  script  Agit_Event  -1,{
   end;
OnClock2100:  //start time for Tues(2), Thurs(4)
OnClock2300:  //end time for Tues(2), Thurs(4)
OnClock1600:  //start time for Sat(6)
OnClock1800:  //end time for Sat(6)
OnAgitInit:
   // starting time checks
   if((gettime(4)==2) && (gettime(3)>=21 && gettime(3)<23) ||
      (gettime(4)==4) && (gettime(3)>=21 && gettime(3)<23) ||
      (gettime(4)==6) && (gettime(3)>=16 && gettime(3)<18)) {
       if (!agitcheck()) {
           AgitStart;
           callsub S_DisplayOwners;
       }
       end;
   }
   // end time checks
   if ((gettime(4)==2) && (gettime(3)==23) ||
       (gettime(4)==4) && (gettime(3)==23) ||
       (gettime(4)==6) && (gettime(3)==18)) { 
       if (agitcheck()) {
           AgitEnd;
           callsub S_DisplayOwners;
       }
       end;
   }
   end;
S_DisplayOwners:
   setarray .@maps$0],"aldeg_cas01","aldeg_cas02","aldeg_cas03","aldeg_cas04","aldeg_cas05";
   setarray .@maps$5],"gefg_cas01","gefg_cas02","gefg_cas03","gefg_cas04","gefg_cas05";
   setarray .@maps$10],"payg_cas01","payg_cas02","payg_cas03","payg_cas04","payg_cas05";
   setarray .@maps$15],"prtg_cas01","prtg_cas02","prtg_cas03","prtg_cas04","prtg_cas05";
   for( set .@i, 0; .@i <= 19; set .@i, .@i+1 ) {
       if (GetCastleData(.@maps$.@i],1)) {
           Announce "The " + GetCastleName(.@maps$.@i]) + "] castle has been conquered by the " + GetGuildName(GetCastleData(.@maps$.@i],1)) + "] guild.",bc_all|bc_woe;
       }
       else {
           Announce "The " + GetCastleName(.@maps$.@i]) + "] castle is currently unoccupied.",bc_all|bc_woe;
       }
   }
   end;
}
```
### `OnClock####`
You need one of these labels for each time you want WoE to start or stop, so if you want the WoE to start at 9pm and end at 11pm you would need this.

```
OnClock2100:
OnClock2300:
if((gettime(4)==2) && (gettime(3) >= 21 && gettime(3) < 23)) goto L_Start;
```
* `gettime(4)==2`

Will check what the day is, 0 = Sun 1 = Mon 2 = Tue etc etc...  
This is currentally day 2, so this would result in a success if it was a Tuesday

* `gettime(3)>=21`

Will check the hour of the day, 00 = Midnight 01 = 1am etc...  
This is currentally 9pm (21:00) the `>=` mean if the current time is after 9pm return a success

* `gettime(3)<23`

Work the same as above, but will be the end of your WoE, the `<` means if the current time is before 11pm (23:00) it will return a success, if at any point the current time is equal to or more that 11pm it will return a fail.

* `if((gettime(4)==2) && (gettime(3)>=21 && gettime(3)<23)) goto L_Start;`

Only if everything inside the outer bracket is a success will it goto `L_Start` and start the WoE.

**Example 1**:  
It is tuesday, it is 10pm, you have just had to restart the server cause it has crash or whatever, it runs past that line of code.
```
	if((gettime(4)==2 ) && //Hm yes it is 
	(gettime(3)>=21 && // Yes it is after 21 
	gettime(3)<23)) // oh and it is before 23
		goto L_Start;
```

**Example 2**:  
It is Tuesday, it is 11:30pm.
```
	if((gettime(4)==2) && // Hm yes it is 
	(gettime(3)>=21 && // Yes it is after 
	gettime(3)<23)) // wait no it is after 23
	 goto L_Start; 
```
**Example 3**:  
It is Wednesday, it is 10pm.
```
	if((gettime(4)==2) && // Wait it is not day 2
	(gettime(3)>=21 && // Yes it is after 21
	gettime(3)<23)) // oh and it is before 23
		goto L_Start;
```
```
	if((gettime(4)==2) && (gettime(3)==23)) goto L_End;
```

* `gettime(4)==2`

Same as above, used for checking the day, you will need one of these for everyday you make,  
that is unless you decide to have one everyday at the same time then I wont mind, you will need just one, and it wont need to check the day

* `gettime(3)==23`

This would be the hour you want the WoE to end at, again 1 is needed for every WoE day/time you set

**Example 1**:  
This query is reached after passing through the first "Example 2".  
It is the same, Tuesday and 11:30pm.
```
	if((gettime(4)==2) && // Why yes, it is day 2 
	(gettime(3)==23)) 
		goto L_End;
```
This will then end your WoE

**Example 2**:  
This query is reached after passing through the first "Example 3".  
It is Wednesday, it is 10pm.
```
	if((gettime(4)==2) && // Why no, it isnt day 2
	(gettime(3)==23)) // and it is not hour 23
		goto L_End;
```
## Setting WoE Times
-----------------
1.  Make a list of when you want WoE to start and end during the week. If any times are the same, only list that time once.
2.  Add each of these times in the **OnClock** section of labels.
3.  In the first line of arguments enter the day, the start time, then the end time
4.  In the second line of arguments enter the day and the end time
5.  You can add as many lines as you'd like, but overlapping times can get annoying and messy :P

### Turn OFF WoE in Some Castles
----------------------------
WoE is a server-wide setting, so it's either ON everywhere, or OFF everywhere.  
To get around this and "turn off" woe in certain castles, this is what you can do:

1.  Edit and comment out the castles you are NOT using for WoE (put // in front of the line). This turns of all woe functions for that castle.
2.  Optional: to remove the warp portal entrance, edit and comment-out the warps into the castles you are not using.

### Separate WoE Times in Separate Towns/Castles
--------------------------------------------
WoE is a server-wide setting, so it's either ON everywhere, or OFF everywhere.  
(you can't have it on in one castle only).  
To get around this, you need to code 3 separate events in the file.

StartWOE1:

-   close portal into WoE castle2
-   kick people out of WoE castle2
-   open portal into WoE castle1 (and start woe)

StartWOE2:

-   close portal into WoE
-   kick people out of WoE castle1
-   open portal into WoE castle2 (and start woe)

EndWOE:

(same for both)

-   (end woe)
-   open portals into both castle1 & castle2

### See Also
--------
-   [Toasty's WoE Controller](http://rathena.org/board/topic/57377-toastys-woe-controller/)