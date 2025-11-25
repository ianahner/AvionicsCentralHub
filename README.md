# Avionics Central Hub

![3D Render](https://github.com/ianahner/AvionicsCentralHub/blob/main/CentralAvionicsHub_3D.jpg)

## Design Goals
This project was designed to solve a number of problems encountered while laying out the electrical wiring for an experimental aircraft. I wanted to accomplish the following:
- Single Point Ground for all panel avionics
- Eliminate as many splices as possible from wiring harness
- Simplify harness design, ideally having only a single harness branch to each device
- Allow for easy future expansion or modification if an individual instrument is changed without having to rework significant portions of the harness

## Component Considerations
My panel consists of the following:
- GRT Horizon 10.1 PFD
- GRT Mini G2 MFD
- Garmin GNX375 GPS/XPDR
- Trig TX56A NavCom
- Small Switch and annunciator panel
- GRT Autopilot

## Physical Footprint
The GRT Horizon 10.1 EFIS includes mounting holes on the rear of the display unit for the GRT SafeFly GPS. As I am not using the SafeFly GPS in my build due to having the Garmin, I have made this board fit the mounting hole pattern of that device. This will allow the board to mount directly to the rear of the PFD. 

The board is slightly larger in outside dimensions than the SafeFly, but the mounting holes are the same. When mounting to the rear of the PFD this is no big deal, but if you are mounting in some other tucked away spot be aware of the outside dimensions. 

In the future I plan to design a simple 3D printed cover for this board. I'll add it to this repo if/when that ever happens.

## Audio Mixing Resistors
This audio mixing solution is of course not intended to be a high fidelity audio solution. The intention here is to mix the mono "annunciator" signals from instruments for messages like "AP Disconnect" or "Minimums." I highly discourage anyone from using this solution for something like radio audio or even non-essential music audio as the results are likely to be less than desirable. For the purposes of mixing alert tones, it should be perfectly acceptable.

The resistors exist simply to prevent one audio device from backfeeding the driver of another device. The value was chosen based on the output impedance of the devices I have, but should be reasonable for the vast majority of situations you're likely to encounter. 

As an aside, though this LOOKS extremely hacky (and it sort of is) it comes straight out of the manual for the PSE certified intercom and others, and is a rather common old-school approach to audio mixing, back before engineering was invented. 

## LED Series Resistor values assumptions
The LED series resistors R1-R5 are optional for use with panel mount LEDs that either don't have a series resistor, or have a voltage range that isn't high enough for the 14.5V our alternators tend to run. 

The resistor specified in the BOM below is a 620Ω which was calculated to provide 20mA to a 2V LED assuming a bus voltage of 14.5V. Adjust this to your needs, or simply install a 0Ω jumper. 

## Why does Fuse F1 exist? 
This fuse does not need to exist at all, and you can jumper it in many cases if you do not like the idea of a fuse in your ground. The purpose of that fuse is rather specific to my application. I intend to ground GND1 (J6) directly to battery negative in my aircraft. My aircraft is a composite pusher configuration with the battery in the nose and the engine on the rear. There is a single very large negative battery lead running the length of the fuselage, and the fuselage being composite is of no use for grounding. 

The intention in this application is to run the secondary fused ground all the way back to the grounding stud where the primary alternator is grounded. This protects against any failure of the main battery negative or of the GND1 connection to the battery. 

I have included the fuse to protect against a very unlikely fault condition where that main ground lead to the rear of the airplane is damaged, or the engine to firewall bonding strap is broken. In that case if a pilot were to attempt to start the aircraft, the starter current could try to go through this board. That would not only blow the traces off the board, but also potentially damage the relatively small #12 or #10 wire used for this redundant ground. 

The fuse should be sized to protect the wire, assumed to be 20-30A. If a ground strap is broken and a pilot tries to start the plane, the fuse will blow. The pilot will also be unable to start the plane, so this should be sign enough to troubleshoot the problem, and then replace the fuse. A fuse is fine here instead of a CB because there is no reasonable situation where this would blow in flight that could be fixed by resetting a CB. 

## BOM for Population
QTY | DK PN | REFs
--- | --- | ---
1 | 36-3568-ND | F1
1 | A35173-ND | J8
5 | A35183-ND | J1, J2, J3, J4, J5
1 | A35186-ND | J9
2 | 63824 | J6, J7
5 | 541-RCP1206W620RFEACT-ND | R1, R2, R3, R4, R5
3 | RMCF0805JT470RCT-ND | R6, R7, R8






