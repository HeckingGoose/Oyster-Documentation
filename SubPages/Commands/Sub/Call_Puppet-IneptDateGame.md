---
layout: page
title: Call_Puppet-IneptDateGame
permalink: /supportedcommands/base/call_puppet/ineptdategame
parent: Call_Puppet
---

# Call_Puppet - Speed Dating for the Socially Inept

Shown below are parameters supported by Speed Dating for the Socially Inept:

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