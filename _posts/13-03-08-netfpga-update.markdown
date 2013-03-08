---
layout: post
title: OpenFlow NetFPGA Update
---

So I've been at this a while and I have been making steady progress on my
project however I seem to keep running into issues with the board's
tool-chain.  With NetFPGA release 3.0.1 they moved their testing suite to 
python which is nice, except that it doesn't seem like the documentation
has nearly caught up yet.  Fortunately, I've already had considerable
experience with python so stepping through the code is fairly easy.

###Platform

Some of the issues I ran into were both platform and software based. I just
moved the board into a new computer this past weekend since I needed more
PCI-E slots to fit some additional Ethernet modules for regression tests.
This went fairly smoothly but when I booted, I only saw one of the devices.
So I go into the bios and see nothing about PCI devices or Ethernet devices
(besides boot order) so I feel out of luck there.  Just before I'm at the
point where I think I need to flash an update, I find one single field in
a remote menu which the description reads that you an modify the bandwidth
of certain slots.  So I go ahead and increase the bandwidth on the x8/x16
slots in exchange for disabling the x1 slots entirely.  Sure enough this
fixed the issue.

###Software

Next I was having trouble with getting the regression tests working with
the board.  Going off the NetFPGA site, it's still somewhat hard to tell 
which scripts you're supposed to be using since all the documentation has
the different versions of the NetFPGA somewhat mixed up with notes here and
there mentioning small things changing from version to version. Anyway,
after I found I was supposed to be using a python script when I was using
the Perl script, I was able to work with that.  It didn't really work the
first run through, but after I stepped through the code with pdb, it was 
clear what was going wrong.  (For those interested, it was `nf_test.py` and
the Global Setup test was failing because the output was mismatched, even
though the setup itself succeeded.)

###You can never read too much

Anyway, I am in no means bashing on the documentation of either the NetFPGA
maintainers or the motherboard manufacturers for these issues.  Docs are
difficult to maintain, and software often moves faster than docs.  However
I continue to be reminded that thorough reading will often save you a lot
more time than trying to fix things outright using your own intuition.

###Edit:

I forgot to mention that when I initially did the selftest on the NetFPGA,
there were issues with the test passing the DMA test after moving it to the
new computer (it worked fine on the last one).  I wasn't actually able to 
track down the specific issue, but by swapping out the patch cables, I was
able to get the test passing.  I'm not sure why the cables would affect 
DMA, but that's something to investigate later.
