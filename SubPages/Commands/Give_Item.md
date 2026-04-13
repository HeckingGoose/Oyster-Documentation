---
layout: page
title: Give_Item
permalink: /writing/supportedcommands/grovegame/give_item
parent: Christmas at Greyling Grove
---

# Give_Item

## Parameters

### Required:

**Parameter1**: A string representing the name of the item to give.

### Optional:

*No optional parameters*

## Functionality

Attempts to give the player the named item, given that the player cannot accept the item due to a full inventory, the player will be forced to drop their current item into the world to make room for the new item.

## Examples

```oscript
Give_Item ["About three quid"]
```
Tells the game to give the player an item that is named `About three quid`.

## Version Info

This command has been supported as of Oyster 4.0.0.