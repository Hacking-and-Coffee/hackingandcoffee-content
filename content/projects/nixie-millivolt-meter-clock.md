---
title: "Nixie MilliVolt Meter Clock"
date: 2016-04-06
draft: true
author_image: 'images/about.jpg'
author: 'hon1nbo'
---

(another from the project archives)

# A Nixie Clock... Meter?
I have been interested in the quirky sides of electronics for as long as I can remember, but I don’t know how Nixies evaded my eye for so long. Only during my first semester of college did I come across them. Such an awesome looking display, the 3D look to it and the glow of a tube-like device. Like many before me, I instantly decided that I needed to make a clock.

The other day, I managed to come across a pile of electronics that were being dispose of and there was something I was looking for: a Nixie Tube based Volt Meter…. er, “Volt meter” is a bit misleading, it’s actually a milliVolt meter. It wouldn’t turn on at first, but a good whack to the tube board fixed that… no joke, it works a lot more often than it should.

Now came the interesting part. I wanted to make a clock out of it, but not ruin the normal functionality. Normally with these projects a voltmeter like this is gutted and replaced with clock innards, or people just take out the tubes and their respective driver boards, but I wanted to be able to use this tool (never know if it’ll come in handy!). So, after a little thought and knowing I had some free time, I came up with this.

Time to Complete: 2 hours for design, construction, and fine-tuning  (3.5 if you count debugging the issue with different power sources for the board as described below)

### Bill of Materials:
- Microcontroller with at least three PWM outputs, more if you need zero-correction control or if you need two pins for properly control minutes. Arduino is a great board for beginners.
- Resistors matched to bring 5V to scale on the meter (while there are parts numbers listed here, please see notes farther down about how to calculate the ideal value and then why those aren’t used).
- A meter to display it on, unless you can see electrons flowing in wires ; )
- 
Full disclosure, the Allied electronics parts list was made because, at the time, I had a sponsorship to write these guides for a Magazine as long as they used their part numbers to purchase supplies.

Allied Electronics Parts List (note the arduino they list is a microchip based kit, rather than a standard Atmel-based that I used):

| StockNumber	| MfrPartNumber |	QtyOrdered |
| -------- | -------- | -- |
| 296-6505 |	OK10G5E |	1 |
| 296-6513 |	OK5115E |	1 |
| 296-6598 |	OK8225E |	1 |
| 383-3815 |	TDGL002 |	1 |
| 437-0408 |	LR1F430R |	1 |

# The Build
This circuit can be built on a breadboard like I did, or you can get a piece of Protoboard

*NOTE: I did not include a zero-correction resistor in the BOM since it was specific for my meter. You can find a suitable value for your equipment, or adjust the zero on the hardware (which will have to be re-adjusted before using to measure voltages, but simple enough)

date of completion of design and testing: 10/21/2011

The clock operates by an Arduino** that keeps the time using the Time library, and outputs variable voltages via four/five (depends on mode) PWM pins. These are maxed out at 5V, and cannot operate at the milliVolt level the meter needs on their own, so I put each output through a Resistor Divider to compensate and tune it in.

With the resistor dividers, the clock time is output as a voltage anywhere from 0-0.0XXXX V where the X’s mark the time. For example, if the time was 12:30, the output voltage would be 0.01230V or 12.30mV

** I have used this same arduino for an absurd number of things, I always can just pop it from one thing to another with a quick reprogram, but I want this running always so I am choosing a barebones uC and an actual RTC to keep things nice and smooth. Heck, I may even remake the circuit with all TTL gates since I am doing nothing better in required-before-taking-anything-else digital logic class right now.

The day I picked up the meter, I went home and did the math for the voltage dividers. After a few tries (due to ADD on my part regarding the scale of the voltages being output, and then again since I switched to the 100mV scale rather than the 1000mV scale to take advantage of the decimal point placement), I had the set of resistors needed. However, some of the values either A could not exist (infinite decimals) or B, were too bizarre. So I rounded them down the closest value that was simple to implement, and then use some tweaking to determine the maximum PWM value to make the maximum output the divider should have, and all clock calculations are done accordingly.

The values *calculated* were as follows:

Vout = Vin*(R2/(R1 + R2)  (this only works for no-load circuits, but that’s Ok for us using a mete which has such a high impedance it is not considered a significant load)

- Common Resistor to Ground for each divider: 1 Ohm (just to keep it simple, and fewer resistors)
- Hours left digit: 449 Ohms –> ~490 Ohms with PWM output mapping
- Hours right digit: 554.5 repeating Ohms –> 550 Ohms with PWM mapping
- Minutes left digit: 8332.3 repeating Ohms –> 8.3 kOhms with PWM mapping
- Minutes right digit: 55554.5 repeating Ohms –> 55kOhms with PWM mapping

However, calculations are great and all but in the end they only give you a ballpark with things like this. You have to fiddle around with what you have, and you may find better results. I found out that I needed first a variable PWM output to compensate the meter which usually is -0.65mV from 0 with no outputs be but varies based on whether or not I use a USB bus for power or 5V adapter so yes, PWM is needed to compensate via software for both situations. I also realized I had enough accuracy in the PWM output for the left minutes digit to control the entire minutes range without issue, except again when on 5V external adapter. I think my board’s regulator may be damaged at the rate in which I keep bringing it up, time to make a new one 

**Here are the resistor values I** ***actually*** **used:**
- Common Resistor to Ground: 1 Ohm
- Hours left digit: 430 Ohms with PWM mapping (the resistor was on hand, and worked better without the 56 Ohm I had to bring it closer to target)*
- Hours right digit: 510 Ohm (resistor was on hand)*
- Minutes both digits: 8.2 kOhm (resistor on hand, and realized that it had enough resolution even when mapped to work as both digits accurately)*
- Zero Correction Pin: a 50 kOhm and a 9.7 kOhm resistor in parallel  to create a 8.124 kOhm*
-- Turns out I didn’t need this, the zero is easy enough to adjust when switching from clock to meter modes

  *I had them on hand, and it worked out (again, trial and error helps as doing math for every possible combination of things is either to much work for the thousands+ combinations, or gives you bizarre results like the calculations showed above

The Arduino Sketch is at the bottom of the page.

The build was done on a breadboard for quick and easy tweaking, and since I wanted to get this working for a demo ASAP (ok, in reality because I’m still deciding on a different uC and will make a proper PCB rather than use perfboard, as I haven’t opened a bottle of Ferric Chloride in, quite literally, years.

Photos: The circuit on the breadboard; the basic schematic; and a photo of everything working

TKTK photos

# Results
The clock worked after a lot of tweaking, but there are still a couple of quirks. First, there are points at which it will be running fast, and others where it is running slow, which is similar to the design of “Lord Vetinari’s Clock” which is meant to drive people mad. This will only drive you mad if you realize the minutes either change too ofter or too little, or if the least significant digit flickers between two values due to the presence of voltages below 0.01mV adding up (which it does… A LOT).

As for general drift, it seems like I am getting quite a bit, but I shouldn’t be losing 9 minutes after an hour! – I have noticed that this old meter performs differently over time, maybe I should just let it run for a while and see how far off the tuning operations are when run. If they have gone off, the meter adjusted from temperature or long term operation. If they are the same, then my clock is drifting or programming wrong. So far my programming has tested right on everything, but I do know that the time library is also meant to grab time from serial. I am probably going to set this thing up with my spare network shield and pull from the universal clock for fun, I’ll check for more drift then.

There also is the occasional value of minutes around 99, this is due to the resolution of the HOURS output, which if I turned it up one notch higher, would put it several mV above ideal. I figured I’d rather have closest to a number rather than only real numbers. (ex: if I set only valid values could be output, then assume the actual time is 2:00. If I output real values only, the error is larger and would show 2:03/4. If I want more accuracy, then at 2:00 it may output 1:99 on some values. I’d rather have this as once it hits 2:01 it just shows up as 2:00 and not as far off. This only happens about every other hour.

There is also a strange issue with the power supply arrangement. When setting up, programming, and tuning I used my computer as a power source for the arduino. When I tried to use a standard 5V adapter, I got a lot of absurd results that I could not successfully tune within the capabilities of my very short attention span. It may be that I damaged the voltage regulator on this board on another project (wouldn’t be the first time I’ve done that). I may evaluate this, but likely not as I want to try some other uCs I haven’t used yet and will build a board around it anyways.

### Future Modifications:

- A trimpot on each voltage divider for finer tuning
- A different uC with a proper time keeping circuit
- Tweak the settings to get the device working properly off of a normal 5V power adapter
- A proper PCB for everything
- Input buttons to control it once it is no longer tethered to a computer, as right now the time is set by reprogramming it since I need the computer anyways.
- A selector to use different voltage dividers so that I can use the circuit on virtually any Voltmeter.
 
### Other Thoughts:

None really, so I’ll post some more photos of the Nixie milliVolt meter:
TKTK photos

# Arduino Sketch
(should work on all versions of the software, made particularly in 0018 since the machine I did this on has an old version since some libraries I use broke and I haven’t fixed them yet).

Please do note, that if you try to make this yourself remember that all the values I have given will need to be tweaked for your setup, as when working in milliVolts things get a little more sensitive, for example I have multiple variable sets: one for power from a computer’s USB port, a set for operating on an external 5V adapter, and another that is needing to be written for operating on a USB Wall Wart.

```
/* Arduino PWN Nixie Voltmeter Clock, by Jimmy Hartnett

This sketch is to output the time in the form of a voltage using PWN,
for example 12:34 = 0.1234V

*/
#include <Time.h>

int HoursA_pin = 11;
int HoursB_pin = 10;
int MinutesA_pin = 9;
int MinutesB_pin = 6;
int zero_correction_pin = 5;

/*
These Values are for when powered by the USB bus (not the USB Power Adapters, the actual computer Bus.. I had discrepancies when testing so that’s why if you’re wondering)
*/

int HoursA_max = 220;            //Tuned? – pretty much
int HoursB_max = 231;            //Tuned? – pretty much in software until a resistor adjustment is made
int MinutesA_max = 239;          //Tuned? – pretty much
int MinutesB_max = 255;          //Tuned? –
int zero_correction_value = 241; //Tuned? – pretty much – !!! This is the Value for use with the USB Bus, not the 5V external adapter (no idea why it matters)
int HoursB_offsets[] = {1,1,2,3,3,4,4,5,6}; // This is for USB Bus Power (NOT USB power adapter) (just my situation, adjust as needed for you)

/*
These Values are for when powered by an external 5V power adapter(not USB power, standard power adapter) I had discrepancies when testing so that’s why if you’re wondering
*/
/*
int HoursA_max = 220;            //Tuned? – pretty much
int HoursB_max = 255;            //Tuned? – pretty much in software until a resistor adjustment is made
int MinutesA_max = 255;          //Tuned? – pretty much
int MinutesB_max = 255;          //Tuned? –
int zero_correction_value = 103; //Tuned? – pretty much, maybe +1 – !!! This is the Value for use with the 5V external adapter (no idea why it matters)
int HoursB_offsets[] = {0,0,0,0,0,0,0,0,0}; // This is for 5V External Adapter (just my situation, your mileage may vary)
*/

void setup()  {

pinMode(HoursA_pin,OUTPUT);
pinMode(HoursB_pin,OUTPUT);
pinMode(MinutesA_pin,OUTPUT);
pinMode(MinutesB_pin,OUTPUT);
pinMode(zero_correction_pin,OUTPUT);
analogWrite(zero_correction_pin,zero_correction_value);

hourFormat12();
setTime(03,51,30,21,10,2011);
}

void loop()  {

//These are to test the max outputs during calibration

// analogWrite(HoursA_pin,HoursA_max);
//analogWrite(HoursB_pin,HoursB_max);
//analogWrite(MinutesA_pin,MinutesA_max);
//analogWrite(MinutesB_pin,MinutesB_max);
//analogWrite(HoursB_pin,(((HoursB_max/9)*9) + HoursB_offsets[(9 – 1)]));

// delay(10000); // just here to comment and uncomment to avoid constantly (un)commenting the big thing below this line

while(true)  {

if (hour() <=9)  {
analogWrite(HoursB_pin,((HoursB_max/9)*hour() + HoursB_offsets[(hour() – 1)]));
}
if (hour() > 9)  {
analogWrite(HoursB_pin,((HoursB_max/9)*(hour() – 10) + HoursB_offsets[(hour() – 10 – 1)]));
}

if (hour() <=9)  {
analogWrite(MinutesA_pin,((MinutesA_max/59) * (minute() /* – 1 */ ))); // the -1 in a comment is if it is needed to account for an occassional 0.01mV discrepancy due to resolutions of output
}
if (hour() > 9)  {
analogWrite(MinutesA_pin,((MinutesA_max/59) * (minute() – 3 /* – 1 */))); // the minute() – 3 is to compensate for the low resolution of the HoursA output, which has a 0.03mV discrepancy and the HoursB 0.01mV discrepancy
}
if (hour() >= 10)  {
analogWrite(HoursA_pin,HoursA_max);
}
else  {
analogWrite(HoursA_pin,0);
}

/*
for (int x = 0; x <= HoursA_max; x += (HoursA_max/12) )  {
int HoursB_counter = 0;
analogWrite(HoursA_pin,x);

for (int y = 0; y <= HoursB_max; y += (HoursB_max/9))  {

analogWrite(HoursB_pin,(y + HoursB_offsets[HoursB_counter]));
HoursB_counter++;

for (int z = 0; z <= MinutesA_max; z += (MinutesA_max/59))  {

analogWrite(MinutesA_pin,z);

delay(1000); // test clock as if it were a stopwatch, good for testing
```
