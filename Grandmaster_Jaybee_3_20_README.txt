NPC_SPAWNER:
Class NPCSpawner:
-Requires a reference to:
	-The UnitDatabase
	-A template Unit
	-The "Level" GameObject for the level
	-The "GlobalInfo" ScriptableObject

Class NPCSpawnerDriver:
-Created to test NPCSpawner
-Create object and attach this script(NPCSpawnerDriver) as well as NPCSpawner script to use.
-Creates a row of NPC GameObjects that starts at position POS_X,START_POS_Y and countinue through the next SPAWNS blocks of the map across the Y access.
In other words, it spawns a row of NPCs.
	-SPAWNS is the number of NPCs to spawn
	-POS_X is the X position to start spawning NPCs at.
	-START_POS_Y is the Y position to start spawning the row of NPCs at.
	-The NPC to spawn is chosen randomly from NPCs of ids of MIN_ID to MAX_ID in the UnitDatabase
----------

NPC_WIZARD:
NPC_Wizard now requires input of WeaponDatabase, ArmorDatabase, and AccessoryDatabase for all units
-"UnitDBEntry" is now "Unit"

----------
Skills Classes (SkillsActive, SkillsPassive, GearSkills, RaceBoon (Formerly RaceSkills), Spell, SkillsTemporary (New))
- All now inherit from SkillsBase class
- Have been changed to work with "Mod" classes for the parameter system
- New class: SkillsTemporary (I just thought this might be useful, so I went ahead and implemented it)
	- Designed to be skills that will only exist on units for a certain number of turn cycles and activated by other skills/situations/etc.

Note to JamesJukie: Your Reset() method did not work properly for me. I could create 1 object before having to close and re-open the window.
					I went ahead and commented it's code out. I simply am now setting the temporary object to null instead. This fixes the issue for me.
					This seems to work much better as it resets the GUI to show only the button "Create X Skill" before creating a new skill.
					-I want to make sure I haven't overlooked anything, so tell me if I broke something by doing this or if I mis-interpreted the purpose of this method.
----------
Class GlobalInfo:
-Has reference to the player's highest party level
-Has a reference to the set of Weapon restrictions for which job(s) are compatible with which weapon(s)
	-Created from the file WeaponRestrictionsFile.txt included in the GlobalInfo directory
-An instantiated GameObject with a GlobalInfoInitializer script with a reference to a GlobalInfo object is necessary to use this class.
	-This could be migrated into a singular GameObject
----------

WeaponRestrictionsFile:
-Weapon Restrictions in the GlobalInfo object are set from here
-Format:
JOB_NAME: WEAPON_TYPE1, WEAPON_TYPE2, WEAPON_TYPE3,...
-The GlobalInfo object is expecting
----------

Database<T> class:
-All databases now extend this class
-No methods besides "Verify" are present in this class.
-Some extended classes have new methods
	-WeaponDatabase
	-ArmorDatabase
	-AccessoryDatabase
-The Following I made up and did not submit as they are not actually useful yet, though they may be in the future and I have them on my person:
	-JobDatabase
	-SkillDatabase
	-ItemDatabase
	-AllDatabase*
		*simply holds a reference to all other types of databases
----------
Added Databases:
(these don't actually do anything yet):
-Consumable Database
-MaterialDatabase

(This one is really Important. Is currently in use for holding units.):
-UnitDatabase
----------
Enums:

NEW:
	-WeaponType: now refers to the "type" of weapon i.e. SWORD, LANCE, GUN... (DamageType has replaced old WeaponType. All files should be updated to reflect this.)
		-FILES HAVE BEEN UPDATED FOR THIS:
		-WeaponType- duh
		-Old WeaponType is now DamageType
		-Attack - not so much duh. If there's an error here, rest assured it is my fault
	-DamageType: refers to the type of damage the thing will do i.e. RANGED_PHYSICAL, MELEE_AURA 
	-OptionalRarity: Same as Rarity except with UNDECIDED rarity.
	-Race: The unit's race.
	-Element: The type of any thing's element
	-GearType: Weapon, Armor, Accessory
CHANGES TO OLD:
	-WeaponType: deprecated
	-Rarity: Initialized the values and put EPIC after LEGENDARY.
	-StatTypes: Initialized the values. Makes "Count" easier to understand in my mind
	-JobEnum: Same as old "Job" enum and I added character-unique classes. I just changed the name. Works better while we have "Job" objects
	
-----------

GearPiece and extended classes (Accessory, Armor, and Weapon):
-New "GearPiece" class holds all values shared between (accessories, armor, and weapons)
-Accessory, Armor, and Weapon now extend GearPiece
-----------

SOME MINOR CHANGES TO CLASSES I DID NOT ORIGINALLY WRITE:
Attack class: -Now works with new WeaponDamageType enum
ModApplication class: -Added a ToString() method for testing purposes
SkillsContainer: -Added AddSkills() method for convenience
UnitData: -Commented out Zodiac/Birthdate stuff
----------

Parameters class:	-rewrote SemiRandomLevelUp() method.
					-Added line of code to ApplyModifier() to actually apply the modifier to the real stat (before, it just calculated it)
----------

StatModTypes enum now has its own file and its values are capitalized.

----------
LevelCameraControl class:

Commented out: "mouse was not in window frame" line.