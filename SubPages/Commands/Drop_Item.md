---
layout: page
title: Drop_Item
permalink: /supportedcommands/grovegame/drop_item
parent: Christmas at Greyling Grove
---

# Drop_Item

## Parameters

### Required:

*No required parameters*

### Optional:

**onplayer**: A boolean value that when set to true, causes the dropped item to appear at or near the player. Defaults to false.

## Functionality

Causes the player to drop their currently held item. If 'onplayer' is not set to true, then the item spawns out of bounds.

In games with a concept similar to Greyling Grove's 'Lost N Found', this command cannot act as a 'delete item' command, as the 'Lost N Found' would still bring the item back into bounds when used.

## Version Info

This command has been supported as of Oyster 4.0.0.