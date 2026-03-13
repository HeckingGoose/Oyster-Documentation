---
layout: page
title: Act_Speak
permalink: /supportedcommands/base/act_speak
parent: Base
---

# Act_Speak

## Parameters

### Required:

**Parameter1**: A string containing text to display.

### Optional:

**instant**: A boolean describing whether the script should push all characters instantly or not, defaults to false.

**wait**: A boolean describing whether the script should wait for user input when done or not, defaults to true.

**mute**: A boolean describing whether Oyster should play any speech sounds while text is being pushed, defaults to false.

## Functionality

Replaces the contents of the main text box with the given text.

When not muted, plays back a random sound from the character's `CharacterSound` component at a fixed rate while text is being pushed. Defaults to 2.5x the rate at which characters are pushed to the text display. Setting the integer variable `mumblesPerSecond` earlier in the script than an act command will override this default behaviour such that the time between sounds is one divided by `mumblesPerSecond`.

## Version Info

This command has been supported as of Oyster 4.0.0.