
# Project 1 README

  

Student: Dunh Adam Lee (921476881)

  

## Project Status

All circuits are complete.

## Compare
This circuit accepts two 3-bit digits, X and Y, as inputs and outputs if X = Y and X < Y.

#### Equality

To make an equality circuit for the inputs, we can check whether each of their respective bits are equal with an XNOR gate, then we AND the result of all the XNOR gates to see if all of the bits are equal. 

The boolean expression for equality looks like this:

(X2 XNOR Y2) AND (X1 XNOR Y1) AND (X0 XNOR Y0)

#### X < Y

To determine if X < Y, we can check the MSBs, X2 and Y2. if X2 is 0 and Y2 is 1, then X < Y is true, otherwise false. However, if both of the MSBs are equal, then the next significant bits, X1 and Y1, need to be checked with the same logic as the MSBs, that is, return true if X1 = 0 and Y1 = 1. 

Since checking the next bits rely on the MSB of X and Y to be equal, there needs to be an XNOR gate for X1 and Y1 ANDed with the result of X1 and Y1. If X1 and Y1 are equal, we extend this logic to the LSB, which relies on both X2 and Y2 to be equal, and X1 and Y1 to be equal in order to determine if X < Y. 

Therefore, our equation for X < Y is expressed as:
(&not; X2 AND Y2) OR ((X2 XNOR Y2) AND (&not; X1 AND Y1)) OR ((X2 XNOR Y2) AND (X1 XNOR Y1) AND (&not; X0 AND Y0))

## Gray Code
In this part, we convert the binary input into the gray code that corresponds with the last digit of our SSID. Mine is 1 so I'll focus on column 1. We have four inputs B3, B2, B1, and B0 and we have four outputs G3, G2, G1, G0. We can find a relation between the inputs and outputs, but we don't know exactly what that relation is. 
<br/>
To find a relation, we'll use a K-map to map every bit in the input to a bit in the output. Meaning, we will have 4 K-maps for each bit in the output to find the expressions that can convert 4-bit binary to gray code.
<br/>
<br/>
The K-maps and boolean expressions are shown below:

<img src="kmaps/2.png" alt="G3 and G2 K-map" width="400"/>
<img src="kmaps/1.png" alt="G2 and G1 K-map" width="400"/>
<img src="kmaps/0.png" alt="Boolean Expressions" width="400"/>

Using these boolean expressions, I'm able to build circuits that convert 4-bit binary into gray code.
## Seven-Segment Display

  For the seven-segment display, the truth tables for digits 0-4 and 5-9 are the same and only differ by the Z input. So, my process was to make a truth table for digits 0-4 for only the vertical line inputs.  Once the Boolean equations for the vertical line inputs are obtained, a number from 0-4 will be displayed if Z is off or a number from 5-9 will be displayed if Z is on.
<br/>
There is an OR gate connected to each output A-G to be able to handle multiple possible inputs.
<br/>
### Determining display
It made sense to determine the digits in pairs since the respective digits from 0-4 and 5-9 share the same amount of vertical lines. The process:
* Use the amount of vertical lines for digits 0-4 to make a truth table for each of them. 

* Use the truth table to obtain a Boolean expression for the vertical line inputs. Digit pairs (0,5), (1,6), .., and so on, share the same vertical line Boolean expressions. Simplify the expression if possible.
* If the same expression appears multiple times, then reuse its circuit.
* For each digit pair, AND the Boolean expression for vertical lines with &not;Z if it is a digit from 0-4, or Z if the digit is 5-9, to determine which digit from the pair to display based on if Z is off or on.
*  Determine which output segments are required to display each digit by looking at what's given.
* Connect the output of each digit's circuit to the output segments required for the digit to be displayed

#### Walkthrough process for digits 0 and 5
Digits 0 and 5 have no vertical lines.
When 0 is displayed, segments [A, B, C, D, E, F] are on.
When 5 is displayed, segments [A, C, D, F, G] are on.

The vertical line inputs for 0 and 5 are expressed as this Boolean equation:  
ZERO_FIVE = \(&not; V &and; &not; W &and; &not; X &and; &not; Y)

Here, we make a NOR gate for all the vertical lines because 0 or 5 is displayed when all the vertical lines are off.
<br/>
<br/>
To determine if 0 or 5 is displayed, I used two separate AND gates to check if Z was on or off.
<br/>
0 is displayed when Z is off and ZERO_FIVE is true, so we want to AND &not; Z with the ZERO_FIVE equation. 
<br/>
<br/>
The equation for 0 is:
ZERO = ZERO_FIVE &and; &not; Z
<br/>
<br/>
5 is displayed when Z is on, so we AND Z with ZERO_FIVE. 
<br/>
The equation for 5 is: 
<br/>
FIVE = ZERO_FIVE &and;  Z
<br/>
<br/>
The following digit pairs: (1,6), (2,7), (3,8), (4,9) follow the same process as above. 
