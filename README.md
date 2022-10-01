- 👋 Hi, I’m @Elapriya
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Elapriya/Elapriya is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
CODE:
import random 
while(True):
a=random.randint(10,99)
 b=random.randint(10,99) 
if(a>35 and b>60):
print("high temperature and humidity of:",a,b,"%","alarm is on")
 elif(a<35 and b<60):
print("Normal temperature and humidity of:",a,b,"%","alarm is off")
break
Assignment: 1
Code
the final Python Script
the final HTML Code
the final CSS Code
the final Python ScriptPython

# Raspberry Pi 3 GPIO Pins Status And Control Using Flask Web Server and Python
import RPi.GPIO as GPIO
from flask import Flask, render_template, request

app = Flask(__name__)

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

ledRed = 13
ledYellow= 19
ledGreen= 26

ledRedSts = 0
ledYellowSts = 0
ledGreenSts = 0

GPIO.setup(ledRed, GPIO.OUT)
GPIO.setup(ledYellow,GPIO.OUT)
GPIO.setup(ledGreen, GPIO.OUT)

GPIO.output(ledRed, GPIO.LOW)
GPIO.output(ledYellow, GPIO.LOW)
GPIO.output(ledGreen, GPIO.LOW)

@app.route('/')
def index():
    ledRedSts = GPIO.input(ledRed)
    ledYellowSts = GPIO.input(ledYellow)
    ledGreenSts = GPIO.input(ledGreen)
   
    templateData = { 'ledRed' : ledRedSts,
    'ledYellow' : ledYellowSts,
    'ledGreen' : ledGreenSts }
   
    return render_template('index.html', **templateData)

@app.route('/<deviceName>/<action>')
def do(deviceName, action):
    if deviceName == "ledRed":
        actuator = ledRed
    if deviceName == "ledYellow":
        actuator = ledYellow
    if deviceName == "ledGreen":
        actuator = ledGreen

    if action == "on":
        GPIO.output(actuator, GPIO.HIGH)
    if action == "off":
        GPIO.output(actuator, GPIO.LOW)

    ledRedSts = GPIO.input(ledRed)
    ledYellowSts = GPIO.input(ledYellow)
    ledGreenSts = GPIO.input(ledGreen)

    templateData = { 'ledRed' : ledRedSts,
    'ledYellow' : ledYellowSts,
    'ledGreen' : ledGreenSts }

    return render_template('index.html', **templateData )

if __name__ == "__main__":
app.run(host = '0.0.0.0', debug=True
