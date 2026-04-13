---
layout: page
title: Set_IntVar
permalink: /writing/supportedcommands/base/set_intvar
parent: Base
---

# Set_IntVar

## Parameters

### Required:

**Parameter1**: A string representing the name of the variable.

**Parameter2**: An integer representing the variable value.

### Optional:

*No optional parameters*

## Functionality

Declares a variable with the given value. If the variable already exists, then it updates the value of the variable to the given value. When updating the value of a variable, the type must be the same as the original value, or else this command will skip updating the value.

Integers are stored internally as 32-bit signed integers.

## Examples

```oscript
Set_IntVar ["MyInt", 56]
```
Sets an integer variable named `MyInt` to the value `56`. Given the variable does not exist, creates it.

## Version Info

This command has been supported as of Oyster 4.1.0.