---
layout: page
title: Making A New Implementation
permalink: /newengineimplementations/
---

# Implementing Oyster for a new game engine

This page will discuss creating a new engine-specific integration for your chosen game engine. Due to it being focussed on being a general guide, no specific game-engines will be mentioned here, instead a list of classes that should be implemented will be discussed. On top of that, it will be mentioned how 'Required' it is to implement each of these classes.

If rather than reading, you'd rather look at an example to learn, take a look at the [Unity Implementation](https://github.com/HeckingGoose/Oyster-UnityIntegration) which implements all functionality of Oyster for Unity. However, as it is targetting Unity, there is an extra layer of object-oriented design, with the inherited classes being wrapped by MonoBehaviour classes to allow them to be added in editor, which may add some confusion in understanding the implementation.

## General Notes

This section is less of a 'Implement this class' and more of a 'Do this when using Oyster'. Always remember to:

- Have a script calling the `Update(float)` method within Oyster frequently, passing the time between the last call,
- Have a script that calls the `Nudge()` method within Oyster when user input corresponding to interacting with Oyster (e.g. progressing dialogue) occurs.

Oyster also uses its own internal `Colour` class that stores colours as a set of four bytes. It is recommended to implement extension methods to convert to and from this colour format and the one used by the game-engine being used. However, this is not required if you intend to work exclusively in Oyster's internal `Colour` class.

## Required classes

These classes must be implemented, or else Oyster will not function as expected, or at all.

### A_CharacterTalker

Simply implement the constructor.

### A_CharacterData

Implement required methods, with syntax for file paths and variables for storing script names being up to the implementation. Take a look at the Unity implementation's [CharacterData.cs](https://github.com/HeckingGoose/Oyster-UnityIntegration/blob/main/Integration/Inherit/CharacterData.cs) for an example on how this can be done.

### A_PlayerTalker

Simply implement the constructor.

### A_SpeechDisplay

Simply implement the constructor.

### A_SceneScript

Simply implement the constructor.

### A_BackgroundAssetLoader<AssetType>

As this is a generic class, its implementation will be required by multiple other classes.

General rules for implementing this class are:

- Implement required `void BeginAssetLoad()` method, such that on the asset being loaded, a `LoadDone' method is called,
- This load done method should store the loaded asset into `_asset` and invoke the `InvokeOnAssetLoad(LoadResult)` event with `LoadResult` being either a success or failure depending on if the asset loaded or not.

## Probably-gonna-need-to-implement classes

These classes are likely going to be required if you want to utilize the majority of Oyster's functionality. However, all of these classes can be skipped in implementation, and Oyster will simply not run commands that attempt to access these features.

### A_CharacterSound

This class implements all functionality related to characters creating sound. Only one method is required to be implemented for this class, beyond passing the correct values to the constructor of the base class. This method is `A_BackgroundAssetLoader<A_Sound>LoadSound(string name)` where functionality must be implemented to load a given sound asset from a string representing the location of the file. The string provided will be defined by oscript using a command that passes a parameter to request a sound to be played, and once the load is completed, the abstract implementation handles adding the sound to the internal dictionary of sounds automatically. As such, the method should only be responsible for creating the asset loader and requesting that it begins to load.

If this class is not implemented, a null reference can simply be passed to the character talker being used.

### A_SoundPlayer + A_Sound

These will only need to be implemented if the class `A_CharacterSound` is implemented. When implementing `A_Sound`, make sure that the sound asset stored within is passed as an object reference within the constructor, and not stored within the implementation side itself, as Oyster will use the object reference to fetch the sound. It is important to note though, that no base Oyster commands directly make use of this runtime audio loading functionality, and as such the implementation of this loading can be left to throw an error when used, unless you choose to add a custom command that requests a specific sound to be played by name.

For `A_SoundPlayer`, simply implement all required methods using whatever audio playback is available in the engine being used, there are no extra considerations required when implementing this class, as long as all methods required for the code to compile are implemented.

### A_CharacterSprite

Simply implement required functionality for code to compile, along with a reference for the character's 'display' to update when sprites are swapped, with `void OnspriteSet(A_Sprite sprite)` being where the this 'display' must be swapped to the provided sprite.

Sprites are not forced to be sprites, sprites are defined by the implementation of `A_Sprite`, but their naming is specific for simplicity when describing the character display functionality.

If this class is not implemented, a null reference can simply be passed to the character talker being used.

### A_Sprite

Only required by `A_CharacterSprite`. Can be implemented with any sprite-adjacent functionality in the engine, in Unity's case it is implemented with materials.

### ITextField

This interface should be implemented as a unit of text that can be drawn to whatever display the game-engine uses (text-based, graphical, etc). Simply implement all methods required by the interface via using a reference to some text-like concept within the chosen game-engine.

It is required for the speech display's `NameText` and `MainText` fields.

### IShowAndHide

This interface should be implemented as a texture that can be toggled between being drawn and not drawn, by the methods stated in the interface.

It is used as part of `ITextField`, and as the `NameTextBacking` and `MainTextBacking` fields of the speech display.

## Optional classes

These classes may depend on the game-engine (or potentially specific game) that it is being implemented for - take for example how a 2D game engine may not require the camera to 'look' at a target when dialogue starts.

### A_Camera

If not implemented, can be passed as null when creating player talker. To implement, simply implement all required functionality using a reference to whatever camera-adjacent 'thing' exists in the game-engine being used.

### A_Looker

Implemented similar to `A_Sprite` and `A_Sound`. Only required for the functionality of having the camera 'look at' objects when in conversation.