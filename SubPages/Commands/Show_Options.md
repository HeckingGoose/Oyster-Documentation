---
layout: page
title: Show_Options
permalink: /writing/supportedcommands/ineptdategame/show_options
parent: Speed Dating for the Socially Inept
---

# Show_Options

## Parameters

### Required:

**Parameter1**: A string representing the display text for the first option.

**Parameter2**: A string representing the display text for the second option (for choices with only one option, do not supply this parameter).

**Parameter3** A string representing the display text for the third option (for choices with two or fewer options, do not supply this parameter).

### Optional:

**lm1**: A string representing the name of the line marker to jump to when option one is selected. Technically required due to this, but is written like an optional.

**lm2**: A string representing the name of the line marker to jump to when option two is selected. Required for choices with two or more options.

**lm3**: A string representing the name of the line marker to jump to when option three is selected. Required for choices with three or more options.

## Functionality

This command is a weird one. The definition of required and optional parameter get a bit grey here, so pay close attention to the description of the parameters to know how to write it.

When called, this command will cause a set of options to appear, and will pause script execution until the player selects an option.

## Examples

```oscript
Show_Options ["Option1", lm1="LineMarker1"]
```
Will display a single option on the screen, containing the text `Option1`, which when selected will jump to `LineMarker1`

```oscript
Show_Options ["Option1", "Option2", lm1="LineMarker1", lm2="LineMarker2"]
```
Will display a pair of options on the screen, containing the text `Option1` for the first option, and `Option2` for the second option. Selecting `Option1` will jump the script to `LineMarker1` and selecting `Option2` will jump the script to `LineMarker2`.

## Version Info

This command has been supported as of Oyster 4.0.0.