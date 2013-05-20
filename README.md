xre
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

    xre14\_5 ise to start ISE 14.5 (once you've set up that copy of XRE)  
    xre12\_3 ise to start ISE 12.3  
    ...etc.  

Why?
===

XRE solves two problems.

1) On Ubuntu and Debian 64-bit Linux, Xilinx's ISE toolset is kind of
broken as of the time of this writing. It's true that neither of the
distributions at listed on Xilinx's website as being ISE-compatible,
but Debian-based distributions make up a majority of Linux installations.

The only thing I found that needed fixing to make ISE Debian-compatible
was that the disro-supplied libstdc++ needed to be used instead of the
ISE-supplied copy.

XRE takes care of this by using LD\_PRELOAD.

2) In a production FPGA environment, it can be important to keep the "right"
versions of the tools around, for supporting legacy builds. XRE allows you
to easily change from one tool version to the next (either by editing your
XRE script file, or by having copies that are configured for different
installations)






