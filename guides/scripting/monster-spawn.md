A **permanent monster spawn** is a monster which is intended to spawn and then respawn naturally via timer.  
Monsters spawned in this fashion will continue to respawn automatically at set intervals. This is in contrast to NPC spawned monsters which are spawned only under certain conditions set forth in the script. Most monsters in Ragnarok Online are permanent monster spawns. The files which spawn monsters this way are usually located in *npc/mobs/*, but this is not a requirement.

## Script Syntax
-------------
```
string[32](*map_name*),ushort(*x*),ushort(*y*)[,short(*x2*) = 0[,short(*y2*) = 0]]<TAB>**monster**<TAB>string[24](*name*)<TAB>short(*mob_id*),ushort(*amount*)[,uint(*delay*)= 0[,uint(*variance*) = 0[,string[50](*event*)] = null]]`
```

## Script Explanation
------------------
!!! info "`<TAB>`"
	Replace this with a tab

=== "map_name"
	Map Name ("this" is actual map)
=== "X"
	X (horizontal) coordinates on map_name
=== "Y"
	Y (vertical) coordinates on map_name
=== "X2"
	X2 (horizontal) rectangle
=== "Y2"
	Y2 (vertical) rectangle
=== "Name"
	Name that will show
=== "mob_id"
	Monster ID(from mob_db)
=== "amount"
	Amount to be spawned
=== "delay"
	Delay (in milliseconds)
=== "variance"
	Delay variance (in milliseconds)
=== "event"
	NPC event that will be called when the monster dies
	??? example
		`NPCName::Label`

## Script Examples
---------------
`prt_fild08,0,0,0,0 monster Poring  1002,70,0,0,0`

In this example 70 Porings (Monster ID \#1002) will be spawned randomly on the map prt_fild08. They will respawn instantly upon death.

`prt_fild08,0,0 monster Poring  1002,70`

This will produce the same results as above, but omits the optional fields.

`prt_fild08,0,0,0,0 monster Poring,50   1002,70,0,0,0`

This will produce the same results as above, but spawn Porings with level 50.

`prt_maze03,0,0,0,0 monster Baphomet    1039,1,7200000,600000,0`

In this example one Baphomet (Monster ID \#1039) will be spawned randomly on the map prt_maze03. It will respawn in about 2 hours (7200000/1000/60/60 = 2). The variance is 10 minutes, so it will respawn sometime between 2 hours to 2 hours and ten minutes after death.

`pay_dun04,120,115,0,0  monster Moonlight Flower    1150,1,3600000,600000,0`

In this example one Moonlight Flower (Monster ID \#1150) will be spawned at X:120 Y:115 on the map pay_dun04. It will respawn in about 1 hour (3600000/1000/60/60 = 1). The variance is 10 minutes, so it will respawn sometime between 1 hour to 1 hour and ten minutes after death.

## Parse function in Source
------------------------
npc_parse_mob() in [map/npc.cpp](https://github.com/rathena/rathena/blob/master/src/map/npc.cpp)