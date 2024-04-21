# What do you need to use the PLD (ATF16V8)

## What is a PLD?

The key to this module's compactness is a "Programmable Logic Device" (PLD). Some people
call them "PAL" or "GAL" instead. These chips don't do anything out of the box; they contain a
collection of "cells", each cell containing a flip-flop and a few gates. Using a
compatible programmer (many EEPROM programmers will do the trick), you can interconnect
those existing components to create different behaviours, and map them into different
input/output pins. 

## What do you need to use them?

* Hardware: To "configure" a PLD, you need an EEPROM programmer that supports this chip. 
  **Not every EEPROM programmer does; in particular, Arduino-based programmers can't write PLDs**.
  I'm using a T48, the successor of the popular TL866-ii+; both are relatively cheap and
  can write these PLDs. The instructions below assume you have one of those.
* Software: You need two main pieces of software. The first one transforms some
  definitions describing what you want the chip to do into a cell interconnection
  that can be "burned" into the chip. The output of that is a ".jed" file. Then, you can
  use software specific for your programmer to burn the .jed file into the device.
  * I use Atmel's "WinCUPL" software, which generates the JED file. Other alternatives include
    PALASM (very old!), GALasm (non-commercial use only), and Galette (which has been
    intermittently unmaintained but seems to be active as of April 2024).
    These use very different syntaxes to specify the logic definition.
  * For the T48 or TL866, the manufacturer-provided software can do this, although I use 
    [minipro](https://gitlab.com/DavidGriffith/minipro) (Note: I added the T48 support in minipro, and it is still experimental, but it seems to work for me).

## WinCUPL

Atmel, owned by Microchip makes the ATF16V8. The chips are supported and still
manufactured. Microchip has a philosophy of rarely stopping to make old parts, so designs
relying on their ICs can keep being maintained. However, there's not a lot of effort in
improving the software support features. The official software for using older PLDs is
called [WinCUPL](https://www.microchip.com/en-us/development-tool/wincupl) and can be
downloaded for free from [Microchip's website](https://www.microchip.com/en-us/products/fpgas-and-plds/spld-cplds/pld-design-resources); it
asks for a license number, but there's a free one on the download page itself.

WinCUPL is very old, has a UI that looks taken out of the '90s (because it probably is),
and includes an IDE that's extremely unreliable: For me, the syntax highlighter messed up
the colours of my code after a bit of edition, and it crashed after every compile to JED
(the compile worked but then the IDE closed itself). So I avoid it like the plague.

However, when you install it, you get some command line tools that are actually quite
reliable. It also comes with several example files to help you understand how to design the logic
formulas that get translated to cell interconnects. I've run it in Windows 10 and
Linux (through the WINE emulation layer), and it works ok. You'll need to be familiar
with a command line.

Installing it is relatively straightforward. By default, it goes into `c:\Wincupl`. If you
have a cupl file like [the one for this project](https://github.com/siliconchronicles/clock-module/blob/main/cupl/be8clock.pld),
you can build it with this command:

```
c:\wincupl\shared\cupl.exe -j -u c:\wincupl\shared\Atmel.dl be8clock.pld
```

Or in Linux:
```
wine 'c:\wincupl\shared\cupl.exe' -j -u 'c:\wincupl\shared\Atmel.dl' be8clock.pld
```


If your file is correct, you will get a `be8clock.jed` file.

## minipro

minipro is an open-source programmer that's compatible with the TL866 family of devices
by xgecu (including the T48 and T56). These reasonably priced, widely available
devices support a wide range of ICs.

If you have it, you can install minipro (check their webpage for up-to-date install
instructions), insert the ATF16V8 in the device, and write the JED file with the following
command:

```
minipro -u -w be8clock.jed -p ATF16V8B
```

After minipro writes the cell configuration into the chip, it will verify. If
verification fails, check if you're using the right IC (see below) and that there are no
compilation issues with your cupl file. **Don't use the misconfigured PLD**. A badly
written PLD could have an internal invalid configuration that shorts itself or overheats, and
you may end up damaging the PLD or other components.

## Using a different PLD

There are a few variants of the 16x8 PLD that are slightly different. Most will support
this project but may have different programming algorithms. Check the following if you
are using a different device:

* The cupl file has a "device" line that I've set to `g16v8a`. If your device is
  different you may need something else here. The WinCUPL buggy IDE has a list of
  devices and specifies for the chip name what's the corresponding "device" label
  that you required in the CUPL file.
* Different variants may need different programming algorithms or voltages.
  minipro may require you to change the `-p ATF16V8B` to something else. Check the
  output of `minipro -l` to see if your device is listed.

