# PS1 YPbPr Adapter

## Goal

To get the best possible image quality from the original Sony Playstation, the video signal needs to
be transported in some form of component signal (to avoid the quality loss involved in
encoding/decoding composite video or even S-Video).
The PS1 basically supports RGB output natively, but this standard is not suitable to directly
feed into a mid-range TV. The way to go with current TVs is component video (a.k.a YPbPr) that
has basically the same quality as RGB but uses a different way to encode everything.

There are external converters available for this task, but they add some bulk to the setup 
and additionally need a PS1-to-SCART cable and external power supply.

So, I wanted to build a custom converter circuit that is directly powered from the 
PS1 via its AV-multiout port. By directly using the available Lum output (part of the S-Video signal)
which already carries the necessary sync information, I only had to construct the 
Pb and Pr signals from the R,G,B outputs.

## Implementation

The circuit consists of three main parts:
- Input: Bring the R,G,B signals to a defined DC level
- Create Pb, Pr: Use a resistor matrix and an OpAmp to generate an inverted luminance signal 
    which will then be added to each of the R and B signals to get the Pb and Pr levels.
- Output: Amplify the signals for transmission over the output cable. 

The main problem with the whole project was to get/create a plug for the AV multi-out 
that not only carries the RGB signals, but also the Lum, the power and Audio signals
as well. None of the existing cables in the market actually does that.

None except this one: The SCPH-1160 was a small adapter box from Sony intended to break out
audio and composite video while providing an additional multi-out for additional stuff to
be connected. So all 12 pins of the multi-out and even the shielding ground are connected
through. Even better, the cable itself can be detached from the circuit board to
easily connect some prototyping circuit. With some luck I could find a second hand
part on e-bay.

After some serious board layout work, I was able to squeeze my whole electronics 
into the case of the SCPH-1160, and could even use the original RCA connectors
to now output the YPbPr signal instead of AV. I added a 3.5mm stereo jack to make the
device complete.

## Results

I was playing mainly "CastleVania: Symphony of the Night" to test the setup
and the video and sound quality is very good on my Samsung UE22K5000AK.
This TV seems to have special support for game consoles and handles the 280p signal
(I have a PAL version of the Playstation) very well. The pixels are pretty sharp,
there is no noise in solid color regions and I can not notice any lag whatsoever.
The only bad thing is that the image seems to have a slight flicker of the 
luminance when the game scrolls and the screen is mainly half-bright. I have
not yet figured out if this is a problem of the Lum output of the PS1 or caused by 
my circuit. Nevertheless I am very happy with the image quality now.

