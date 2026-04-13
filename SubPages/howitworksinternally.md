---
layout: page
title: Conversation Overview
permalink: /games/howitallworks/
parent: For Game Developers
---

# Conversation Overview

## Loading an OSF file

The game hosting the Oyster runtime is responsible for providing a 'promise' in the form of an `A_BackgroundAssetLoader`. Oyster then subscribes to an event provided by this promise that should return a valid string containing the conversation once it has done loading.

## Parsing an OSF

Oyster then parses the OSF to generate an array of potentially valid lines by searching for which lines contain the 'command [parameters]' format that it expects. At this stage it has not built any of the commands yet.

# The main loop

The game running Oyster is responsible for calling the `Update()` function, passing the time since the last call to it so that Oyster can ensure it runs at its target tickrate.

Each tick Oyster loads in the current command if it is not currently loaded, runs the current command, and loads the next 'safe to load' command. A command is considered safe to load if its type does not implement any interfaces that suggest it modifies Oyster variables.

In this way, commands are 'lazy loaded', allowing for variables to be referenced only once when the command loads without causing issues.

When Oyster is told to jump to a different part of the script by something such as a `Jump_To`, all commands are set to `null` to force them to be reloaded, as the jump may bring Oyster to a section of the script that has already been loaded, before later variables may have modified the contents of the command.

The game is also responsible for calling the `Nudge()` function when - for example - the user clicks the mouse. This function tells Oyster to make the current command 'go faster', which could be to skip some text or to move onto the next command if the current command is waiting for input.

# When does it end?

A conversation ends when Oyster reaches the last line in the script. To prevent a conversation from ending early, a jump can be done to move to a further up part of the conversation, or to end a conversation faster a jump to the end can also be done.