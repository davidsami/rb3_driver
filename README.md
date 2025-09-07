RB3 Wireless MIDI Keyboard Driver
=================================

This is a user-mode "driver" for the Harmonix Rock Band 3 wireless MIDI
keyboard ("keytar") in wireless mode.

So far, it has only been tested with the Wii version of the keytar, although there's reason in principle why most functionality should not work with the
other versions.

Please see the bottom of this document for licensing and disclaimers.


What is the keytar?
-------------------

The keytar is a 2-octave (25-key) keyboard with full-size spring-loaded
velocity-sensitive keys, octave shift and program change buttons, a
footswitch/modulation pedal jack, and a dual-function modulation/pitch-bend
touch panel.  It comes with a USB dongle that communicates wirelessly with the
keytar.  It also has a standard MIDI out (DIN) jack.


What is this driver supposed to do?
-----------------------------------

Using this driver (although I make no representation that it will work for
you), you can use the keytar to send MIDI messages wirelessly to your computer
using the dongle that comes with the device.

The dongle does not support standard USB-MIDI, so this driver converts the
dongle's USB packets into MIDI and sends the messages to a MIDI output
interface of your choosing.

To use the driver's output as input to another program, you need some way of
patching the MIDI "Out" of this program to the MIDI "In" of the other program.
On Linux, you can use ALSA. On modern Windows, you can use loopMIDI.
On Windows Vista and earlier, this can be done using [MIDI Yoke](http://www.midiox.com).


Do I need to install it / is it complicated to use?
---------------------------------------------------

No, it's just a normal program.

Upon running rb3_driver, you will be presented with a numbered list of MIDI output devices.
Just type the number of your chosen output device, and press the Enter key on
your keyboard.  If something goes wrong, the program will display an error
message, then exit automatically after a few seconds.  To close the program at
any time, just press Control-c or close the window .  While in use, you can minimise the program in
the normal way if you want to avoid cluttering up your screen.

It should automatically detect the correct USB (input) device, provided that
the keytar dongle is plugged in.


What are the dependencies / how do I compile it?
------------------------------------------------

This fork has been successfully compiled under Linux and Windows (using MSYS2 for 64-bit systems, or MSYS and MinGW32 for 32-bit systems).

The main dependencies are libusb (http://libusb.org/) and PortMidi
(http://portmedia.sourceforge.net/portmidi/).

On Linux, you can install them with aptitude:

```sh
sudo apt install libusb-1.0-0-dev libportmidi-dev
```

On Windows MSYS2, you can install them with pacman. For example, to install them in the CLANG64 environment,

```sh
pacman -S mingw-w64-clang-x86_64-libusb mingw-w64-clang-x86_64-portmidi
```

Once you have those in place (and your C compiler/build system obviously!),
just type "make".


How much of the keytar's functionality is implemented?
------------------------------------------------------

At the moment, the keys themselves (including velocity), octave & program
change buttons, the modulation/pitch-bend touch panel, drum split, all foot
pedal features (including stomp and mode change), and the sequencer control
buttons, are fully implemented.  (Let me know if you find any bugs or missing
features.)

Note that drum split requires a General MIDI-compliant synthesizer program.  If
your synthesizer program is not General MIDI compliant, it may output either
nothing at all, or a confusing array of jumbled up notes, when drum split is
active and the drum keys (i.e. the lower 12) are pressed.

Also note that the velocity-sensitivity is limited to at most 5 simultaneous
keys - if 5 keys are held down and you strike another, it will register as
having a velocity of exactly 64 (50% of the maximum value), regardless of the
actual velocity.  This is an unavoidable limitation of the keytar's USB packet
format.

LED output is so far not implemented.


License
-------

Original Copyright (c) 2015 Martin Sidaway

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


Additional legal disclaimers
----------------------------

The authors can not be held responsible for the content, safety, security,
freeness from bugs or viruses, or fitness-for-purpose of websites
mentioned/linked to from this file/this repository, nor of the third-party
programs and libraries mentioned here or anywhere in this repository (even
those mentioned as dependencies).  If you download, install, or otherwise use
any of these programs and libraries, or visit any of the websites, you do so
entirely at your own risk.

The authors of this software are not associated or affiliated with Harmonix Music
Systems, Inc., or Nintendo Co., Ltd. and this software is not in any way
endorsed or approved by those companies or their subsidiaries/associates.

The authors take no responsibility for any attempt to use this software with
Harmonix and/or Nintendo products, and provides no guarantee or affirmation
that it is legal to do so in your jurisdiction.

Harmonix and Rock Band are trademarks of Harmonix Music Systems, Inc.  Nintendo
and Wii are trademarks of Nintendo Co., Ltd.  The authors do not claim any
rights over those trademarks.
