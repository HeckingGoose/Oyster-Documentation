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

### Variables
#### Basic Usage

Variables can be used in various places within Oyster. The basic syntax for passing a variable is:

```
$variableName
```

Where '`variableName`' is the name of the variable and `$` states that a variable is being used.

Variables can be passed to any valid Oyster command, given that the variable type matches that of the parameter that is being replaced.

#### Within strings

Variables can also be used within strings, to do this the string should be proceeded with a `$`. An example of this would be:
```
$"I am a string, {variableName}"
```

#### Declaring a Variable

To declare a variable, the command `'Set_Var'` should be used, an example is shown below:
```
Set_Var ["MyNumber", 100]
```

As another example, a variable can be passed to initialise a variable:
```
Set_Var ["MyCopy", $myVar]
```