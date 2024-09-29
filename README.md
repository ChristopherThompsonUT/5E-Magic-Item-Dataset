# magic-item-data-storage
CSV files of magic items based on the rules of Dungeons and Dragons 5e. 

## Total Magic Items: 15677 ## 

# Data Formatting Guidelines #
## Magic Item Data ##
Each item has the following categories, which are explained below:

* Name - The name of the magic item as given at the beginning of the description.

* Type - The Magic Item Category as found on pages 139-140 of the DMG. The categories are enumerated type, and fall under the following categories:
  * Armor
  * Potions
  * Rings
  * Rods
  * Scrolls
  * Staffs
  * Wands
  * Weapons
  * Wondrous Items
 
When looking to add this information, it is typically under the name and falls within the nine types. This includes any elaborating information following  the type in parenthesis

* Rarity - Rarity describes the rough measure of the item's power relative to oterh magic items. Rarities are an enumerated types, and fall under the following categories.
    * Common
    * Uncommon
    * Rare
    * Very Rare
    * Rarity Varies
    * Legendary
    * Artifact
    * Other - (A category which doesn't fit any of the others)

When a magic item is added to a .csv, it is stored as an array of strings for each type. For example, the magic item "Weapon +1, +2, or +3" can have 'uncommon', 'rare' or 'very rare.' In the csv file, this is denoted as `['uncommon', 'rare', 'very rare']`. 

The following Python code walks you through how to get the rarity of the magic items. `details[1]` is a string  which contains the Type, Rarity, and Attunement. 

```
    #Get the rarity(s) of the item
    rarity = []
    
    #Since the uncommon and common have a common substring, we need to distinguish 
    #each case
    if details[1].count("common")>1:
        rarity.append("common")
        rarity.append("uncommmon")
    elif "uncommon" in details[1]:
        rarity.append("uncommon")
    elif ("common" in details[1] and ("uncommon" not in details[1])):
        rarity.append("common")
    
    #Similar to common, but for rarities with "rare"
    if details[1].count("rare")>1:
        rarity.append("rare")
        rarity.append("very rare")
    elif "very rare" in details[1]:
        rarity.append("very rare")
    elif ("rare" in details[1] and ("very rare" not in details[1])):
        rarity.append("rare")
    
    if "legendary" in details[1]:
        rarity.append("legendary")
    if "artifact" in details[1]:
        rarity.append("artifact")
    if "rarity varies" in details[1]:
        rarity.append("rarity varies")
    
    if len(rarity) == 0:
        rarity.append("other")

```

* Attunement - Attunement is labeled as a Y/N if attunement is required to use the magic item. This is stated after the magic item category. It can be found if "requires attunment" is in the text.

* Attunement Req. - If Attunement is required, then this provides any conditions necessary to attune to the item. This is stated after the Attunement. It can be found if "by a" or "by an" is in the text.

* Description - The Description  of the text which describes what the item looks like, what it does mechanically, etc. It is to be placed in a list/array seperated by the newline character/ paragraph.

## Text Formatting Guidelines for Descriptions ##

To preserve some structure in the magic item descriptions, the following characters are required to denote certain elements common in magic item descriptions

**Bolded Text** - Bolded text will be preceeded and succeeded with "\*\*" on both sides of the word. For example, if a magic item has the **Cursed** in it, it will be formatted as \*\*Cursed\*\*.

**Bulleted Lists** - Bulleted lists will be preceded with a \*. For example, if a magic item has the bullet point " * Shield" in it, it will be formatted as \*Shield.

**Tables** - Tables are to be preceeded and succeeded with a set of brackets `[]`. Each row is to be preceeded and succeeded with a set of brackets `[]`. Finally, each table cell is to be preceeded and succeeded with a set of brackets `[]`. An example is given in the below image. 

![Table Layout Image](https://github.com/ChristopherThompsonUT/5E-Magic-Item-Dataset/blob/main/Table_Example.png)
