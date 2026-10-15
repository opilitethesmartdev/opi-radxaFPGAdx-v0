---
title: "radxaFPGAdx"
github: "https://github.com/opilitethesmartdev/opi-radxaFPGAdx-v0"
description: "HAT for my Radxa Zero 3E featuring an FPGA"
created_at: "2026-10-15"
total_time: "42m"
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
