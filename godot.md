# [Starforge Games](https://www.starforge-games.com) Godot Style Guide

## Table of Contents

> 1. [Directory Structure](#structure)
> 1. [Static Meshes](#s)
> 1. [Levels / Maps](#levels)
> 1. [Textures](#textures)

<a name="2"></a>
<a name="structure"></a>
## 2. Content Directory Structure

Equally important as asset names, the directory structure style of a project should be considered law. Asset naming conventions and content directory structure go hand in hand, and a violation of either causes unneeded chaos.

There are multiple ways to lay out the content of a Godot project. In this style, we will be using a structure that relies more on filtering and search abilities of the File Browser for those working with assets to find assets of a specific type instead of another common structure that groups asset types with folders.

<a name="2e1"></a>
### 2e1 Example Project Content Structure
<pre>
|-- GenericGame
    |-- <a href="#2.4">_art</a>
    |-- <a href="#2.5">_dev</a>
    |   |-- debug
    |   |-- dan
    |   |-- mike
    |-- <a href="#2.6">addons</a>
    |-- <a href="#2.7">core</a>
    |   |-- actors
    |   |-- ai
    |   |-- inputs
    |   |-- engine
    |   |-- environment
    |   |-- <a href="#2.1.2">game_modes</a>
    |   |-- items
    |-- effects
    |   |-- electrical
    |   |   |-- sounds
    |   |-- fire
    |   |-- weather
    |-- entities
    |   |-- common
    |   |   |-- <a href="#2.3">animations</a>
    |   |   |-- sounds
    |   |-- actors
    |   |   |-- npcs/group_name
    |   |   |   |-- jack
    |   |   |   |   |-- dialog
    |   |   |   |-- steve
    |   |   |-- <a href="#2.1.3">zoe</a>
    |   |-- items
    |   |   |-- interactables
    |   |   |-- pickups
    |   |-- player
    |   |   |-- dialog
    |   |   |-- sounds
    |   |-- vehicles
    |   |   |-- buggy
    |   |   |-- tank
    |   |-- weapons
    |   |   |-- common
    |   |   |-- pistols
    |   |   |   |-- desert_eagle
    |   |   |   |-- rocket_pistol
    |   |   |-- rifles
    |-- environment
    |   |-- music
    |   |-- industrial
    |   |   |-- ambient
    |   |   |   |-- sounds
    |   |   |-- machinery
    |   |   |-- pipes
    |   |-- nature
    |   |   |-- ambient
    |   |   |-- foliage
    |   |   |-- rocks
    |   |   |-- trees
    |   |-- office
    |-- <a href="#2.8">maps</a>
    |   |-- campaign_1
    |   |-- campaign_2
    |   |-- experimental
    |-- <a href="#2.9">materials</a>
    |   |-- debug
    |   |-- metal
    |   |-- paint
    |   |-- utility
    |   |-- weathering
    |-- ui
    |   |-- fonts
    |   |-- hud
    |   |-- materials
    |   |-- menus
    |   |-- sounds
</pre>

The reasons for this structure are listed in the following sub-sections.

### Sections

- 2.1 [Folder Names](#structure-folder-names)
- 2.2 [`Assets` and `AssetTypes`](#structure-assettypes)
- 2.3 [Large Sets](#structure-large-sets)
- 2.4 [Raw Art Assets](#structure-art)
- 2.5 [Developer Folders](#structure-developers)
- 2.6 [Addons and Marketplace Assets](#structure-addons)
- 2.7 [Core](#structure-core)
- 2.8 [Maps](#structure-maps)
- 2.9 [Material Library](#structure-material-library)
- 2.10 [No Empty Folders](#structure-no-empty-folders)

<a name="2.1"></a>
<a name="structure-folder-names"><a>
### 2.1 Folder Names

These are common rules for naming any folder in the content structure.

<a name="2.1.1"></a>
#### 2.1.1 Always Use snake_case[<sup>*</sup>](#terms-cases)

snake_case refers to using only lowercase letters and then instead of using spaces use underscores. For example, `desert_eagle`, `rocket_pistol`, and `a_series_of_words`.

See [Cases](#terms-cases).

<a name="2.1.2"></a>
#### 2.1.2 Never Use Spaces

Re-enforcing [2.1.1](#2.1.1), never use spaces. Spaces can cause various engineering tools and batch processes to fail. Ideally, your project's root also contains no spaces and is located somewhere such as `D:\Project` instead of `C:\Users\My Name\My Documents\Godot Projects`.

<a name="2.1.3"></a>
#### 2.1.3 Never Use Unicode Characters And Other Symbols

If one of your game characters is named 'Zoë', its folder name should be `Zoe`. Unicode characters can be worse than [Spaces](#2.1.2) for engineering tool.

Using other characters outside `a-z`, `A-Z`, and `0-9` such as `@`, `-`, `_`, `,`, `*`, and `#` can also lead to unexpected and hard to track issues on other platforms, source control, and weaker engineering tools.

<a name="2.2"></a>
<a name="structure-assettypes"></a>
### 2.2 Do Not Create Folders Called `assets` or `asset_types`

<a name="2.2.1"></a>
#### 2.2.1 Creating a folder named `assets` is redundant.

All assets are assets.

<a name="2.2.2"></a>
#### 2.2.2 Creating a folder named `meshes`, `textures`, or `materials` is redundant.

All asset names are named with their asset type in mind. These folders offer only redundant information and the use of these folders can easily be replaced with the robust and easy to use filtering system the Content Browser provides.

Want to view only static mesh in `environment/rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will also be sorted in alphabetical order. Want to view both static meshes and skeletal meshes? Simply turn on both filters. This eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

<a name="2.3"></a>
<a name="structure-large-sets"></a>
### 2.3 Very Large Asset Sets Get Their Own Folder Layout

This can be seen as a pseudo-exception to [2.2](#2.2).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `entities/common/animations` and may have sub-folders such as `locomotion` or `cinematic`.

> This does not apply to assets like textures and materials. It is common for a `rocks` folder to have a large amount of textures if there are a large amount of rocks, however these textures are generally only related to a few specific rocks and should be named appropriately. Even if these textures are part of a [Material Library](#2.8).

<a name="2.4"></a>
<a name="structure-art"></a>
### 2.4 Raw Art Files

Any raw source data for art and other assets used in the game folder, like Blender's `.blend` files, Substance Painters `.spp`, or Affinity Designers `.afdesign` files, should also be versioned in the `_art_` folder. This folder should be located in the godot projects' root. The `_art` folder should mirror the project structure. For example, the 3D model of the player should be stored under `_art/entities/player/player.blend`. This makes it easy to find the raw art files for the in-game assets.

It can be versioned either in the same source control repository as the Godot project or a different repository if the raw files' size grows too big.


<a name="2.5"></a>
<a name="structure-developers"></a>
### 2.5 Use Developers Folder For Local Testing

During a project's development, it is very common for team members to have a sort of 'sandbox' where they can experiment freely without risking the core project. Because this work may be ongoing, these team members may wish to put their assets on a project's source control server. Not all teams require use of Developer folders, but ones that do use them often run into a common problem with assets submitted to source control.

It is very easy for a team member to accidentally use assets that are not ready for use, which will cause issues once those assets are removed. For example, an artist may be iterating on a modular set of static meshes and still working on getting their sizing and grid snapping correct. If a world builder sees these assets in the main project folder, they might use them all over a level not knowing they could be subject to incredible change and/or removal. This causes massive amounts of re-working for everyone on the team to resolve.

If these modular assets were placed in a Developer folder, the world builder should never have had a reason to use them and the whole issue would never happen. The Content Browser has specific View Options that will hide Developer folders (they are hidden by default) making it impossible to accidentally use Developer assets under normal use.

Once the assets are ready for use, an artist simply has to move the assets into the project specific folder and fix up redirectors. This is essentially 'promoting' the assets from experimental to production.

<a name="2.6"></a>
<a name="structure-addons"></a>
### 2.6 Samples, Templates, and Marketplace Content

When adding sample content, template files, or assets bought from the marketplace, place them all under the `addons` folder to keep them clearly separated from the assets created by ourselves.

<a name="2.7"></a>
<a name="structure-core"></a>
### 2.7 Use A `Core` Folder For Critical Blueprints And Other Assets

Use `/Project/core` folder for assets that are absolutely fundamental to a project's workings. For example, base `game_mode`, `game_state`, and related classes should live here.

This creates a very clear "don't touch these" message for other team members. Non-engineers should have very little reason to enter the `Core` folder. Following good code structure style, designers should be making their gameplay tweaks in child classes that expose functionality. World builders should be using prefab Blueprints in designated folders instead of potentially abusing base classes.

For example, if your project requires pickups that can be placed in a level, there should exist a base Pickup class in `core/pickups` that defines base behavior for a pickup. Specific pickups such as a Health or Ammo should exist in a folder such as `/Project/entities/items/pickups/`. Game designers can define and tweak pickups in this folder however they please, but they should not touch `core/pickups` as they may unintentionally break pickups project-wide.

<a name="2.8"></a>
<a name="structure-maps"></a>
### 2.8 All Map[<sup>*</sup>](#terms-level-map) Files Belong In A Folder Called Maps

Map files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in `Project/maps`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders of `maps`, such as `maps/campaign_1/` or `maps/arenas`, but the most important thing here is that they all exist within `Project/maps`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's maps are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well as QA processes.


<a name="2.9"></a>
<a name="structure-material-library"></a>
### 2.9 `Material Library`

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Project/materials`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `materials`.

The `materials` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `materials/utility`.

Any testing or debug materials should be within `materials/debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<a name="2.10"></a>
<a name="structure-no-empty-folders"></a>
### 2.10 No Empty Folders

There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:

1. Be sure you're using source control.
1. Immediately run Fix Up Redirectors on your project.
1. Navigate to the folder on-disk and delete the assets inside.
1. Close the editor.
1. Make sure your source control state is in sync (i.e. if using Perforce, run a Reconcile Offline Work on your content directory)
1. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong, and try again.
1. Ensure the folder is now gone.
1. Submit changes to source control.


**[⬆ Back to Top](#table-of-contents)**

<a name="4"></a>
<a name="Static Meshes"></a>
<a name="s"></a>
## 4. Static Meshes

This section will focus on Static Mesh assets and their internals.

### Sections

> 4.1 [UVs](#s-uvs)

> 4.2 [LODs](#s-lods)

> 4.3 [Modular Socketless Snapping](#s-modular-snapping)

> 4.4 [Must Have Collision](#s-collision)

> 4.5 [Correct Scale](#s-scaled)

<a name="4.1"></a>
<a name="s-uvs"></a>
### 4.1 Static Mesh UVs

<a name="4.1.1"></a>
<a name="s-uvs-no-missing"></a>
#### 4.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

<a name="4.1.2"></a>
<a name="s-uvs-no-overlapping"></a>
#### 4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

<a name="4.2"></a>
<a name="s-lods"></a>
### 4.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

<a name="4.3"></a>
<a name="s-modular-snapping"></a>
### 4.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="4.4"></a>
<a name="s-collision"></a>
### 4.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

<a name="4.5"></a>
<a name="s-scaled"></a>
### 4.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**

<a name="5"></a>
<a name="Levels"></a>
<a name="levels"></a>
## 5. Levels / Maps

[See Terminology Note](#terms-level-map) regarding "levels" vs "maps".

This section will focus on Level assets and their internals.

### Sections

> 5.1 [No Errors Or Warnings](#levels-no-errors-or-warnings)

> 5.2 [Lighting Should Be Built](#levels-lighting-should-be-built)

> 5.3 [No Player Visible Z Fighting](#evels-no-visible-z-fighting)

> 5.4 [Marketplace Specific Rules](#evels-levels-mp-rules)

<a name="5.1"></a>
<a name="levels-no-errors-or-warnings"></a>
### 5.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

<a name="5.2"></a>
<a name="levels-lighting-should-be-built"></a>
### 5.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

<a name="5.3"></a>
<a name="levels-no-visible-z-fighting"></a>
### 5.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

**[⬆ Back to Top](#table-of-contents)**


<a name="6"></a>
<a name="textures"></a>
## 6. Textures

This section will focus on Texture assets and their internals.

### Sections

> 6.1 [Dimensions Are Powers of 2](#textures-dimension)

> 6.2 [Texture Density Should Be Uniform](#textures-dimension)

> 6.3 [Textures Should Be No Bigger than 8192](#textures-max-size)

> 6.4 [Correct Texture Groups](#textures-textures-group)

<a name="6.1"></a>
<a name="textures-dimensions"></a>
### 6.1 Dimensions Are Powers of 2

All textures, except for UI textures, must have its dimensions in multiples of powers of 2. Textures do not have to be square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="6.2"></a>
<a name="textures-density"></a>
### 6.2 Texture Density Should Be Uniform

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixel per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be 1024x1024, as that is the closest power of 2 that matches the project's texture density.

<a name="6.3"></a>
<a name="textures-max-size"></a>
### 6.3 Textures Should Be No Bigger than 8192

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this big is simply just a waste of resources.

<a name="6.4"></a>
<a name="textures-group"></a>
### 6.4 Textures Should Be Grouped Correctly

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**
