---
layout: page
title: Set_Looker
permalink: /writing/supportedcommands/base/set_looker
parent: Base
---

# Set_Looker

## Parameters

### Required:

**Parameter1**: A string describing the name of the desired look target.

### Optional:

*No optional parameters*

## Functionality

Attempts to swap the current look target to the object of the given name, if the target object is not present, it does nothing, if the value **'default'** is passed, it returns to the original look target always.

A "looker" is a place in space usually represented by a vector (3D vector for 3D games as an example). The player's camera will slowly turn to look at the current look target.

Look targets are searched for by querying a list stored within the scene script. To add a look target to a scene, create the look target and add a reference to it to this list.

## Examples

```oscript
Set_Looker ["MyLookTarget"]
```
Sets the look target of the player's camera to `MyLookTarget`, given the look target exists.

```oscript
Set_Looker ["default"]
```
Sets the look target of the player's camera back to the look target of the NPC that they started the conversation with.

## Version Info

This command has been supported as of Oyster 4.0.0 in Speed Dating for the Socially Inept, and was brought into Base Oyster with version 4.1.0.