---
description: HTTP Live Streaming
---

# HLS

### HTTP Live Streaming

Apple에서 iOS 3.0과 QuickTime X를 위해 2009년에 내놓은 프로토콜.

스트리밍 데이터를 MPEG-2 Transport Stream에 담아 시간 단위로 잘게 쪼개서 전송한다.

그리고 어떤 파일을 재생해야 하는 지에 대한 정보는 m3u8 파일을 이용하여 플레이어에 전달한다.

HLS는 iPhone과 iPad의 사용자 수가 늘어남으로써 자연스럽게 그 수요가 늘어나게 되었다. 또한, 규격 자체의 단순함과 IETF\(Internet Engineering Task Force\)를 통한 표준화 작업 등을 통해 다른 업체들도 쉽게 HLS를 지원할 수 있게 했다.

그 결과로, Adobe는 Flash Media Server 4.0에서, Microsoft는 IIS Media Server 4.0에서 HLS를 정식으로 지원하며, 모바일 운영체제에서 상대 진영이라 할 수 있는 Google의 Android에서도 3.0 버전인 Honeycomb부터 HLS를 지원하기 시작했다.

* 미디어 컨테이너 포맷 : .mp2ts\(.ts\), .mp4\(.fmp4\)
* menifest : .m3u8
  * 하나 또는 여러 비디오 파일의 경로를 plain text로 작성한 파일
  * extended m3u
* 비디오 코덱 : h264
* 오디오 코덱 : aac





{% embed url="https://developer.apple.com/streaming/" %}





