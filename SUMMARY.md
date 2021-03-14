# Table of contents

* [Initial page](README.md)

## LANGUAGE <a id="programming-language"></a>

* [C/C++](programming-language/c-c++.md)
* [Javascript](programming-language/javascript/README.md)
  * [OLDER](programming-language/javascript/older.md)
  * [ES6](programming-language/javascript/es6.md)

## Multimedia

* [Codec](multimedia/h264/README.md)
  * [영상 압축기술의 발전과 기초지식](multimedia/h264/h264_02-bbb.md)
  * [\[01\] Q/A로 배우는 \[H264/AVC\]의 기초](multimedia/h264/h264_01-aaa.md)
  * [예측과 양자화](multimedia/h264/5.md)

## Library/Framework

* [FFmpeg](library-framework/ffmpeg/README.md)
  * [Windows에서 FFmpeg 빌드하기](library-framework/ffmpeg/windows-ffmpeg.md)
  * [FFmpeg Source 분석](library-framework/ffmpeg/ffmpeg-source/README.md)
    * [Core Structure](library-framework/ffmpeg/ffmpeg-source/core-structure.md)
    * [Decoding process](library-framework/ffmpeg/ffmpeg-source/decoding-process/README.md)
      * [avformat\_open\_input\(\)](library-framework/ffmpeg/ffmpeg-source/decoding-process/avformat_open_input.md)
      * [avformat\_find\_stream\_info\(\), avcodec\_find\_decoder\(\), avcodec\_open2\(\)](library-framework/ffmpeg/ffmpeg-source/decoding-process/avformat_find_stream_info-avcodec_find_decoder-avcodec_open2.md)
      * [av\_read\_frame\(\), avcodec\_send\_packet\(\)/avcodec\_receive\_frame\(\)](library-framework/ffmpeg/ffmpeg-source/decoding-process/av_read_frame-avcodec_send_packet-avcodec_receive_frame.md)
    * [Encoding Process](library-framework/ffmpeg/ffmpeg-source/encoding-process/README.md)
      * [avformat\_alloc\_output\_context2\(\)](library-framework/ffmpeg/ffmpeg-source/encoding-process/avformat_alloc_output_context2.md)
      * [avio\_open2\(\)](library-framework/ffmpeg/ffmpeg-source/encoding-process/avio_open2.md)
      * [avformat\_write\_header\(\)](library-framework/ffmpeg/ffmpeg-source/encoding-process/avformat_write_header.md)
      * [avcodec\_send\_frame\(\) / avcodec\_receive\_packet\(\)](library-framework/ffmpeg/ffmpeg-source/encoding-process/avcodec_send_frame-avcodec_receive_packet.md)
      * [av\_write\_frame\(\) / av\_interleaved\_write\_frame\(\)](library-framework/ffmpeg/ffmpeg-source/encoding-process/av_write_frame-av_interleaved_write_frame.md)
      * [av\_write\_trailter\(\)](library-framework/ffmpeg/ffmpeg-source/encoding-process/av_write_trailter.md)
* [DirectShow](library-framework/directshow/README.md)
  * [Introduction](library-framework/directshow/introduction.md)
  * [Building Filter Graph](library-framework/directshow/building-filter-graph.md)
  * [Data Flow](library-framework/directshow/data-flow.md)
  * [Control / Event Handling / Clock](library-framework/directshow/control.md)
* [Media Foundation](library-framework/media-foundation/README.md)
  * [Introduction](library-framework/media-foundation/introduction.md)
  * [Media Foundation Transforms](library-framework/media-foundation/media-foundation-transforms.md)
  * [Media Foudation Sources](library-framework/media-foundation/media-foudation-sources.md)
  * [Media Foundation Sinks](library-framework/media-foundation/media-foundation-sinks.md)
  * [Custom Media Sessions](library-framework/media-foundation/custom-media-sessions.md)

## BACKEND

* [NodeJS](backend/nodejs.md)

## etc

* [CMake](etc/cmake.md)
* [Googletest](etc/googletest.md)
* [Media Container](etc/media-container/README.md)
  * [MPEG-4 Container](etc/media-container/mpeg-4-container.md)
* [Multimedia Framework Data Flow Model](etc/multimedia-framework-data-flow-model.md)
* [Image Filtering](etc/image-filtering.md)

