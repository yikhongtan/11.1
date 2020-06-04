# import libraries
import RPi.GPIO as GPIO
import time

# broadcom soc channel and disable warnings
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

# This are ultrasonic sensor connect to gpio 18 and 24 
TRIG = 18
ECHO = 24

# when the operation start to run it will first print out this word.
print("Distance Measurement In Progress")

# Set trigger as output echo as input and led as gpio 23 output
GPIO.setup(TRIG,GPIO.OUT)
GPIO.setup(ECHO,GPIO.IN)
GPIO.setup(23,GPIO.OUT)

# define measure, trigger a pulse then print "waiting for sensor to settle" wait for 0.5 second the trigger a pulse for true data 
        GPIO.output(TRIG, False)
        print("Waiting For Sensor To Settle")
        time.sleep(.5)
        GPIO.output(TRIG, True)
        time.sleep(0.00001)
        GPIO.output(TRIG, False)

# include a while loop when input == 0 then pulse start when input == 1. to find pulse duration time by using end time plus start time. To find distance = (time* speed of sound)/2 because sound has to travel back and forth.
        while GPIO.input(ECHO)==0:
                pulse_start = time.time()

        while GPIO.input(ECHO)==1:
                pulse_end = time.time()

        pulse_duration = pulse_end - pulse_start
        distance = pulse_duration * 17150
        distance = round(distance, 2)
	
# Set a distance below 20 cm. In the terminal it will show print led on and off when the led blink on and off. When the distance above 20 then continue the loop above.	
				if distance < 20 :
                print("LED on")
                GPIO.output(23,GPIO.HIGH)
                time.sleep(1)
while True:
        measure()
                print("LED off")
                GPIO.output(23,GPIO.LOW)

        print("Distance:",distance,"cm")
