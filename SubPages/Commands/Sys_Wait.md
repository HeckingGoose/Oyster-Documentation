---
layout: page
title: Sys_Wait
permalink: /writing/supportedcommands/base/sys_wait
parent: Base
---

# Sys_Wait

## Parameters

### Required:

**Parameter1**: An integer representing the amount of time to wait for, in milliseconds

### Optional:

**canSkip**: A boolean value describing whether the player can click to skip this wait or not. Defaults to false.

## Functionality

Waits for the given amount of time, or skips on player input, if that parameter is set.

## Examples

```oscript
Sys_Wait [300]
Sys_Wait [300, canSkip=False]
```
Pauses script execution for `300` milliseconds, with the player being unable to skip the wait.

```oscript
Sys_Wait [400, canSkip=True]
```
Pauses script execution for `400` milliseconds, with the player being able to skip the wait by calling Oyster's `Nudge` function.

## Version Info

This command has been supported as of Oyster 4.0.0.