# Compact Clock Module for debugging

Here's my description of a debugging clock generator. This is not a
"clock" in the colloquial sense, it generates pulses to synchronise
sequential digital circuits.

![Picture of clock module](docs/pictures/module-photo.jpg)

I call this a "debugging" clock because it's not meant to run regular and fast. Instead
it allows me adjust its speed on the fly (by turning a small knob), and to step by step
the circuit it's connected to.

You can see a quick demo of it in action in [my youtube channel](https://www.youtube.com/@dmoisset)

It's main features are:

* Two-mode selector (automatic or single-step), with indicators
* Adjustable frequency control (0.7Hz to 480Hz). frequency can be changed while running
* HLT input: when high, clock stops running. Useful for controlling electronically; if unused
  it can be tied to ground. It's very easy to modify the design to make this line active low if desired.
* Tiny footprint: fits a quarter-size (170 contact) solder-pad breadboard. Requires a few
  wires soldered on the bottom.
* LED indicator of clock cycles.
* 5V TTL levels.
* Compatible drop-in replacement for [Ben Eater's clock module](https://eater.net/8bit/clock)

If you are familiar with Ben Eater's clock, this is very similar in functionality
(but more compact and less educational). If you want to understand how this works rather
than just building it, I recommend you watch [his videos](https://eater.net/8bit/clock).

You can build this on a solderless breadboard if you prefer; although my design goal with
this project was to be able to solder it to get a more reliable and stable clock generator
that I can use in multiple projects.

## Building the module

* [List of materials](docs/materials.md)
* [Schematic](docs/schematic.md)
* [Physical layout and build tips](docs/layout.md)
* Programming the PLD (Programmable Logic Device)
  * [Software and hardware](docs/pld-tooling.md)
  * [Logic definitions (CUPL) for the PLD](docs/cupl.md)
* [Testing](docs/testing.md)
