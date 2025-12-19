---
layout: page
title: Set_BoolVar
permalink: /suppportedcommands/base/set_boolvar
parent: Base
---

# Set_BoolVar

## Parameters

### Required:

**Parameter1**: A string representing the name of the variable.

**Parameter2**: A boolean representing the variable value.

### Optional:

*No optional parameters*

## Functionality

Declares a variable with the given value. If the variable already exists, then it updates the value of the variable to the given value. When updating the value of a variable, the type must be the same as the original value, or else this command will skip updating the value.

## Version Info

This command has been supported as of Oyster 4.1.0.