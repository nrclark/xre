XRE
===

XRE - the Xilinx Runtime Executer.

This is an easy-to-customize BASH script for launching Xilinx executables
from an installation of Xilinx ISE or EDK.

This script is intended to make it easier to use Xilinx's tools from the
command line, particularly on Ubuntu or other Debian-based distributions
for which Xilinx's tools don't all work right out of the box.

I'm currently using the script with great success on Ubuntu 13.04 64-bit.

Basically, you edit the script to change a couple of variables in a 
block at the beginning, and then you use it to launch Xilinx programs. 
The script takes care of setting up the environment variables and linking
in the right stdlibc++ to make everything work.

Once you set it up, launching ISE is as easy as running:
xre ise

If you copy xre and modify it (say, to have two side-by-side installations),
you could run:

> **xre14\_5 ise** to start ISE 14.5 (once you've set up that copy of XRE)  
> **xre12\_3 ise** to start ISE 12.3 (ditto)  
    ...etc.  

If you wanted to run the 32-bit tools for whatever reason, you could
make a copy of XRE, comment out the 64-bit group of variables,
and uncomment the 32-bit group. Save the new one as xre_32 and the
original as xre_64, and you're good to go for both versions.

If get bored with typing 'xre' all the time and you want to start
a shell, xre's got you covered. Just run:

> **xre bash**, and you'll find yourself in a shell with all the Xilinx
runtime variables set up and ready.  

Why?
===

XRE solves two problems.

1) On Ubuntu and Debian 64-bit Linux, Xilinx's ISE toolset is kind of
broken as of the time of this writing. It's true that neither of the
distributions at listed on Xilinx's website as being ISE-compatible,
but Debian-based distributions make up a majority of Linux installations.

The only thing I found that needed fixing to make ISE Debian-compatible
was that the distro-supplied libstdc++ needed to be used instead of the
ISE-supplied copy.

XRE takes care of this automagically by using LD\_PRELOAD. It doesn't
need to change any files in your ISE installation.

2) In a production FPGA environment, it can be important to keep the "right"
versions of the tools around, for supporting legacy builds. XRE allows you
to easily change from one tool version to the next (either by editing your
XRE script file, or by having copies that are configured for different
installations)

How?
===

Using XRE is simple. Three easy steps.

1) Download it. It's a script file.
2) Open it in a text editor and change the variables to match your computer.
3) Rename it whatever you want and put it in your path.
4) There is no step 4. Use it to launch Xilinx stuff.


XRE uses a block of settings to configure itself. You'll want to change
those settings for your own machine. On my machine (running ISE 14.5 / 
XUbuntu 13.04 64-bit), my settings are:

    XILINX="/opt/Xilinx/14.5/ISE_DS"
       
    LIB_PATH="/usr/lib/x86_64-linux-gnu"
    LIBSTDC="libstdc++.so.6"
    SETTINGS="settings64.sh"
    PRELOAD_NAME="LD_PRELOAD"
    RUNTIME_PREFIX="linux64"

If I wanted to set it up for 32-bit, I'd keep my Xilinx path the same,
but I'd change the rest of the variables accordingly:

    LIB_PATH="/usr/lib/i386-linux-gnu"
    LIBSTDC="libstdc++.so.6"
    SETTINGS="settings32.sh"
    PRELOAD_NAME="LD_PRELOAD_32"
    RUNTIME_PREFIX="linux32"






