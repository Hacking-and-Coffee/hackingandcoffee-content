---
title: "Underwater Remote Operated Vehicle Project"
date: 2011-01-01
draft: false
author_image: 'images/about.jpg'
author: 'hon1nbo'
---

A Remote Operated Vehicle, or an ROV for short, is any vehicle that is remotely controlled. This term, however, generally applies to remotely operated underwater vehicles, and that is precisely what this project is. My goal was (and in a sense still is) to create an ROV with live cameras, room for expandability, internet control, full maneuverability, and a true variable ballast buoyancy control system (similar to what Submarines and SCUBA divers use, rather than make a neutral system and use props which is boring).

This project was undertaken as a project during my time in high school, and is something I intended to pick back up at a later date. With SBCs and hobby level PLCs becoming ubiquitous, I think this can be done quite well should I try it again. This is here to show what was feasible on a shoestring budget in 2010, with zero machine shop access and a single studcent working on it. I even got it controlled over the internet from an iphone with a live camera feed by the time I was done. Honestly, I'm proud of that for the time it was.

The below is the report I presented to my high school senior project advisor, who coincidentally worked on a submarine for years so maybe it was fitting or maybe it was terrifying. This much time later, I can hardly remember.

# Introduction
The goal of this project is to make a Remote Operated underwater Vehicle (commonly referred to as an ROV). This ROV will have live cameras, full maneuverability, and full control from an electronic control device on the surface. The applications are very diverse, from an educational venture to an underwater camera rig for film (both entertainment and research filming), to a rig capable of operating tools underwater too long for technical scuba diving. The unit, measuring at 45x20x22 inches, is large enough to support cameras and other items, yet small enough to fit in the back of a large SUV. The ROV has a few main components: the **Control Interface**, the **ROV Main Body**, the **ROV-to-Surface Tether**, and the **ROV Electronics**. All descriptions before the full work documentation are of the current system, for older design refer to the work log itself farther down the page

# The Control Interface
The controls can be incorporated into any electronic device capable of operating over a standard WiFi or Ethernet network, such as a laptop or, for experimental purposes, a Cell Phone. All control is done using a web browser such as Internet Explorer or Firefox. Firefox is my preference because it is easier to customize, and I can use GreaseMonkey to help modify my control web page to make things easier on the ROV web server. These controls allow propulsion in all three dimensions and control over any other apparatuses that may be attached as accessories to the ROV as well as display a live video feed from the mounted cameras. A custom program for a laptop will eventually be written using Visual Basic for simplicity, but at this point in time a standard iPod Touch has done wonders controlling the ROV over a WiFi connection using the web browser. Also, by using a Sony PSP (PlayStation Portable) to view the live video feed also via a wireless connection, it is possible to have all of the controls fit inside one’s pocket and even control the unit from anywhere in the world over the internet, the only downside to this is that the live camera feed over the internet would have a potentially low refresh rate when long distances are involved. If a laptop is used as the control interface, it can have real time control and two live camera feeds on display simultaneously.

# The Main Body
The hull is a surprisingly tricky and important part of the ROV. Not only does it have to provide structural support for all of the parts, but it also has to be waterproof at depth for extended periods of time while allowing the ability to service the components in the field. Also, counter to intuition, it must be very heavy. Why must it be heavy? With the volume inside the hull, the air per unit volume weighs much less than any water per unit volume, and therefore it adds a significant amount of buoyancy. This must be counteracted in two ways: add weight to the hull, and consume air volume with either a smaller hull or heavier objects which take up free space. My design has multiple considerations: I have an open frame of PVC tubing surrounding the hull reducing buoyancy and making resistance to movement decrease as well as making mounting and removing components easier, I have a double hull for all of the electronics, such that if the primary hull is breached, the secondary hull will hold off until the unit can surface (the double hull also takes up extra internal volume, thus reducing buoyancy); there are two sets of Electrical feed through that keep water out of the electrical wiring and out of the hull by using modular waterproof electrical connectors, each supporting up to two devices, and a fixed and sealed connection between the hulls. The hulls also use a lid opening such that it is easy to open and modify the interior yet the latches provide enough force on the seal to operate at depth. Inside the double hull system, the electronics take up a large amount of room and add weight, reducing buoyancy. After all of this, it still has a lot of room for improvement. The current design uses Pelican Cases as the primary and secondary hulls, specifically a 1600 and a 1520 respectively. These will not tolerate at depth greater than a few feet alone, but by using a double hull system and by adding some modifications, I believe I can make these handle much deeper waters possibly up to 50 feet after factoring in possible problems. Also, with my current design, there is still enough air volume on the inside to require more than 75 pounds of Static Ballast to sink the ROV, without the Buoyancy Control attached which might drop off a few pounds. The final issue I will address in the future is the polycarbonate mounting sheet I used to mount the pelican cases and propulsion. It is only 1/8 Inch and there is only PVC crossbeam underneath it to aid the two horizontal supports on the edges. I will likely both increase the thickness and add in more cross supports in the revised framework I am building

# The Tether
Another seemingly unimportant, but very critical, component of the system is the usage of a tether extending from the ROV to the surface, where it is either terminated at a computer or a Networking Device for WiFi or internet control. The most common misconception is that a wireless control would be better in almost all ways. Well, it is not and in fact it is much worse and, potentially, dangerous! Before I explain the benefits of a tether, let me explain why wireless is a bad idea as I cam commonly questioned on this matter by everyone I discuss this project with. First off, even though I am licensed by the FCC (Federal Communications Commission) to build and modify my own transmitters including devices for Radio Control (R/C), the frequencies at which data communication operates with high performance cannot penetrate water without an absurd amount of transmitting power. I may be licensed for up to 1.5 kW of transmitter power, but it is impractical to use that much and problematic. The frequencies which can penetrate water more readily, some of which I am licensed to use, are impractical for several reasons. First, the antennas at these frequencies are very large, some of them several hundred feet long wires. Ok, lets assume I was willing to wire across the surface of the water. Then, the wire would have to remain stable, the insulation on the wire has to be constantly maintained due to corrosion from salt water etc, otherwise a deadly amount of electricity could go into the water, and destroy the transmitter. Now, lets assume that this could be managed and I assure you it can with care, but it removes all practicality from the ROV after adding a significant amount of work. At these frequencies, data transmission rates are relatively slow, and this would make the live video feed near impossible. Also, this would allow for possible interference from other transmitters in the world operating on these frequencies. Where in the world? All over because these frequencies have a high rate of propagation, and will travel for hundreds of miles. On top of all of these drawbacks, if the ROV fails there is no means to surface it without either sending down another one or risking a diver. When a tether is used, it counters all of these drawbacks and adds several features. It allows for a very high, real-time data stream in both directions; it gives a means to retrieve the ROV in case of a failure by using a winch attached to the tether; it doesn’t consume a large mount of power; it can be made impervious to interference; it is actually cheaper than the transmitters required for wireless; and it is easier to maintain and operate. The tether on this ROV is comprised of two things; a standard SC Fiber Optic Cable, and a Vinyl Sheath to protect the fiber optics from being torn at. When I get the chance, I will also add in a steel cable to make retrieving the ROV easier once deeper waters are involved. The Fiber Optic Cable has advantages over using copper: it is thinner, lighter, does not carry an electrical current, and can run very long distances without need for an amplifier. With low grade “multi-mode” SC cable, my Fiber Media Converters can support up to a full mile of cable. There also are a few plumbers pipe insulation pieces spread around the tether to add a slightly positive buoyancy. The tether only dives when the ROV dives, thus drag is reduced because the minimum amount of tether is underwater.

# The ROV Electronics
The last main components are the Electronics on the ROV end. These electronics take a command from the surface, and actuate the mechanics of the ROV. There are a few subsections here: the Power Supply, CPU, Network Control, Power Switching, Propulsion, Buoyancy Control, Water Leak Detectors, and the A/V System.

The Power Supply is composed of two batteries, a 12 Volt 3.4 Ah Sealed Lead Acid (SLA) battery for the main electronics and propulsion, and a set of 8 AA batteries which are temporarily providing 12V for the Buoyancy control circuit until a second SLA is purchased. AA batteries are not very suitable for such an application, but for pure testing purposes they have done just fine. The buoyancy control unit needs a dedicated power supply for the time being due to the current failsafe method described later on. The primary battery, the SLA, provides 12V to the CPU, A/V system, and the Power Drive Circuit which require 12V, and by using a regulator in parallel with the other devices it also supplies 5V to the Fiber Optic Media Converter and, once the video system is fully installed, 9V to the Ethernet Switch. This SLA battery will be instead used for Buoyancy Control once another, higher capacity, battery has been purchased. All power supply batteries and regulators, as well as the main power switch and fuse, are in an isolated compartment made from a standard Otterbox, which is also waterproof for extra security. This is good in case any battery decides it doesn’t want to live anymore and explodes due to a short or other freak occurrence.

The CPU is an Arduino Diecimilla using an ATMEGA168 chip running at 16 MHz. The programming is a combination of my code, and the Inventgeek Ethernet Outlet code which I used as a tutorial for Arduino Ethernet control, which this is my first ever project using. The Arduino runs an HTTP web server using a purchased ethernet shield (the official design) and this ethernet shield is connected via a small CAT5 patch cable to the Fiber Optic Media Converter to communicate over the tether to the surface. When the A/V system is fully operational, all three networked devices will be connected via a standard ethernet switch. The arduino is controlled via a web browser of a simply homemade program which can send an HTTP request. Rather than have the arduino web page have several buttons, I am instead using the URL to control the unit as I can just bookmark the controls, operate on low power internet devices such as a cell phone, and it frees up programming space for future expansion. Even if I wanted the buttons, I got errors I could not resolve when I tried to add more than one button. The arduino has 4 of the 14 digital I/O pins reserved for the ethernet shield, six digital I/O pins reserved for propulsion and buoyancy control, and one pin is being reserved for a Parallax Ping Ultrasonic Range Finder. This leaves few I/O pins unless I use shift registers, but I plan to upgrade the arduino to a Dual Core Design I have used in the past, in which two arduinos communicate via I2C, or possibly to an Arduino Mega. The CPU is located in a dedicated Otterbox along with the Fiber Optic Media Converter to keep it isolated in case of a hull failure or another unforeseen event.

The Network Control is handled the arduino ethernet shield operating in cooperation with a ConnectGear Fiber Optic Media Converter, which converts a standard CAT5 connection to a SC fiber optic connection. To the arduino and any other networked devices, it doesn’t even appear to be there. When the video system is fully installed, it will also share the fiber media converter with the Arduino on a micro-sized five port ethernet switch. All devices are accessible via standard networking protocols, and allows the addition of axillary ethernet controlled devices such as a secondary CPU, additional networked cameras, and other accessories.

The Power Switching Circuit takes the signal from the CPU and drives the higher voltage/current devices, such as the propulsion, buoyancy control, and other miscellaneous components. The circuit uses Optoisolators to protect the CPU from a voltage spike which can easily occur with motors and solenoids, and also make it easier to prevent ground loops from forming which could cause a power surge or other form of interruption interfering with CPU operations. The optoisolators in turn drive NPN power transistors which are mounted to a piece of Copper Clad Board which acts as a 12V bus line and as a basic heat sink. I should not need a more proper heat sink for a while, as the transistors are operating far below their capacity and non-continuously.

Propulsion for the ROV is provided with submersible Rule non-automatic Bilge Pumps. These act similar to the Impeller on a jet ski, providing a flow of water out of a nozzle which provides thrust. This keeps the moving parts contained, and less likely to become jammed. However, even though they need less maintenance they need more diligent work when there is a problem. Also, when I make the move to a Propeller Design which offers higher efficiency, I can use the waterproof motors from these pumps to drive the propellers. For forward propulsion, a 1100 Gallon Per Hour (GPH) pump is used mounted aft. For turning, two 500 GPH pumps are used mounted forward on both sides. Reverse propulsion is currently not installed due to cost considerations, but the electronics and electrical connections are there for when I get another pump. A nice feature about this propulsion system is that it has a rather low Impulse (change in force per unit time), allowing for rather smooth movement ideal for a camera system.

The Buoyancy Control for the ROV is currently handles by a modified Scuba Diver Buoyancy Compensator Device (BCD). A BCD works by having a large flexible, though not necessarily elastic, bag which stores air and increases in volume to gain a positive buoyancy. To reduce buoyancy, the air is allowed to escape and thus decrease the bag volume. The BCD I am using supports up to a 45 pound shift in buoyancy. The static ballast is set to have the ROV retain negative (sinking) buoyancy naturally, and when the BCD is half inflated it becomes neutrally buoyant (hovers neither sinking nor Surfacing). When the BCD is fully inflated the ROV becomes positively buoyant and it surfaces. To control the BCD electronically, I have installed Solenoids to actuate the rubber seals on the air intake and air dump valves. This has proven problematic as it is very hard to dial in the spring strength such that the high air pressure from the air tank and BCD do not crack open the valves. Currently, until I can acquire parts for a more efficient and conservative buoyancy control unit, I am letting air seep into the BCD and programmed the electronics to either keep the air dump valve open or open it frequently so that there is never enough air at one given time to have positive buoyancy until either I close the valve via controls, or the air tank loses enough air such that it becomes buoyant itself such that the ROV will surface (yes, when an aluminum Scuba tank drops below a certain amount of air pressure it becomes buoyant. Steel tanks exhibit this behavior as well, but do not necessarily overcome their heavier weight with the added buoyancy). This also is beneficial for the time being because if the electronics fail or the battery dies the ROV will naturally surface because the dump valve will automatically close. This is also why the buoyancy control has a dedicated battery: it runs constantly until I can get proper electric air valves rated for at least 150 PSI.

The Water Leak Detectors are ready to install, but have not been yet due to time constraints getting this project ready for a school grade. However, I will document them as if they were installed because the design will not change and they are next on the list of to-do’s. There are multiple detectors: in between the primary and secondary hulls, inside the main electronics compartment, and inside the camera enclosures. The water sensors are just about as basic as it gets: two electrodes, one connected to a positive voltage and the other connected to a pin on the CPU and separated by a non-conductive gap. When water bridges this gap the voltage is registered by the CPU and measures are taken to protect the hardware. The CPU will warn the operator and start to surface automatically unless the operator overrides the alert (and yes, there are times when I might want to do that). To make the water sensors more reliable, I am etching a zig-zag pattern onto a large PCB and placing them in various locations in the different compartments based on these considerations: where water will possibly enter, where the water will collect, and where the water can do damage. The primary water sensors, for the hull and electronics, will be on the same CPU input. However, the other ones will be dedicated for aforementioned reason of intentionally allowing the water to come in (test coatings on circuits, experimental, etc).

The A/V System has yet to be installed, but as with a few other subsystems it is ready to install once I have time. It is comprised of two live cameras, one reserved for piloting the ROV and the other as an auxiliary camera for different angles or a higher quality camera for film use. The pilot camera is a basic miniature camera that I use because it is only $10, so if it fries it is easy to replace. The video feeds from the cameras are standard composite, though with a slight change in hardware I can support HD or Ethernet Network cameras. The composite feed goes to a Sony Location Free video system which supports two A/V devices and sends the video stream over a network. This is similar the the more well-known SlingBox, but cheaper and it supports the PSP allowing for more compact display and control for certain applications. The location free unit also can use IR sensors to control the A/V devices, and I could use this as an alternate method of sending commands in case of a CPU failure or for controlling auxiliary devices such as audio systems, or even the cameras themselves. I am also considering using the audio signal from the pilot camera to perform sonar operations if the parallax Ping does not perform well in this situation, but this remains to be seen.

# The Build Progress
The design was conceived just before Spring Break in March of 2010 and I ordered the first components. The ROV in its basic form and functionality was due to my school as of May 3, 2010. This project will be continued for a long time, as I can mix various forms of electronic skills, science, experiments, research, and fun into this project.

Listed below are the components I started out with, including the items discarded from the design and excluding the second design items until farther in the work log. All progress is in Chronological Order unless otherwise noted and rather than make an individual entry for every step, progress was lumped into several day periods of similar or rapid work.

——————————————————————————-

TKTK setup new gallery for photos on new website

### April 18, 2010
I started building the Power Drive Circuit for the electronics board and I installed and sealed the wiring between the CPU Otterbox and the rest of the board. I used TIP101 transistors which I have used for countless applications without issue. However, I think part of the reason I never had issue is that I never had many connections close together as usually I just need one for a small circuit that isn’t as sensitive as this. Needless to say, after building and doing a basic test of this board it was obvious that I needed to just get some standard NPN Transistors, but I decided to finish the rest of the surrounding board to avoid putting off the rest of the work. One thing this part of the build taught me is that Rainbow Ribbon Wire is Awesome! – Especially when breaking out of ribbon wire is needed and a large number of wires are present, I may be using a dip connector on one end but I have to be able to tap directly into the wires in the future.

The CPU Otterbox with wiring installed. As it turns out I later noticed at the end of the build that I skipped a pin on the Arduino, but that pin was not used until final testing so I never noticed!

### April 20, 2010
I rebuilt the Power Switching Circuit, and used a fresh piece of green Protoboard which turned out to be a death sentence for two day’s worth of work (under the laquer was a complete 2d matrix of tracelines nearly invisible with laquer to the naked eye. Fried everything). The board was supposed to just be solder pads for each hole with no traces. I also installed Terminal Blocks for the connections to the pumps etc so that when I remove the board from the ammo case I can take the board away from the case as I work at a desk and just make general maintenance and testing easier. I also mounted a fuse holder and a three position key Switch (on-off-on) onto the Power Supply Otterbox. Why a key switch? With a key switch, because it is made for security it is very difficult for it to be affected by jerking, motion, and so forth. Also, it has a very low profile, and it keeps me from rapidly turning anything on without thinking (which has happened in the past). I have not yet installed another power switch to use between the time of activating the key and loading the electronics into the case, but that was a bonus feature I didn’t care about then but do need to add in the future.

### April 22, 2010
I started testing my water seals with the newly installed third waterproof electrical connector and the PVC Compression Fitting. To install these I used tin snips to help widen the hole as the spoon drill method took over an hour a hole. As it turns out, these seals did not want to hold at all. The holes were slightly irregular and deformed such that making the proper seal was very difficult, especially due to the difficulty in shaping the steel of the ammo case.

Therefore, I decided to move on and use a couple of Pelican Cases.  Two of them are nested like russian dolls, a 1600 and a 1520. This was done to help with the pressure over a large pelican case, and to help mitigate the fact I had an upcoming deadline with little time to acquire new parts. The larger 1600 will be kept for this job, while the inner 1520 is used in such a way that I can still use it for other things. I also mounted the 1100 GPH bilge pump for forward propulsion. I also acquired a BCD from a local scuba shop for cheap, so I will be modifying that for Buoyancy Control .

### April 26, 2010
I started testing out my Arduino Code, but had problems making the connection between the arduino and the computer stable. It would work, then it wouldn’t work and was very unpredictable. I then pulled out an old router and set the Arduino gateway to the router to see if things would become smoother, and they did. Plus, with the addition of this router I gained WiFi control over the unit. I even got the iPod touch control working within minutes of adding the router. The next issue was adding more than one button to the arduino web page. I have never used the arduino ethernet shield before this project, so forgive me if it is something obvious that I am missing. What I ended up doing is having one button (for show) and controlling everything with the URL commands. Here is the Arduino code (with old additions of code commented out, but left for historical purposes):

***NOTICE: This code has been reported to not compile under the new versions of the Arduino IDE.***

```
#include <WString.h>

#include <Ethernet.h>

// This code was modified from the Network Outlet code available from InventGeek to suit an ROV Program

// I modified this code because I used it as a basic tutorial for Arduino Ethernet coding

byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED }; //physical mac address

byte ip[] = { 192, 168, 1, 110 }; // ip in lan

byte gateway[] = { 192, 168, 1, 1 }; // internet access via router

byte subnet[] = { 255, 255, 255, 0 }; //subnet mask

Server server(80); //server port

//int speakerPin = 13; // speaker connected to digital pin 9

//int ledPin = 1; // LED pin

int ballastfloodpin = 4;

int ballastdrainpin = 2;

int rightbilge = 3;

int leftbilge = 5;

int reversebilge = 7;

int forwardbilge = 9;

//int inputPin3 = 3; // choose the input pin (for a pushbutton)

int val = 0; // variable for reading the pin status

boolean LEDON = false; //LED status flag

String readString = String(30); //string for fetching data from address

void setup(){

Ethernet.begin(mac, ip, gateway, subnet);

// pinMode(ledPin, OUTPUT);

// pinMode(inputPin3, INPUT); // declare pushbutton as input

pinMode(ballastfloodpin, OUTPUT);

pinMode(ballastdrainpin, OUTPUT);

pinMode(rightbilge, OUTPUT);

pinMode(leftbilge, OUTPUT);

pinMode(reversebilge, OUTPUT);

pinMode(forwardbilge, OUTPUT);

digitalWrite(ballastfloodpin, LOW);

digitalWrite(ballastdrainpin, LOW);

digitalWrite(rightbilge, LOW);

digitalWrite(leftbilge, LOW);

digitalWrite(reversebilge, LOW);

digitalWrite(forwardbilge, LOW);

Serial.begin(9600);

// pinMode(speakerPin, OUTPUT); // sets the speakerPin to be an output

}

void loop(){

Client client = server.available();

if (client) {

while (client.connected()) {

if (client.available()) {

char c = client.read();

if (readString.length() < 30)

{

readString.append(c); //store characters to string

}

if (c == '\n') { //if HTTP request has ended

// ledstatus(); //LED Status Sub

//htmlcontent(); //LED Html Content Sub

floodstatus();

drainstatus();

rightstatus();

leftstatus();

reversestatus();

forwardstatus();

// htmlcontent(); //LED Html Content Sub

readString=""; //clearing string for next read

client.stop(); //stopping client

delay(100);

}

}

}

}

}

void htmlcontent(){

Client client = server.available();

client.println("HTTP/1.1 200 OK"); // now output HTML data starting with standart header

client.println("Content-Type: text/html");

client.println();

client.print("<body>");

//client.println("<form method=get name=LED><input type=checkbox name=L value=1>Activate Outlet<br><br><input type=submit value=submit></form>");

//client.println("<form method=get name=LED><input type=checkbox name=L value=1>Flood Ballast<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=LED><input type=checkbox name=L value=2>Drain Ballast<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=LED><input type=checkbox name=L value=3>Right Bilge<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=LED><input type=checkbox name=L value=4>Left Bilge<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=LED><input type=checkbox name=L value=5>Reverse Bilge<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=LED><input type=checkbox name=F value=6>Forward Bilge<br><br><input type=submit value=submit></form>");

client.println("<form method=get name=DIVE><input type=checkbox name=L value=1>DIVE!!!<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=SURFACE><input type=checkbox name=L value=2>Surface<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=RIGHT><input type=checkbox name=L value=3>Right Bilge<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=LEFT><input type=checkbox name=L value=4>Left Bilge<br><br><input type=submit value=submit></form>");

// client.println("<form method=get name=REVERSE><input type=checkbox name=L value=5>Reverse Bilge<br><input type=submit value=submit></form>");

// client.println("<form method=get name=FORWARD><input type=checkbox name=F value=6>Forward Bilge<br><input type=submit value=submit></form>");

// client.print("Outlet status: ");

// if (LEDON)

// client.println("ON");

// else

// client.println("OFF");

client.println("<br ><br >");

client.println("</body></html>");

}

void floodstatus(){

if(readString.contains("L=1")) //lets check if LED should be lighted

{

digitalWrite(ballastfloodpin, HIGH); // set the LED on

digitalWrite(ballastdrainpin, HIGH);

//LEDON = true;

// delay(1000);

// digitalWrite(ballastfloodpin, LOW);

Serial.print("DIVE");

}else{

//digitalWrite(ledPin, LOW); // set the LED OFF

//LEDON = false;

}

}

void drainstatus(){

if(readString.contains("L=2")) //lets check if LED should be lighted

{

// digitalWrite(ballastdrainpin, HIGH); // set the LED on

//LEDON = true;

// delay(1000);

// digitalWrite(ballastdrainpin, LOW);

digitalWrite(ballastfloodpin, LOW);

digitalWrite(ballastdrainpin, LOW);

Serial.print("SURFACE");

}else{

// digitalWrite(ledPin, LOW); // set the LED OFF

//LEDON = false;

}

}

void rightstatus(){

if(readString.contains("L=3")) //lets check if LED should be lighted

{

digitalWrite(rightbilge, HIGH); // set the LED on

//LEDON = true;

delay(6000);

digitalWrite(rightbilge, LOW);

Serial.print("RIGHT");

}else{

// digitalWrite(ledPin, LOW); // set the LED OFF

// LEDON = false;

}

}

void leftstatus(){

if(readString.contains("L=4")) //lets check if LED should be lighted

{

digitalWrite(leftbilge, HIGH); // set the LED on

// LEDON = true;

delay(6000);

digitalWrite(leftbilge, LOW);

Serial.print("LEFT");

}else{

// digitalWrite(ledPin, LOW); // set the LED OFF

// LEDON = false;

}

}

void reversestatus(){

if(readString.contains("L=5")) //lets check if LED should be lighted

{

digitalWrite(reversebilge, HIGH); // set the LED on

//LEDON = true;

delay(6000);

digitalWrite(reversebilge, LOW);

Serial.print("REVERSE");

}else{

// digitalWrite(ledPin, LOW); // set the LED OFF

// LEDON = false;

}

}

void forwardstatus(){

if(readString.contains("L=6")) //lets check if LED should be lighted

{

digitalWrite(forwardbilge, HIGH); // set the LED on

//LEDON = true;

delay(6000);

digitalWrite(forwardbilge, LOW);

Serial.print("FORWARD");

}else{

// digitalWrite(ledPin, LOW); // set the LED OFF

// LEDON = false;

}

}
```

I also made the BCD control valve:
TKTK image

# Results
Now where are the final testing results? Currently, I don’t know. I had this report handed in to my instructor back in high school. I had thrown together a crappy website before for project docs, but I never completed the documentation there. In the years since, with hard drives lost and my, in hindsight, misplaced distrust of public cloud. I have since done end-to-end protection so I will use some cloud services. Hopefully one day I can find and recover the last test videos of it with the BCD data (which also happens to be the first certified dive of a buddy of mine as a scuba diver when he helped film it… so two people at least care about it).
