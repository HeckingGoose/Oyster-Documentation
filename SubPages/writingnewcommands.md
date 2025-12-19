---
layout: page
title: Writing New Commands
permalink: /writingnewcommands/
---

# Writing new Oyster commands

Oyster is designed to be extended by the game developers using it. To this end developers are able to write their own custom commands that will be recognised by Oyster during script parsing.

Below is all that is required to make a command that can be understood and executed by Oyster as part of an oscript:

## The Basics

### How the command is gonna be created at runtime

A more detailed discussion of what's brought up here is in the section [Letting Oyster know it exists](#letitknowitexists), however it is brought up here as it will be relevant for the section [Making something that Oyster will be happy with](#makingsomethingoysterwillbehappywith).

Commands are not created via their constructor, but instead via a method that takes in a set of strings representing raw paramter values in either the form `[parameterValue]` or `[parameterName]=[parameterValue]` and then returns an `ISpeechCommand?`.

Therefore, the built-in methods discussed in the next section all assume that they are being called from a method of this form, as they take in these raw parameters to convert them to something useful.

### Making something that Oyster will be happy with {#makingsomethingoysterwillbehappywith}

To write a command for Oyster, the command should inherit from `A_Command`, which is an abstract class that implements all the required functionality and interfaces for Oyster to recognise it as a command.

`A_Command` also contains a couple of methods which make writing commands relatively simple. These methods are:

#### LoadParameterValue

```cs
bool LoadParameterValue<VariableType>(string rawValue, ref VariableType? destination)
```

This method is intended to be used for loading any required parameters of a command, via passing the parameter value (where the parameter is in the form `[parameterValue]`) and a variable of the intended data type, which will then store the output of the command.

If the command succeeds at parsing the value, it will be the value that the `rawValue` string represented, but as the given data type, plus the method will return true.

Given the command does not succeed, `destination` will be set to either null or the default value for value types, and the method will return false.

#### LoadOptionalParameterValues

```cs
void LoadOptionalParameterValues(string[] optionalParameters, ref Dictionary<string, (object value, Type type)> destination)
```

This method is the optional parameter equivilent to 'LoadParameterValue' in that it loads parameters in the same way as 'LoadParameterValue' but instead works with parameters of the form `[parameterName]=[parameterValue]`.

An important note for this method is that instead of it working on a single parameter at a time, it instead works on all optional parameters provided by `destination`. These parameters are provided by passing in a pre-existing dictionary filled with the expected optional parameters and their default values. Given that an optional parameter is found in `optionalParameters` and it is read in successfully, the relevant value in `destination` will be updated.

If the same optional parameter is provided twice or more in `optionalParameters`, the last successfully read occurance will be the final value by the end of the method.

#### ParseForRTT

```cs
string ParseForRTT(string line, int startPoint)
```

This method is intended for commands that handle displaying text. All it does is read ahead in the string, and given that there is a Rich Text Tag directly after `startPoint` in `line`, the returned string swaps from being simply the next character to being the next character plus all characters that make up the detected Rich Text Tag.

It's not intended to be used during command creation, but instead during runtime when the command is displaying text.

## Extra Interfaces

Oyster has a few interfaces that it uses to differentiate different types of command, to ensure that certain commands function as intended, or do not cause issues with other commands during or after execution.

### ITakesTime

This interface exposes a method called `MakeItGoFaster`, which is the method that Oyster calls when the user attempts to (for example) rapidly click through dialogue to skip waiting for the text to appear.

### ITextPusher

This interface is required for commands that push text to the main text box to visually work correctly. It exposes a boolean value called `HasCharactersRemaining` that Oyster uses to check for whether it should or should not display a prompt to imply that the text has finished being displayed.

### IModifiesVariables

This interface must be implemented for commands that make changes to variables to work correctly. While this interface does not explicitly require any extra code in a command itself, it is used internally to halt the loading of new commands upon reaching a command that uses this interface.

The point of this being to ensure that if a command makes changes to variables, they are reflected in the commands that come after, as variables are read at command load time, rather than command execution time.

### ILineMarker

This interface is more intended for internal use as any command that is marked as an `ILineMarker` has its position in the script and its marker name cached so that commands such as `Jump_To` can use it to move around the script.

While this is the case, the `Run` method is still called on this command, so line markers that run custom code when jumped to could be implemented using this. However, it is important to note that as the script goes line by line, if normal script execution crosses one of these line markers, the `Run` method will still be called, even if the marker was not explicitly jumped to.

## Letting Oyster know it exists {#letitknowitexists}

For Oyster to know that a command exists, it needs to be added via the `AddCommand` method, an example of this can be seen below:

```cs
OysterMain.AddCommand("act_speak", Act_Speak.MakeSelf);
```

The first parameter to be passed is the written name of the command. This is the name that will be written within oscript files to call the command. It is not case-sensitive.

The second parameter is the method to call to make the command. Ideally this method should be a static method within the command itself that returns a constructed version of that command, however this method only requires that the method passed takes an array of strings and returns a potentially null `ISpeechCommand`.

## A Written Example

For a written example on how commands should be implemented, check out the source code of `Act_Append` [here](https://github.com/HeckingGoose/Oyster/blob/main/Oyster/Commands/Act_Append.cs).