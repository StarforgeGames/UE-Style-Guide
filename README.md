# [Starforge Games](https://www.starforge-games.com) Style Guides

## Style Guides

### Digital Content Creation

- [Blender](blender.md)
- Substance Designer
- Substance Painter

### Game Engine Coding Conventions

- [Godot](godot.md)
- [Unreal Engine](unreal-engine.md)

## Important Terminology

### Levels/Maps

The word 'map' generally refers to what the average person calls a 'level' and may be used interchangeably. See this term's history [here](https://en.wikipedia.org/wiki/Level_(video_gaming)).

### Identifiers

An `Identifier` is anything that resembles or serves as a "name". For example, the name of an asset, or the name of a material later, or a property, a variable, or a folder name, or for a data table row name, etc...

### Cases

There are a few different ways you can `CaseWordsWhenNaming`. Here are some common casing types:

#### PascalCase

Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.

#### camelCase

The first letter is always lowercase but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.

#### Snake_case

Words can arbitrarily start upper or lowercase but words are separated by an underscore, e.g. `desert_eagle`, `Style_Guide`, `a_Series_of_Words`.

### Variables / Properties

The words 'variable' and 'property' in most contexts are interchangable. If they are both used together in the same context however:

#### Property

Usually refers to a variable defined in a class. For example, if `Barrel` had a variable `IsExploded`, `IsExploded` may be referred to as a property of `Barrel`.

When in the context of a class, it is often used to imply accessing previously defined data.

#### Variable

Usually refers to a variable defined as a function argument or a local variable inside a function.

When in the context of a class, it is often used to convey discussion about its definition and what it will hold.

## 0. Principles

These principles have been adapted from [idomatic.js style guide](https://github.com/rwaldron/idiomatic.js/).

### 0.1 If your project already has a style guide, you should follow it.

If you are working on a project or with a team that has a pre-existing style guide, it should be respected. Any inconsistency between an existing style guide and this guide should defer to the existing.

Style guides should be living documents. You should propose style guide changes to an existing style guide as well as this guide if you feel the change benefits all usages.

> **"Arguments over style are pointless. There should be a style guide, and you should follow it."**
> [_Rebecca Murphey_](https://rmurphey.com)

### 0.2 All structure, assets, and code in any project should look like a single person created it, no matter how many people contributed

Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style. Simply follow the instructions. This style guide is written with best practices in mind, meaning that by following this style guide you will also minimize hard to track issues.

### 0.3 Friends do not let friends have bad style.

If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community such as [Unreal Slackers](http://join.unrealslackers.org/), it is far easier to help and to ask for help when people are consistent. Nobody likes to help untangle someone's spaghetti code or deal with assets that have names they can't understand.

If you are helping someone whose work conforms to a different but consistent and sane style guide, you should be able to adapt to it. If they do not conform to any style guide, please direct them here.

## 00. Globally Enforced Opinions

### 00.1 Forbidden Characters

#### Identifier Names

In any `Identifier` of any kind, **never** use the following unless absolutely forced to:

- White space of any kind
- Backward slashes `\`
- Symbols i.e. `#!@$%`
- Any Unicode character

Any `Identifier` should strive to only have the following characters when possible (the RegEx `[A-Za-z0-9_]+`)

- ABCDEFGHIJKLMNOPQRSTUVWXYZ
- abcdefghijklmnopqrstuvwxyz
- 1234567890
- _ (sparingly)

The reasoning for this is this will ensure the greatest compatibility of all data across all platforms across all tools, and help prevent downtime due to potentially bad character handling for identifiers in code you don't control.
