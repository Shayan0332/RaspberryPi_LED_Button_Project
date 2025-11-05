import RPi.GPIO as GPIO
import time

# Setup GPIO mode
GPIO.setmode(GPIO.BOARD)

# Define pins
LED_PIN = 11
BUTTON_PIN = 13

# Setup GPIO pins
GPIO.setup(LED_PIN, GPIO.OUT)
GPIO.setup(BUTTON_PIN, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)

print("Program started...")

try:
    while True:
        if GPIO.input(BUTTON_PIN) == GPIO.HIGH:
            GPIO.output(LED_PIN, GPIO.HIGH)  # LED ON when button pressed
            print("Button Pressed - LED ON")
        else:
            # LED Blinks when button not pressed
            GPIO.output(LED_PIN, GPIO.HIGH)
            time.sleep(0.5)
            GPIO.output(LED_PIN, GPIO.LOW)
            time.sleep(0.5)
            print("Button Released - LED Blinking")
except KeyboardInterrupt:
    GPIO.cleanup()
    print("Program stopped")
