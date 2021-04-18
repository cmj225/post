# Intro

### FFmpeg

A complete, cross-platform solution to record, convert and stream audio and video.

FFmpeg is the leading multimedia framework, able to **decode**, **encode**, **transcode**, **mux**, **demux**, **stream**, **filter** and **play** pretty much anything that humans and machines have created. It supports the most obscure ancient formats up to the cutting edge. No matter if they were designed by some standards committee, the community or a corporation. It is also highly portable: FFmpeg compiles, runs, and passes our testing infrastructure [FATE](http://fate.ffmpeg.org/) across Linux, Mac OS X, Microsoft Windows, the BSDs, Solaris, etc. under a wide variety of build environments, machine architectures, and configurations.                                                             `-> FFmpeg 이란?`

 It contains **libavcodec, libavutil, libavformat, libavfilter, libavdevice, libswscale** and **libswresample** which can be used by applications.                                                                                                                                            

* **libavutil** is a library containing functions for simplifying programming, including random number generators, data structures, mathematics routines, core multimedia utilities, and much more.
* **libavcodec** is a library containing **decoders** and **encoders** for audio/video codecs.
* **libavformat** is a library containing **demuxers** and **muxers** **for multimedia container formats.**
* **libavdevice** is a library containing **input and output devices** for grabbing from and rendering to many common multimedia input/output software frameworks, including **Video4Linux, Video4Linux2, VfW, and ALSA**.
* **libavfilter** is a library containing **media filters**.
* **libswscale** is a library performing **highly optimized image scaling** and **color space/pixel format conversion** operations. `-> SW based`
* **libswresample** is a library performing **highly optimized audio resampling, rematrixing** and **sample format conversion** operations.

`-> FFmpeg Libraries`

As well as **ffmpeg, ffplay** and **ffprobe** which can be used by end users for **transcoding** and **playing**.

* **ffmpeg** is a command line tool to convert multimedia files between formats.
* **ffplay** is a simple player based on [**SDL**](https://www.libsdl.org/) and the FFmpeg libraries.
* **ffprobe** is a simple multimedia stream analyzer.

 `-> FFmpeg Tools`



### Reference

{% embed url="https://ffmpeg.org/" %}

{% embed url="https://github.com/FFmpeg/FFmpeg" %}

{% embed url="https://ffmpeg.org/doxygen/4.1/index.html" %}



