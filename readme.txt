== Introduction

This document describes a methodology to use TCL scripts within Vivado to create an FPGA design for the Zynq MicroZed platform.


== TCL Advantages

The use of TCL has many advantages.  

- Full control of source files
- compatibility with GIT and SVN version control tools.
- Repeatable build process
- minimum interaction with annoying GUI interfaces

== The Files

This flow uses several TCL scripts to compile code.

- setup.tcl - This script creates a fresh proj.xpr Vivado project file from scratch.  It adds all source
files from your version controlled source directories including IPI block diagrams, core generator cores and HDL.

- compile.tcl - This script opens proj.xpr and runs synthesis through config file generation.

- add_ila.tcl - This script defines debug signal and attaches an ILA debug core to the design. It is 
optionally called from compile.tcl.

== How to Use

=== Check out the files

    git clone https://github.com/hdlguy/vivado_zynq.git


=== Get to the Vivado TCL prompt

==== Linux
In linux you need to source a script that sets up the environment. Like this:

    source /opt/Xilinx/Vivado/2015.2/settings64.sh

Then change directory to your working directory, like

    cd ~/proj/vivado_zynq/implement

Then start Vivado in TCL mode.

    vivado -mode tcl

==== Windows

From the start button, open Vivado TCL Shell

In the TCL Shell change director to the working directory

    cd {C:\path_to_implement_director}

Note: use the {} brackets to avoid having to edit all the '\' to '/'.


=== Run setup.tcl

    source setup.tcl


=== Run compile.tcl

    source compile.tcl


=== Review results

In the implement/results folder you will find these files.

ila1.ltx  - when adding an ILA core this file is what is used to import signal names into the ILA user interface.
io_regs.rpt  - report of which I/O pins are registered in the IOB.
post_imp_io.rpt  - the regular I/O report
post_route.dcp  - post place and route checkpoint. 
post_route_timing_summary.rpt  - this shows worst timing paths for each constraint
post_synth.dcp  - post synthesis ch3eckpoint.
top.bit  - the fpga bit file ready to load from download cable.
top.bit.bin  - the fpga bit file formatted so that Zynq linux can load


=== Test with Linux on Zynq

    sudo cat top.bit.bin > /dev/xdevcfg

=== Working with the FPGA design.

The setup.tcl script creates a complete ready-to-open Vivado project file called proj.xpr.  You can open that
file from the linux command line like this:

    vivado proj.xpr

You can compile the design inside the Vivado GUI and browse the results in the RTL schematic editor.

You can also open the IP Integrator block diagram part of the design.  If you make any changes 
you can save them back into the source folder this way.

    write_bd_tcl -force ../source/system.tcl





