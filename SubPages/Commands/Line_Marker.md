---
layout: page
title: Line_Marker
permalink: /writing/supportedcommands/base/line_marker
parent: Base
---

# Line_Marker

## Parameters

### Required:

**Parameter1**: A string describing the name for this line marker.

### Optional:

*No optional parameters*

## Functionality

Informs the speech system that this line should be tracked as a line marker, by the given name.

A line marker can be considered as similar to a label in assembly programming, with a line marker simply representing a named line number in the script that can be requested to be jumped to.

## Examples

```oscript
Line_Marker ["PaulSuccess"]
```
Defines a line marker named `PaulSuccess`, which can be jumped to using the `Jump_To` command.

## Version Info

This command has been supported as of Oyster 4.0.0.