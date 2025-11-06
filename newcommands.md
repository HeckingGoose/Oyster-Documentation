# Writing new Oyster commands

Oyster is designed to be added to via writing new commands. For Oyster to know that a given type is a command, it can implement any mix of the below interfaces, with the only requirement being that it at least implements 'ISpeechCommand':

### ISpeechCommand

This tells the speech system that this object is a speech command, it is the base interface that all commands are referenced by.

It forces the command to implement:
```cs
public bool Run() { } // Called once per frame when this is the current commnad in conversation.
public ISpeechCommand MakeSelf(string[] rawParameters) { } // Called to make an instance of the relevant command.
```

### ILineMarker

This tells the speech system that this command is a line marker.

It forces the command to implement:
```cs
public string Name { get; } // Access to the name parameter stored within Line_Marker.
```

### ITakesTime

This tells the speech system that this command takes time to complete.

The intended use of this interface is for commands such as 'Act_Speak' or 'Sys_Wait' where the command **will** take a measurable amount of time in seconds to complete. Technically, a command that takes time does not have to implement ITakesTime, however not implementing this command means that the user reading the dialogue has no way of skipping said command.

It forces the command to implement:
```cs
public void MakeItGoFaster() { } // When called, tells the command that we want it to go faster (given the command's parameters, it may just ignore this).
```

### ITextPusher

This tells the speech system that this command pushes text to the display.

It forces the command to implement:
```cs
public bool HasCharactersRemaining { get; } // Whether this text pusher has finished pushing characters (Used to know when to display a 'click to continue' icon).
```
