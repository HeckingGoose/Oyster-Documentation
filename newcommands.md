# Writing new Oyster commands

Oyster is designed to be extended by the game developers using it. To this end developers are able to write their own custom commands that will be recognised by Oyster during script parsing.

Below is all that is required to make a command that can be understood and executed by Oyster as part of an oscript:

## The Basics

### How the command is gonna be created at runtime

A more detailed discussion of what's brought up here is in the section 'Letting Oyster know it exists', however it is brought up here as it will be relevant for the section 'Making something that Oyster will be happy with'.

Commands are not created via their constructor, but instead via a method that takes in a set of strings representing raw paramter values in either the form `[parameterValue]` or `[parameterName]=[parameterValue]` and then returns an `ISpeechCommand?`.

Therefore, the built-in methods discussed in the next section all assume that they are being called from a method of this form, as they take in these raw parameters to convert them to something useful.

### Making something that Oyster will be happy with

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

## Letting Oyster know it exists

For Oyster to know that a command exists, it needs to be added via the `AddCommand` method, an example of this can be seen below:

```cs
OysterMain.AddCommand("act_speak", Act_Speak.MakeSelf);
```

The first parameter to be passed is the written name of the command. This is the name that will be written within oscript files to call the command. It is not case-sensitive.

The second parameter is the method to call to make the command. Ideally this method should be a static method within the command itself that returns a constructed version of that command, however this method only requires that the method passed takes an array of strings and returns a potentially null `ISpeechCommand`.

## A Written Example

Below is the source code for `Act_Append`, a command that makes use of a majority of supported interfaces:

```cs
public class Act_Append : A_Command, ITakesTime, ITextPusher
{
    // Const
    protected const bool DEFAULT_INSTANT = false;
    protected const bool DEFAULT_WAITFORUSERINPUT = true;
    protected const bool DEFUALT_MUTE = false;
    protected const int START_POS = 0;

    protected const string PARAMETER_INSTANT_NAME = "instant";
    protected const string PARAMETER_WAITFORUSERINPUT_NAME = "wait";
    protected const string PARAMETER_MUTE_NAME = "mute";


    // Private Variables
    protected string _textToDisplay;
    protected float _timer;
    protected int _currentCharacterIndex;

    // Constructors
    protected Act_Append(
        string textToDisplay,
        bool instant,
        bool waitForUserInput,
        bool mute
        ) : base()
    {
        // Pass in values
        _textToDisplay = textToDisplay;
        _optionalParameters.Add(PARAMETER_INSTANT_NAME, (instant, typeof(bool)));
        _optionalParameters.Add(PARAMETER_WAITFORUSERINPUT_NAME, (waitForUserInput, typeof(bool)));
        _optionalParameters.Add(PARAMETER_MUTE_NAME, (mute, typeof(bool)));

        // Default
        _timer = START_POS;
        _currentCharacterIndex = START_POS;
    }

    // Public Methods
    public static ISpeechCommand? MakeSelf(string[] rawParameters)
    {
        // Declare stores
        string? textToDisplay = string.Empty;

        // Attempt to read in the first value as a string
        LoadParameterValue(rawParameters[0], ref textToDisplay);

        // On fail return null
        if (textToDisplay == null) { return null; }

        // Now read in any optional parameters
        Dictionary<string, (object value, Type type)> optionals = new Dictionary<string, (object value, Type type)>
        {
            { PARAMETER_INSTANT_NAME, (DEFAULT_INSTANT, typeof(bool)) },
            { PARAMETER_WAITFORUSERINPUT_NAME, (DEFAULT_WAITFORUSERINPUT, typeof(bool)) },
            { PARAMETER_MUTE_NAME, (DEFUALT_MUTE, typeof(bool)) }
        };
        List<string> t = [.. rawParameters];
        t.RemoveAt(0);
        LoadOptionalParameterValues(t.ToArray(), ref optionals);

        // Make and return self
        return new Act_Append(
            textToDisplay,
            (bool)optionals[PARAMETER_INSTANT_NAME].value,
            (bool)optionals[PARAMETER_WAITFORUSERINPUT_NAME].value,
            (bool)optionals[PARAMETER_MUTE_NAME].value
            );
    }
    public override bool Run()
    {
        // Is this text intended to be instant?
        if ((bool)_optionalParameters[PARAMETER_INSTANT_NAME].value)
        {
            DumpAllRemaining();
        }

        // Are we at the end?
        if (_currentCharacterIndex >= _textToDisplay.Length)
        {
            // Return true if allowed to auto-progress
            return !(bool)_optionalParameters[PARAMETER_WAITFORUSERINPUT_NAME].value;
        }

        // Are we ready for the next character?
        if (_timer > OysterMain.CharacterTalker!.Data.TimeBetweenCharacters)
        {
            // Reset it
            _timer -= OysterMain.CharacterTalker!.Data.TimeBetweenCharacters;

            // Get a character and push it
            string toAdd = ParseForRTT(_textToDisplay, _currentCharacterIndex);
            OysterMain.PlayerTalker!.SpeechDisplay.MainText.Text += toAdd;

            // Increment counter by this length
            _currentCharacterIndex += toAdd.Length;
        }

        // TODO: Figure out how audio should be implemented

        // Increment timer
        _timer += Definitions.TICKRATE_WAITTIME;

        // Return that we're not done yet
        return false;
    }

    public void MakeItGoFaster()
    {
        // Are we not at the end?
        if (HasCharactersRemaining)
        {
            DumpAllRemaining();
        }

        // Otherwise
        else
        {
            // Time to skip! To do this we just tell ourself that we no longer care for user input
            _optionalParameters[PARAMETER_WAITFORUSERINPUT_NAME] = (false, typeof(bool));
        }
    }

    // Private Methods
    private void DumpAllRemaining()
    {
        // Then push all remaining characters
        OysterMain.PlayerTalker!.SpeechDisplay.MainText.Text += _textToDisplay.Substring(_currentCharacterIndex);

        // And update position accordingly
        _currentCharacterIndex = _textToDisplay.Length;
    }

    // Accessors
    public bool HasCharactersRemaining
    {
        get
        {
            // Return if there are any characters left
            return _currentCharacterIndex < _textToDisplay.Length;
        }
    }
    /// <summary>
    /// Returns the text that this command will display.
    /// </summary>
    public string TextToDisplay { get { return _textToDisplay; } }
    /// <summary>
    /// Returns whether this command will complete within one tick.
    /// </summary>
    public bool Instant { get { return (bool)_optionalParameters[PARAMETER_INSTANT_NAME].value; } }
    /// <summary>
    /// Returns whether this command will wait for user input before going to the next command.
    /// </summary>
    public bool WaitForUserInput { get { return (bool)_optionalParameters[PARAMETER_WAITFORUSERINPUT_NAME].value; } }
    /// <summary>
    /// Returns whether this command will produce speech sounds or not.
    /// </summary>
    public bool Mute { get { return (bool)_optionalParameters[PARAMETER_MUTE_NAME].value; } }
}
```