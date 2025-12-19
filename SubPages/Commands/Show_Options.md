---
layout: page
title: Show_Options
permalink: /suppportedcommands/ineptdategame/show_options
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

## Version Info

This command has been supported as of Oyster 4.0.0.