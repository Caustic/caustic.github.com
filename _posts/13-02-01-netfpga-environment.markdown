---
layout: post
title: Setting up NetFPGA Development Environment
---
### Obtain Hardware

1. Buy the NetFPGA
stuff
2. Obtain a PC to use as the host Machine

### Installing from git

1. `git clone git@github.com:Caustic/netfpga.git`

2. You'll need some bitfiles from [the netfpga wiki](http://wiki.netfpga.org/foswiki/NetFPGA/OneGig/Releases) Copy the `cpci*.bit` bitfiles from the tgz release. Just copy all bitfiles from their bitfile directory into your ~/netfpga/bitfiles.

3. Plug in the NetFPGA and boot up!

4. Add `vmalloc=256M` to `/boot/grub/grub.conf` or edit `/etc/default/grub` and run `grub2-mkconfig`. Failing to complete this step will result in the NetFPGA interfaces not getting initialized.

5. Add the necessary NF\_ Environment variables: `source bashrc_addon.sh`

6. Create simlinks for system binaries.

        # ln -s ~/netfpga /usr/local/netfpga
        # ln -s /usr/local/netfpga/lib/scripts/cpci_config_reg_access/loadregs.sh /usr/lcoal/sbin/loadregs.sh
        # ln -s /usr/local/netfpga/lib/scripts/cpci_config_reg_access/dumpregs.sh /usr/local/sbin/dumpregs.sh

7. Install the driver

        $ cd ~/netfpga/lib/C
        $ make
        $ sudo make install
        $ modprobe nf2

8. Reboot.

9. Check to see if things work

        $ ~/netfpga/lib/scripts/cpci_config_reg_access/dumpregs.sh -f ~/defaultregs # for problem recovery
        $ ~/netfpga/lib/scripts/cpci_config_reg_access/loadregs.sh -f ~/defaultregs # do this if cpci_reprogram fails half way
        $ sudo ~/netfpga/lib/scripts/cpci_reprogram/cpci_reprogram.pl
        $ sudo /usr/local/bin/nf_download /usr/local/netfpga/bitfiles/reference_nic.bit
        # ifconfig nf2c[0-3] 10.0.1[0-3].1/24 for the 4 ports

####Sources:

[ObtainHardwareAndSoftware](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/ObtainHardwareAndSoftware)

[InstallSoftware](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/InstallSoftware)

[VerifyHardwareAndSoftware](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/VerifyHardwareAndSoftware)

[InstallSoftware10](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/InstallSoftware10)

### Issues I had and how I fixed them (Fedora 17 vanilla install):

    # Error
    Can't locate XML/Simple.pm in @INC
    $ sudo yum install cpan

    # Error
    Can't locate Switch.pm in @INC
    # Copied Switch.pm from my ubuntu machine to the perl lib on fedora

    # Error
    /usr/bin/ld: cannot find -lncurses
    $ sudo yum install ncurses-static

    # Error
    fatal error: libnet.h: No such file or directory
    $ sudo yum install libnet-devel

### TODO:

1. Run Selftests
2. Run Regression Tests
