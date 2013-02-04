---
layout: post
title: Using Linux with the STM32L V2 Discovery Board.
---
### Purpose

So this semester I'm taking some classes that involve using the [STM32L board](http://www.st.com/internet/evalboard/product/250990.jsp) from STMicroelectronics.  I've used this embedded board before but last time I did, I found it didn't have great linux toolchain support (partially because I still wasn't a linux convert).

Today it appears that it has quite good linux toolchain support.  I was able to get my board up and running with some basic programs within a matter of one hour by just forking a couple repositories!  One important thing to note is that I've got a V2 board which means I don't need to program it through JTAG and can do everyting through usb instead.  Here are the steps I took for reference:

* Fork/Clone the following repositories:

<pre><code>git clone git://github.com/texane/stlink.git
git clone git://github.com/esden/summon-arm-toolchain.git
git clone git://github.com/libopencm3/libopencm3.git
</code></pre>

* Install them using their guides.
* Plug in your STM32L Board.
* Start the STLink local server from the stlink repository.
* Run:

<pre><code>$ARM_TOOLS_BIN/arm-none-eabi-gdb program.elf
(gdb) tar ex :4242
(gdb) load
(gdb) c
</code></pre>

And thats it!  I've got my program up and running on my STM32L board with hardly any effort at all!

### Considerations and Sources:

I did notice that instead of the stlink flashing program, another program called OpenOCD (heh) supported the STM32L as well.  I'm not sure if it's smoother than what I was able to do with the stlink program but its worth looking into.

[STLink for Linux](github.com/texane/stlink)

[SAR toolchain for Linux](github.com/esden/summon-arm-toolchain)

[Cortex M3 Open Library](github.com/libopencm3/libopencm3)

And some assorted blog posts:

http://sourcegate.wordpress.com/2012/09/18/getting-started-with-an-stm32l-discovery-with-linux-and-gcc/

http://electronics.stackexchange.com/questions/32991/how-do-i-develop-for-stm32-discovery-on-linux

http://gostm32.blogspot.com/
