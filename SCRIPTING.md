# GODOT ENTITY SCRIPTING PLAN

Designed to make a simple reusable entity script for entity AI and cutscenes, especially in platformers, in Godot.

## TWO NOTES ON LETTER CASE
*For ease of typing of this language, all commands and other strings, including entity `UNIQUE_ID` values, are interpreted as if lowercase. For ease of writing this documentation, all commands are written in UPPERCASE, and where an arguemnt type would go, the type is written as `[ARGUMENT_TYPE]`, not `<ARGUMENT_TYPE>`.*

## ARGUMENT TYPES

### `CONDITION`
Condition to wait upon. The following are valid conditions:

* `FLOOR` The entity waits until it is on the floor.
* `PIT` The entity waits until its movement would put it in a pit. No effect if idle.
* `WALL` The entity waits until its movement would have it hit a wall. No effect if idle.

*Conditions can be combined by simply listing them all together as a `PARAGRAPH` (see below), e.g. `PIT WALL`. Combined conditions are treated as `OR` not `AND`.*

### `INT`, `FLOAT`, `STRING`, `PARAGRAPH`
Standard types of integer, float, and "string". Unless otherwise noted, all `STRING` arguments consist of one-word strings and only of letters, numbers, and underscores. `PARAGRAPH` is used to denote where multi-word strings with more characters are acceptable.

### `COMMAND`
A variant of `PARAGRAPH` -- a command to pass to another entity. See `#COMMAND` below.

### `DIRECTION`
Direction to move in. Accepts these values: `IDLE`, `LEFT`, `RIGHT`, `PLAYER`, `CURRENT`, `COORDINATE [INT]`, `REVERSE` where `[INT]` is the desired X-coordinate. `PLAYER` faces the player. `CURRENT` means the object's current direction will be used. `REVERSE` means the opposite of this direction will be used.

### `FILE_PATH `

File path. Written as per Godot file-path parlance, e.g. starting with `res://` if seeking a file within the project folders or `user://` if looking in the game's user-data directory.

### `UNIQUE_ID`
A single-word `STRING` which serves as the unique ID of an entity. `UNIQUE_ID` values can be stored in save-data as true, which will help the game know which items, coins, etc. have been collected at this time.

## SCRIPTING REFERENCE

These scripting commands can be used by any platforming entity in the game. Many are also usable by the cutscene director object, although some of them will be less than useful in one context or the other.</p>

### `:[STRING]`
Create label `[STRING]` at this line in the object's command queue.

### `#ANIMATE [STRING]`
If `[STRING]` exists in the entity's animation player, play it immediately. The following special strings can also be used, with a second argument as necessary, and in projects using this scripting, should not be used as names for animations.

* `FRAME [INT]` Causes the entity sprite to change to frame `[INT]`.
* `QUEUE [STRING]` Causes the animation player to queue the resulting animation `[STRING]` rather than switch to it immediately.
* `RESUME` Causes the animation player to resume its automatic updates based on player state.
</ul>

*All animation commands except `#ANIMATION RESUME` will stop normal animation processing.

### `#CHOICE BEGIN [PARAGRAPH]`
Creates a text-box on screen which is presents a choice to the player with prompt [PARAGRAPH]. Choices are coded by using `CHOICE OPTION [STRING] [PARAGRAPH]`.

### `#CHOICE END`
Ends the list of choices.

### `#CHOICE OPTION [STRING] [PARAGRAPH]`

Presents a choice option to the player. When a given option `[PARAGRAPH]` is picked, the program immediately executes the command `#GOTO [STRING]`.

### `#COMMAND [UNIQUE_ID] [COMMAND]`
Pass `[COMMAND]` to the entity `[UNIQUE_ID]`, causing it to add `[COMMAND]` to its command queue. `#COMMAND` cannot itself be passed as `[COMMAND]`.

### `#CUTSCENE [FILE_PATH]`
Sends the cutscene manager the relevant `[FILE_PATH]` as a script to process. The script is appended to the manager's current command queue.

### `#DIRECTION [DIRECTION]`
Causes the entity to face the stated direction. Forces animation direction update. E.g.:

* `#DIRECTION TURN` causes the entity to turn around.

### `#GOTO [STRING]`
Go to label `[STRING]` in the object's command queue.

### `#FORCEMOVE [INT]`
Causes the entity to force its x-coordinate to the given x-coordinate of `[INT]`.

### `#JUMP [DIRECTION]`
Causes the entity to jump in the stated direction.

### `#LOADSCRIPT [FILE_PATH]`
Entity loads the script at `[FILE_PATH]`. This script becomes the new entity script and the current script is discarded.

### `#LOCKINPUT`
Entity locks its input. Relatively useless for non-player entities.

### `#MOVE [DIRECTION]`
Causes the entity to move in the stated direction with no stated end condition.

### `#MOVE [DIRECTION] UNTIL [CONDITION]`
Causes the entity to move in the stated direction until the given condition is TRUE.

### `#MUSIC CLIP [STRING]`
Attempts to have the audio handler play the music clip with id `[STRING]` from the current set. Only when adaptive music is in use and a track is currently playing.

### `#MUSIC TRACK [STRING]`
Attempts to have the audio handler play the music track (or 'set' in the case of adaptive music setups) with audio handler id `[STRING]`.

### `#SAVEGAME [STRING] [INT1] [INT2]`
Saves the current (temporary) save data as the game's save data, `[STRING]` as the one-string room ID in the game's save-data object, [INT1] as the player's X-coordinate, and [INT2] as the player's y-coordinate. Writes the resulting save data to disk.

### `#SFX [STRING]`
Attempts to have the audio handler play the sound effect with id `[STRING]`.

### `#STORE COUNTABLE [STRING]`
Increases the number of `[STRING]` stored in save data by 1. Adds `[STRING]` to the countable save data if it isn't there.

### `#STORE UNIQUE [UNIQUE_ID]`
Causes `[UNIQUE_ID]` to be stored in the save data as TRUE.

### `#TEXTBOX [PARAGRAPH]`
Creates a text-box on screen which is cleared with player input.

### `#UNIQUECHECK [UNIQUE_ID]`
Causes any entity with `[UNIQUE_ID]` in the current scene to re-evaluate its spawn condition. If `[UNIQUE_ID]` is not supplied, causes all relevant entities to do so.

### `#UNLOCKINPUT`
Entity unlocks its input. Relatively useless for non-player entities.

### `#WAIT [FLOAT]`
Causes the entity to wait for the given lenght of time, [FLOAT], in seconds.

### `#WAIT [CONDITION]`
Causes the entity to wait for the given condition. The script will stay on this command until the relevant condition is met.

## EXAMPLES:

A quick example of code for an entity that goes back and forth on a platform until it hits a pit or a wall, turns around, then repeats:

    :PATROL
    #MOVE CURRENT UNTIL PIT WALL
    #DIRECTION TURN
    #WAIT 0.5
    #GOTO PATROL
