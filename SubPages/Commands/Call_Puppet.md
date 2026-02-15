---
layout: page
title: Call_Puppet
permalink: /supportedcommands/base/call_puppet
parent: Base
---
 
# Call_Puppet

## Parameters

### Required:

**Parameter1**: A string representing the command name.

### Optional:

*No optional parameters*

## Functionality

A command for when you are too lazy to write a new command. Allows for a string to be passed, where when the command is run, an event within Oyster is called with that string passed to it. From that there should be a script within the game that is listening for that event, which will then use that string to decide what to do.

The event is raised once per time the command is encountered.

## Version Info

This command has been supported as of Oyster 4.0.0 in Speed Dating for the Socially Inept, and was brought into Base Oyster with version 4.1.0.