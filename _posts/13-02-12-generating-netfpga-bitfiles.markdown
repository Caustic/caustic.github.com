---
layout: post
title: Generating Bitfiles for the NetFPGA from verilog
---

In one of my earlier posts I mentioned that I'd need to be compiling verilog files for my NetFPGA.  Having no experience with Xilinx ISE, I thought it would be a pretty daunting task.

### First things first

There are a couple of prequisites:
* Have a NetFPGA fully installed and passing self tests. [See Here](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/VerifyHardwareAndSoftware)
* Make sure that [Xilinx ISE 10.1](http://www.xilinx.com/support/download/index.htm) is installed with [Service Pack 3 and IP pack](http://www.xilinx.com/support/download/index.htm) installed.

So I pulled up my terminal and set to work figuring out how to compile the reference bitfiles from the verilog.  Using [this page](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/VerifyHardwareAndSoftware#Run_regression_scripts_on_new_bi) as a guide, I was able to do it relatively easily.

Whats more?  I don't ever have to open an IDE to generate bitfiles!  (Although I'm sure I'll need it at some point.)

Cheers!

