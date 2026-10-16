---
title: "radxaFPGAdx"
github: "https://github.com/opilitethesmartdev/opi-radxaFPGAdx-v0"
description: "HAT for my Radxa Zero 3E featuring an FPGA"
created_at: "2026-10-15"
total_time: "2h 36m"
---

# October 15, 2026: Set up the project
<!-- fabricate:entry 491 -->

I set up the KiCad project and GitHub repository, wrote a medium-short README, then went on the hunt for the Gowin GW1NR-LV9 FPGA files. Because while the Gowin does have better price2perf ratio than the MAXII i wanted to take, it is proportionately less available.
I had to go through a pretty sketch process from a Mouser app, Library Loader:
![](https://fabricate.hackclub-assets.com/dd973f5373198a7635c55d905f6150c4138ab3b80c3275e98b996114765c23a2/image-png/image.png)
And there was some struggles / issues / crashes, until i (somehow tbh) finally managed to get it loaded:
![](https://fabricate.hackclub-assets.com/80ba40c35b5b094083575237885803183a51458f10eca463953d26a58806b33d/image-png/image.png)
(and a cool thing i just now noticed is that the IOs are named by their position on the chip - which is cool because i dont have to compare to the footprint each time)

Timelapse: https://lapse.hackclub.com/timelapse/eM9td_A0Eja8

**Total time spent: 42m**

# October 16, 2026: Added some components, researched powering
<!-- fabricate:entry 524 -->

I added some of the components i was planning, like an ATmega16u4, the pin header, and two USB ports, because if i'm doing an fpga hat then i wanna make sure i can potentially use USB - especially since the atmega also has a usb interface.
![](https://fabricate.hackclub-assets.com/1b0125f79cedde4f990e8a4dcb543d90378b945c66cd8840088bf4239eadc9a7/image-png/image.png)
*(Components i've added: the FPGA (for which i also finally configured the footprint, the ATmega, the usbs, and a power mux for the usbs)*

However, soon came the question of power - the simplest solution was to just not connect vbus - but thats mid. simply wiring the VBUS to the power rail - which could mean my radxa gets them shoved in its poor PMIC - is kinda not a good idea (so i've heard), but the one thing i REALLY dont like is having multiple usb cables - i HATE that. And yet, there doesnt seem to be a wonderful "integrated 3 channel power mux where one channel can be the source".
Meaning, we need our custom solutions.

Luckily, with the help of chatty (to be specific, chatty only said "we need a discrete transistor solution", and i did the rest myself), i tinkered around this rigid online circuit simulator and came up with this rather simple design:
![](https://fabricate.hackclub-assets.com/80d630c495a56ab3ba8915ff48885c58872b7feaad9fd687640b14e4a62f7cd1/image-png/image.png)
*you can try it for yourself:*
https://lapse.hackclub.com/timelapse/Aux67nB0mxHi

Each switch represents a power supply input - the left LED represents our HAT, the right LED represents the Radxa. As we can see- well we cant really see it like that, let me show you here:
![](https://fabricate.hackclub-assets.com/c1f126e30e7aa48dbd8cf6449c06f8d12269a164b518f0291361667e96f4d2f4/image-png/image.png)
*(Note how the yellow dots between each source and their load are blurred while the dots between them arent)*
As we can see, when both sources are on, each only feeds their respective load, and no cross sharing (the sim says 400 nA leak, but chatty says that's actually good).
And when only one source is on, it automatically feeds the other's load:
![](https://fabricate.hackclub-assets.com/355f5e6275e143481461eaa50c264fdacbc95ae4120bcefd0f7cd2d8688fea32/image-png/image.png)
![](https://fabricate.hackclub-assets.com/8e63530e55303ec9d4ebfa768b4b60a7561bf7155be1c92d8cced0cdc653340b/image-png/image.png)
But i'd really want to test that first, so i'm actually thinking of making it a different project

Timelapse: https://lapse.hackclub.com/timelapse/Aux67nB0mxHi

**Total time spent: 1h 54m**
