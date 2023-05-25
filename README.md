doc refer to :
https://pimylifeup.com/minecraft-pi-edition-api-reference/

Minecraft Pi Edition API Reference
This guide features a reference sheet for the Minecraft Pi Edition Python API.

Minecraft Pi Edition API
Before making use of this reference guide you should first have Minecraft Pi Edition installed to your Raspberry Pi.

The Minecraft Pi Edition Python API consists of three separate libraries, all designed to interact with the game client in various ways.

minecraft.py – This is the main library for interacting with the game. The library provides five different classes for interacting with the game client.
Class Minecraft – This is the main class for interacting with the game and contains four sub-classes.
Class camera – Used to modify the player’s camera angle and position.
Class player – Allows us to get and modify the player’s position in the game world.
Class entity – Gives the ability to get and set the position of entities (players) in the game world.
Class events – Allows you to retrieve events that have happened within the game.
block.py
Class Block – This class defines a block within the game world and is used to describe a block’s type and subtype. This file also contains a constant for each of the possible blocks.
event.py
Class BlockEvent – With this class, you can check what event happened to a block. This event gives details of what block it happened to, what player caused the event and what the event was.
Minecraft API Class
This section references the core functions of the Minecraft Pi Edition API. These functions are typically used to interact with the Minecraft game world.

.create() function
.create(address = "localhost", port = 4711)
This function creates a connection to a Minecraft Pi Edition client and returns an object that you can use to interact with the client.

There are two different ways you can use this function. The first is not to use any of the parameters.

Without any parameters, the .create() function makes a connection to the localhost client on port 4711.

#Use default address and port
mc = minecraft.Minecraft.create()
Alternatively, you can provide an IP address and a port to connect to. Defining an IP address will allow you to connect to a remote Minecraft Pi Edition client.

#Specify both IP address and port
mc = minecraft.Minecraft.create("192.168.1.1", 4711)
.getBlock() function
.getBlock(x, y, z)
This function retrieves the ID of a block at the specified x, y, and z position. It returns the ID of the block as an integer.

For example, using the following will retrieve the ID of the block at position 0, 0, 0.

#Retrieves the block ID for the block at position 0, 0, 0
blockID = mc.getBlock(0, 0, 0)
.getBlocks() function
.getBlocks(x0, y0, z0, x1, y1, z1)
This is similar to the previous function but instead gets the ID’s of blocks from a cuboid. These ID’s are returned as integers within a Python list.

You can loop through the returned list to see the ID of each of the blocks.

For the following example, we will check the blocks in the area from 1, 1, 1 to 2, 2, 2.

#Retrieves block ID's from 1, 1, 1 to 2, 2, 2
blockIdList = mc.getBlocks(1, 1, 1, 2, 2, 2)
for block in blockIdList:
    print(block)
.getBlockWithData() function
.getBlockWithData(x, y, z)
This is similar to the previous functions, however instead of returning the block ID as an integer it instead returns a Block object.

The block object contains information about the block such as it’s block ID and it’s data ID.

You can use this function just like the previous ones. All you need to do is specifiy the x, y and z position of the block.

#Gets a Block object from the specified position
blockObj = mc.getBlockWithData(0, 0, 0)
.setBlock() function
.setBlock(x, y, z, blockID, [blockSubtype])
Using the .setBlock() function we are able to change the block at the specified position to the specified block ID.

It has an optional fifth parameter for blocks that have subtypes, for example, the wool block.

Below we have an example of using the .setBlock() function. One example uses just the block ID and the other uses the block subtype as well.

#Sets the block at 0, 0, 0 to a stone (ID 1) block
mc.setBlock(0, 0, 0, 1)
#Sets the block at 1, 1, 1 to a red (Subtype 14) wool (ID 35) block
mc.setBlock(0, 0, 0, 35, 14)
.setBlocks() function
.setBlocks(x1, y1, z1, x2, y2, z2, blockID, [blockSubtype])
Using this function you are able to set a cuboid of blocks to a defined ID.

This function will fill in all blocks between the two sets of positions with the defined block.

#Sets blocks between 1, 1, 1, and 2, 2, 2 to stone (ID 1)
mc.setBlocks(1, 1, 1, 2, 2, 2, 1)
.getHeight() function
.getHeight(x, z)
This function will return the y position of the highest non-air block at a specified x and z position.

#find the y position at 0, 0,
y = mc.getHeight(0, 0)
.getPlayerEntityIds() function
.getPlayerEntityIds()
This function returns the entity ID’s of all connected players.

The ID’s are returned as integers stored in a list.

playerEntities = mc.getPlayerEntityIds()

for playerEntities in playerID:
    print(playerID)
.saveCheckpoint() function
mc.saveCheckpoint()
Saves a checkpoint, creating a snapshot of the world as it stands.

You can restore the Minecraft world to this checkpoint at any time.

.restoreCheckpoint() function
mc.restoreCheckpoint()
Restores the Minecraft game world to how it was when the first checkpoint was created.

Before running this command, you must first run the .saveCheckpoint() function.

.postToChat() function
.postToChat(message)
This function allows you to post a message into the game chat.

Below is an example of using the function to post the text “Hello World” into the chat.

mc.postToChat("Hello World")
.setting() function
mc.setting(settings, status)
Using this function, you can change the settings for the current game.

All you need to do is specify the name of the setting then the value you want to assign to it.

#Sets the nametags_visible setting to false
mc.setting("nametags_visible", False)
Minecraft Player API Class
The functions referenced here are for interacting with players within the game world.

.player.getPos() function
.player.getPos()
This function is used to retrieve the position of the player.

The position is returned as a vector but can be unpacked using Python. The values in this vector are stored as floats.

#Gets the position of the player and stores it as a vector 
pos = mc.player.getPos()

#Print the players x position
print(pos.x)

#Gets the position of the player and unpacks the result to the x, y and z variables
x, y, z = mc.player.getPos()
.player.setPos() function
.player.setPos(x, y, z)
This function moves the player to the specified x, y, and z position.

Below is an example of moving the player to position 0, 0 and 0 in the world.

mc.player.setPos(0, 0, 0)
.player.getTilePos() Function
.player.getTilePos()
Gets the position of the “tile” that the player is currently on.

This function returns the position as a vector. The tile position is stored as an integer as it represents the blocks exact position within the game world.

Like the .getPos() function, you can also use Python’s unpack ability to unpack this vector back to the individual x, y, and z values.

#Retrieves the tile position as a vector
tilePos = mc.player.getTilePos()

#retrieves the individual x, y and z positions of the tile
tileX, tileY, tileZ = mc.player.getTilePos()
.player.setTilePos() Function
.player.setTilePos(x, y, z)
This function moves the player to the tile specified at the x, y and z co-ordinates.

Below we have an example of moving the player to the tile at 0, 0, 0.

mc.player.setTilePos(0, 0, 0)
.player.setting() Function
.player.setting(setting, status)
Using this function you are able to change the settings for the player.

Below we have an example of setting the players “AutoJump” option to “True“.

mc.player.setting("autojump", True)
Minecraft Entity API
The Minecraft Entity API allows you to interact with different players on a server. This API should be used in conjunction with the .getPlayerEntityIds() function.

These are similar to the player functions but can be used to specify individual players.

.entity.getPos() Function
.entity.getPos(entityId)
Retrieves the position of the specified entity and returns it as a vector.

Below is an example of retrieving the position of an entity.

#Retrieves the vector position of the specified ID
entityPos = mc.entity.getPos(entityId)

#Retrieves the unpacked positions for the entity
entX, entY, entZ = mc.entity.getPos(entityId)
.entity.setPos() Function
.entity.setPos(entityId, x,  y, z)
Moves the specified player the the specified x, y and z position in the world.

mc.entity.setPos(entityId, 0, 0, 0)
.entity.getTilePos() Function
.entity.getTilePos(entityId)
Retrieves the tile position of the specified user. This position as returned as a vector.

#Gets the tile position of the specified entity as a vector
entityTilePos = mc.entity.getTilePos(entityId)

#Gets the unpacked tile position for the entity
entTileX, entTileY, entTileZ = mc.entity.getTilePos(entityId)
.entity.setTilePos() Function
.entity.setTilePos(entityId, x,  y, z)
Moves the entity to the specified tile at the x, y, and z coordinates.

mc.entity.setTilePos(entityId, 0, 0, 0)
Minecraft Camera API
This part of the Minecraft Pi Edition API let’s you control the camera.

.camera.setNormal() Function
.camera.setNormal(entityId)
This function sets the camera mode for the specified entity back to normal.

mc.camera.setNormal()
mc.camera.setNormal(entityId)
.camera.setFixed() Function
.camera.setFixed()
Sets the camera mode to a fixed view.

mc.camera.setFixed()
.camera.setFollow() Function
.camera.setFollow(entityId)
This command sets the camera to follow a specified entity.

You can use this API function to get the camera to follow a particular player.

mc.camera.setFollow(entityId)
.camera.setPos() Function
.camera.setPos(x, y, z)
Changes the position of the camera to the specified x, y and z position.

Below you can see an example of using this to move the camera to the position, 0, 0, 0.

mc.camera.setPos(0, 0, 0)
Minecraft Block Event API
This API allows you to handle block events within Python.

The BlockEvent Object
This object contains five different variables that tell us about the event.

These objects are returned by the .pollBlockHits() function.

blockEvent = mc.events.pollBlockHits()
.type – This variable stores the event type.
blockEventType = blockEvent.type
.pos – Stores a vector (x, y, z) with the position of where the event occured.
blockEventPos = blockEvent.pos
blockX, blockY, blockZ = blockEvent.pos
.face – The face of the block where the event occured.
blockEventFace = blockEvent.face
.entityId – The ID of the entity that caused this event to occur.
blockEventEntityId = blockEvent.entityId
.events.pollBlockHits() Function
This command returns all the block hit events that have occured since the function was last called.

These events are returned as a “BlockEvent” object. This object gives you various bits of information about the event.

Every time this function is called, all events in the queue are removed.

Below is an example of polling for events then printing out the event. By printing out the event, you can see the information that is returned.

blockHitEvents = mc.events.pollBlockHits()

for blockEvent in blockHitEvents:
    print blockEvent
.events.clearAll() Function
.events.clearAll()
This function clears all existing events from the queue.

Using this function is similar to running the .pollBlockHits() function, however, no data is returned.

mc.events.clearAll()
Minecraft API Block Object
.id – The ID of the blocks type. You can see the corresponding constants below.
.data – The subtype of a block. You can see the block subtypes below.
Block Constants
Below is a list of all the Block Constants and their corresponding ID.

Constant Name	Block ID
AIR	0
STONE	1
GRASS	2
DIRT	3
COBBLESTONE	4
WOOD_PLANKS	5
SAPLING	6
BEDROCK	7
WATER_FLOWING	8
WATER	8
WATER_STATIONARY	9
LAVA_FLOWING	10
LAVA	10
LAVA_STATIONARY	11
SAND	12
GRAVEL	13
GOLD_ORE	14
IRON_ORE	15
COAL_ORE	16
WOOD	17
LEAVES	18
GLASS	20
LAPIS_LAZULI_ORE	21
LAPIS_LAZULI_BLOCK	22
SANDSTONE	24
BED	26
COBWEB	30
GRASS_TALL	31
WOOL	35
FLOWER_YELLOW	37
FLOWER_CYAN	38
MUSHROOM_BROWN	39
MUSHROOM_RED	40
GOLD_BLOCK	41
IRON_BLOCK	42
STONE_SLAB_DOUBLE	43
STONE_SLAB	44
BRICK_BLOCK	45
TNT	46
BOOKSHELF	47
MOSS_STONE	48
OBSIDIAN	49
TORCH	50
FIRE	51
STAIRS_WOOD	53
CHEST	54
DIAMOND_ORE	56
DIAMOND_BLOCK	57
CRAFTING_TABLE	58
FARMLAND	60
FARMLAND_INACTIVE	61
FARMLAND_INACTIVE	61
FURNACE_ACTIVE	62
DOOR_WOOD	64
LADDER	65
STAIRS_COBBLESTONE	67
DOOR_IRON	71
REDSTONE_ORE	73
SNOW	78
ICE	79
SNOW_BLOCK	80
CACTUS	81
CLAY	82
SUGAR_CANE	83
FENCE	85
GLOWSTONE_BLOCK	89
BEDROCK_INVISIBLE	95
STONE_BRICK	98
GLASS_PANE	102
MELON	103
FENCE_GATE	107
GLOWING_OBSIDIAN	246
NETHER_REACTOR_CORE	247
Block Subtypes
Below is a list of blocks that have special subtypes, use this list to find the ID’s you require.

Wool

0 : White
1 : Orange
2 : Magenta
3 : Light Blue
4 : Yellow
5 : Lime
6 : Pink
7 : Grey
8 : Light Grey
9 : Cyan
10 : Purple
11 : Blue
12 : Brown
13 : Green
14 : Red
15 : Black

Wood

0 : Oak (Up / Down)
1 : Spruce (Up / Down)
2 : Birch (Up / Down)

Sapling

0 : Oak
1 : Spruce
2 : Birch

GRASS_TALL

0 : Shrub
1 : Grass
2 : Fern

TORCH

1 : Pointing East
2 : Pointing West
3 : Pointing South
4 : Pointing North
5 : Facing Up

STONE_BRICK

0 : Stone Brick
1 : Mossy Stone Brick
2 : Cracked Stone Brick
3 : Chisled Stone Brick

STONE_SLAB/STONE_SLAB_DOUBLE

0 : Stone
1 : Sandstone
2 : Wooden
3 : Cobblestone
4 : Brick
5 : Stone Brick

TNT

0 : Inactive
1 : Ready to explode

Leaves

1 : Oak Leaves
2 : Spruce Leaves
3 : Birch Leaves

Sandstone

0 : Sandstone
1 : Chiseled Sandstone
2 : Smooth Sandstone

STAIRS_[WOOD, COBBLESTONE]

0 : Ascending East
1 : Ascending West
2 : Ascending South
3 : Ascending North
4 : Ascending East (Upside Down)
5 : Ascending West (Upside Down)
6 : Ascending South (Upside Down)
7 : Ascending North (Upside Down)

LADDER, CHEST, FURNACE, FENCE_GATE

2 : Facing North
3 : Facing South
4 : Facing West
5 : Facing East

[WATER, LAVA]_STATIONARY

0 – 7 : Level of water, 0 is lowest, 7 is highest.

NETHER_REACTOR_CORE

0 : Unused
1 : Active
2 : Stopped / Used Up

Hopefully this resource has helped you understand the Minecraft Pi Edition Python API.

Python-Minecraft-Examples
=========================

A set of examples of how to use the Minecraft Python API and Minecraft Pi edition

To use these examples first you need to have Minecraft installed:

If you have a recently updated version of Raspbian you can install Minecraft-Pi from the repositories.

1. Open LXTerminal by double clicking on the icon on the desktop or click on :
  Start Menu > Accessories > LXTerminal
2. Type the following commands and press enter after each one:
  * `sudo apt-get update`
  * `sudo apt-get install minecraft-pi`
3. You should now see a minecraft shortcut icon on the desktop. Double click on this to start minecraft pi

Alternatively you can start minecraft from the terminal:

1. Open LXTerminal by double clicking on the icon on the desktop or click on :
  Start Menu > Accessories > LXTerminal
2. type `minecraft-pi` and press enter. Note if you wish to start minecraft in the background you need to type `minecraft-pi &`


If you have an older version of Raspbian you need to do the following:

1. Go to http://pi.minecraft.net
2. Click on *Downloads* in the menu bar
3. Click on the download link
  * As of 15th May 2014 the link was:
  * https://s3.amazonaws.com/assets.minecraft.net/pi/minecraft-pi-0.1.1.tar.gz

4. Unzip/Uncompress this file by navigating to it in the *File Manager* and right clicking on it and click on *Extract here*
5. Go into the newly created folder *mcpi*
6. Double click on the file *minecraft-pi* and choose *Execute*
7. This will have opened up Minecraft, you need to start a game and create a new world

Now that Minecraft is running and you are in the world you can run the examples.
All examples can be run from the command line in LXTerminal. 
To run in IDLE some examples need slight modification first to replace the usage of command line arguments

##Running the Examples in LXTerminal

1. Open LXTerminal by double clicking on the icon on the desktop or click on :
  Start Menu > Accessories > LXTerminal

2. Navigate to the folder where these examples are, assuming you have uncompressed the zip folder or cloned the repository in your home folder :
 `cd Python-Minecraft-Examples`
3. Type: `python filename.py` and press enter (where filename is the examples to try)
4. Where the script expects arguments you supply those after the filename. or example:
   `python 02-sendArgsMessageToChat.py "This is a message"`
5. Have fun in Minecraft! 


##Running the Examples in IDLE

1. Open IDLE by double clicking on the icon on the desktop or open LXTerminal and type `idle &` and press enter
2. Go to : File > Open 
3. Open an example file
4. Press F5 or in the Menu go to  Run > Run Module

Note: for those  examples that require command line arguments this is easily worked around.
For example with file *02-sendArgsMessageToChat.py* we edit the file so that below the line that reads :
```python
if __name__ == '__main__':
```
We add the following line so it becomes:
```python
if __name__ == '__main__':
    sys.argv = [sys.argv[0], "this is a message"]
```
NOTE : the new line should begin with 4 spaces for correct indentation

In general you can add any number of arguments this way
```python
if __name__ == '__main__':
    sys.argv = [sys.argv[0], argument1, argument2, argument3]
```
