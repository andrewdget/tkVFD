# pyVFD

**Note: pyVFD is under development**
+ **Core module functionality is in place.**
+ **Not yet added to The Python package Index.**
+ **Currently working on documentation, non-principle features (i.e. adding a built-in clock display function), and testing.**

**Expected project completion date of Feb 2024**

## Overview

The [pyVFD module](https://github.com/andrewdget/pyVFD) allows for the easy implementation of customizable graphical 7-segment and/or 16-segment displays into any [Tkinter](https://docs.python.org/3/library/tkinter.html) application.

The displays generated by pyVFD are styled after Vacuum Flourescent Displays, a beautiful cathodoluminescent predecesor to modern LCD digital/alpha-numeric displays. 

Though pyVFD can also simulate the look of backlit LCD displays. 

## Installation

Install pyVFD with **pip**:

> ```python3 -m pip install --upgrade pip```<br>
> ```python3 -m pip install pyVFD```<br>

## Usage

### 7-Segment Displays

class **```pyVFD.seg7(parent, **kw):```**<br>
Tkitner-compatable 7-Segment VFD/LCD like display that can be used everywhere Tkinter expects a canvas object.

PARAMETERS:<br>
**parent** - Parent Tkinter object.

**width** - Display width in pixles. *Note: If only one display dimension parameter is passed (i.e. width but not height or vice versa) the unspecified dimension parameter is adjusted automatical to preserve default aspect ratio.*


**height** - Display height in pixles. *Note: If only one display dimension parameter is passed (i.e. height but not width or vice versa) the unspecified dimension parameter is adjusted automatical to preserve default aspect ratio.*

**on_color** - The color of the display segments which are "switched on" as expressed as an RGB row vector i.e ```[red, green, blue]``` where each color is represented as a number between 0 and 255 *(default: ```on_color=[204, 246, 250]```)*.

**off_color** - The color of the display segments which are "switched off" as expressed as an RGB row vectore i.e. ```[red, green, blue]``` where each color is represented as a number between 0 and 255 *(default: ```off_color=[59, 56, 56]```)*.

**bg** - Background color of display canvas, accepts all standard Tkinter color inputs, including locally defined standard color names and 4/8/12 bit hexadecimal RGB color formats *(default: ```bg='black'```)*.

**use_DP** - If ```True``` the display will include a decimal point segment *(default: ```use_DP=False```)*.

**use_CC** - If ```True``` the display will include colon segments *(default: ```use_CC=False```)*.

**use_Grid** - If ```False``` the display will not include a visual "grid" making the display look more LCD like *(default: ```use_Grid=True```)*.

***method*** **```.control(switches, **kw)```**<br>
This method is used to directly control which segments of the display are "switched" on or off. *Note: If nither this method or the ```.char()``` method are used the display will exist internally, but it will not be vissible on the screen as the state (i.e. on or off) of the display's segment will be indeterminate.*


PARAMETERS:<br>
**switches** - A row vector with 7 elements, each describing the binary state (i.e. ```1=on```, ```0=off```) of the coresponding segment of the display in alphabetical order from A-G according to the diagram below. *Note: Control over decimal point and/or colon segments is handled seperatly via the parameters below.*

<p align='center'>
	<img src='https://upload.wikimedia.org/wikipedia/commons/e/ed/7_Segment_Display_with_Labeled_Segments.svg' alt='Segment names of a 7-Segment display with an eighth Decimal Point segment.' width='auto' height='200'><sup>[2]</sup>
</p>

**DP<** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the decimal point segment, assuming the decimal point segment was enabled when the display was initialized (i.e. ```pyVFD.seg7(parent, use_DP=True)```).

**CC** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the colon segments, assuming the colon segments were enabled when the display was initialized (i.e. ```pyVFD.seg7(parent, use_CC=True)```.

method **```.char(char, **kw)```**<br>
This method is used to automaticaly display common alpha-numeric characters. Alpha-numeric characters supported by ```.seg7()``` are capital A-Z and 0-9. *Note: 7-Segment displays are best suited for numeral-only displays. For displays required to represent alphabetical characters, 16-Segment display are recomended. (see Background section for more)*

PARAMETERS:<br>
**char** - A single alpha-numeric string character (i.e. ```'A'``` or ```'9'```), see above for supported characters.

**DP** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the decimal point segment, assuming the decimal point segment was enabled when the display was initialized (i.e. ```pyVFD.seg7(parent, use_DP=True)```.

**CC** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the colon segments, assuming the colon segments were enabled when the display was initialized (i.e. ```pyVFD.seg7(parent, use_CC=True)```.
							
method **```.clear()```**<br>
This method resets the state of the display after being set and must be called before either ```.control()``` or ```.char()``` can used again on an existing display.	

### 16-Segment Displays
	
class **```pyVFD.seg16(parent, **kw):```**<br>
Tkitner-compatable 16-Segment VFD/LCD like display that can be used everywhere Tkinter expects a canvas object.
			
PARAMETERS:<br>
**parent** - Parent Tkinter object.
					
**width** - Display width in pixles. *Note: If only one display dimension parameter is passed (i.e. width but not height or vice versa) the unspecified dimension parameter is adjusted automatical to preserve default aspect ratio.*
					
**height** - Display height in pixles. *Note: If only one display dimension parameter is passed (i.e. height but not width or vice versa) the unspecified dimension parameter is adjusted automatical to preserve default aspect ratio.*
					
**on_color** - The color of the display segments which are "switched on" as expressed as an RGB row vector i.e ```[red, green, blue]``` where each color is represented as a number between 0 and 255 *(default: ```on_color=[204, 246, 250]```).*
					
**off_color** - The color of the display segments which are "switched off" as expressed as an RGB row vectore i.e. ```[red, green, blue]``` where each color is represented as a number between 0 and 255 *(default: ```off_color=[59, 56, 56]```).*

**bg** - Background color of display canvas, accepts all standard Tkinter color inputs, including locally defined standard color names and 4/8/12 bit hexadecimal RGB color formats*(default: ```bg='black'```).*

**use_DP** - If ```True``` the display will include a decimal point segment *(default: ```use_DP=False```).*

**use_CC** - If ```True``` the display will include colon segments *(default: ```use_CC=False```).*

**use_Grid** - If ```False``` the display will not include a visual "grid" making the display look more LCD like *(default: ```use_Grid=True```).*

Example:
					
method **```.control(switches, **kw)```**<br>
This method is used to directly control which segments of the display are "switched" on or off. *Note: If nither this method or the ```.char()``` method are used the display will exist internally, but it will not be vissible on the screen as the state (i.e. on or off) of the display's segment will be indeterminate.*
					
PARAMETERS:<br>
**switches** - A row vector with 16 elements, each describing the binary state (i.e. ```1=on```, ```0=off```) of the coresponding segment of the display in alphabetical order from A-M (and applicable sub-segments) according to the diagram below. *Note: Control over decimal point and/or colon segments is handled seperatly via the parameters below.*

<p align='center'>
	<img src='https://upload.wikimedia.org/wikipedia/commons/9/95/16-segmente.png' alt='Segment names of a 16-Segment display with a seventeenth Decimal Point Segment.' width='auto' height='200'> <sup>[3]</sup>
</p>
							
**DP** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the decimal point segment, assuming the decimal point segment was enabled when the display was initialized (i.e. ```pyVFD.seg16(parent, use_DP=True)```).

**CC** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the colon segments, assuming the colon segments were enabled when the display was initialized (i.e. ```pyVFD.seg16(parent, use_CC=True)```.
							
method **```.char(char, **kw)```**<br>
This method is used to automaticaly display alpha-numeric characters. Alpha-numeric characters supported by ```.seg16()``` are A-Z (capital and lower-case) and 0-9 (see Background section for more).
					
PARAMETERS:
**char** - A single alpha-numeric string character (i.e. ```'A'``` or ```'9'```), see above for supported characters.
							
**DP** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the decimal point segment, assuming the decimal point segment was enabled when the display was initialized (i.e. ```pyVFD.seg16(parent, use_DP=True)```).
							
**CC** - Sets the binary state (i.e. ```1=on```, ```0=off```) of the colon segments, assuming the colon segments were enabled when the display was initialized (i.e. ```pyVFD.seg16(parent, use_CC=True)```.

method **```.clear()```**<br>
This method resets the state of the display after being set and must be called before either ```.control()``` or ```.char()``` can used again on an existing display.	

## Sample/Example

## Background

A Vacuum Fluorescent Display (VFD) is a analog-digital display device once commonly used in consumer electronics.

<p align='center'>
	<img src='https://upload.wikimedia.org/wikipedia/commons/d/d3/Vacuum_fluorescent_2.jpg' alt='Close-up example of a VFD.' width='auto' height='300'><sup>[1]</sup>
</p>

VFDs function in a similar fashion to the Liquid Crystal Display (LCD), more common today, however they operate on the principle of cathodoluminescense. Each tube in a VFD has a mesh control grid and phosphor-coated carbon anode that is bombarded by electrons emitted from a cathod filament. 

This allows VFDs to natively emit a very bright light with high contrast and can support displays with mutliple elments of various colors. <sup>[1]</sup>

VFDs, like LCDs, primarily come in two varietes:

- **seven-segment (7-Segment) displays;** Best suited for numeral only displays (such as a digital clock). It is possible for displays of this type to represent alphabetical characters but the clarity/unambiguity is generaly poor as a result of the available segment geometries (for example the letter "Y") and it is not possible to differentiate between capitol/lower case characters. For purposes where these limitations are prohibitive, 16-Segment displays offer a solution. <sup>[2]</sup>

<p align='center'>
	<img src='https://upload.wikimedia.org/wikipedia/commons/e/ed/7_Segment_Display_with_Labeled_Segments.svg' alt='Segment names of a 7-Segment display with an eighth Decimal Point segment.' width='auto' height='200'><sup>[2]</sup>
</p>


- **sixteen-segment (16-Segment) displays;** Operate on the same principle as 7-segment displays but incorporate additonal segments allowing for clear representation of more complex characters including alpha-numeric characters/symbols. <sup>[3]</sup>

<p align='center'>
	<img src='https://upload.wikimedia.org/wikipedia/commons/9/95/16-segmente.png' alt='Segment names of a 16-Segment display with a seventeenth Decimal Point Segment.' width='auto' height='200'> <sup>[3]</sup>
</p>

## References

[1] https://en.wikipedia.org/wiki/Vacuum_fluorescent_display<br>
[2] https://en.wikipedia.org/wiki/Seven-segment_display<br>
[3] https://en.wikipedia.org/wiki/Sixteen-segment_display<br>