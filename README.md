# RPi Servo controller

Author : Brydon Gibson + [the internet]

Feel free to file pull requests/bug reports if you find anything wrong with this class.

This is a class to control a servo on a raspberry pi 3. It should work on a rpi2 but it is untested.
Connect the signal pin (the white/light brown wire) to the GPIO pin sent to the constructor of this class. Pinouts for the RPi can be found online.
Make sure to power the servo appropriately, most don't have reverso polarity protection and most cannot handle more than 5 volts.

A servo works by reading the length of a rectangular pulse, at 50Hz. A 2000us high pulse moves the servo all the way one way, and a 1000us pulse moves it all the way the other way.
Due to rounding (PULSE_RATIO), the servo does not actually get a 2000us pulse at 180*. Most servos don't actually move a full 180* either.
You can send most servos down to 900us and up to about 2100us, and they might move a little further.
If the servo is shaking a lot, please shut it off, they have no temperature protection and might melt themselves.


Note : this class was intended to be run in its own thread, and should be started as such. Example:
Servo myServo = new Servo("24");
new Thread(myServo).start();
myServo.increment_angle();
... etc

Be careful when adding things to this class, long prints or long operations on this thread (in the functions) will cause the servo to shake and be inaccurate (see PWM jitter).
It is best to leave this thread as is and do most operations on another thread.

A note for passive applications :
most servos will shut off when the signal pin is pulled low or floating (ie no signal), this is useful for saving power if the servo is going to remain in the same position for a long period of time
