---
layout: page
title: Set_Sprite
permalink: /writing/supportedcommands/base/set_sprite
parent: Base
---

# Set_sprite

## Parameters

### Required:

**Parameter1**: A string representing the name of the sprite to swap to.

### Optional:

*No optional parameters*

## Functionality

Changes the current sprite to the one described by the above parameter, if the sprite does not exist, should swap to an error sprite.

## Examples

```oscript
Set_Sprite ["Idle"]
```
Tells the game to swap the character being spoken to to their `Idle` sprite. If the sprite does not exist, the game should swap the character to an error sprite.

## Version Info

This command has been supported as of Oyster 4.0.0.