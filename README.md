# Alexa-Project

The project involves creating a voice-controlled virtual assistant similar to Amazon's Alexa using Python.
The objective of the Alexa Python model (or Alexa Skills Kit (ASK) using Python) is to enable developers to create voice-driven capabilities for Alexa, Amazon's virtual assistant. By using Python, developers can write
the backend logic for Alexa skills that handle user requests, process inputs, and provide responses.

## Features 
* __Speech Recognition (speech_recognition library):__
The sr.Recognizer class and recognize_google method are used to capture and interpret voice commands. The microphone is accessed via sr.Microphone().
* __Text-to-Speech (pyttsx3 library):__
The pyttsx3 library is used for converting text to speech. The engine_talk function uses the engine to speak out text. The voice property is set to the second available voice (often female, but it can vary based on the system's voices).
* __YouTube Search and Play (pywhatkit library):__
The assistant can play songs on YouTube using the pywhatkit.playonyt(song) function. The song's name is extracted from the user's command.
* __Time Announcement (datetime library):__
The current time can be announced using datetime.datetime.now().strftime('%I:%M %p') to format the time in a 12-hour format with AM/PM.
* __Wikipedia Search (wikipedia library):__
The assistant can fetch a summary of a topic from Wikipedia using wikipedia.summary(name, 1), which fetches the first sentence of the summary.
* __Jokes (pyjokes library):__
The assistant can tell a joke using the pyjokes.get_joke() function.

## Code Overview
### Importing Libraries
```
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes
```
__speech_recognition:__ For capturing and recognizing speech input.
__pyttsx3:__ For text-to-speech conversion.
__pywhatkit:__ For accessing YouTube and playing videos.
__datetime:__ For fetching the current time.
__wikipedia:__ For retrieving summaries from Wikipedia.
__pyjokes:__ For generating jokes.

### Initialization

```
listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty("voices")
engine.setProperty('voice', voices[1].id)
```
__listener:__ An instance of Recognizer to process audio input.
__engine:__ An instance of pyttsx3 to handle speech synthesis.
__voices:__ A list of available voices. The second voice is selected for the engine.
### Text-to-Speech Function
```
def engine_talk(text):
    engine.say(text)
    engine.runAndWait()
```
__engine_talk:__ A function that converts text to speech and speaks it out.

### Voice Command Recognition
```
def user_commands():
    try:
        with sr.Microphone() as source:
            print("Start Speaking!!")
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa', '')
                print(command)
    except:
        pass  
    return command
```
__user_commands:__ Listens for the user's voice, converts it to text, and processes it. The keyword "alexa" is used to activate the assistant, and it is removed from the command before further processing.
### Main Function (run_alexa)
```
def run_alexa():
    command = user_commands()
    if 'play' in command:
        song = command.replace('play', '')
        engine_talk('playing ' + song)
        pywhatkit.playonyt(song)

    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        engine_talk('The time right now is ' + time)

    elif 'who is' in command:
        name = command.replace('who is', '')
        info = wikipedia.summary(name, 1)
        engine_talk(info)
    
    elif 'tell me' in command:
        joke = pyjokes.get_joke()
        engine_talk(joke)
        
    else:
        exit
```
__run_alexa:__ Executes the appropriate action based on the command:
__Play Music:__ Searches for and plays a song on YouTube.
__Tell Time:__ Announces the current time.
__Wikipedia Search:__ Provides a brief summary of a person or topic.
__Tell a Joke:__ Tells a random joke.
__Exit:__ Exits the function if the command doesn't match any known patterns.
### Program Execution
```
run_alexa()
```
Calls the run_alexa function to start the voice assistant.

## Contributing
If you'd like to contribute to this project, feel free to fork the repository and submit a pull request.

## License
This project is licensed under the MIT License.
