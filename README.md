# Desktop-Assistant-Jarvis-
import pyttsx3
import speech_recognition as sr
import datetime
import webbrowser

# Initialize voice engine
engine = pyttsx3.init()

def speak(text):
    print("Jarvis:", text)
    engine.say(text)
    engine.runAndWait()

def take_command():
    recognizer = sr.Recognizer()

    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)

        audio = recognizer.listen(source)

    try:
        command = recognizer.recognize_google(audio)
        print("You said:", command)
        return command.lower()

    except Exception:
        speak("Sorry, I could not understand.")
        return ""

def wish_user():
    hour = datetime.datetime.now().hour

    if hour < 12:
        speak("Good Morning!")

    elif hour < 18:
        speak("Good Afternoon!")

    else:
        speak("Good Evening!")

    speak("I am Jarvis, your desktop assistant.")
    speak("Intern ID CITS1138")

def run_jarvis():
    wish_user()

    while True:
        command = take_command()

        if "time" in command:
            current_time = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {current_time}")

        elif "open google" in command:
            speak("Opening Google")
            webbrowser.open("https://www.google.com")

        elif "open youtube" in command:
            speak("Opening YouTube")
            webbrowser.open("https://www.youtube.com")

        elif "exit" in command or "stop" in command:
            speak("Goodbye!")
            break

        else:
            speak("Command not recognized.")

# Start Assistant
run_jarvis()
