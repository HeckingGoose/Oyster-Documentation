---
layout: page
title: Set_Achievement
permalink: /writing/supportedcommands/grovegame/set_achievement
parent: Christmas at Greyling Grove
---

# Set_Achievement

## Parameters

### Required:

**Parameter1**: A string representing the name of the achievement to unlock.

### Optional:

*No optional parameters*

## Functionality

Unlocks the achievement, given it exists.

In Christmas at Greyling Grove, the achievement implementation allows for achievements to have 'requirements', which themselves are like hidden achievements, which can be used to create achievements that require multiple conditions or for something to happen multiple times.

## Examples

```oscript
Set_Achievement ["AchievementName"]
```
Unlocks the achievement `AchievementNAme`.

```oscript
Set_Achievement ["Part1"]
Set_Achievement ["Part2"]
```
Unlocks the achievements `Part1` and `Part2`, in Christmas at Greyling Grove these achievements can be set as "hidden" with an achievement having them as its requirements, thus allowing one achievement to be unlocked via multiple interactions (such as interacting with many doors).

## Version Info

This command has been supported as of Oyster 4.0.0.