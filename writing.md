# Writing an oscript

Oyster scripts use the .osf file extension and are stored as plaintext.

## Writing a Line

A line in Oyster can be one of three things:

- A command,
- A blank line,
- A comment.

### A Command

These are written as shown in the 'How to supply parameters' section of the document.

### A blank line

It's as simple as it sounds, just leave a blank line and Oyster will ignore it when parsing the script.

### A comment

Comments start with '#' and may only span one line.
Comments cannot occur on the same line as a command.
An example of one valid and one invalid comment would be:

```OScript
# I'm a valid comment

act_speak ["Pineapple"] # I'm going to cause problems!
```

## How to supply parameters

Parameters are supplied in the following format:
```OScript
COMMAND [REQUIRED1, REQUIRED2, OPTIONAL1=VALUE, OPTIONAL2=VALUE]
```
Where:
- COMMAND is the speech command being used,
- REQUIRED1, REQUIRED2 are required parameter **values** in order,
- OPTIONAL1 and OPTIONAL2 are optional parameter **names** and can be specified in any order,
- VALUE specifies the value for the above named optional parameter and is seperated from the name by an '='.

## Parameter formatting
### Strings

Supplied as:
```
"String content herrreeee"
```

Supported as of Oyster 4.0.0.

### Integers

Supplied as:
```
1000
```

Supported as of Oyster 4.0.0.

### Booleans

Supplied as:
```
True
False
```

They are not case sensitive.

Supported as of Oyster 4.0.0.