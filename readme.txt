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

=== Run setup.tcl

=== Run complile.tcl

=== Review results

=== Test with Linux on Zynq

    sudo cat top.bit.bin > /dev/xdevcfg



