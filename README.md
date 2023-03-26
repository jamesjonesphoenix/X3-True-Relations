# True Relations

* True relations does two things.
  * Dynamically changes notoriety with each race in response to notoriety changes with allies and enemies of that race.
  * Fixes IFF settings for stations and their owned ships across the galaxy.
* It started off as a port of the "True Relations" features of [Improved Races 2](https://forum.egosoft.com/viewtopic.php?t=319529). Hence the name. 

## Install

Download the latest release from Github. Unzip the download and copy paste files into the `X3/addon/` folder. Files in the `scripts/` folder go into the `scripts/` folder. File in the `t/` folder go into the `t/` folder.

Launch the game and load a save or start a new game. Navigate to Main menu->Gameplay->Artificial life Settings and activate the plugin.

## Uninstall

Colour By Race creates a global variable as part of its initialisation. It deletes the global as part of deactivation.
To make sure the global isn't recreated when you load a save, follow these steps.

* Launch the game and load your save.
* Navigate to `Main menu->Gameplay->Artificial life Settings` and deactivate the plugin.
* Save your game.
* Delete the plugin files.
    * Open the `X3\addon\script` folder in Explorer and delete the relevant scripts. They all
      contain `plugin.jj.true.relations` as part of their filename.
    * Open the `X3\addon\t` folder and delete the `9964` translation files unless you are using the [Colour By Race](https://github.com/jamesjonesphoenix/colour-by-race) plugin which also uses the `9964` t file.
* Load the save you made after deactivation. True Relations should be gone from the Artificial Life menu and its global will be removed from this save.

## Debug

To log debugging information run this MSCI code.

    $pluginData = [THIS]-> call script 'plugin.jj.true.relations.init.global' :
    $pluginData[3] = [TRUE]

Info will be logged to `log09964.txt`. By default this file is saved to `C:\Users\Username\Documents\Egosoft\X3AP` but may differ for your installation.

## Bugs

Found a bug? I'm keen to hear about it. Report it as a Github issue or on the Egosoft forum thread.

## Activation

When the plugin is first activated it records the notorieties between the AI races to the plugin's global array. If the relations between the AI races change you should deactivate and reactivate the plugin so these relations are re-analysed. A typical example would be the Albion Prelude Terran-Commonwealth war kicking off or ending. 

## Dynamic Relations

With every cycle the plugin will check how notoriety has changed between you and the X3 races. For every race you've gained notoriety with you'll gain notoriety with their allies and lose notoriety with their enemies. These cycles are randomised somewhat. They should occur about every 15 minutes on average.

The plugin will notify what notoriety you've lost or gained as a result of dynamic relations and also inform you if you've gained or dropped a race rank.

## IFF Fixer

When the plugin is first activated it scans every AI station in the galaxy and sets its IFF settings according to the race's relations to one another and to you. It does the same for any ships owned by the station.

From there the plugin will cycle every 3 minutes. With each cycle it will select a random sector in the galaxy and check the stations in that sector. The plugin knows which sectors it has already scanned so you can be sure it will scan every sector eventually. Upon completion it will begin running through the universe again. Because it only scans one sector at a time it has little CPU impact.   

The IFF Fixer is particularly useful for two situations

* Pesky hostile stations which won't turn friendly even though you've raised your notoriety with the relevant race.
* Using a mod like [Terran Conflict Plots for Albion Prelude](https://forum.egosoft.com/viewtopic.php?t=324236) which deactivates the Albion Prelude Terran-Commonwealth war. This plugin fixes stations that stay hostile as if the war hadn't been deactivated.

## Compatibility

* AP - Yes.
* TC - I'm not sure, but probably. Try it and let me know!
* Farnham's Legend - Probably clashes with FL's own dynamic relations functionality. 
* XRM - Yes
* Litcube's universe - I've never played it, so I'm not sure. Try it and let me know!

## Ancillary stuff

### Languages

Currently English only. If there's demand for other languages I can probably add them.

### Why an X3 mod in 2023?

Because I'm an idiot.

### Thanks

* Thanks Egosoft for making a great game.
* Thanks Jack08 for Improved Races 2. I began this plugin as a port of the True Relations feature of that mod. 
