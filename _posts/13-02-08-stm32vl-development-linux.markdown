---
layout: post
title: Using Linux with the STM32VL Discovery Board.
---
### Update

So the board we're using in class is actually the [STM32VL](www.st.com/stm32-discovery) board instead of the one I made a post about earlier.  The setup is essentially the same but there are some key differences I'd like to expand upon.  Without further adieu, the guide.

* Fork/Clone/Download the following repositories:

<pre><code>git clone git://github.com/esden/summon-arm-toolchain.git
git clone git://github.com/texane/stlink.git
git clone git://github.com/libopencm3/libopencm3.git
</code></pre>

* Install them using their guides.
    * [Summon Arm Toolchain (SAR)](https://github.com/Caustic/summon-arm-toolchain/blob/master/README.markdown)
    * [STLink](https://github.com/Caustic/stlink/blob/master/README.markdown)
    * [LibopenCM3](https://github.com/Caustic/libopencm3/blob/master/README)
* Setup linux to recognize boards.

    cp $STLINK_INST_DIR/stlink_v1.modprobe.conf /etc/modprobe.d/
    modprobe -r usb-storage && modprobe usb-storage
    cp $STLINK_INST_DIR/49-stlinkv1.rules /etc/udev/rules.d/
    udevadm control --reload-rules

* Plug in your STM32L Board.
* Start the STLink local server from the stlink repository.

    <pre><code>$STLINK_INST_DIR/st-util</code></pre>

* Flash the rom and run the program!:

    $ARM_TOOLS_BIN/arm-none-eabi-gdb program.elf
    (gdb) tar ex :4242
    (gdb) load
    (gdb) c

And thats it!  I've got my program up and running on my STM32VL board with hardly any effort at all!

### Considerations and Sources:

This is just a reference to get you started.  I wouldn't suggest using the linux toolchain over IAR if you're unfamiliar with linux.  If you have any questions, first refer to the respective guides, and if you can't find it there, feel free to ask me.

I did notice that instead of the stlink flashing program, another program called OpenOCD (heh) supports the STM32 line of boards as well.  I'm not sure if it's smoother than what I was able to do with the stlink program but its worth looking into.

[OpenOCD](http://openocd.sourceforge.net/)

[STLink for Linux](github.com/texane/stlink)

[SAR toolchain for Linux](github.com/esden/summon-arm-toolchain)

[Cortex M3 Open Library](github.com/libopencm3/libopencm3)

And some assorted blog posts:

http://sourcegate.wordpress.com/2012/09/18/getting-started-with-an-stm32l-discovery-with-linux-and-gcc/

http://electronics.stackexchange.com/questions/32991/how-do-i-develop-for-stm32-discovery-on-linux

http://gostm32.blogspot.com/
