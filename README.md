# Table of Contents

- [Credits](#credits)
- [Community](#community)
- [Downloadable Content](#downloadable-content)
- [Intro](#intro)
- [Design](#design)
  - Linkage
  - Legs
  - Leg Pair + Frame and Crank
  - Frame and Crank
  - Gearbox and Frame
  - Crank
  - Six Legs
  - Full Assembly
  - Editable Design Files
- [Printing](#printing)
- [Assembly](#assembly)
- [Electronics](#electronics)
- [Firmware](#firmware)

**Update 2024-10-31**

* The square shafts were originally printed in PLA-CF, but two out of 3 got damaged very quickly. I reassembled the whole thing using 8x8mm steel rods. Here in Belgium these rods can be bought in DIY stores. You'll have to cut them to size, see dimensions in the build log below.
* Manually chamfered the round parts of the cranks, to make it less likely to collide with the bottop part of the legs.
* Added a M8 nut which hides under the outter black spacers, to make the frame more rigid.
* Added rounded shoes (printed in PETG), to let feet slide sideways during turns.

All these changes (except chamfer of the cranks) is in the latest version of STEP models.

# Credits

This project was inspired by [Carpentopod](https://www.decarpentier.nl/carpentopod) created by Giliam de Carpentier, all credits should go to him.

# Useful Content

Here is a Youtube clip of the [thing walking steered using Nintendo controller](https://youtu.be/jmLX-odWrtY):
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/jmLX-odWrtY/0.jpg)](https://www.youtube.com/watch?v=jmLX-odWrtY)

The latest Fusion 360 models in STEP format is uploaded into the [STP/](https://github.com/abbbe/carpentopod-v43/tree/main/STP) folder on GitHub. Normally the STEP file includes all the subcomponents. (If you want individual models of the elements described in "Design" section, check previous commits). Once you open the model you should get something like this:
![Two Halves v7 - Thumbnail](images/Two%20Halves%20v7.png)

An interactive 3D model is available on the [Autodesk site](https://a360.co/3A7hhCD).

Here is a screen recording of the [animation of the joint movements in Fusion 360](https://youtu.be/IclcQic5kn8) on YouTube. Done from different view angles, with some legs and plates removed to make the crankshaft movements visible. I did not recreate it since the original upload, so there are no shoes (you can see those via the Autodesk link above).

Printable 3MF files are uploaded into the [3MF/](https://github.com/abbbe/carpentopod-v43/tree/main/3MF) folder. Made in OrcaSlicer, printed on a Bambu X1C with 0.4mm hardened steel nozzle (see the Printing section below for more details).

The models are also published on [Printables](https://www.printables.com/model/1052837-carpentopod-v43).

I have created a [thread](https://discord.com/channels/1299814326185627702/1300201396834140271) on Giliam's Discord server, if you have any questions feel free to ask there. Or create GitHub issue or a pull request.

# Intro

I have been playing with Fusion 360 and various linkages for couple months when I saw a video of the [Carpentopod](https://www.decarpentier.nl/carpentopod) published by Giliam De Carpenter. He was kind enough to release exact linkage dimensions. I figured it could be a nice Fusion 350 challenge to design the mechanism behind the scene.

As you will see below, I have focused mostly on the mechanical side, not the artistic value of the piece. There is rudimentary electronics curcuitry and firmware to control it, I have described it on the high level at the end of the document.

At this point as I have no particular plans to continue with this project. If you found this design entertaining or useful, I will be happy to hear about it. Feel free to contact me if you have any questions.

And as far as any intellectual property (accidentally) created by me goes -- I am licensing it away under two conditions: (1) you put a star to this Github repo and (2) you will not use it for any military purposes. **Make robots, not war!**

# Design

## Linkage

I have turned the original linkage diagram black and white for easier printing and named each joint.
![Linkage Diagram](images/Pasted%20image%2020241026052440.png)

## Legs

The first part I designed was a leg. I have made an attempt to parameterise the design. It was not obvious what units Giliam's diagram used exactly, so I have included a scaling factor which I can tune the size of the model for my printer.
![Alt text](images/Pasted%20image%2020241026052941.png)

Unfortunately, I couldn't find a way to share parameters between designs in Fusion 360. So some of these values ended up being copy-pasted into other designs. If you know how to do this properly, please tell me.

The design is as simplistic as it gets, I have made no attempt to replicate the beautiful curves of Carpentopod's legs. Here is another view without the top plates:
![Alt text](images/Pasted%20image%2020241026053241.png)

To keep things 3D-printable I had to make a separate spacer:
![Alt text](images/Pasted%20image%2020241026053802.png)
I have randomly chosen the thickness of the larger levers (AE, BD) to be 10mm. It means levers CH and FH became 2.5mm thick (there was no spacing in between the levers, but there is spacing between the yellow levers and the red plates). This turned out to be a bad choice, because when I 3D-printed it using normal 0.20 layer height, the slicer makes it slightly bigger, something like 2.60. Not a big deal as such, but 4 levers stacked together (combined with other artefacts of 3D printing process) became too thick. I worked around this issue by printing using 0.16mm layer height.

## Leg Pair + Frame and Crank

Next I have put together a pair of legs.
![Alt text](images/Pasted%20image%2020241026053454.png)
H1-H1 joint is connecting H joints of the legs. Other joints you see on the picture is my way to help stacking the leg pairs later down the road. There is another design included into this file called Frame and Crank. Left, Right and Crank joints link the pair of legs to corresponding sketch points of that design.

## Frame and Crank

I have made a separate design file in attempt to work around lack of shared parameters in Fusion. It includes two sketches and no bodies.

Left, right and bottom circle on Frame sketch are the horizontal M8 rods which link the whole thing together. I have actually had another rod on the top, but eventually dropped it. The central circle is the motor shaft (point I).
![Alt text](images/Pasted%20image%2020241026054927.png)
The Crank sketch contains a circle positioned in the same place as the central circle (I) on the frame. Another circle is point H, which turns around point I.
![Alt text](images/Pasted%20image%2020241026055336.png)

This Frame and Crank design file is included into other design files. Unfortunately at some point I have edited this design without properly updating other design files. If I do it now, things fall apart. I am not sure how this problem can be resolved.

## Gearbox and Frame

The next design file includes the motor and a large plate to fix it on. I have used [OpenQDD v1 actuators](https://www.aaedmusa.com/projects/openqdd) designed by Aaed Musa (slightly adapted to use MKS ODrive Mini). These mighty things are probably overkill for this project, but I have just built a pair and had no better use for it yet.

![Alt text](images/Pasted%20image%2020241026060032.png)

## Crank

And here comes probably the most complicated part of my design, the crankshaft. I have spent probably a week trying to figure it out, then printed something rather ugly that survived for just long enough to allow me to come up with a rather nice design I think. It  consists of just 3 unique elements.

Two **RadialCrankShaft**. One will be combined with the motor output in the next design. Another is meant to be glued with a little lever which plugs into a ball bearing on the outer plate.
![Alt text](images/Pasted%20image%2020241026061138.png)

Four **ChordHalfCrank** pieces, which are glued together back to back to make two components.
![Alt text](images/Pasted%20image%2020241026061449.png)

Six inserts. ![Alt text](images/Pasted%20image%2020241026061626.png)

I was not sure if the plastic will be strong enough, so I have chosen 8mm square shafts. I figured I can just use metal rods from any DIY store if 3D printed parts do not hold.

Originally the shaft were in this design too, but the length of the two of the shafts actually depends on other elements, so I have moved them to the next file.

## Six Legs

Finally, all of the above are assembled together:
![Alt text](images/Pasted%20image%2020241026060822.png)

I used M8 rods with nuts and washers to keep the whole thing together. They are 250mm long in this design, but in the physical world they are 500mm. Not all fasteners are included into Fusion 360 project, see the pictures/videos of the assembled contraption for finer details.

There is another dumb green plate. I was thinking about redoing them in black with a honeycomb pattern but this never happened. It embeds a ball bearing. I had a pair of 6001Z left from OpenQDD assembly, so I used them. Simple 608 would do the trick as well I am quite sure.

You can also see a bunch of black PLA spacers. There are also some inserts, rendered transparent red acrylic, but actually printed in grey PETG.

![Alt text](images/Pasted%20image%2020241026064713.png)

The piece which gets attached to the motor is called CombinedDriveCrank. It is a combination of RadialCrank (from previous design) and DriveCrank component. If you regenerate 3MF files note that you only need to export the combined part. ![Alt text](images/Pasted%20image%2020241026071920.png)
**Note the hole on the elevated part of this element is larger than two other M3 holes. It was mean to accommodate a head of M3 screw. It has turned out to be too small for my screw. Consider resizing it to 6mm or something.**

## Full Assembly

And here are just two halves joined together.
![Alt text](images/Pasted%20image%2020241026064947.png)

## Editable Design Files

All the design files are published in in STP/ folder:
```
Leg v30.step
Leg Pair v19.step
Frame and Crank v11.step
Gearbox Frame v20.step
Cranks v19.step
Six Legs v49.step
Two Halves v4.step
M8 Cylinder v1.step
```

# Printing

See in 3MF/ folder:
```
Levers PLA YELLOW.3mf
Leg Plates PLA RED.3mf
Gearbox Frame PLA GREEN.3mf
Crank PURPLE PLA-CF.3mf
Inserts PETG-HF GREY.3mf
Spacers PLA BLACK.3mf
Outer Plate PLA GREEN.3mf
M8 Cylinder v1.3mf
```
If you need parts for both halves, you have to print all all these 3MF files twice (except the M8 cylinder tool).

STP files for OpenQDD v1 are published on [Aaed Musa website](https://www.aaedmusa.com/projects/openqdd). As I mentioned above, this is overkill by a large stretch, a simple DC motor with a gearbox should do just fine.

## Leg Levers

"Levers PLA YELLOW.3mf". I printed them in Bambu PLA Basic Red.

**If you print in 0.20mm it will not fit nicely (see explanations above).** 0.16mm layer height worked for me just fine. Settings in the 3MF file I publish are a blend of "0.16mm Optimal" and "0.20 Strength" profiles.

![Alt text](images/Pasted%20image%2020241026070153.png)

## Leg Plates

"Leg Plates PLA RED.3mf" also gives you 3 pairs of legs. I printed it in Bambu PLA Basic Red using standard "0.20 Strength" profile with random seams.

Coulpe remarks:
* Plate 01 is packed rather tight. It prints just fine on my X1C, but you better remove [Shifty](https://makerworld.com/en/models/83480#profileId-89128)
* I am not sure if the orientation of parts on plate 03 is correct. If you care about the texture of the finished part - print one and see for yourself.
![Alt text](images/Pasted%20image%2020241026070519.png)

## The crankshaft

"Crank PURPLE PLA-CF.3mf" was printed in purple Bambu PLA-CF, using the default "0.20 Strength" profile with random seams and 100% infill.
![Alt text](images/Pasted%20image%2020241026071620.png)

## Spacers

"Spacers PLA BLACK.3mf" - probably the least critical element of the design. Printed in "0.20 Standard" process using black Bambu PLA Basic.
![Alt text](images/Pasted%20image%2020241026072527.png)

When assembling you will be using two smaller spacers back to back in between the leg pairs. Next iteration of the design should probably have them merged to reduce the number of parts.

## Inserts

"Inserts PETG-HF GREY.3mf" - printed in Bambu PETG-HF using default "0.20 Strength" process with random seams.

![Alt text](images/Pasted%20image%2020241026072942.png)

## Green Plates

"Outer Plate PLA GREEN.3mf" and " Gearbox Frame PLA GREEN.3mf" are the elements I am the least proud of. Printed in green Bambu PLA Basic using default "0.20 Strength" process with random seams.
![Alt text](images/Pasted%20image%2020241026073717.png)

![Alt text](images/Pasted%20image%2020241026111514.png)

# Assembly

The assembly process is rather straightforward. I have started documenting it towards the end of the project and only made photos of the assembly of one half. Please forgive the not so clean background.

### Preparation

Here we have a bunch of 3D printed parts:
![Alt text](images/Pasted%20image%2020241026113001.png)
Some weird optical illusion make the photo appear trapezoid, but it is a rectangle I swear ;).

They will go to into a half-assembled contraption.
![Alt text](images/Pasted%20image%2020241026112930.png)

Above you can see the motors are mounted on the frames and 3x 500mm M8 rods. On top of this I will use a handful of fasteners:
* 16x M8 regular nuts,
* 6x M8 nuts with plastic inserts,
* 9x large M8 washers,
* 4x small M4 washers,
* 3x M3x6 screws (to attach the output disk to the gearbox),
* 8x self-threading 3.5x12mm screws (to fix the ball bearing).

You will also need:
* a couple of 13mm wrenches,
* a screwdriver for your M3 screws,
* grease (I used [APP ST 250 PTFE Dry Lubricant Aerosol PTFE Grease](https://www.amazon.fr/dp/B004AHMVOM/ref=sspa_dk_detail_2?psc=1&pd_rd_i=B004AHMVOM&pd_rd_w=nyWz9&content-id=amzn1.sym.d15aafde-9691-4d5f-85f2-056701d026bf&pf_rd_p=d15aafde-9691-4d5f-85f2-056701d026bf&pf_rd_r=7MGMT81QDTRC1AAFFD23&pd_rd_wg=B5cd6&pd_rd_r=16cb370e-badc-40b7-b058-b565330e0f72&s=industrial&sp_csd=d2lkZ2V0TmFtZT1zcF9kZXRhaWw)]),
* a deburring tool and 8mm drill bit.

You will want to debur the holes in the yellow levers to the point they rotate nicely. In my case something went wrong with the yellow PLA levers and I had to do a lot of deburring and even use 8mm drill bit to enlarge. _Next design should add chamfers to these parts._

You also want to sort the the purple square shafts by length:
* 41.40mm - goes into the motor crank disk at the very beginning,
* 43.40mm - used at the very end of the assembly,
* 46.40mm - the longest one, used in the middle.
_It would be nice to make some kind of identification marks on the shafts ot make them all same length_.

## Mount the Gearbox and Frame

Move a couple of M8 nuts and washers down the M8 rods. If you bothered to print the M8 cylinder you can move two nuts in one go.
![Alt text](images/Pasted%20image%2020241026113921.png)

Put the gearbox on top, add the spacers and a washer with a couple nuts on the bottom rod. Put the first shaft (the shortest 41.40mm one) before screwing in the purple part and mount it on top of the gearbox.
![Alt text](images/Pasted%20image%2020241026120724.png)
As I mentioned above, the hole in the RadialCrank element turned out too small to fit the head of my M3 nuts. I used a 6mm drill to widen it. There will be no force tearing this plate off, but it is better not to drill it through (like I almost have done). _The next design iteration should fix this little bug._

## Legs

The next step is to assemble the legs. Use plenty of grease on all the axes and on the faces of the yellow levers around the large hole.
![Alt text](images/Pasted%20image%2020241026115237.png)

The covers just nap into place.
![Alt text](images/Pasted%20image%2020241026120505.png)

Put the grey inserts, grease it all.
![Alt text](images/Pasted%20image%2020241026120555.png)

## Mount the First Leg Pair

Normally everything just slides into place. In my case the PETG inserts were probably over-extruded a bit, it took quite some force to push them down the square shaft, but it worked. _You better calibrate your PETG and PLA-CF extrusion and/or add tolerances_. Again, don't forget to grease the inserts.
![Alt text](images/Pasted%20image%2020241026121206.png)

## The crankshaft

Now it is time to glue the shaft together. I used some contact glue to fix the ChordCranks together. They are all identical, just make sure the square holes are aligned. _A better design would include some alignment pins I guess_.

Here is the final result:
![Alt text](images/Pasted%20image%2020241026121806.png)

On the photo below I have put all the elements of the crankshaft together just to give you an idea of how it looks like inside the mechanism. To continue the assembly process you obviously only need one element in place so **the photo below is for illustration purposes only and is not a real assembly step**.
![Alt text](images/Pasted%20image%2020241026121633.png)

## Assemble Two Remaining Leg Pairs

I guess it is straightforward to assemble and mount the remaining two pairs of legs.
* In between the leg pairs go the black PLA spacers. Two spacers go on each M8 rod one after another. _There is no good reason for it and an improved design should have these two spacers merged I guess._
* The second shaft is the longest one (46.40mm) and the last one is the shortest one (43.40mm).
* Note there are no stoppers and nothing stops the shaft from slipping away. It was not a problem for me in practice, the shafts fit just right and do not slip away. _A better design would include some stoppers and/or side screws to fix the shafts in place_.

Here is a photo of 2nd pair of legs mounted.
![Alt text](images/Pasted%20image%2020241026122155.png)

## The Last Step

Finally, you add:
* longer black spacers (one piece per M8 rod),
* the last crank shaft,
* another couple of M8 nuts and a washer on the bottom M8 rod.
![Alt text](images/Pasted%20image%2020241026123921.png)

I don't have photos of the assembly process of the green plates, because those were made at the very beginning of this project. Just snap the ball bearing in place and secure them with the ring and 3 screws.

Finally, mount the green plate on the M8 rods, push the outer end of the purple crankshaft into the ball bearing, and fix the purple washer with another screw.
![Alt text](images/Pasted%20image%2020241026140831.png)

## Fully Assembled View
Here's how it looks in the horizontal position:
![Alt text](images/Pasted%20image%2020241026124621.png)

With electronics (the serial links to the ODrives are not attached):
![Alt text](images/Pasted%20image%2020241026142441.png)

Fully assembled and switched on:
![Alt text](images/Pasted%20image%2020241026142533.png)

# Electronics

I might document the electronic part later in greater details, but on the high level it consists of:
* A 22.2V LiPo battery with an XT60 connector
	* Aliexpress [HRB Lipo Battery 6S 5000mah](https://www.aliexpress.com/item/4000389770504.html?spm=a2g0o.order_list.order_list_main.71.22b418023OYCrn)
	* Might be overkill for this project
* A toggle switch
	* Aliexpress: [Large Current High Load Switch AMASS XT60](https://www.aliexpress.com/item/1005005224857810.html?spm=a2g0o.order_list.order_list_main.41.22b418023OYCrn)
	* Not sure I can recommend this particular model. The switch has failed to go OFF at least once
* Couple custom Y splitters to feed ODrives and the step-down converter
	* Aliexpress [Male Female Connector Plug with Silicon 12 AWG](https://www.aliexpress.com/item/1005003489220110.html?spm=a2g0o.order_list.order_list_main.53.22b418023OYCrn)
	* Next time I would probably go for a 14AWG, easier to work with
* A step-down converter
	* Amazon [Retoo LM2596 DC-DC Power Adapter Step-Down Module](https://www.amazon.fr/dp/B09QMDL7FH?ref=ppx_yo2ov_dt_b_fed_asin_title)
	* Seems to work fine, but very bulky
* LOLIN D32 board
	* Aliexpress [LOLIN D32 V1.0.0](https://www.aliexpress.com/item/1005005305131344.html?spm=a2g0o.order_list.order_list_main.124.22b418023OYCrn)
	* A very nice board in itself, but maybe not the ideal choice here. I bought it for something else because it has on-board LiPo battery charging circuits. This is quite pointless and even counterproductive as one has to add an extra wire to be able to power the board off external source.
* Custom serial cables, to control ODrives from LOLIN D32. Those are specific to OpenQDD, no point to got into any details here.

The LOLIN D32 / DC-DC converter / the batteries / the cabling -- all is screwed/velcroed to a  platform hanging in between the M8 rods.

# Firmware

The source code is published [here](https://gitlab.com/abbbe/bluepad-32-carpentopod-v-43/-/tree/carpentopod-v43?ref_type=heads), in the 'carpentopod-v43' branch of my fork of [Bluepad32](https://gitlab.com/ricardoquesada/esp-idf-arduino-bluepad32-template.git) repo.

To build the firmware [install the ESP-IDF 4.4 framework](https://docs.espressif.com/projects/esp-idf/en/v4.4/esp32/get-started/index.html) first (ESP-IDF command line tools worked for me on Windows 11). Then do the following to fetch my branch, build it, flash into ESP32, and run the serial console monitor:
```
git clone --recursive -b carpentopod-v43 https://gitlab.com/abbbe/bluepad-32-carpentopod-v-43.git
cd bluepad-32-carpentopod-v-43
idf.py build flash monitor
```

If things don't work use the hello_world project from ESP-IDF repo to troubleshoot your setup.

The following files were modified/added:

* main/sketch.cpp - existing file, calls couple functions defined in carpentopod.h from existing setup(), loop(), and processGamepad() functions.
* main/carpentopod.* - new file, manages ODrive's idle/running state, tranlsates joystick readings to velocity commands.
* main/odrive.* - new file, talks to ODrives over USARTs.

The firmware does the following:

* Initializes BLE controller and waits for a game controller to pair. This code comes from the upstream repo.
* Initializes ODrives and puts them in idle mode.
* If a controller is connected, it translates readings for Y axes of left and right joysticks to ODrive velocity commands. This is done by dividing the readings (-512 to +512 range) by 100, so ODrives go up to around 5 RPMs on full throttle.
* If a controller get disconnected, it switches ODrives to idle state.
* Monitors battery voltage and halts the system if voltage drops below safe value. _Ideally it should raise some alarms and put the system into deep sleep. Doable for ESP32, but ODrives do not support deep sleep._ 

Some remarks:
* The firmware contains tons of redundant code. Any game controller, a bluetooth mouse, a keyboard trying to join it will be accepted (but only game controller joystick events will be used).
* I could not figure out how to use Bluepad32 on my M1-based Macbook Pro - installation of ESP-IDF 4.4 fails there. Used Windows 11 instead.
* I used the [offline installer](https://objects.githubusercontent.com/github-production-release-asset-2e65be/342348458/8d0419b3-daf4-496a-97cf-b81cf14f8095?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20241020%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241020T095018Z&X-Amz-Expires=300&X-Amz-Signature=f52cd7ab3df60e30b361044a04adcc3b42f47ff7e4f7fc85b68b0381f551533c&X-Amz-SignedHeaders=host&response-content-disposition=attachment%3B%20filename%3Desp-idf-tools-setup-offline-4.4.8.exe&response-content-type=application%2Foctet-stream).
* PlatformIO did not work for me, my guess ESP-IDF 4.4 is too old, but I am not sure. VSCode with the ESP-IDF plugin works just fine, but you don't really need VSCode if you don't plan to edit code, command line tools which come with ESP-IDF 4.4 are enough.

THE END.
