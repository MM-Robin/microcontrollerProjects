# Dimming-a-LED-with-the-help-of-an-analog-XY-joystick
a C program that regulates an LED's brightness based on the position and pressure of an external joystick button.

XY Joystick
The outputs X and Y each provide an output signal between 0 and 4 volts, depending on the
position of the joystick.
Medium rest position ≙ 2 V
Lever to the right ≙ 4 V
Lever to the left ≙ 0 V
Button switch at rest ≙ 0 V pressed ≙ 3.3 V

Scope of functions to be implemented:
1.) If the joystick is moved to the right, the brightness should increase slowly.
2.) If the joystick is moved to the left, the brightness should decrease slowly.
3.) The last brightness level is retained in the middle rest position.

JoyStick button:
4.) Press and release the button ≙ full brightness permanently.
Press and release the button again ≙ minimum brightness permanently.
Press and release the button again ≙ full brightness again permanently.
Regardless of this, the dimmer function must always be possible


Using the internal ADC, PWMs and  interruptsof the board TM4C1294 ,  we implement the functions above.

A timer is used to set the duty cycle of a 1 KHz square wave frequency, allowing for a range of 5% to 95%, in order to implement PWM. This timer establishes the output signal's low and high times. There should be no change in the sum of the two times.
