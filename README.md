![True Relations](https://user-images.githubusercontent.com/15099626/228601102-5e6e55a9-19da-4713-9a39-cbdb95bf1179.jpg)
# True Relations

* True relations does two things.
  * Dynamically changes notoriety with each race in response to notoriety changes with allies and enemies of that race.
  * Fixes IFF settings for stations and their owned ships across the galaxy.
* It started off as a port of the "True Relations" features of [Improved Races 2](https://forum.egosoft.com/viewtopic.php?t=319529). Hence the name. 

## Install

Download the latest release from Github. Unzip the download and copy paste files into the `X3/addon/` folder. Files in the `scripts/` folder go into the `scripts/` folder. File in the `t/` folder go into the `t/` folder.

Launch the game and load a save or start a new game. Navigate to Main `Main menu->Gameplay->Artificial life Settings` and activate the plugin.

## Uninstall

True Relations creates a global variable as part of its initialisation. It deletes the global as part of deactivation.
To make sure the global isn't recreated when you load a save, follow these steps.

* Launch the game and load your save.
* Navigate to `Main menu->Gameplay->Artificial life Settings` and deactivate the plugin.
* Save your game.
* Delete the plugin files.
    * Open the `X3\addon\script` folder in Explorer and delete the relevant scripts. They contain `plugin.jj.true.relations` or `plugin.jj.lib` as part of their filename. Be careful as [Colour By Race](https://github.com/jamesjonesphoenix/X3-Colour-By-Race) also uses some of the same `plugin.jj.lib` files.
    * Open the `X3\addon\t` folder and delete the `9963` translation files.
* Load the save you made after deactivation. True Relations should be gone from the Artificial Life menu and its global will be removed from this save.

## Debug

As of v1.2, True Relations has a dedicated script for activating debugging. To log debugging information run this MSCI code.

    = [THIS]-> call script 'plugin.jj.true.relations.set.debug' :

Info will be logged to `log09963.txt`. By default this file is saved to `C:\Users\Username\Documents\Egosoft\X3AP` or `C:\Users\Username\Documents\Egosoft\X3TC`. Your installation may differ.

You can disable debugging by running the same script with the "disable" flag set to true:

    = [THIS]-> call script 'plugin.jj.true.relations.set.debug' : disable=[TRUE]

Deactivating True Relations in the AL game menu will also disable debugging. 

## Bugs

Found a bug? I'm keen to hear about it. Report it as a Github issue or on the Egosoft forum thread.

## Activation

When the plugin is first activated it records the notorieties between the AI races to the plugin's global array. If the relations between the AI races change you should deactivate and reactivate the plugin so these relations are re-analysed. A typical example would be the Albion Prelude Terran-Commonwealth war kicking off or ending. 

## Dynamic Relations

With every timer interval the plugin has a `20%` chance of checking how notoriety has changed between you and the X3 races. This `20%` value is editable in the t file. When the notoriety check runs you'll gain dynamic notoriety with the allies of any races you gained notoriety with and vice versa for their enemies. With default settings this check will occur once every 15 minutes on average.

The plugin will notify what notoriety you've lost or gained as a result of dynamic relations and also inform you if you've gained or dropped a race rank.

The notoriety effect is calculated as a fraction of the original notoriety change via the following formula.
 
`notoriety-effect = notoriety-gain x (fight-rank + trade-rank - 1) / 100`
 
The effect increases the higher your trade rank and fight rank. It's always possible to become friends with every race.

If you want a different magnitude of dynamic ratio change you can set the ratio in the `9963` t file. The ratio is set to `100` by default.

## IFF Fixer

When the plugin is first activated it scans every AI station in the galaxy and sets its IFF settings according to the race's relations to one another and to you. It does the same for any ships owned by the station.

From there the plugin will run on each timer interval defaulting to `180` seconds and editable in the t file. With each cycle it will select a random sector in the galaxy and check the stations in that sector. The plugin knows which sectors it has already scanned so you can be sure it will scan every sector eventually. Upon completion it will begin running through the universe again. Because it only scans one sector at a time it has little CPU impact.   

The IFF Fixer is particularly useful for two situations

* Pesky hostile stations which won't turn friendly even though you've raised your notoriety with the relevant race.
* Using a mod like [Terran Conflict Plots for Albion Prelude](https://forum.egosoft.com/viewtopic.php?t=324236) which deactivates the Albion Prelude Terran-Commonwealth war. This plugin fixes stations that stay hostile as if the war hadn't been deactivated.

## Compatibility

* AP - Yes.
* TC - Yes
* Farnham's Legend - Probably clashes with FL's own dynamic relations functionality. 
* XRM - Yes
* Litcube's universe - I've never played it, so I'm not sure. Try it and let me know!

## Ancillary stuff

### Languages

* English (my native language)
* German (checked by Olsch)
* French
* Spanish
* Italian
* Czech 
* Polish

### Why an X3 mod in 2023?

Because I'm an idiot.

### Thanks

* Thanks Egosoft for making a great game.
* Thanks Olsch for help with translations
* Thanks Jack08 for Improved Races 2. I began this plugin as a port of the True Relations feature of that mod. 

## Changelog
##### 1.2

* Separated True Relations & [Colour By Race](https://github.com/jamesjonesphoenix/X3-Colour-By-Race) into separate t files. True Relations now uses 9963. Previously it used 9964. Colour By Race uses 9964 and 9965.
* Refactored some functions from jj.true.relations to jj.lib, shared between this plugin and Colour By Race.
* Moved some constants hardcoded in script files into t file. This makes them more easily editable.
    * Ratio of dynamic reputation change.
    * Timer interval.
    * Chance of notoriety check.
* Improved informational messages and debug logging.
    * Plugin will now inform you when your race title changes.
    * Plugin uses game tips where appropriate.
* Added snipped to prevent True Relations being available in FL.
 
##### 1.1

* Added German, French, Italian, Czecha and Polish translations.
* Updated lib scripts in line with . 
