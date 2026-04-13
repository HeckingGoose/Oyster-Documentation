---
layout: page
title: Inc_Affection
permalink: /writing/supportedcommands/ineptdategame/inc_affection
parent: Speed Dating for the Socially Inept
---

# Inc_Affection (Speed Dating for the Socially Inept)

## Parameters

### Required:

*No required parameters*

### Optional:

**half**: A boolean value, when set to true, the character's affection is increased by only half a point. Defaults to false.

## Functionality

Increases the affection of the character currently in conversation by one point, or by half a point if the optional parameter is provided.

## Examples

```oscript
Inc_Affection []
Inc_Affection [half=False]
```
Both commands perform the same behaviour, with them increasing the affection of the character being spoken to by an entire point.

```oscript
Inc_Affection [half=True]
```
The character being spoken to will have their affection increased by half of a point.

## Version Info

This command has been supported as of Oyster 4.0.0.