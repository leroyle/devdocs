---
description: Helium development using PlatformIO within Visual Studio Code
---

# Getting started with Helium and PlatformIO

![](../.gitbook/assets/artboard-copy-63.jpg)

### PlatformIO - An Easier Way to Develop Embedded Applications 

[PlatformIO ](https://platformio.org/)is a cross-platform, cross-architecture, multiple framework, professional tool for embedded systems engineers and for software developers who write applications for embedded products.

[PlatformIO ](https://platformio.org/)provides developers with a modern integrated development environment \([Cloud & Desktop IDE](https://docs.platformio.org/en/latest/integration/ide/index.html#ide)\) that works cross-platform to:
- support many different software development kits \(SDKs\)
- provide access to various [Frameworks](https://docs.platformio.org/en/latest/frameworks/index.html#frameworks)
- allow sophisticated debugging \([PIO Unified Debugger](https://docs.platformio.org/en/latest/plus/debugging.html#piodebug)\)
- enable unit testing \([PIO Unit Testing](https://docs.platformio.org/en/latest/plus/unit-testing.html#unit-testing)\)
- support automated code analysis \([PIO Check](https://docs.platformio.org/en/latest/plus/pio-check.html#piocheck)\)
- enable remote management \([PIO Remote](https://docs.platformio.org/en/latest/plus/pio-remote.html#pioremote)\).

It is architected to maximize flexibility and choice by developers, who can use either graphical or command line editors \([PlatformIO Core \(CLI\)](https://docs.platformio.org/en/latest/core/index.html#piocore)\), or both.

If you are used to developing using the Arduino IDE but constantly feel constrained by the environment, you are going to love what [PlatformIO ](https://platformio.org/)opens up for you.

![](../.gitbook/assets/image%20%285%29%20%282%29%20%281%29.png)



This guide will walk through installing PlatformIO and deploying a Helium Arduino program on a target device.
Here, as an example, we will detail the steps required to integrate a specific board type, the [ST Discovery Development Kit](../devices/devkit/).

However, this guide can be also used to on-board many other types of target devices. In most cases one can just substitute your target device in place of the ST developer board.

If there are extensive differences they can be found within documentation provided for supported target device examples.


### Installing PlatformIO

[Download ](https://code.visualstudio.com/)and install Microsoft's Visual Studio Code, PlatformIO IDE is built on top of it as an extension.

{% embed url="https://code.visualstudio.com/\#alt-downloads" %}

1. Open VSCode Extension Manager
2. Search for official PlatformIO IDE extension
3. Install PlatformIO IDE. \([https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide](https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide)\)

![](../.gitbook/assets/image%20%2869%29.png)

It is highly recommended to give the quick-start guide a read. It will help you navigate the new interface. [https://docs.platformio.org/en/latest/integration/ide/vscode.html\#quick-start](https://docs.platformio.org/en/latest/integration/ide/vscode.html#quick-start)

In this tutorial, as an example we will be using the [Helium Developer Kit](https://developer.helium.com/devices/devkit). One can substitue your target device as needed.

![](../.gitbook/assets/image%20%2817%29.png)

Once PlatformIO is installed, you should be welcomed to VSCode with the following "PIO Home" screen:

![](../.gitbook/assets/image%20%2879%29.png)

### Starting a new PlatformIO Project
#### Project Wizard

Let's click on "New Project" to get started.

Enter a project name and select the following board:

![](../.gitbook/assets/pio001%20%281%29.png)
Note: If your target device is different start to enter the device manufacturer in the "Board" field, PlatformIO will attempt to fill in the entry with those devices that it is aware of. Hopefully your device will be presented in the list. If so, select it.

The target devices will support one or more runtime frameworks. Choose what is appropriate for your target.
Our example will be using the Arduino Framework, so ensure it is selected and click "Finish".

At this point PlatformIO will download any runtime support libraries that may be missing. Thus the first time you create a project with a new device or framework this step will take a bit longer. 

#### File Explorer
You should soon be left with a project that looks as follows:

![](../.gitbook/assets/pio002.png)

#### Project Sources

If we look into `src/main.cpp`, we see the familiar empty Arduino sketch structure:

![](../.gitbook/assets/pio003.png)
Note: PlatformIO does not under the covers include "Arduino.h", thus you will notice it is included specifically inside this sample.

#### platformio.ini

Let's take a second here to look at the `platformio.ini` file in the root of our new project:

![](../.gitbook/assets/pio004.png)

This is where one defines project configuration definitions. In the Arduino world one would do this via the IDE tool bar. Note: when this file is modified the entire project will be rebuilt when the project is next built or uploaded.

Notice that we specify the environment that we are going to be developing in using the following variables:

* platform
* board
* framework

These defines will be different depending upon which target platform you are implementing. Refer to provided sample target device documentation for details.

#### Build the sample project

At this point, you may click the **PlatformIO Build** checkbox in the status bar, and the project will build \(just don't expect it to do anything yet\):

![](../.gitbook/assets/image%20%287%29.png)

You may notice something unexpected here \(but very cool, and we will get into that here in just a bit\):


![](../.gitbook/assets/pio005.png)

![](../.gitbook/assets/pio007.png)

Due to the defines Within platformio.ini, PlatformIO is able to determine the project board and framework dependencies. Any missing dependencies are automatically installed at build time, thus this process may be see in the build output. This feature allows us to add libraries into our platformio.ini file, and they will be added in for us at build time.

#### Show attached devices

If, on the **PIO Home** page, you select the "Devices" icon on the left, you will see the physical devices that are connected to your development machine, and what ports they are connected to:

![](../.gitbook/assets/image%20%2873%29.png)

#### Uploading binary to target device#

Now that the code has built successfully, if a target device is attached to your computer the resulting binary can be uploaded to the target device.

Prior to attempting to upload your binary make sure any terminal session that might be attached to the debug comm port has been deleted. Occasionally but not always, PlatformIO will automatically close the comm port. If it does not upload errors will occur.

## LAL Add button
Click on the Upload button within the bottom Status bar.

Below you will see a typical output as the binary is uploaded to the target board.

## LAL add output


#### Supporting JLink within Platformio

Notice that under **Description**, it says we are running "JLink" rather than "ST-Link". If we were to attempt to flash the board at this point, we would get a failure that looked like this:

```text
Configuring upload protocol...
AVAILABLE: blackmagic, jlink, mbed, stlink
CURRENT: upload_protocol = stlink
Uploading .pio\build\disco_l072cz_lrwan1\firmware.elf
xPack OpenOCD, 64-bit Open On-Chip Debugger 0.10.0+dev (2019-07-17-11:28)
Licensed under GNU GPL v2
For bug reports, read
        http://openocd.org/doc/doxygen/bugs.html
debug_level: 1

srst_only separate srst_nogate srst_open_drain connect_deassert_srst

Error: open failed
in procedure 'program'
** OpenOCD init failed **
shutdown command invoked

*** [upload] Error 1
===================================================================================== [FAILED] Took 16.63 seconds =====================================================================================
The terminal process terminated with exit code: 1

```

What happened here? Well, we have this board set up to use a `SEGGER JTAG` interface rather than the `ST-Link` interface that is integrated into the Discovery board. There are a number of advantages of this approach, and I would _highly_ suggest doing this. It will make your development iteration process much faster.

Luckily, `SEGGER` has provided a method to \(non-destructively\) replace the ST-Link on our board with a JTAG interface.

![](../.gitbook/assets/image%20%288%29%20%281%29%20%281%29.png)

[Head here](https://www.segger.com/products/debug-probes/j-link/models/other-j-links/st-link-on-board/) to walk through the simple process. 

We then need to add one additional line to our `platformio.ini` file to let PlatformIO know that we will be using a JTAG interface to our board \(written as `jlink` in your file\):

![](../.gitbook/assets/pio006.png)

The next time we build and attempt to upload our project, we will be presented with the following Terms of Use:

![](../.gitbook/assets/image%20%2829%29.png)

Accept this agreement, and you should see the following popup:

![](../.gitbook/assets/image%20%2885%29.png)

And there you have it. At this point, we have successfully programmed an empty sketch onto our Helium Developer Kit using PlatformIO!  Check out the [Helium LongFi PlatformIO repo](https://github.com/helium/longfi-platformio) for some example programs to get you started.

**Go forth and build magical things.** 



