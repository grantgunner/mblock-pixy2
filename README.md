# mblock-pixy2

## Overview

This package is an extension for mBlock that provides support for the Pixy2 camera.
mBlock is a graphical programming tool based on Scratch which simplifies coding for
Makeblock products as well as other Arduino-based boards
(I have used with a Makeblock mBot and a basic Arduino Uno).

Note: mBlock uses the term "blocks" to refer to the graphical programming blocks used in the Scratch-based interface but Pixy2 also uses the term "blocks" to refer to objects it detects. To avoid confusion, I will use the term "mBlock blocks" for mBlock and use just "blocks" for Pixy2 detected objects.

The mBlock blocks added by this extension map somewhat closely to the Pixy2 API. I have included basic details below but have not tried to rewrite the Pixy2 API documentation. Please refer to the following links for more detailed information on the Pixy2 API that this accesses:

* https://docs.pixycam.com/wiki/doku.php?id=wiki:v2:general_api
* https://docs.pixycam.com/wiki/doku.php?id=wiki:v2:ccc_api

Note: I have only added the main functions I was interested in so not everything is available. Let me know if you would like something added or have a go at adding yourself.

## get blocks

Arduino code: pixy.ccc.getBlocks()

*Parameters:*
* wait (default = true)
* sigmap (default = 255)
* maxblocks (default = 255)

Notes:
* the parameters are all optional in the API but I included them in the mBlock block. The default values are pre-populated so it is easy to get the default behaviour.
* if you look at the Arduino code generated, numeric parameters are casted to the datatype used by the API. Scratch does not have explicit datatyping so if this was not done, errors could result depending on how a parameter in passed in.

*Returns:*
* count of blocks detected

Note: the API also has a numBlocks member variable but I have not implemented an mBlock block for this. I thought that getting this from the getBlocks call was sufficient.

*Description:*

This function gets all detected blocks in the most recent frame. Along with returning the count,
it populates data in an array for access in the next mBlock block.

## get block {variable}

Arduino code: pixy.ccc.blocks[*blocknum*].{variable} e.g. pixy.ccc.blocks[0].m_signature

*Parameters:*
* blocknum - the number of the block you wish to inspect. Block numbering starts at zero i.e. if there are 4 blocks, they will be numbered 0, 1, 2 and 3.

*Variables:*
* signature (Arduino: m_signature)
* x pos (Arduino: m_x)
* y pos (Arduino: m_y)
* width (Arduino: m_width)
* height (Arduino: m_height)
* angle (Arduino: m_angle)
* index (Arduino: m_index)
* age (Arduino: m_age)

*Description:*
Returns the specified attribute for a given block retrieved in the most recent getBlocks() call.

## print block

Arduino code: pixy.ccc.blocks[*blocknum*].print()

*Parameters:*
* blocknum - the number of the block you wish to inspect.

*Description:*
Prints a summary of block variables to the console for debug purposes.

## set lamp

Arduino code: pixy.setLamp()

*Parameters:*
* Top - on/off - controls the top two white LEDs
* Bottom - on/off - controls the lower RGB LED (set to maximum for all colour channels to provide white light)

*Description:*
Turns on/off Pixy2's integrated light source.

## set LED

Arduino code: pixy.setLED()

*Parameters:*
* Red component (0-255)
* Green component (0-255)
* Blue component (0-255)

*Description:*
Sets the colour to be shown on the Pixy2 RGB LED.

## set servos

Arduino code: pixy.setServos()

*Parameters:*
* pan position (0-1000)
* tilt position (0-1000)

*Description:*
Control the servo positions of the pan/tilt kit.
(Sorry but I haven't tested this out much so not entirely sure if it is working correctly in terms of positions)
