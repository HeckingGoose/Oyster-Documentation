---
layout: page
title: Set_Script
permalink: /supportedcommands/base/set_script
parent: Base
---

# Set_Script

## Parameters

### Required:

**Parameter1**: A string representing the name of the script to change the character to.

### Optional:

*No optional parameters*

## Functionality

Changes the script that the current character is pointing to to the given value, intended to allow for characters to change conversation between chats or based on given events. **Does not reload the script after being called, player has to manually re-enter conversation, nor does it cause the current conversation to end**.

Supplying a blank string as the parameter causes the character to go to the script prior to their current one, or the script they are already using, if there is no prior script.

## Version Info

This command has been supported as of Oyster 4.0.0.