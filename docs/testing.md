# How to test this clock module

## Basic functionality test

Connect a jumper wire from GND to 0V in your power supply (or the 0V rail of a powered
breadboard). Connect the HLT line to 0V too. Connect the VCC line to 5V.

As soon as you power up, one of the green LED indicators should light up. If it's the
one on the right, toggle the switch.

You should see a blinking blue LED. If it doesn't blink turn the POT knob around. This
should change the blinking speed, going from fast at one end, to slow at the other.
At the fast extreme you probably can't see the blinking, just the light looking a bit
more dim.

Leave the speed at something reasonably high (pulses should be short, or "invisible"),
and toggle the switch to single-step mode. After this, the push-button should turn the
blue LED once. The LED should stay on while you keep the button pressed. Once released
it will go off, possibly after a short delay (the delay will be longer if you move the
knob to a "slow" speed).

Finally, put the clock back in automatic mode, and try moving the HLT line to 5V and back
to 0V. The clock should stop immediately when the HLT line is not on GND.

That's it!

## Troubleshooting

### General advice

If it doesn't work, something may be misplaced, or the PLD may contain the wrong logic.
A simple way to test is removing the PLD completely from the socket, and putting a jumper
wire in the socket from pin 1 to pin 12. You should have the blinking blue LED
functionality, and the potentiometer should still adjust the speed (the switch and single
step will not work without the PLD). If this doesn't work, the problem is the 555 side
of the circuit and you can debug that. If that works, check that the programming of
your ATF16V8 worked ok, and the connections around switches and PLD

### Double counting

A problem I experienced with a counter is that the LED output looked visually ok, but
when connected to a counter, each pulse counted as two rather than one. After some
debugging, I found out that some clock pulses were detectable on ground due to power
surges in the 555, and that created a very short "double pulse" at the beginning of
each clock cycle.

In my case, that was because I forgot to add C2 to the original design. If it fails for
you, check that C2 is properly soldered. If you still have this issue, it may be worth
soldering it directly to the 555 pins like in [this picture](https://github.com/siliconchronicles/clock-module/blob/main/docs/pictures/module-photo.jpg).
