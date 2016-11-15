#!/usr/bin/env python

from pylms.server import Server
from pylms.player import Player

import RPi.GPIO as GPIO
import os
import subprocess
import time

# GPIO Setup.
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

# LED pin mapping.
red_pin = 17
green_pin = 27
blue_pin = 22

GPIO.setup(red_pin, GPIO.OUT)
GPIO.setup(green_pin, GPIO.OUT)
GPIO.setup(blue_pin, GPIO.OUT)

# Clear all existing color values.
red = GPIO.PWM(red_pin, 100)
green = GPIO.PWM(green_pin, 100)
blue = GPIO.PWM(blue_pin, 100)

# connect to LMS server and get mode
sc = Server(hostname="127.0.0.1", port=9090)
sc.connect()
sq = sc.get_player("00:1f:1f:cf:95:df")

# Values for standby
value = 0
increment = 2
increasing = True

# Values for Pause
pause_dim = True

# Standby function
def standby(pin):
  pin.start(0)
  global value
  global increasing

  pin.ChangeDutyCycle(value)

  if increasing:
      value += increment
      time.sleep(0.002)
  else:
      value -= increment
      time.sleep(0.002)

  if (value >= 100):
      increasing = False

  if (value <= increment):
      increasing = True
#!/usr/bin/env python

from pylms.server import Server
from pylms.player import Player

import RPi.GPIO as GPIO
import os
import subprocess
import time

# GPIO Setup.
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

# LED pin mapping.
red_pin = 17
green_pin = 27
blue_pin = 22

GPIO.setup(red_pin, GPIO.OUT)
GPIO.setup(green_pin, GPIO.OUT)
GPIO.setup(blue_pin, GPIO.OUT)

# Clear all existing color values.
red = GPIO.PWM(red_pin, 100)
green = GPIO.PWM(green_pin, 100)
blue = GPIO.PWM(blue_pin, 100)

# connect to LMS server and get mode
sc = Server(hostname="127.0.0.1", port=9090)
sc.connect()
sq = sc.get_player("00:1f:1f:cf:95:df")

# Values for standby
value = 0
increment = 2
increasing = True

# Values for Pause
pause_dim = True

# Standby function
def standby(pin):
  pin.start(0)
  global value
  global increasing

  pin.ChangeDutyCycle(value)

  if increasing:
      value += increment
      time.sleep(0.002)
  else:
      value -= increment
      time.sleep(0.002)

  if (value >= 100):
      increasing = False

  if (value <= increment):
      increasing = True

  time.sleep(0.05)
  return

# Pause function  
def pause(pin):
  global pause_dim

  if pause_dim:
      value = 5
      pause_dim = False
  else:
      value = 100
      pause_dim = True

  pin.start(value)
  time.sleep(0.9)
  return

while True:
  # Check LMS server mode
  mode = sq.get_mode()

  if (mode == 'play'):
    blue.start(100)
    red.stop()
    green.stop()

  elif (mode == 'pause'):
    blue.stop()
    red.stop()
    pause(green)

  elif (mode == 'stop'):
    blue.stop()
    standby(red)
    green.stop()
