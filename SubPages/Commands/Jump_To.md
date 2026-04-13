---
layout: page
title: Jump_To
permalink: /writing/supportedcommands/base/jump_to
parent: Base
---

# Jump_To

## Parameters

### Required:

**Parameter1**: A string representing the name of the line marker to jump to.

### Optional:

*No optional parameters*

## Functionality

Moves the current line-number to the line-number described by the line of the given name (implemented via Line_Marker), or does nothing if the given Line_Marker does not exist.

Line markers can be created using the `Line_Marker` command.

A line marker can be considered as similar to a label in assembly programming, with a line marker simply representing a named line number in the script that can be requested to be jumped to.

## Examples

```oscript
Jump_To ["PaulSuccess"]
```
Jumps the current location of the script to the line marker named `PaulSuccess` if it exists. Given the line marker does not exist, simply continues to the next line of the script.

## Version Info

This command has been supported as of Oyster 4.0.0.