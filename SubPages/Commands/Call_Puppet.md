---
layout: page
title: Call_Puppet
permalink: /suppportedcommands/base/call_puppet
parent: Base
---

# Call_Puppet

**This page's documentation is outdated and needs re-writing.**

## Parameters

### Required:

**Parameter1**: A string representing the command name.

### Optional:

*No optional parameters*

## Functionality

This entire command is one huge hack to speed up game development. Do not use it.

Internally, the 'puppet' is listening to Oyster and waiting for this command, each scene has its own specialised puppet that responds to specific things.

Effectively, this command allows for oddly specific pieces of functionality to be controlled through Oyster, without designing a new command. Making games in a week is tough.

Here is a list of valid 'Parameter1's:

### Presenter's Scene

#### Contestant Display

- ShowContestantsDisplay,
- HideContestantsDisplay.

Enables or disables the contestant display.

- ShowContestantsPre,
- ShowNarin,
- ShowKarin,
- ShowEvelyn,
- ShowCeri,
- ShowNika,
- ShowMila.

Sets the image on the contestants display, all of them should be self explanatory, other than 'ShowContestantsPre' which simply shows a cover image, intended to be used to show a blank-ish screen before contestants get introduced.

#### Multi-Speaker Implementation

- SetSpeaker_All,
- SetSpeaker_Arthur,
- SetSpeaker_Dusk,
- SetSpeaker_Dawn,
- SetSpriter_Arthur,
- SetSpriter_Dusk,
- SetSpriter_Dawn.

The presenter scene does some hackery to get three characters all talking in one conversation. The main way it does this is by implementing its own set of scripts for what would usually make up a character, which contains its own code to manage each character separately, one at a time. Using any of these tells the respective script to swap to the stated character.

### Main Date Room

- DateEnd,
- FadeOut,
- FadeIn.

These should all be self explanatory:

- DateEnd moves the game to the next day,
- FadeOut causes the screen to fade out,
- FadeIn causes the screen to fade in.

## Version Info

This command has been supported as of Oyster 4.0.0 in Speed Dating for the Socially Inept, and was brought into Base Oyster with version 4.1.0.