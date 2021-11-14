---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: Creating micro:bit extensions for MakeCode
toc: true
hide_footer: true 

---
## Intro

This blog is a summary of my experience writing extensions for the micro:bit. I've really enjoyed contributing to the micro:bit community for a variety of reasons:

* I think the platform is really fantastic.  It's cheap, but quite powerful.  I think it's a great tool to make computing and computing hardware more accessible.
* Extensions can be technically challenging but  have a pretty small scope.  This is an area where I can contribute things that are really useful, but they are small enough to fit my limited free time.

I've written now written three official extensions and one "un-official" extensions.  Each has had different challenges and improved my ability to work with the platform:

* [Time & Date](https://makecode.microbit.org/pkg/bsiever/microbit-pxt-timeanddate) provides a software based real-time clock.  This extension required a deep understanding of the micro:bit's underlying clocks and run-time. Designing the blocks required careful consideration of semantics needed to work with "time" in a block-based language.
* [DSTemp](https://makecode.microbit.org/pkg/bsiever/microbit-dstemp) provides support for the Dallas Semiconductor (no Maxim) 18B20 temperature sensor.  This was developed to support science curricular materials for [WashU](https://wustl.edu/)'s [Institute for School Partnership](https://schoolpartnership.wustl.edu/).  The 18B20 has a unique serial protocol and requires precise timing.  This required a fair amount of low-level testing/debugging.
  * This [Video Overview](https://vimeo.com/445128371) shows an experiment using the extension and sensors.  Here's the guide for teachers: [mySci Extensions](https://docs.google.com/presentation/d/1CIyQK71pNGHjf5gfHqg3yD-sWP0rnXZlt6-MK9j_ISk/edit#slide=id.g5475e6f318_0_0)
  * I also made a [PCB carrier](https://github.com/bsiever/DS18B20Carrier) board to make it classroom-friendly:<br />![Carrier Board](https://github.com/bsiever/DS18B20Carrier/blob/main/ConnectedToMB.JPG?raw=true){: width="250" }
* [DSTemp 2-wire](https://makecode.microbit.org/pkg/bsiever/microbit-dstemp-2wire) is another variation that supports the 18B20.  There are a lot of [counterfeit](https://github.com/cpetrich/counterfeit_DS18B20) sensors that are sold as DS18B20s, but some genuine DS18B20s support "parasitic" power mode and can run without a separate power supply. I was able to get parasitic power mode to work with the micro:bit's internal pull-up.  Technically this isn't quite appropriate, but it has worked for my test cases and reduces the wiring to just two wires, which teachers can assemble themselves ([instructions here](https://github.com/bsiever/microbit-dstemp-2wire/blob/master/README.md)):<br /> ![](https://github.com/bsiever/microbit-dstemp-2wire/blob/master/docs/static/7_Final.jpg?raw=true){: width="250" }

The above are all "official" extensions that are listed in the MakeCode editor.  I've also done one "unofficial extension":
* [i2cPins](https://github.com/bsiever/microbit-pxt-i2cpins), which was sponsored by [MakeKit](https://www.makekit.no/), allows the external i2c on the micro:bit v2 to be re-directed to different pins. The heart of it is just 5 lines of C++, but it required a deep dive into the micro:bit runtime to figure out _which_ lines.




## Debugging

I use my "WebUSB" console example: [Console](https://bsiever.github.io/microbit-webusb/) ([source](https://github.com/bsiever/microbit-webusb))

1. Connect


## Error Codes

[Microbit.org Error Code list](https://support.microbit.org/support/solutions/articles/19000016969-micro-bit-error-codes)
[Device Error Codes](https://support.microbit.org/support/solutions/articles/19000016969-micro-bit-error-codes)
[DAL (v1]) ErrorNo.h](https://github.com/lancaster-university/microbit-dal/blob/master/inc/core/ErrorNo.h)
[CODAL Compatibility codes](https://github.com/lancaster-university/codal-microbit/blob/master/inc/compat/MicroBitCompat.h)
[CODAL Core ErrorNo.h](https://github.com/lancaster-university/codal-core/blob/master/inc/core/ErrorNo.h)


Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Orci dapibus ultrices in iaculis nunc sed. Scelerisque felis imperdiet proin fermentum leo. Risus nec feugiat in fermentum. Ligula ullamcorper malesuada proin libero nunc consequat. A cras semper auctor neque vitae tempus quam. Lacus sed viverra tellus in hac habitasse. Purus sit amet volutpat consequat mauris nunc. Ultricies leo integer malesuada nunc. Blandit cursus risus at ultrices mi. Mus mauris vitae ultricies leo integer. Laoreet id donec ultrices tincidunt arcu non. Bibendum enim facilisis gravida neque convallis a cras. Volutpat sed cras ornare arcu dui vivamus arcu felis. Hendrerit gravida rutrum quisque non tellus orci ac. Mauris a diam maecenas sed enim. In hendrerit gravida rutrum quisque non tellus orci ac auctor.

Scelerisque varius morbi enim nunc faucibus a pellentesque sit. Quis auctor elit sed vulputate. Cras sed felis eget velit aliquet sagittis id consectetur purus. Enim sit amet venenatis urna cursus eget nunc. A cras semper auctor neque vitae tempus. Amet commodo nulla facilisi nullam vehicula. Eu sem integer vitae justo eget. Vulputate ut pharetra sit amet aliquam. Risus sed vulputate odio ut enim blandit. Laoreet non curabitur gravida arcu ac tortor dignissim convallis aenean. Mattis ullamcorper velit sed ullamcorper morbi tincidunt ornare massa eget. Tristique senectus et netus et malesuada fames ac turpis egestas. Lorem sed risus ultricies tristique nulla aliquet enim tortor.

A arcu cursus vitae congue. Enim praesent elementum facilisis leo vel fringilla. Potenti nullam ac tortor vitae purus. Pulvinar mattis nunc sed blandit libero. Vitae aliquet nec ullamcorper sit amet risus nullam. Ornare lectus sit amet est placerat in egestas. Gravida cum sociis natoque penatibus et magnis dis parturient montes. In nisl nisi scelerisque eu. Et egestas quis ipsum suspendisse ultrices gravida. Porttitor leo a diam sollicitudin tempor id. Posuere urna nec tincidunt praesent. Quis viverra nibh cras pulvinar mattis nunc sed blandit libero. Dolor magna eget est lorem ipsum dolor sit amet consectetur. Risus feugiat in ante metus. Felis eget velit aliquet sagittis id consectetur purus ut faucibus. Mattis nunc sed blandit libero volutpat.

Vivamus at augue eget arcu. Ac ut consequat semper viverra nam libero justo laoreet. Ut eu sem integer vitae justo eget magna fermentum iaculis. Venenatis cras sed felis eget velit aliquet sagittis id. Turpis nunc eget lorem dolor sed. Elit scelerisque mauris pellentesque pulvinar pellentesque habitant. Amet venenatis urna cursus eget nunc scelerisque viverra. Justo nec ultrices dui sapien eget mi proin sed libero. Vulputate ut pharetra sit amet aliquam id diam maecenas ultricies. Commodo viverra maecenas accumsan lacus. Rhoncus mattis rhoncus urna neque viverra justo. Tempor nec feugiat nisl pretium fusce.

Faucibus purus in massa tempor nec. Neque volutpat ac tincidunt vitae semper. Nisl suscipit adipiscing bibendum est ultricies. Ipsum nunc aliquet bibendum enim facilisis gravida neque convallis. Nisl pretium fusce id velit. Lectus quam id leo in. Porta non pulvinar neque laoreet suspendisse interdum consectetur libero. Amet porttitor eget dolor morbi non arcu risus quis varius. Sed adipiscing diam donec adipiscing tristique. Mi ipsum faucibus vitae aliquet nec ullamcorper sit amet. Velit aliquet sagittis id consectetur purus ut faucibus pulvinar. Et leo duis ut diam quam.


## This is second

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget est lorem ipsum dolor sit amet. A iaculis at erat pellentesque adipiscing commodo. Amet mauris commodo quis imperdiet massa tincidunt nunc pulvinar sapien. Fermentum et sollicitudin ac orci phasellus egestas tellus rutrum. Sapien pellentesque habitant morbi tristique senectus et. Tellus mauris a diam maecenas sed enim ut sem viverra. Praesent elementum facilisis leo vel. Urna cursus eget nunc scelerisque viverra mauris. Id cursus metus aliquam eleifend. Vel risus commodo viverra maecenas accumsan. Auctor neque vitae tempus quam pellentesque nec nam aliquam. Ut morbi tincidunt augue interdum velit euismod. Nulla facilisi etiam dignissim diam quis enim lobortis scelerisque. Sit amet nulla facilisi morbi tempus iaculis. Sem fringilla ut morbi tincidunt augue interdum. Quis viverra nibh cras pulvinar mattis nunc sed blandit libero. Nunc lobortis mattis aliquam faucibus purus in. Ut morbi tincidunt augue interdum velit.

Cursus turpis massa tincidunt dui. Fermentum odio eu feugiat pretium nibh. Augue ut lectus arcu bibendum at varius vel pharetra. Ac placerat vestibulum lectus mauris ultrices eros. Adipiscing enim eu turpis egestas pretium aenean. Commodo nulla facilisi nullam vehicula ipsum a arcu cursus vitae. Risus nullam eget felis eget nunc. Natoque penatibus et magnis dis parturient. Ornare lectus sit amet est placerat in. Eget dolor morbi non arcu risus quis. Quis blandit turpis cursus in.

## third

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget est lorem ipsum dolor sit amet. A iaculis at erat pellentesque adipiscing commodo. Amet mauris commodo quis imperdiet massa tincidunt nunc pulvinar sapien. Fermentum et sollicitudin ac orci phasellus egestas tellus rutrum. Sapien pellentesque habitant morbi tristique senectus et. Tellus mauris a diam maecenas sed enim ut sem viverra. Praesent elementum facilisis leo vel. Urna cursus eget nunc scelerisque viverra mauris. Id cursus metus aliquam eleifend. Vel risus commodo viverra maecenas accumsan. Auctor neque vitae tempus quam pellentesque nec nam aliquam. Ut morbi tincidunt augue interdum velit euismod. Nulla facilisi etiam dignissim diam quis enim lobortis scelerisque. Sit amet nulla facilisi morbi tempus iaculis. Sem fringilla ut morbi tincidunt augue interdum. Quis viverra nibh cras pulvinar mattis nunc sed blandit libero. Nunc lobortis mattis aliquam faucibus purus in. Ut morbi tincidunt augue interdum velit.

Cursus turpis massa tincidunt dui. Fermentum odio eu feugiat pretium nibh. Augue ut lectus arcu bibendum at varius vel pharetra. Ac placerat vestibulum lectus mauris ultrices eros. Adipiscing enim eu turpis egestas pretium aenean. Commodo nulla facilisi nullam vehicula ipsum a arcu cursus vitae. Risus nullam eget felis eget nunc. Natoque penatibus et magnis dis parturient. Ornare lectus sit amet est placerat in. Eget dolor morbi non arcu risus quis. Quis blandit turpis cursus in.
## 4th

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Eget est lorem ipsum dolor sit amet. A iaculis at erat pellentesque adipiscing commodo. Amet mauris commodo quis imperdiet massa tincidunt nunc pulvinar sapien. Fermentum et sollicitudin ac orci phasellus egestas tellus rutrum. Sapien pellentesque habitant morbi tristique senectus et. Tellus mauris a diam maecenas sed enim ut sem viverra. Praesent elementum facilisis leo vel. Urna cursus eget nunc scelerisque viverra mauris. Id cursus metus aliquam eleifend. Vel risus commodo viverra maecenas accumsan. Auctor neque vitae tempus quam pellentesque nec nam aliquam. Ut morbi tincidunt augue interdum velit euismod. Nulla facilisi etiam dignissim diam quis enim lobortis scelerisque. Sit amet nulla facilisi morbi tempus iaculis. Sem fringilla ut morbi tincidunt augue interdum. Quis viverra nibh cras pulvinar mattis nunc sed blandit libero. Nunc lobortis mattis aliquam faucibus purus in. Ut morbi tincidunt augue interdum velit.

Cursus turpis massa tincidunt dui. Fermentum odio eu feugiat pretium nibh. Augue ut lectus arcu bibendum at varius vel pharetra. Ac placerat vestibulum lectus mauris ultrices eros. Adipiscing enim eu turpis egestas pretium aenean. Commodo nulla facilisi nullam vehicula ipsum a arcu cursus vitae. Risus nullam eget felis eget nunc. Natoque penatibus et magnis dis parturient. Ornare lectus sit amet est placerat in. Eget dolor morbi non arcu risus quis. Quis blandit turpis cursus in.
### 4B

This is a test...
