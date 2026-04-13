---
layout: page
title: Set_Name
permalink: /writing/supportedcommands/base/set_name
parent: Base
---

# Set_Name

## Parameters

### Required:

**Parameter1**: A string representing the value to set for the name display.

### Optional:

*No optional parameters*

## Functionality

Changes the value of the name display in the conversation to the given name. **Does not change the name of the character themselves**, the change is only visual for the current conversation. Is intended to be used to spoof multiple characters, alongside Set_Looker.

## Examples

```oscript
Set_Name ["Paul"]
```
Sets the text of the name display to `Paul`.

## Version Info

This command has been supported as of Oyster 4.0.0.