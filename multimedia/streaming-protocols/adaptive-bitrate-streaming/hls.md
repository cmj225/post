---
description: HTTP Live Streaming
---

# HLS

### [HTTP Live Streaming](https://developer.apple.com/streaming/)

Apple에서 LIVE, on-demand 오디오/비디오 전송을 위해 내놓은 프로토콜.

웹과 동일한 프로토콜을 사용하여 기존의 웹 서버와 CDN을 이용해 효과적으로 동영상 컨텐츠를 서비스할 수 있다.

미디어 컨테이너 포맷으로 .mp2ts를 사용하도록 개발되었고, 현재는 .mp4\(.fmp4\).도 지원한다.

* menifest : .m3u8
  * 하나 또는 여러 비디오 파일의 경로를 plain text로 작성한 파일
  * extended m3u
* 비디오 코덱 : h264
* 오디오 코덱 : aac



### HLS 서비스의 구조

주요 컨셉은 영상을 Stream segmenter를 이용해 작은 단위로 분리하고, 이 파일들의 목록을 만들어 웹 서버를 통해 배포하는 것이다.

![components of an HTTP Live Stream](../../../.gitbook/assets/image%20%2885%29.png)



아래 사항들이 주요 기능인데 각각을 어떻게 지원하는지 정

HLS supports the following:

* Live broadcasts and prerecorded content \(video on demand, or _VOD_\)
* Multiple alternate streams at different bit rates
* Intelligent switching of streams in response to network bandwidth changes
* Media encryption and user authentication

The following figure shows the components of an HTTP Live Stream.



### Contents 보호의 지원





### Adaptive Birtate Streaming의 지원





{% embed url="https://developer.apple.com/streaming/" %}





