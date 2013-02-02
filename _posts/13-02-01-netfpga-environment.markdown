---
layout: post
title: Setting up NetFPGA Development Environment
---
### Obtain Hardware

1. Buy the NetFPGA
2. Obtain a PC to use as the host Machine

### Obtain/Install Software

1. Install Fedora or other rpm based distro.
2. Install the the [RPMforge](http://wiki.centos.org/AdditionalResources/Repositories/RPMForge) repsoitory. // Necessary for Fedora?
3. Add the NetFPGA yum repository GPG Key:
<pre><code>
    rpm -Uhv http://netfpga.org/yum/el5/RPMS/noarch/netfpga-repo-1-1_CentOS5.noarch.rpm
</pre></code>
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


Sources:
http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/ObtainHardwareAndSoftware
http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/InstallSoftware
http://wiki.netfpga.org/foswiki/bin/view/NetFPGA/OneGig/VerifyHardwareAndSoftware
