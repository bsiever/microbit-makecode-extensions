---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: Creating micro:bit extensions for MakeCode
toc: true
hide_footer: true 

---

## Intro

This is a summary of my experiences writing extensions for the micro:bit.  I've really enjoyed contributing to the micro:bit community for a variety of reasons:

* I think the platform is  fantastic.  It's a cheap, powerful tool to make computing and "making" more accessible.
* Extensions can be technically challenging, but they have a small scope.  This combination allows me to use my technical skills to provide useful things in a way that fits my limited free time.

## My Extensions

I've written three official extensions and one un-official extensions.  Each has had different challenges and improved my ability to work with the platform

### Time & Date

[Time & Date](https://makecode.microbit.org/pkg/bsiever/microbit-pxt-timeanddate) provides a software based real-time clock.  This extension required a deep understanding of the micro:bit's underlying clocks and run-time. Designing the blocks required careful consideration of semantics needed to work with time in a block-based language.

### DSTemp

[DSTemp](https://makecode.microbit.org/pkg/bsiever/microbit-dstemp) provides support for the Dallas Semiconductor (now Maxim) 18B20 temperature sensor.  This was created for [WashU](https://wustl.edu/)'s [Institute for School Partnership](https://schoolpartnership.wustl.edu/)(ISP), which developed science curricular materials that require recording temperature over time.

This [Video Overview](https://vimeo.com/445128371) shows an experiment using the extension and two sensors.  Here's the guide for teachers developed by the ISP: [mySci Extensions](https://docs.google.com/presentation/d/1CIyQK71pNGHjf5gfHqg3yD-sWP0rnXZlt6-MK9j_ISk/edit#slide=id.g5475e6f318_0_0)

The 18B20 has a unique serial protocol and requires precise timing.  This required a fair amount of low-level testing/debugging.

I also made a [PCB carrier](https://github.com/bsiever/DS18B20Carrier) board to make it classroom-friendly:<br />![Carrier Board](https://github.com/bsiever/DS18B20Carrier/blob/main/ConnectedToMB.JPG?raw=true){: width="250" }

### DSTemp 2-wire

[DSTemp 2-wire](https://makecode.microbit.org/pkg/bsiever/microbit-dstemp-2wire) is another variation that supports the 18B20.  There are a lot of [counterfeit](https://github.com/cpetrich/counterfeit_DS18B20) sensors that are sold as DS18B20s, but some genuine DS18B20s support "parasitic" power mode and can run without a separate power supply. I was able to get parasitic power mode to work with the micro:bit's internal pull-up.  Technically this isn't quite appropriate, but it has worked for my test cases and reduces the wiring to just two wires, which teachers can assemble themselves ([instructions here](https://github.com/bsiever/microbit-dstemp-2wire/blob/master/README.md)):<br /> ![](https://github.com/bsiever/microbit-dstemp-2wire/blob/master/docs/static/7_Final.jpg?raw=true){: width="250" }

### i2c Pins

[i2cPins](https://github.com/bsiever/microbit-pxt-i2cpins), which was sponsored by [MakeKit](https://www.makekit.no/), allows the external i2c on the micro:bit v2 to be re-directed to different pins. The heart of it is just 5 lines of C++, but it required a deep dive into the micro:bit runtime to figure out _which_ lines.

Unlike the others, I haven't asked to have "i2c Pins" considered for an official extension (yet).

## Getting Started

### Dev Tools

Extensions can be developed [entirely in MakeCode](https://www.youtube.com/watch?v=ztrm4XehfGo), which is a pretty good approach for purely TypeScript-based extensions.  I think it's a poor choice for extensions that use C++ (like all of mine) for two reasons:
1. You don't get feedback on C++ compilation errors!
2. It uses a cloud-based build system, which is very slow.

Consequently, I use a local build system.  

#### Installing local build system (macOS on an M1)

1. Install [Homebrew](https://brew.sh/)
2. Install [Node.js](https://nodejs.org/en/)
3. Open a terminal window and use `npm` to install [`pxt`](https://github.com/microsoft/pxt): `npm install -x pxt`.
   * `pxt` is the command line interface for the "Programming eXperience Toolkit", which is the name of MicroSoft's open source editor (MakeCode).

There are two ways to do a local build:  
1. Using a [Docker](https://en.wikipedia.org/wiki/Docker_(software)) image that contains the build system.  In my experience this was slow and still made it difficult to get compiler feedback.
2. Using [`yotta`](https://yottabuild.org/). Yotta was meant to provide a cross-platform build system for ARM mBed targets.  Yotta is now depricated and is not longer being updated/maintained. None the less, I build extensions with Yotta.

To install yotta:

1. Install needed packages and the ARM compiler: `brew install cmake ninja arm-none-eabi-gcc`
2. Install `srecord`: `brew install srecord`
3. Install `yotta` (which is a python package): `sudo pip3 install yotta`
4. I am working on an M1 mac.  When I installed there were some inconsistencies:
   1. I had to edit two of the yotta files, `/opt/homebrew/lib/python3.9/site-packages/yotta/lib/[pack,target].py` and remove the `@fsutils.dropRootPrivs` annotation (See [Yotta Issue #863](https://github.com/ARMmbed/yotta/issues/863))
   2. `cmake` wasn't handling the M1 architecture correctly.  I had to edit `/opt/homebrew/Cellar/cmake/3.20.1/share/cmake/Modules/Platform/Darwin-Initialize.cmake` and comment out `set(_CMAKE_APPLE_ARCHS_DEFAULT "${CMAKE_HOST_SYSTEM_PROCESSOR}")` (which was on line #36 for me)

## Projects

I start by cloning an existing project and updating settings as needed.  Usually I start with my [DSTemp](https://github.com/bsiever/microbit-dstemp) extension since it is relatively simple.  It has just two blocks, both a TypeScript and a C++ file, and shows how to connect a part in the simulator.


### Files

Although this isn't very significant, I start by changing file names.  I rename `dstemp.ts` and `dstemp.cpp` to reflect my new project. If the new project won't use a simulator image, remove the `parts` directory and files.  Otherwise rename and edit them. 

### pxt.json

The `pxt.json` is the magic that describes the entire structure of the repo.  Here's the description of the interface/structure: https://github.com/microsoft/pxt/blob/master/docs/extensions/pxt-json.md

Update the main descriptive items (`name`, `version`, `description`, and `dependencies`).  If any files were renamed, be sure to update them (`files`).  




## Running (w/ Yotta)

### Command Line Build

```
export PXT_NODOCKER=1
pxt build --local 
```

Note that this builds for both DAL and CODAL.  
### Command Line Build & Deploy

```
export PXT_NODOCKER=1
pxt deploy --local 
```

### Local Server

```
export PXT_NODOCKER=1
pxt serve --local
```

### CODAL vs. DAL

```
#if MICROBIT_CODAL
#else
#endif
```

### Bluetooth

```
        // May also be using 24-bit timer
#ifdef SOFTDEVICE_PRESENT
        if (!ble_running()) // Only configTimer if either no soft-dev or no ble
#endif
                configTimer();
#endif
```

## Debugging

I use my "WebUSB" console example: [Console](https://bsiever.github.io/microbit-webusb/) ([source](https://github.com/bsiever/microbit-webusb)).  It can't be used while MakeCode is connected to the micro:bit. 

1. Connect


## Error Codes

* [Microbit.org Error Code list](https://support.microbit.org/support/solutions/articles/19000016969-micro-bit-error-codes)
* [Device Error Codes](https://support.microbit.org/support/solutions/articles/19000016969-micro-bit-error-codes)
* [DAL (v1) ErrorNo.h](https://github.com/lancaster-university/microbit-dal/blob/master/inc/core/ErrorNo.h)
* [CODAL Compatibility codes](https://github.com/lancaster-university/codal-microbit/blob/master/inc/compat/MicroBitCompat.h)
* [CODAL Core ErrorNo.h](https://github.com/lancaster-university/codal-core/blob/master/inc/core/ErrorNo.h)

## MicroBit Sources

### Codal

* [MicroBit.h](https://github.com/lancaster-university/codal-microbit-v2/blob/master/model/MicroBit.h) and [MicroBit.cpp](https://github.com/lancaster-university/codal-microbit-v2/blob/master/model/MicroBit.cpp) define the `uBit` object. 
* 