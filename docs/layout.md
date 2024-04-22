# Layout

This section describes the physical layout of the circuit. It relies on the breadboard
markers with rows A to J (bottom to top), and columns 1 to 17 (left to right).

## Cutting tracks

Some of the tracks need to be interrupted with a track cutter. Test that the track is properly cut with a multimeter. It's easy to make the cuts before you start soldering. But cuts are
easily bridged with solder, so re-test after you're done soldering and clean/re-cut any
bridges.

You need to cut through the following tracks:

* Row 4, between F and G
* Row 5, between G and H
* Row 12, between H and I
* Row 14, between H and I
* Row 16, between H and I

## Component positioning

The grid below shows you which component goes in each breadboard hole. "*" markers indicate there's something
unusual there, read the notes before soldering. Numbers ①,②,③,... indicate the ends of jumper wires.

|Row|        1|   2|    3|    4|       5|    6|    7|    8|   9|10|11|      12|     13|      14|15|     16|     17|
|---|---------|----|-----|-----|--------|-----|-----|-----|----|--|--|--------|-------|--------|--|-------|-------|
| J |J3(VCC)⑪ |    |POT  |     |POT     |     |     | ⑪  |    |  |  | LEDI1+ | LEDI-*| LEDI2+ |J1| LED1+ | LED1- |
| I |J3(VCC)  |    |     |     |        | ⑫   |     |     |    |  |  | RL1    |       | RL2    |J1| RL3   | ⑫    |
| H |R1       |R1  |     |POT:C|        |     | RP2 | RP2 |    |  |  |        |       |        |J1|       |       |
| G |RP3*     |R2  |     | R2  |RP3*/SWI|SWI:C| SWI | RP  |    |  |  | RL1    |       | RL2    |J1| RL3   |       |
| F |U1:+⑩    |U1  |U1①*| U1  | ③      | RP1 | ④  | U2+ |U2  |U2|U2| U2     | U2    | U2     |U2| U2    | U2⑨   |
|   |         |    |     |     |        |     |     |     |    |  |  |        |       |        |  |       |       |
| E |U1:-     |U1①*|U1   | U1⑩| ③      | RP1 | ④  | U2② |U2②|U2|U2| U2     | U2    | U2     |U2| U2    | U2-⑨  |
| D |         |    | ⑧   | BUT |  ⑥    | BUT |     | ⑧   |    |  |⑥|        |       |        |  |       |       |
| C |C1-      |C1+ |     |     |        |     | ⑦   |     |    |  |  | ⑦     |       |        |  |       |       |
| B |⑬        |    |     | C2  |        |     |     |     |    |  |  |        |       |        |  |       | ⑬    |
| A |C2*      |    |     | BUT |        |BUT⑤ |     |     |    |⑤|  |        |       |        |  |J2(HLT)|J2(GND)|

Notes:
* RP3 goes on the bottom side of the board. The pin on G5 shares the space with one of the side pins of SWI, so you'll have to get them together before soldering. Solder the other pins of SWI first so the switch stays in place before fitting in the wire from RP3 and soldering that.
* Jumper wires ①, ②, ⑨, ⑩, ⑪, ⑫ and ⑬ go on the bottom side of board. Except for ⑫ and ⑬ they share pins with other components. You will need to solder the wire and pin together.
* LEDI- is the place where both cathodes for LEDI1 and LEDI2 go together. Usually you should be able
  to fit both without issue. Make sure you do so before soldering.
* The "-" and "+" sign tell you the orientation of polarized components. For capacitors use
  the obvious meaning. For LEDs, "+" is the anode. For ICs, "+" is the Vcc pin, and "-"
  is the GND pin.
* The ":C" refer to the "common" pin in SWI and POT
* In the clock I built and photographed, you can see C2 in a different location, directly soldered to the power pins of the 555; that's because it was a "late" addition so I had to hack it in after everything else was soldered. The location above should be a bit more convenient, although the decoupling effect may be a bit weaker and I haven't tried it (decoupling is important here, otherwise you get clock pulses on ground, which are read by some circuits as double pulses). So let me know if you seem to have issues with this.

## Build recommendations

The following sequence for putting everything together should be reasonably convenient:

1. Start with the components that go across the middle: RP1, wires ③ and ④ . After clipping the ends of RP1, keep the bits of wire, you'll need them
2. Place the socket for U2 (or a pre-programmed U2 directly if you prefer not to use a socket) in place. Make sure it is the right way in (unlike mine :) ) and put one of the bits of wire to form ② between pins 1 and 2 (at locations E8 and E9, under the board). It doesn't need to go in the hole, just help you build the bridge. Solder pins 1 and 2; with the wire there the solder will form the desired bridge between the two pins.
3. Make sure the socket is tightly in place (it will be harder to move around once you solder the rest of the pins). Put wire ⑨ in position (locations E17 and F17), you can use the other bit of wire from step 1. Solder those in.
4. Solder the rest of the U2 socket.
5. Solder pins 1 and 5 of U1 (locations E1 and F4) so it stays in place
6. Solder jumper wire ① below the board. ① and ⑩ cross each other so at least one of them needs insulation. These share pins with U1.
7. Solder jumper wire ⑩, ensuring a good connection between wire, IC, and PCB. You can test from the other side with a multimeter that pins 4 and 8 of the timer IC have a continuous path.
8. Solder remaining pins of U1
9. Place in BUT and ⑤. Ensure the button is in the right orientation (there should be no connection between A4 and A6 if the button is not pushed). Solder the common joint (location A6). Solder the rest of the pins for the push button and the wire.
10. Solder ⑥ and ⑧. Then solder ⑦.
11. Solder J2; then ⑬ (below the board). Then C2
12. Solder C1, checking the polarity.
13. Solder J3 and ⑪ on the backside. The shared pin here is a tricky one, there's not a lot of space for the wire to go in.
14. Solder R1 and R2. They will be at a bit of an angle, there's no space to get them flush.
15. Solder the point shared by SWI and RP3 (location G5). Remember that RP3 goes below the board (it has enough space to go flush). Solder the other point of RP3
16. Solder the common point of POT. Depending on the physical dimensions of POT and SWI you may need to squeeze/bend them slightly to fit both next to each other (which should be doable while only one pin of each is soldered)
17. Solder the rest of POT and SWI
18. Solder RP2
19. Solder ⑫. That's the last jumper wire!
20. Solder J1
21. Solder all of RL1, RL2, RL3
22. Solder all of the LEDs. note that the 3mm LEDs share the cathode pin at J13, put both through before soldering.

This should be all! Once you're done you can program your 16V8 and place it into the socket.
