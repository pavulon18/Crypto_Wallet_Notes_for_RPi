# Crypto_Wallet_Notes_for_RPi
A few notes that I have gathered from trying to compile several different wallets on my 32-bit RPi running Raspian

Although I will try to put these notes into some sort of order, they may start out disorganized.  I will also try to give credit where credit is due.  Also understand that I am not a C++ programmer.  I appologize if I use the wrong terminology.

Feel free to submit a pull request if you have any suggestions, error corrections, or changes that need to be made.

Even if a wallet compiles on the Pi, it may not run on the Pi.  Some wallets were designed for 64bit architectures.  When they are executed on a 32 bit machine, the software will throw a segmentation fault.

If you are running the standard installation of Raspbian on an SD card, you probably won't have much luck getting any of these projects to compile.  I had to move my OS off the SD card and on to an old HDD that I had lying around the house.  Need to find the credit  for this resource

It seems that MAKE system does not handle the identification of the ARM processor exactly right.  Normaly, MAKE will identify the processor and build the software for that processor with no additional intervention.  On the Pi, MAKE will indentify the processor as "armv7l-unknown-linux-gnueabihf".  This will throw up errors saying something to the effect of "armv7l-unknown-linux-gnueabihf cannot be found" after running a short time.  To combat this error, I run this command.  "make HOST=arm-linux-gnueabihf".  The "HOST=" qualifier lets the programmer tell the compiler to build the system for a different architecture.  In our case, this command simply corrects the misidentification of the architecture.  Need to find the source for this resource.

Some wallets will have a directory called "depends".  Go into this directory and issue "make HOST=arm-linux-gnueabihf".  On my system, this wil run for a long time.  I also see a lot of warnings scroll through.

Newer versions of libssl will cause the compiler to throw errors out about BIG_NUM.  I had to downgrade that package to the libssl found in jessie.  I need to find the exact error message and the resource where I found this information.

I also had to edit the "Makefile.am" to point to the resources built in the "depends" directory rather than trying to use the system's software. (This may not be accurate.  Although I did it for one project, there may be a better way of doing it.)

use "./configure --prefix=`pwd`/depends/arm-linux-gnueabihf"
https://github.com/PIVX-Project/PIVX/blob/master/depends/README.md

