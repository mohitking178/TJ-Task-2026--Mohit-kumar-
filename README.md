# TJ-Task-2026--Mohit-kumar-

SO HOW IT WORKS -
> listen - it take input from microphone and then it converts spoken language into written text .
> think - it sends the text to LLM and it get response.
> speak - then it converts the response into the audio and play back to user
> loop - then it keep running block of code till the use type "quit,exit,stop"

LIBRARY USED AND WHAT ARE THE ROLES OF THEM-
> the python libraries  used in the block of code are SpeechRecognition,gtts,playsound,request,ollama

explaination-
> Speech Recognition - it captures the audio of user and transcribe the audio
> gtts - it convert text to speech
> play sound- it plays the generated audio
> request- its for Api call
> ollama- it is for local LLM inteference

### start template
''' python 

import speech_recognition as sr
import olama

def listen():
    recognizer = sr.recognizer()
    with sr.Microphone() as source:
         print(" speak now....")
         audio = recognizer.listen(source)
    try:
        text= recognizer.recognize_google(audio)
        print(f"You said : {text}")
        return text
    except sr.UnknownValueError:
        print(" could not understand audio")
        return None

def ask_llm(prompt)
    response = ollama.chat(model="llama3", message=[{"role":"user","content":prompt}])
    reply = rresponse['message']['content']
    print(f" ai: {reply}")
    return reply

from gTTs import gTTs 
import playsound
import os 

def speak(text):
    tts = gTTs (text=text, lang="en")
    filename = "response.mp3"
    tts.savefilename()
    playsound.playsound(filename)
    os.remove(filename)

def main():
    print("Voice Assistant Ready! Say 'quit' to exit.")
    while True:
        user_input = listen()
        if not user_input:
           continue
        if user_input.lower() in ["quit", "exit", "stop"]:
            print("Goodbye!")
            break
        ai_reply = ask_llm(user_input)
        speak(ai_reply)

  if _ _name_ _ == "_ _ main_ _":
       main()
'''


