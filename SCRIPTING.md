Below, in command syntaxes:

* capitalization below is only to indicate syntax. All scripting is interpreted as lowercase in real-time, and can as such be written lowercase without consequence.
* The ONE exception is text used with textbox commands--anything after the line count--which will ALWAYS retain its casing.
* #commands are lowercase with a pound sign before them (note: commands WILL NOT execute without the # sign!)
* NECESSARY ARGUMENTS are capitalized
* [OPTIONAL ARGUMENTS] are capitalized and bracketed
* OPTION A/OPTION B are divided if they are the only valid argument options

#### `#addentity ENTITY`

Adds entity to scene by ENTITY in CommonAssets.

#### `#animate [MODIFIER] ANIMATION`

The script's parent node will act based on the following logic:

If MODIFIER does not contain any special value of "frame", "resume", or "queue", its animation node will play ANIMATION.

If MODIFIER is "queue", the animation node will instead queue up ANIMATION.

If MODIFIER is "frame", the parent node attempt to set its sprite to the integer represented by ANIMATION. This modifier should only be used for PlatformingBody2D.

All three cases above will cause the object's animation node to stop automatically animating based on things like EntityStates.

If MODIFIER is "resume" this will cause the animation node to RESUME

#### `#attack` - PlatformingBody2D use only

Trigger the attack function for this PlatformingBody2D

#### `#attackwatch [on/off]` - PlatformingBody2D use only

When in attack-watch mode, a PlatformingBody2D will auto-seek to the ":attack" label once the player is detected. Use "ON" or without modifier to turn attack watch on, or "OFF"
to disable it. When attackwatch triggers the auto-seek, it automatically turns off.

#### `#color` - PlatformingBody2D use only

Cause a parent PlatformingBody2D node to change its color modulation at the Canvas level

#### `#command UNIQUE_ID COMMAND`

Commands the entity with the unique ID to execute COMMAND--COMMAND should be formatted as if it is a whole separate command line.

#### `#createprojectile X0 X1 Y0 Y1`

Creates a projectile between X0 and X1 and between Y0 and Y1. Currently it's just a falling spike.

#### `#die` - enemies with Stats only

Set the entity's stats to zero.

#### `#direction DIRECTION` - PlatformingBody2D use only

Causes PlatformingBody2D to begin facing in a direction. Valid directions are IDLE (stop moving), LEFT, RIGHT (as stated), REVERSE (opposite of its current facing direction) and CURRENT (the current facing direction.)

#### `#end`

Stop processing the script here.

#### `#forcemove [INT]` 

Sets x-position to the given INT.

#### `#goto LABEL`

Seek to label :label. Does not resume processing if the script processing is stopped.

#### `#gotoif LABEL`

Goes to LABEL if the camera variable for the room is set.

#### `#gotoandresume LABEL`

Seek to label :label. Resumes processing if the script processing stopped.

#### `#healplayer`

Heals the player to full!

#### `#if [NOT/U/UNIQUE] UNIQUE_ID COMMAND`

Executes COMMAND if the given unique ID value is found in the current working save file. U or UNIQUE can be used as the second argument to be expressly clear what kind of data check we're doing.

COMMAND should be formatted as if it is a whole separate command line.

#### `#if C/COUNT COUNTABLE_VARIABLE [==/>=/<=/</>] VALUE COMMAND.

Executes COMMAND if the given COUNTABLE_VARIABLE value meets the given comparison condition.

COMMAND should be formatted as if it is a whole separate command line.

#### `#jump` - PlatformingBody2D use only

Cause the PlatformingBody2D to jump. Presently has no modifiers, so the full jump will always be used.

#### `#loadscript FILE_NAME`

Load the script FILE_NAME and begin processing. Discard the current script. Can be called by its 'name' NAME without .txt or total path to call the file NAME.txt in the script folder.

#### `#lockinput`

Causes the PlatformingBody2D to stop taking input from its Input node (player or AI)

#### `#matchplayerposition`

Makes the entity position match the player's position.

#### `#music [CLIP/SET] MUSIC_STRING` 

Change current music clip (adaptive-music-wise) or overall set (set of adaptive music.) SET wasn't really used in Beast jam version.

#### `#move DIRECTION` - PlatformingBody2D use only

Causes PlatformingBody2D to begin moving in a direction. Valid directions are IDLE (stop moving), LEFT, RIGHT (as stated), REVERSE (opposite of its current facing direction) and CURRENT (the current facing direction.)

#### `#movearea GOAL_X GOAL_Y VELOCITY_X VELOCITY_Y` - TriggerArea use only

Moves the given TriggerArea to the given GOAL_X,GOAL_Y coordinates at a constant velocity of VELOCITY_X,VELOCITY_Y. All numbers will be interpreted as integers.

#### `#queuefree`

Causes the entity to leave the scene tree.

#### `#resetcamerabox":

Resets camera box to the default setting for the room.

#### `#savegame ROOM_PATH SAVE_POSITION_X SAVE_POSITION_Y SAVE_AREA_LOCATION`

Saves the game with ROOM_PATH for scene reload, save_position x,y for player placement, and save_area_description for the save file location. Normally this is auto-set by save points but can be called manually by scripts for special circumstances, e.g. being used at the start of the postjam version of the game to save the game at "Caves, Landing" and the appropriate scene.

#### `#scenechange NEW_SCENE_PATH DIRECTION INTERNAL_ROOM_OFFSET_X INTERNAL_ROOM_OFFSET_Y`

Causes the player object to be taken to a new scene at NEW_SCENE_PATH in the project's res:// folder.

For DIRECTION, valid directional values are N, S, E, and W. Each room scene in the game is broken up into "subrooms"--e.g. The Landing is a 1x1 room, "The Drop" is several rooms high and one room wide. If the cardinal direction values are used, the INTERNAL_ROOM_OFFSET coordinates refer to the offset/difference needed to get the player to the expected 'subroom coordinates' for the 'exit point' of the scene change, versus the 'subroom coordinates' the player is at in the current (entry) point of the scene change.

If DIRECTION is SAVE, then the offset values are taken to be the expected new player coordinates instead.

#### `#setif`

Sets the camera variable for the room. This is used to determine whether the camera has done a 'hard' or 'instant' reset to match the player position yet.

#### `#showself` - PlatformingBody2D Only

Show its sprite.

#### `#sfx SFX`

Have the sound effects handler play the SFX given. Here SFX is the string expected in the sounds dictionary.

#### `#state` - PlatformingBody2D Only

Causes this PlatformingBody2D to attempt to change it state by string name.

#### `#store [UNIQUE/COUNTABLE/MYID] [VALUE]`

Stores:
* UNIQUE: Stores unique ID of type VALUE in game data.
* COUNTABLE: Stores unique ID of type VALUE in game data and countable.
* MYID: Special case of UNIQUE: stores the unique ID of the entity processing the script in game data. VALUE is not considered or required here as such.

#### `#tempcounter MODIFIER INT`

By MODIFIER, causes the following behavior in the "Room" node for its internal "local" variable:

* WATCH causes Room to "watch" for its internal "local" variable to hit a the value of INT or higher (must be positive)
* INC causes Room to "increase" its internal "local" variable by the value of INT
* DEC causes Room to "decrease" its internal "local" variable by the value of INT

#### `#textbox LINE_NUMBER TEXT`

Creates a textbox with LINE_NUMBER of lines and containing writing TEXT.

#### `#textboxclose`

Close the current textbox.

#### `#textboxoffset OFFSET_X OFFSET_Y`

Offset the text box from the current location.

#### `#textboxspeaker [OFFSET_X] [OFFSET_Y]`

Sets the current textbox so that it centers on the object's position. Optionally, then offset the textbox by OFFSET_X and OFFSET_Y from that position.

#### `#unlockinput`

Causes the PlatformingBody2D to begin taking input from its Input node (player or AI)

#### `#setcamerabox [INSTANT] X0 Y0 X1 Y1`

Resets the camera bounding box to have X0,Y0 as the top-left and X1,Y1 at the bottom right. X1-X0 should be no less than 320. Y1 - Y0 should be no less than 180.

If "instant" is declared, and the current camera box is not within the new bounds, will instantly set the new box. If "instant" is not declared, will move gradually instead.

#### `#uniquecheck`

Check this entity's own UNIQUE_ID--if it's stored in save data, thie entity leaves the scene.

#### `#uxoff`

Turn off player health display.

#### `#uxon`

Turn on player health display.

#### `#wait TIME [MAX_TIME]`

Waits either for TIME seconds, or TIME through MAX_TIME seconds, depending on whether MAX_TIME is given.

#### `#wallcheck` - PlatformingBody2D

Turns on wall-check for the PlatformingBody2D.

#### `#waituntil CONDITION`

Pause script execution until CONDITION is met, the move on to the next line.

Valid CONDITIONS:

* attackfinished (PlatformingBody2D only) - attack is finished
* ai_pit (PlatformingBody2D only) - the AI ray detects a wall
* ai_wall (PlatformingBody2D only) - the AI ray detects a wall
* interact (TriggerArea only) - player uses interact key and is within area
* movementfinished (TriggerArea only) - movement is finished (as with #movearea)
* playerdetected (TriggerArea only) - player object is within the area
* playerinput - any player input is triggered
* tempcounterdrained - temp counter condition as with #tempcounter is 'met'

#### A quick scripting example for enemy AI

The scripting can be used like so to make an enemy move back and forth between two walls and/or pits (this is very simple code and a `#wait` may be wanted at some place:

```
:label
#move current
#waituntil ai_pit ai_wall
#move reverse
#goto label
```




