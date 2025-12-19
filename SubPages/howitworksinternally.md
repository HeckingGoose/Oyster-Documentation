---
layout: page
title: How Oyster Works Internally
permalink: /howitworksinternally/
---

# How conversations are read in

Firstly, commands are read in to be a command and a string array of parameters.

Then those are passed to each individual command, based on the command derived prior, where the command itself is responsible for translating those string parameters to the correct values for the command.

This creates the array of commands used to run the conversation itself, the command itself is responsible for telling Oyster to go to the next line or to skip to a different line.

The conversation ends when the last line ends.


**This page is yet to be fully written :) (in other words, most of the words on this page are actually pretty outdated!).**