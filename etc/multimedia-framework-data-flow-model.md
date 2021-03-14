---
description: 다양한 멀티미디어 프레임워크의 데이터 플로우 모델과 그 변화 과정
---

# Multimedia Framework Data Flow Model

## Multimedia Framework

* an API for multimedia applications
* media data processing - Encoding, Decoding, Transforming, ...
* Pipeline Building \(Media Type handling\)
* **Data Flow Control - Push / PULL**
* Synchronization

## Pipeline

* 멀티미디어 데이터를 처리하는 일련의 필터들의 집

![](../.gitbook/assets/image%20%2832%29.png)

## Data Flow Model

* 파이프라인 내의 필터 간 데이터를 어떻게 전달할 지에 관한 모델
* Push Model
  * Upstream Push, Limited Buffer, Pipeline Full

![](../.gitbook/assets/image%20%2829%29.png)

* Pull Model
  * Downstream Pull, Supplier's Availability, Pipeline Empty

![](../.gitbook/assets/image%20%2833%29.png)

* History

![](../.gitbook/assets/image%20%2835%29.png)



## Push to Partial Pull

* DirectShow
  * filter, pin, filter graph, filter graph manager

![](../.gitbook/assets/image%20%2831%29.png)

* GStreamer
  * element, pad, pipeline

![](../.gitbook/assets/image%20%2830%29.png)

* Appearance of Seekable Media Container
  * Pull Media와 [Seekable Container](https://app.gitbook.com/@cheonminjae225/s/post/~/drafts/-MVjsa2aS9FREL5hLCBv/etc/media-container)의 등장

![](../.gitbook/assets/image%20%2837%29.png)



