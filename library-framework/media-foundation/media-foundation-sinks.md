---
description: Sink description
---

# Media Foundation Sinks

## Media Sinks overview

**Media Sink**

* MF의 미디어 파이프라인에서 하나 이상의 입력 스트림을 가지지만, 출력 스트림을 가지지 않는 객체
* Source에서 나와 MTFs를 거치며 처리된 데이터들을 최종적으로 모두 소모시키는 것이 목적
* **MF의 pull data flow model에서 source components에 데이터를 요청할 책임을 가짐**

**Media Sink의 3가지 유형**

* **renderer sink** : 스트림을 user에게 랜더링
* **archive sink :** 여러 스트림을 muxing하여 media file로 저장한다.
* **streaming sink** : 네트워크를 통해 데이터를 전송한다.

**Instantiation**

sink의 경우 discovery system을 가지고 있지 않으며, COM objects로 관리되어 다음과 같은 방식으로 인스턴스화

* CLSID와 CoCreateInstance\(\)를 이용
* built-in MF sink creation function을 이용
  * hard-coded lists of internal sink objects
  * MFCreateVideoRenderer\(\)
  * MFCreateAudioRenderer\(\)

## Media Sink Object Structure

 ![](../../.gitbook/assets/.png%20%281%29.png) 

* \[Stream Object + Sink Object\] 가 일반적이지만 필수는 아님
* **`IMFStreamSink`, `IMFMediaSink`** 인터페이스만 필수적으로 구현해주면  됨
* **`IMFClockStateSink`** 도 playback을 위한 경우\(timing 관리\) 구현 필요

## Request Samples Flow

* fires sample request events, which are received by the sink's client.
* then, client request samples from the component upstream from the sink
* upstream component pull data from its upstream component

## IMFMediaSink

used to **dynamically discover, add, and remove stream sink object to and from the media sink.**

* AddStreamSink\(\)
  * Create and Add a new stream sink object
  * specifying its ID and \(optionally\) its media type
* GetStreamSinkByID\(\)
* GetStreamSinkByIndex\(\)
* GetStreamSinkCount\(\)
* RemoveStreamSink\(\)

used to **allow a client to get and set the presentation clock \(`IMFPresentationClock`\)**

* SetPresentationClock\(\)
* GetPresentationClock\(\)

used  to **get the characteristics of the sink**

* GetCharacteristics\(\)

used to **shut down the sink**

* ShutDown\(\)

## IMFClockState**Sink**

allows a client to control the sink playback.

used by the presentation clock to **pass commands to the media sink.**

then media sink **pass the command to the stream objects.**

**IMFClockStateSink**

* OnClockStart\(\)
* OnClockPause\(\)
* OnClockRestart\(\)
* OnClockStop\(\)
* OnClockSetRate\(\)

**presentation clock**

* is an object that control the timing of the sink
* allows synchronization between individual sinks in to topology.
* implements **`IMFPresentationClock`**
* **`IMFClockStateSink`**와 **`IMFPresentationClock`**은 상호 참조

## Stream Playback Control

OnClockStart\(\)가 불리면, 각각의 MediaStream Object의 Internal call로 다음의 이벤트들을 발행

* MEStreamSinkStarted - sink object  has started operating
* MEStreamSinkRequestSample - need more sample

OnClockStop\(\)이 불리면, 각각의 MediaStream Object의 Internal call로 다음의 이벤트를 발행

* MEStreamSinkStopped - stream has stopped and will not be requesting any more samples

## IMFStreamSink

Media Stream is created by Sink's ctor or IMFMediaSink::AddStreamSink\(\);

Media Stream object implements **`IMFStreamSink`** interface.

* **receive and process data** for one data stream.
* **receive various stream-related status events.**
* also **used to send out various commands to other components.**
  * inherits from **IMFMediaEventGenerator**

**IMFStreamSink**

used to facilitate data flow in the stream. \(receive samples, events, and commands\)

* ProcessSample\(\)
* PlaceMarker\(\)
* Flush\(\)

configure the stream object

* GetMediaSink\(\)
* GetIdentifier\(\)
* GetMediaTypeHandler\(\)

## Data Flow Example

 also use asynchronous model

![](../../.gitbook/assets/1-%20%281%29.png)

## 

