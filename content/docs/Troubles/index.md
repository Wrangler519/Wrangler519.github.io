---
title: 'Troubles we met'
date: 2019-02-11T19:27:37+10:00
draft: false
weight: 3
---

**1. Problem 1: Servo motor**

**Problem:** the starting, ending angle of servo motor are not precise. The rotation rate of servo motor is not stable. It frequently clogs when not placed horizontally.

**Solution:** implement an additional servo motor driver voltage level shifter breakout board that takes in a GPIO PWM and outputs a higher- voltage-protected PWM wave that feeds to the servo motor. With separate power supply and reworked PWM wave GPIO output, the behaviour is now stable. It solves the angle precision problem and the clogging problem at the same time with the additional breakout board.

**Problem 2: Sound sensor**
 
**Problem:** sound sensor tends to behave unstably with different main.c settings(loop VS one go). And it tends to have limited accuracy distinguishing between short sharp sounds and long gentle sounds.

**Solution:** Reconfigured the structure of code. Changing looped sound.c to a one-go structure. Redesigned the way function gets called. Redesigned the way ADC reads in the analog input and the threshold values.

![ezgif com-gif-maker (4)](https://user-images.githubusercontent.com/84453030/205533408-7cd24c92-dc22-4238-bcc6-a89e86ae4948.gif)

**Problem 3: joystick**

**Problem:** the analog output range of joystick is quite random and with some delay. Such behavior is not observable through oscillioscope. The output value of a left push and a right push are distinct for every trail and dependent on previous trail if two pushes were conducted in a short period of time.  Because we are using ADC function of QT PY to read in analog ADC count, and the analog output nature of the joystick, the only way to improve the accuracy is algirithmic.. 

**Solution:** We redesigned the determining algorithm to better improve the accuracy and implemented updated timing contraints to the reading function to minimize the effect between each push.

**Problem 4: main logic**
 
**Problem:** our initial plan was to pick up the following inputs in a sequencer: sound->apds->joystick. But when implementing this function, we were struggling in deciding if we should let the Wrangler wait for one sensor to get input then move on, or wait a certain interval of time for input then move on. In either case, a lagging situation is definitely going to happen if user inputs through one sensor when system is currently waiting for another sensor to read inputs. It can also happen that several inputs are made at the same time but only one of them should actually "instruct" the wrangler to behave. This led to an extremely unstable response from the system.

**Solution:** We decided to change the setting to a new algorithm: use APDS sensor(proxomity) to control/switch between 2 modes: 1. sound mode, 2. joystick mode. Waving the hand at the apds will switch one mode to another.
{{< figure src="/logic2.png" alt="dwarf" width="550px" class="content-gallery" >}} 

**Problem 5: APDS Motion Detection**

We attempted ADPS motion detection extensively through adopting the detection algorithm developed in the source code provided(in Python). The behavior, however, is extremely unstable. It certainly is able to detect the presence of our hands but not necessarily the motion/direction. We also adopted a complicated determining algorithm to find the actual motion. But the first step-reading in values, is rather unstable. An example of such error is illustrated below:  when hands waving on top of the sensor, whatever gesture we made, the raw data is present but not in big difference, after calculation, the gesture is most of the time treated as '0'(up).

{{< figure src="/ges.png" alt="dwarf" width="800px" class="content-gallery" >}} 



