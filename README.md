# tHPSaveEditor
If you would like to edit your own theHunter: Primal save this is the place for you.

Table of contents - tHPsave.sav files are labelled by the folder they're in -- the reason for this is so that you can copy the file without renaming it:
- avatars - This folder contains images of the avatars in-game. More info on how to add them to your save below.
- base - Contains a save file for very easy editing.
- maxinv - Contains a save file with every important item/weapon, max camo clothing, and full XP/Gold.
- README.md - This file, contains the guide and table of contents you are currently reading.
- id_list.pdf - A full list of every slot and item/weapon ID in the game. All should be accurate as I have double checked all of them and triple checked the majority of them.

I know that theHunter: Primal is no longer active and has been abandoned due to various issues and loss in player base. That being said, before the game was discontinued the company producing it made it so that save files were editable to get around a bug that deleted saves of players. The code for a tHP save file is quite simple; in this file I will provide a guide for creating your own save file and will have references for each item.

A foreword; I am unaware if theHunter: Primal is accessible outside of Steam or available outside of Windows. This guide will direct you to the location of the save file through Steam and Windows directories. If for whatever reason you have the game elsewhere and want to use the guide, I would suggest finding a different guide to help you determine the location of the save file in your directory. Then, feel free to come back here as the steps to build your own file should be the same.

Step #1: Find the directory

Open your file explorer and find the hard drive your OS is located on. The most common folder you will find what you are looking for in is your C: drive. Once you have entered into that hard drive folder then follow the path from Program Files (x86) to the Steam folder, then find the "userdata" folder. Next step is to find the folder named after your Steam account ID. An easy way to find your ID is to go into the Steam program and go to the add friends page. Your Friend Code is the same as your account ID. Once you have found the correct folder, find theHunter: Primal's directory. It should be named 322920 as that is the ID for the game. Enter the "remote" folder inside and there you go; you should be looking at a nice, shiny "tHPsave.sav" file. If you aren't, try loading the game and playing for a few moments to create a new file if there isn't one already inside.

Step #2: Identify the parts of the file

Open up this file in whatever text editor you prefer (Notepad, Visual Studio Code, Sublime, Atom, doesn't matter as long as it can open text files). What you'll be met with is compressed JSON code which looks like a wall of text or one giant line if you have word wrap disabled. That's ok. It is not as complex as it appears at first.

A few things to note:
- Brackets [ or ] form lists or arrays with various items separated by commas. In this guide, we will call them arrays as that is the proper term for JavaScript and JSON.
- Curly braces { or } will be very prevalent within JSON and especially this .sav file. All they do is keep certain parts of the code held together and orderly. Think of each set of braces as "containers" which hold information in something called key-value pairs.
- Key-value pairs are two fields that correspond to each other. They are separated by a colon (:). On the left of the colon is the key and on the right is the value. Values are assigned to keys and keys have special meanings that the game will read and process. There are only a few keys that can be recognized by the game, however, values are not so strict except for certain cases where there is a limited number of things with values. For example, "avatar" has 4 values it can recognize but "tokens" can take any positive integer as it is an arbitrary value.
- Multiple key-value pairs are separated by commas which form a list of pairs. You will see this within the .sav file. Whenever a key-value pair has a comma at the end, it marks a new pair after it that becomes part of a list inside whatever container (brackets/braces) it is in. You can have lists inside containers inside lists inside containers and so on to infinity or the limit of your computer's storage space.

Certain parts of the file are not entirely definable, so for this guide I will do my best to show you everything I know. Below is everything we will be working with in your save file:

- "avatar" - Selects what the character looks like. There are 4 values you can choose from.
- "health" - How much health you spawn in with.
- "inventory" - You're gonna work with this one A LOT. This includes EVERYTHING in your inventory, including clothing, weapons, items, and the extra backpack space at the bottom.
- "position" - This will decide your position in the world. I have not yet seen it be 100% accurate, but it places you roughly in the right area.
- "seen_intro" - A true/false or boolean value that decides whether or not you've seen the welcome message/intro.
- "tokens" - Important one if you want to use the in-game store which appears before you spawn in. Any positive integer should work, I have not encountered an error in number size yet. This determines how many coins, gold, money, whatever you have for the shop.
- "unlocked_items" - Some items are hidden from the store unless you defeat special dinosaurs. If you have this it completely bypasses that.
- "world" - This includes several different world settings, such as time of day and weather.
- "world_map" - This defines various map settings like where you've explored and what settlements you've found.
- "xp" - XP is your Level and is important for the in-game shop as certain items and weapons are locked out if you aren't a certain level.

Step #3: Create and edit!

There is a save file in the folder "base" that you can use to build your save file. Feel free to copy the code into your own save inside the file path I mentioned earlier. It uses the first avatar, some random coordinates, and an inventory with one improvised machete and a map fragment. Of course, this is not a very interesting save file. Let's learn how to fix that.

Inventory:
Your first wish may be to add some items to your inventory. A machete and a map fragment is the basic drop pod loot and not worth reading this guide for. First, let's disect the inventory key-value:

"inventory":
[
  {"guid":"1","health":-2,"item_id":1005,"slot":4},
  {"guid":"1","health":1,"item_id":363,"slot":1}
]

Everything inside of the [] array is the value of the key "inventory". Inside this array is several items arranged in an order with key-value pairs inside of them. Each of these containers with key-value pairs represents an item within your inventory. Let's break down what each individual term means:

- "guid" - A special identifier for each item. It can be completely arbitrary as long as it is unique. In the bottom or extra area of your inventory, items will arrange themselves in order of ascending guid, so if you want to organize items inside your inventory, arrange your guids the way you wish.
- "health" - How much of an item you have. -2 is the default "one item" value for non-stackable items. You can use any number between and including 1 to whatever positive integer you choose for items that can stack (such as map fragments, ammo, health canisters, or arrows).
- "item_id" - This is what determines the item you are adding to your inventory. In this guide I have a compherensive list of every in-game item and their item ids. If you mistype this value the item will not return how you want it to, so be mindful of typos.
- "slot" - This value determines where in your inventory items will go. There are 18 unique slots, including weapons, ammo, scopes, items, clothes, and the extra bottom box.

The file id_list.pdf details a list of all items and slots with corresponding IDs you can use.

Getting the syntax right on this file is extremely important and sometimes it might be easy to miss a comma or a quotation mark. In most cases the game will either throw an error or fail to read your save file and throw you a completely new game. If this happens, just read through and try and see if there's something you've missed.

Every inventory items follows suite to the ones above, save for the fact that the values will be different. Just remember to place commas after item except for the final item, similar to the above example.

Avatar:
After this, an avatar change might be in store. As stated above there are 4 avatars to choose from. Check the avatars folder to see each one. The name of the file corresponds to the number you need to place in the value field.

Position:
If you want to play with your position and move it around, just change the x and y values. Alternatively if you have somewhere specific in-game you want to go you can enter the Map and check the coordinates from there. That being said, you most likely will not be placed in the exact spot everytime.

Health:
You can change your health if you want to attempt a challenge. As far as I know the default health value is 3500.0. I am not sure if it's possible to give yourself more health than this but I do know you can give yourself lower health if you want to. You can also try a one-hit challenge by setting your health to 1.0.

Seen Intro:
Leave this as true. If it is set to false the game gives you the intro screen but doesn't give you any of your inventory items. Your tokens and XP will be left as normal but you will only spawn in with the machete and whatever else you buy from the store.

Tokens:
Coins for the aforementioned store. This can be whatever positive integer you want. This means even if you die and lose your stuff you can fall back on a few quadrillion coins for that 5.56 and some sweet sweet revenge on a raptor.

Unlocked Items:
Some store items aren't available unless you kill rare dinosaurs so if you place a certain line of code in your save file you will automatically unlock all "secret" items without having to kill anything. The line of code is:

"unlocked_items":[1008,1009,1010,1016,1017,1019]

Just remember to place a comma at the end if this isn't the last key-value pair in the save file.

This unlocks:
Raven Tactical Axe, 5.56 Assault Rifle, 5.56 Ammo, Fang Hunting Crossbow, Drop Pod Beacon, and Crossbow Bolts respectively.

World:
There are two main world settings that set time of day and weather. You can play around with these values a bit and see what you come up with as I am unsure what times and weather each numerical value produces.

World Map:
This will generate based on where youve explored and what part of the map is cleared. This is a game generated value and is recommended to stay null unless you have a certain amount of the map explored that you want to copy over from another save file.

XP:
Your level in-game for the store. The value in the base file is 1252061.3750 which will give you a Lvl 50 save, however I do not know if that is the minimum requirement for Lvl 50.

Step #4: Exporting and playing

If you're done with your save file, you can now get ready to play. You have two options from here: you can make the save file writable by the game (which may get overwritten and reset, so save a backup just in case) or you can make the file read-only which completely prevents the game from writing over it, meaning everytime you load the game you will have the same original file. If you want to make it read-only, right click on the file and select Properties. It should be the first page at the bottom (if not, search around the Properties window as it should be in there).

Once you have done whatever you need to with your file, you can exit the window and load your game. Start up a new session and if everything worked with no errors, you should have a beautiful new save file completely hand-crafted by you!

Thanks for reading the guide, if you have any problems feel free to post an issue and I will try and get to resolving it! :D
