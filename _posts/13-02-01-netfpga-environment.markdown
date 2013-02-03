---
layout: post
title: Setting up NetFPGA Development Environment
---
### Obtain Hardware

1. Buy the NetFPGA
stuff
2. Obtain a PC to use as the host Machine

### Obtain/Install Software

1. Install Fedora or other rpm based distro.
2. Install the the [RPMforge](http://wiki.centos.org/AdditionalResources/Repositories/RPMForge) repsoitory. // Necessary for Fedora?
3. Add the NetFPGA yum repository GPG Key 
    <pre><code>rpm -Uhv http://netfpga.org/yum/el5/RPMS/noarch/netfpga-repo-1-1_CentOS5.noarch.rpm</code></pre>
4. Install the NetFPGA Base package: `yum -y install netfpga-base`
5. Install the [Java GUI](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/InstallJavaGUI20).
6. Create a local user NetFPGA account by running the following command.  WARNING: Back up your data! `/usr/local/netfpga/lib/scripts/user_account_setup/user_account_setup.pl`
This creates some environment variables:

        NF_ROOT
        NF_DESIGN_DIR
        NF_WORK_DIR
        PYTHONPATH
        PERL5LIB

### Install from git

1. `git clone git@github.com:Caustic/netfpga.git`
2. You'll need some bitfiles from [the netfpga wiki](http://wiki.netfpga.org/foswiki/NetFPGA/OneGig/Releases) Copy the `cpci*.bit` bitfiles from the tgz release. just copy all bitfiles from their bitfile directory into your ~/netfpga/bitfiles.
3. Plug in the NetFPGA and boot up!  If it crashes the first boot, reboot and it should work fine. //What?!
4. add `uppermem 524288` and `vmalloc=256M` to `/boot/grub/grub.conf` and reboot. [Found here](http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/InstallSoftware10) // Still necessary?
5. Add the necessary NF\_ Environment variables: `source bashrc_addon.sh`
6. Create simlinks for system binaries.
    <pre><code># ln -s ~/netfpga /usr/local/netfpga
    # ln -s /usr/local/netfpga/lib/scripts/cpci_config_reg_access/loadregs.sh /usr/lcoal/sbin/loadregs.sh
    # ln -s /usr/local/netfpga/lib/scripts/cpci_config_reg_access/dumpregs.sh /usr/local/sbin/dumpregs.sh
    </code></pre>

7. Install the driver
    <pre><code>$ cd ~/netfpga/lib/C
    $ make
    $ sudo make install
    $ modprobe nf2
    </code></pre>

8. Check to see if things work
    <pre><code>$ ~/netfpga/lib/scripts/cpci_config_reg_access/dumpregs.sh -f ~/defaultregs # for problem recovery
    $ ~/netfpga/lib/scripts/cpci_config_reg_access/loadregs.sh -f ~/defaultregs # do this if cpci_reprogram fails half way
    $ sudo ~/netfpga/lib/scripts/cpci_reprogram.pl
    $ sudo /usr/local/bin/nf_download /usr/local/netfpga/bitfiles/reference_nic.bit
    </code></pre>

9. Add some stuff to /etc/rc.local as follows. //???
    <pre><code>/usr/local/netfpga/lib/scripts/cpci_reprogram.pl
    /usr/local/bin/nf_download /usr/local/netpfga/reference_nic.bit
    ifconfig nf2c[0-3] 10.0.1[0-3].1/24 for the 4 ports

10. Note: if you forget to run `cpci_reprogram` with root permissions, it will hang your card and you'll need to reboot and run the `loadregs.sh` command above.



####Sources:

http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/ObtainHardwareAndSoftware
http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/InstallSoftware
http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/VerifyHardwareAndSoftware


### Issues I had (Fedora 17 vanilla install):

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

