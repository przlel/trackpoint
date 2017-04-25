# Trackpoint: step by step

## Target audience

- hard to cover every use-case
- limited to hand-wired, teensy, tmk, mousekeys
- still useful for others

## FAQ

### Q: What should I use for the trackpoint stem/stick?

**A labret cheek piercing! (yes, I know, weird, but it's awesome!)**

- Relatively cheap.
- Super strong (surgical steel, titanium).
- Really thin in diameter (16G is perfect for between keycaps).
- They come in different lengths (8mm to 26mm).
- They have a flat bottom (great for gluing to TP).
- They have a screw on top ball, in different sizes.

I ordered a few sets of different lengths and different diameters (I
wasn't sure if 16G would be strong enough - it is), as well as different
ball sizes from ebay for relatively cheap.

My trackpoint pointer base sits flush under my 3mm switch plate, and
with a cherry MX switch having a height 10.2mm above the switch plate,
and about 1-2mm PBT cherry keycap on top, the 14mm stem with 3mm ball is
kind of perfect.

For extra friction on the ball, I used some sandpaper.

![stem](images/stem.jpg)

### Q: How do I identify the trackpoint pinout?

**With some luck, or a multimeter and a steady hand.**
(A scope would be better, but unfortunately I don't have one).

If you're lucky, someone has already identified the pinout of the
trackpoint you have (see [pinouts][pinouts]), or at least a similar one.

If not, you'll need to identify the pinout yourself, here are some tips:

- The largest tracer is most likely GND.
- The second largest tracer is most likely VCC.
- Using a multimeter and the PTPM754 [datasheet][datasheets], test for
  connectivity:

```
CLK (INT0)    - PTPM754 pin 24
DATA (TXD/1)  - PTPM754 pin 2
RST           - PTPM754 pin 5
GND           - PTPM754 pin 8
VCC           - PTPM754 pin 22
```

- Alternatively, if you have a scope and know what you're doing:

```
CLK  - should have a frequency reading
DATA - should have a 5V reading
RST  - should have a 0V reading
```

## What you need

## Steps

### 1. Solder leads to trackpoint

- 5 leads
- tin pads
- helping hand to heat leads

### 2. Create the reset circuit (RC)

- What you need:

    - 4.7k resistors x2
    - 100k resistor
    - 2.2uF capacitor
    - Veroboard
    - Cutting knife (x-acto, nt-cutter, japanese knife, etc.)
    - Sandpaper
    - Soldering equipment
    - Insulation tape

- Cut a piece of veroboard (6x5 - the 5 is for rails)

    - Using the cutting knife, perform 5-10 cuts on both sides.
    - Using a little pressure, snap the board on the cut.
    - Use sandpaper to smooth out the cut edges.

![veroboard](images/veroboard.jpg)

- Place the components on the veroboard, and solder

    - Resistors

        - Resistors don't have polarity, no need to worry.
        - Bend component legs, insert into veroboard.
        - On the back-side, slightly bend legs so components stay in position.
        - Use insulation tape to hold resistors in position if needed.
        - Snip legs (leaving about 3-5mm) and solder.
        - Snip the protruding legs for extra clearance.

    - Capacitor

        - Capacitors have polarity, usually marked with a minus (negative).
        - Positive leg must go in the VCC rail.
        - Insert capacitor legs partially, so it can be bent off the
          veroboard for clearance inside the keyboard case.
        - On the back-side, bend legs slightly so it stays in position.
        - Use insulation tape to hold capacitor in position.
        - Snip legs and bend negative over to 100k resistor pad, and solder.
        - Snip the protruding leg for extra clearance.

![collage-reset](images/collage-reset.jpg)

### 3. Solder leads to reset circuit (RC)

- What you need:

    - Thin wire (I used wire wrap 30 guage wire).
    - Wire cutter and stripper.
    - Soldering equipment.
    - Bonus: helping hand.

- Solder trackpoint leads to reset circuit.
- Cut, strip and solder leads to reset circuit that will go to the teensy.

![reset-underside](images/reset-underside.jpg)

### 4. Testing on a breadboard

- usart firmware
- connect, flash, test

### 5. Make trackpoint stem hole in case

- What you need:

    - PCB drill / thin rounded file (to make a 1.2mm hole).

- Decide where you want the trackpoint stem - I prefer using my middle
  finger and have a row staggered keyboard, so I positioned it on the
  cross section between U/I/K (QWERTY layout).

- Locate position for trackpoint stem, and scratch or mark the space
  available.

- Remove the keycaps, make the hole (slowly and carefully), replace
  keycaps.

- Test stem diameter in hole. Should be rigid with a slight amount of
  slack.

![collage-hole](images/collage-hole.jpg)

### 6. Make space for trackpoint in keyboard

- What you need:

    - Insulation tape.
    - Wire cutter.

- Add insulation tape to trackpoint to prevent shorts.
- Rewire diodes / column wires if needed for trackpoint clearance.
- Trim switch legs if needed for trackpoint clearance.
- Relocate D2 and D5 pins if they are already being used.

![collage-rewiring](images/collage-rewiring.jpg)

### 7. Test trackpoint clearance and stem length, glue stem

- What you need:

    - Stem for trackpoint (labret cheek piercing 16G, different lengths).
    - Double sided tape.
    - Glue (loctite super glue-3).
    - Sandpaper.

- Remove red cap.
- Stick a stem to trackpoint pointer base with double side tape.
- Insert trackpoint with stem into hole.
- Close case, flip keyboard, screw on stem ball, test.
- Rinse and repeat for other stems until satisfied with length.

- Remove double sided tape, glue stem.
- Use sandpaper to roughen up the stem ball for added friction.

### 8. Solder reset circuit (RC) to teensy

- Solder leads to teensy:

```
VCC  -> teensy VCC
GND  -> teensy GND
CLK  -> teensy D5
DATA -> teensy D2
```

![inside-side-view](images/inside-side-view.jpg)

### 9. Finish up

- verify position, close, screw on ball

### 10. Update tmk_keyboard firmware and flash

- usart update

## TMK firmware changes and tweaks

- usart support diff
- mousekeys reference
- concurrent tp movement and mousekeys
- polling interval delay (dropped key stokes)
- auto-enable mouse layer on tp movement


[pinouts]: ./pinouts/
[datasheets]: ./datasheets/

