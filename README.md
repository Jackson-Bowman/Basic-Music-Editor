# Basic-Music-Editor
The model implementation is the cs3500.music.model.SoundBoard class.  Notes are added to the model
with the addNote method for new Notes.  Notes can be removed with the remove method.
The user can also get the number of beats per measure of the current model with the getMeasure
method.  The reset() method will remove all the Notes from the model but leave the rest of the data
intact.  The Model can return an array with X characters an | characters to mark Notes and how long
they are held for.  This is used as a middleman between the model and the views without leaking
implementation details.  The exception to this is for the Midi view where efficiency became to
much of a problem.  In this case there is a method in Soundboard that will allow the view to see
the Model in its entirety.

Changes to the Model {
- Pitches are now represented by an enumeration instead of a string.
- Created the Playable abstract class which is extended by Notes and Rests
- added instrument and volume fields to Note
- Overrode Hashcode and Equals for Notes to be compared by their fields
- Added Invariant that tones must be between C­1 and G9
- Nested structure of the model is a HashSet instead of an ArrayList
- made the SoundBoard public for use in the view
- implemented the CompositionBuilder in SoundBoard

The View interface requires that every view be able to initialise itself
(produce output in some way) and create the desired type of view using a factory in the
constructView method.  The midi view implements this interface and initialises by playing
every note in the model in the correct order.  The ConsoleView prints the model as a string
in the console.  It has a header at the top to signify each individual pitch and marks an X at
every beat and pitch where a note exists.  A | symbol marks the continuation of a note that
preceded it.  The GuiViewFrame produces a Swing frame with a sidebar containing the pitches.
It represents a composition by drawing each measure a putting each note in it’s appropriate
location corresponding to pitch and beat.

All the views can use the ViewConstants class which, like its name implies, contains miscellaneous
constants that are shared among the views.

The mock objects MidiDebug and ReceiverLog record the messages sent by the MIDI view when it has
been constructed in “debug” mode.  The mock receiver will print the command it has been given when
the close() method is called and it contains the getLog() method to return the log of commands as
a string.

As for our Controller, we have the functionality to add and remove notes by first selecting the
mode you want (Delete for removing notes, Enter for adding notes, Shift for moving note). To add
a note you first select the add mode (Enter) then click where you wish the note to be placed and
drag the left mouse to the desired duration of the note.

To remove a note, first enter the removing mode (Delete) and select the note that you wish to
delete. If you select something that isn’t a note then a JOption panel will warn you that there
exists no note at that position.

To move a note, first enter the moving mode (Shift) and select the note you wish to move, by
holding and releasing the note at the desired new position. Similar to removing a note, a JOption
panel appear if you try to move something that does not exist.

Keyboard Features
(No edits or mode changes are allowed while the piece is playing)
______________________

Delete/Backspace: will enter you into removing note mode.

Enter: will enter you into the adding note mode.

Right Arrow Key: will scroll to the right.

Left Arrow Key: will scroll to the left.

Up Arrow Key: will scroll up.

Down Arrow Key: will scroll down.

Home: will take you to the beginning of the piece.

End: will take you to the end of the piece.

I: will allow the user to change the instrument of notes being added.

V: will allow the user to change the volume of notes being added.

Space: acts as the play and pause function for the MusicEditor.

