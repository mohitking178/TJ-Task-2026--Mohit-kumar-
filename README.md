# TJ-Task-2026--Mohit-kumar-

SO HOW IT WORKS -
> listen - it take input from microphone and then it converts spoken language into written text .
> think - it sends the text to LLM and it get response.
> speak - then it converts the response into the audio and play back to user
> loop - then it keep running block of code till the use type "quit,exit,stop"

LIBRARY USED AND WHAT ARE THE ROLES OF THEM-
> the python libraries  used in the block of code are SpeechRecognition,gtts,playsound,request,ollama,sounddevice,numpy.

explaination-
> Speech Recognition - it captures the audio of user and transcribe the audio
> gtts - it convert text to speech
> play sound- it plays the generated audio
> request- its for Api call
> ollama- it is for local LLM inteference
> NumPy - it lets to store and process and recorded audio sample as data
> sound device - it captures the audio from our device and play audio back , acting as the input and output interface for sound.

### start template
''' python 
import sounddevice as sd
import numpy as np
import speech_recognition as sr
import ollama
import requests
from gtts import gTTS
import playsound
import os


def listen(duration=5, fs=44100):
    print("🎤 Recording... (speak now)")
    recording = sd.rec(int(duration * fs), samplerate=fs, channels=1, dtype=np.int16)
    sd.wait()

recognizer = sr.Recognizer()
    audio_data = sr.AudioData(recording.tobytes(), fs, 2)

 try:
        text = recognizer.recognize_google(audio_data)
        print(f"You said: {text}")
        return text
    except sr.UnknownValueError:
        print(" Could not understand audio")
        return None
    except sr.RequestError:
        print(" Speech Recognition service error")
        return None


def ask_llm_local(prompt):
    response = ollama.chat(
        model="llama3",
        messages=[{"role": "user", "content": prompt}]
    )
    reply = response['message']['content']
    print(f"Ollama: {reply}")
    return reply


def ask_llm_cloud(prompt):
    url = "https://api.openai.com/v1/chat/completions"
    headers = {"Authorization": f"Bearer YOUR_API_KEY"}
    data = {
        "model": "gpt-4o-mini",
        "messages": [{"role": "user", "content": prompt}]
    }
    response = requests.post(url, headers=headers, json=data)
    reply = response.json()["choices"][0]["message"]["content"]
    print(f" Cloud AI: {reply}")
    return reply


def speak(text):
    tts = gTTS(text=text, lang="en")
    filename = "response.mp3"
    tts.save(filename)
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

  ai_reply = ask_llm_local(user_input)   
        speak(ai_reply)

if __name__ == "__main__":
    main()

'''

THE OUTPUT SCREENSHOT -

<img width="1382" height="815" alt="Screenshot 2026-09-26 144250" src="https://github.com/user-attachments/assets/952cc27c-b8b5-4e89-a76b-092a740a61ce" />



