---
layout: page
title: Meta
permalink: /supportedcommands/base/meta
parent: Base
---

# Meta

## Parameters

### Required:

*No required parameters*

### Optional:

**version**: A string representing the game version which this script was designed for. An example would be "4.0.0".

**game**: A string representing the game that this script is targetting. An example would be 'GroveGame'.

## Functionality

This command is never actually seen by the conversation. Its entire purpose is to provide optional info to the implementation of Oyster running the script so that it can handle the script accordingly (Whether that be logging incompatibility as a warning or emulating Oyster features exclusive to that version is up to the implementation).

It's also important to note that multiple 'meta' commands can be written in one script file and that there is no obligation for the 'meta' command to occur first in the script file. Some examples of using the 'meta' command are:

```oscript
meta [game="GroveGame"]
meta [version="4.0.1"]

# Target game is "GroveGame" and script version is "4.0.1"

meta [game="GroveGame"]
meta [version="4.0.1"]
meta [game="Not GroveGame"]

# Target game is "Not GroveGame" and script version is "4.0.1"

meta [game="GroveGame", version="4.0.1"]

# Target game is "GroveGame" and script version is "4.0.1"

```

## Version Info

This command has been supported as of Oyster 4.0.1.