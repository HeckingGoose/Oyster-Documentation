---
layout: page
title: Set_Colour
permalink: /writing/supportedcommands/base/set_colour
parent: Base
---

# Set_Colour

## Parameters

### Required:

**Parameter1**: An integer representing the R value of the target colour.

**Parameter2**: An integer representing the G value of the target colour.

**Parameter3**: An integer representing the B value of the target colour.

**Parameter4**: An integer representing the A value of the target colour.

### Optional:

*No optional parameters*

## Functionality

Sets the colour of the character's name to the parameters specified in one frame.

If all parameters are passed as '-1', then Oyster resets the text colour to its original value from the start of the conversation.

The valid range of values for each parameter is 0-255.

## Examples

```oscript
Set_Colour [0, 0, 0, 0]
```
Sets the character's name colour to be the colour black and fully transparent.

```oscript
Set_Colour [255, 0, 0, 192]
```
Sets the character's name colour to be the colour bright red and a small bit transparent.

## Version Info

This command has been supported as of Oyster 4.0.0 in Speed Dating for the Socially Inept, and was brought into Base Oyster with version 4.1.0.