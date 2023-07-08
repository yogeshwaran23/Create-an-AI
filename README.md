import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes


listener=sr.Recognizer()
engine=pyttsx3.init()
voices=engine.getProperty('voices')
engine.setProperty('voice',voices[1].id)

def voice_change(text):

    engine.say(text)
    print(text)
    engine.runAndWait()


def take_command():
 try:
    with sr.Microphone() as source:

        print("listening..........")
        voice=listener.listen(source)
        command=listener.recognize_google(voice)
        print(command)
 except:
    pass
 return command
def voice_access():
    try:
        with sr.Microphone() as main:
            get=listener.listen(main)
            txt=listener.recognize_google(get)
            return txt

    except:
        pass
def run_AI():
    command=take_command()
    if 'play' in command:
        song=command.replace('play','')
        voice_change('playing'+song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time=datetime.datetime.now().strftime("%I:%M %p")
        voice_change('the current time is '+time)
    elif 'tell me about'in command:
        person=command.replace('tell me about','')
        Info=wikipedia.summary(person,10)
        voice_change(Info)
    elif 'joke' in command:
        voice_change(pyjokes.get_joke())
    elif 'what can you do'in command:
        voice_change("i can do any think u say: try saying play song on youtube or ask time or try saying tell me some joke")
    elif 'open whatsapp'in command:
        pywhatkit.open_web()
    elif 'send message'in command:
        t = int(datetime.datetime.now().strftime('%H'))
        m = int(datetime.datetime.now().strftime('%M'))
        print(t,m)
        voice_change('plese wait untill the message sent')
        pywhatkit.sendwhatmsg('+91 *******', 'hi', t, m+1)

    else:
        voice_change("i cant get you so please tell me again")

while True:
    run_AI()
