# Table of contents

* [Initial page](README.md)

## Language <a id="programming-language"></a>

* [C++](programming-language/c-c++/README.md)
  * [Reference](programming-language/c-c++/reference.md)
* [Golang](programming-language/golang/README.md)
  * [Reference](programming-language/golang/reference.md)
* [Javascript](programming-language/javascript/README.md)
  * [Reference](programming-language/javascript/reference.md)
  * [OLDER](programming-language/javascript/older.md)
  * [ES6](programming-language/javascript/es6.md)

## Multimedia

* [Container](multimedia/container/README.md)
  * [.ts](multimedia/container/.ts.md)
  * [.fmp4](multimedia/container/.fmp4.md)
  * [.mp4](multimedia/container/.mp4.md)
  * [.cmaf](multimedia/container/.cmaf.md)
* [Codec](multimedia/h264/README.md)
  * [Video/Audio Compression](multimedia/h264/h264_02-bbb.md)
  * [PCM](multimedia/h264/pcm/README.md)
    * [Chroma Subsampling](multimedia/h264/pcm/chroma-subsampling.md)
  * [Predicative Coding](multimedia/h264/predicative-coding/README.md)
    * [DPCM](multimedia/h264/predicative-coding/dpcm.md)
  * [Motion Compensate](multimedia/h264/motion-compensate.md)
  * [Vector Quantization](multimedia/h264/vector-quantization.md)
  * [DCT](multimedia/h264/dct.md)
  * [CAVLC](multimedia/h264/cavlc.md)
  * [CABAC](multimedia/h264/cabac.md)
  * [JPEG](multimedia/h264/jpeg.md)
  * [H.264/AVC](multimedia/h264/h.264.md)
  * [H.265/HEVC](multimedia/h264/h.265.md)
* [Streaming Protocols](multimedia/streaming-protocols/README.md)
  * [Video Streaming](multimedia/streaming-protocols/video-streaming.md)
  * [RTSP](multimedia/streaming-protocols/rtsp.md)
  * [RTMP](multimedia/streaming-protocols/rtmp.md)
  * [HLS](multimedia/streaming-protocols/hls.md)
  * [DASH](multimedia/streaming-protocols/dash.md)

## Library/Framework

* [FFmpeg](library-framework/ffmpeg/README.md)
  * [Intro](library-framework/ffmpeg/intro.md)
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
  * [Windows에서 FFmpeg 빌드하기](library-framework/ffmpeg/windows-ffmpeg.md)
* [GStreamer](library-framework/gstreamer/README.md)
  * [Intro](library-framework/gstreamer/intro.md)
* [DirectShow](library-framework/directshow/README.md)
  * [Intro](library-framework/directshow/introduction.md)
  * [Building Filter Graph](library-framework/directshow/building-filter-graph.md)
  * [Data Flow](library-framework/directshow/data-flow.md)
  * [Control / Event Handling / Clock](library-framework/directshow/control.md)
* [Media Foundation](library-framework/media-foundation/README.md)
  * [Intro](library-framework/media-foundation/introduction.md)
  * [Media Foundation Transforms](library-framework/media-foundation/media-foundation-transforms.md)
  * [Media Foudation Sources](library-framework/media-foundation/media-foudation-sources.md)
  * [Media Foundation Sinks](library-framework/media-foundation/media-foundation-sinks.md)
  * [Custom Media Sessions](library-framework/media-foundation/custom-media-sessions.md)
* [Multimedia Framework Data Flow Model](library-framework/multimedia-framework-data-flow-model.md)

## BACKEND

* [NodeJS](backend/nodejs/README.md)
  * [Express](backend/nodejs/express.md)

## front-end

* [Browser](front-end/browser/README.md)
  * [MSE](front-end/browser/mse.md)
* [React](front-end/untitled/README.md)
  * [Create React App](front-end/untitled/create-react-app.md)

## etc

* [CMake](etc/cmake.md)
* [Googletest](etc/googletest.md)
* [Image Filtering](etc/image-filtering.md)

