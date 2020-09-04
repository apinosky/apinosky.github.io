---
layout: post
title: Adaptive RPM Control System
subtitle: PHYS 352 – Electronics II
date: 2014-05-12 02:47:20.000000000 -05:00
categories:
- Projects
tags:
- electronics
- LabView
- UNC BME
permalink: "/2014/05/12/adaptive-rpm-control-system/"
photo: " /assets/images/dans-wheel.png"
---
Designed system including H-bridge controlled DC motor with notched-wheel attachment and optical detector. Used pulse width modulation to operate H-Bridge and modify motor speed. Developed adaptive LabVIEW system to adjust pulse width and force DC motor to match user-specified desired RPM using feedback from optical detector.

Dan’s Wheel is a chopper CD wheel mounted on a small electric motor (_Figure 1)_. The edge of the wheel passes through an optical detector consisting of an infrared LED and a phototransistor (_Figure 2)_. The small notches on the wheel allow light to enter the detector. The first part of this lab required constructing an H-Bridge circuit to drive the bi-directional motor (_Figure 3)_. This H-Bridge contains an extra transistor to allow control of the speed using the duty cycle of the signal entering this transistor. Next, a program called Motor.vi was developed in LabVIEW. This program could be used to start and stop the motor, change the direction of the motor, and set the angular speed to a desired value of revolutions per minute (RPM). Finally, the VI was altered to allow the user to specify the desired end location of a specific slit (3, 6, 9, and 12 o’clock).

<table>
  <colgroup>
    <col width="30%" />
    <col width="30%" />
    <col width="30%" />
  </colgroup>
  <tbody>
    <tr>
      <td markdown="span">![base]( /assets/images/dans-wheel.png) </td>
      <td markdown="span">![base]( /assets/images/slit-detector.jpg) </td>
      <td markdown="span">![base]( /assets/images/dans-wheel-circuit.png) </td>
    </tr>
    <tr>
      <td markdown="span"> Figure 1: Dan's Wheel </td>
      <td markdown="span"> Figure 2: Detector Circuit </td>
      <td markdown="span"> Figure 3: H-Bridge Circuit with Pulse Width Modulation</td>
    </tr>
  </tbody>
</table>

#### **MotorControl.VI**

This VI uses four input lines via the NI USB-6008 data acquisition device (DAQ). Two of these control the direction of a motor via an H-Bridge circuit, one controls the speed of the motor using pulse width modulation, and the final reads the output of the sensor to allow the user to determine the speed of a rotating wheel. (See Lab 9 for a more detailed description).&nbsp; When the START button is pressed, the user may select a desired direction of the wheel as well as a desired set point frequency in RPM. The program runs the wheel with these specifications. The line which reads the output of the sensor is filtered so that only values over 1V are considered "HIGH".&nbsp; The voltages from this line are read and displayed on the front panel. The frequency is detected from this line using a single tone detect VI. Once the output is detected as high, the frequency is divided by 10 (to convert the 6-slitted wheel from Hz to RPM). This value is then divided by the desired RPM and inverted. The error is determined by 1 minus this difference \* 100. Both the detected RPM and RPM Error are displayed on the front panel. Then the desired RPM is divided by 10 and multiplied by this ratio to get the duty cycle. The wheel cannot operate at values under 25 or over 100, so values outside of this range are changed to these limits. The duty cycle is then sent to a square wave which runs from 0 to 5V at a frequency of 100 Hz. This output determines the speed of the wheel.

![MotorControl2p]( /assets/images/motorcontrol2p.png) \\
*Front Panel*

![MotorControl2d]( /assets/images/motorcontrol2d.png) \\
*Block Diagram*

<table>
  <colgroup>
    <col width="30%" />
    <col width="30%" />
    <col width="30%" />
  </colgroup>
  <tbody>
    <tr>
      <td markdown="span">![base]( /assets/images/motorcontrol2d1.png) </td>
      <td markdown="span">![base]( /assets/images/motorcontrol2d2.png) </td>
      <td markdown="span">![base]( /assets/images/motorcontrol2c.png) </td>
    </tr>
    <tr>
      <td markdown="span"> False Condition of RPM Conditional Loop</td>
      <td markdown="span"> False Condition of DAQmx Write Conditional Loop </td>
      <td markdown="span"> Icon </td>
    </tr>
  </tbody>
</table>
