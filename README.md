# tHPSaveEditor
If you would like to edit your own theHunter: Primal save this is the place for you.

I am currently aware that theHunter: Primal is no longer active and has been abandoned due to various issues and loss in player base. That being said, before the game was discontinued the company producing it made it so that save files were editable to get around a bug that deleted saves of players. The code for a tHP save file is quite simple; in this file I will provide a guide for creating your own save file and will have references for each item.

A foreword; I am unaware if theHunter: Primal is accessible outside of Steam or available outside of Windows. This guide will direct you to the location of the save file through Steam and Windows directories. If for whatever reason you have the game elsewhere and want to use the guide, I would suggest finding a different guide to help you determine the location of the save file in your directory. Then, feel free to come back here as the steps to build your own file should be the same.

Step #1: Find the directory
Open your file explorer and find the hard drive your OS is located on. The most common folder you will find what you are looking for in is your C: drive. Once you have entered into that hard drive folder then follow the path from Program Files (x86) to the Steam folder, then find the "userdata" folder. Next step is to find the folder named after your Steam account ID. An easy way to find your ID is to go into the Steam program and go to the add friends page. Your Friend Code is the same as your account ID. Once you have found the correct folder, find theHunter: Primal's directory. It should be named 322920 as that is the ID for the game. Enter the "remote" folder inside and there you go; you should be looking at a nice, shiny "tHPsave.sav" file. If you aren't, try loading the game and playing for a few moments to create a new file if there isn't one already inside.

Step #2: Identify the parts of the file
Open up this file in whatever text editor you prefer (Notepad, Visual Studio Code, Sublime, Atom, doesn't matter as long as it can open text files). What you'll be met with is compressed JSON code which looks like a wall of text or one giant line if you have word wrap disabled. That's ok. It is not as complex as it appears at first.

A few things to note:
- Brackets [ or ] and curly braces { or } will be very prevalent within JSON and especially this .sav file. All they do is keep certain parts of the code held together and orderly. Think of each set of brackets/braces as "containers" which hold information in something called key-value pairs.
- Key-value pairs are two fields that correspond to each other. They are separated by a colon (:). On the left of the colon is the key and on the right is the value. Values are assigned to keys and keys have special meanings that the game will read and process. There are only a few keys that can be recognized by the game, however, values are not so strict except for certain cases where there is a limited number of things with values. For example, "avatar" has 4 values it can recognize but "tokens" can take any positive integer as it is an arbitrary value.
- Multiple key-value pairs are separated by commas which form a list of pairs. You will see this within the .sav file. Whenever a key-value pair has a comma at the end, it marks a new pair after it that becomes part of a list inside whatever container (brackets/braces) it is in. You can have lists inside containers inside lists inside containers and so on to infinity or the limit of your computer's storage space.

Certain parts of the file are not entirely definable, so for this guide I will do my best to show you everything I know.
"avatar" - Selects what the character looks like. There are 4 values you can choose from. Further in the repo there will be a chart with each avatar and what number to use to select them.
"inventory" - You're gonna work with this one A LOT. This includes EVERYTHING in your inventory, including clothing, weapons, items, and the extra backpack space at the bottom. Lower in this file we will talk about breaking apart the inventory key values as it can be confusing at first.
"position" - This will decide your position in the world. I have not yet seen it be 100% accurate, but it places you roughly in the right area.
"seen_intro" - A true/false or boolean value that decides whether or not you've seen the welcome message/intro.
"tokens" - Important one if you want to use the in-game store which appears before you spawn in. Any positive integer should work, I have not encountered an error in number size yet. This determines how many coins, gold, money, whatever you have for the shop.
"unlocked_items" - Some items are hidden from the store unless you defeat special dinosaurs. If you have this it completely bypasses that.
"world" - This includes several different world settings, such as time of day and weather.
"world_map" - This defines various map settings like where you've explored and what settlements you've found.
"xp" - XP is your Level and is important for the in-game shop as certain items and weapons are locked out if you aren't a certain level.
