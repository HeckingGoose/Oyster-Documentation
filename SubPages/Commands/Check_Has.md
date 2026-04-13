---
layout: page
title: Check_Has
permalink: /writing/supportedcommands/grovegame/check_has
parent: Christmas at Greyling Grove
---

# Check_Has

## Parameters

### Required:

**Parameter1**: A string representing the name of the character to check.

**Parameter2**: A string representing the name of the item to check for.

**Parameter3**: A string representing a line marker to jump to if the character has the item.

**Parameter4**: A string representing a line marker to jump to if the character does not have the item.

### Optional:

*No optional parameters*

## Functionality

Checks whether the given character 'has' the given item, as in whether the player has delivered this item to them. Jumps to the respective line markers for whether the check passes or fails.

## Examples

```oscript
Check_Has ["Jenny", "Alyx_0", "FirstPass", "Not Delivered"]
```
Checks if the character `Jenny` has received the gift `Alxy_0`, with it jumping to the line marker `FirstPass` if they have received it, and `Not Delivered` if they have not received it.

## Version Info

This command has been supported as of Oyster 4.0.0.