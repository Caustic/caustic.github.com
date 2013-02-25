---
layout: post
title: Testing and Simulation using the NetFPGA and isim
---

So I've been having trouble testing the NetFPGA because I don't have a full version of 
ModelSIM (overlooked in project planning :/).  Fortunately for me, the NetFPGA has supported 
different test environments since about version 2.1?  I'll be using the Xilinx ISE 10.1 ISim
software for testing my project.

Another issue I ran into while testing was that I didn't have the proper license to generate one 
of the cores. I found [this thread](http://forums.netfpga.org/forums/archive/index.php/t-645.html) 
on the forums that makes it sound like I can just copy the cpci.bit file from the release
versions on the netfpga site.  However, before I found that thread I signed up for an evaluation
license for coregen through Xilinx.  I'll have to investigate the other solution further.

I will be using the python testing scripts from the 3.0.0 release of the NetFPGA repository.  Making
progress on the design and just beginning to get the verilog implementation up and running!
