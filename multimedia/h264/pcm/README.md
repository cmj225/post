---
description: Pulse-code modulation
---

# PCM

### [PCM](https://en.wikipedia.org/wiki/Pulse-code_modulation) \(Pulse-code modulation\)

**아날로그 신호**를  **`샘플링(Sampling)`** + **`양자화(Quantization)`**하여 **디지털 신호로 표현**한 것

* **`샘플링(Sampling)`** : 시간방향과 진폭방향으로 연속적인 아날로그 신호를 일정 간격으로 추출
* **`양자화(Quantization)`** : 샘플링으로 얻은 각 샘플값을 필요한 레벨수의 디지털 표현\(정수치\)으로 변환
  * 몇 비트로 디지털화하는가에 따라 신호가 거칠어지거나 정밀해진다
    * 4bit =$$2^4$$ \(bit depth = 16\)
* ![](../../../.gitbook/assets/image%20%2817%29.png) 
* 음성 디지털화에 주로 사용되는 구조 \(영상신호의 변환도 기본적 원리는 동일\)
* 압축을 수행하지 않으므로, 디지털로 변환된 음성\(또는 영상\)은 원래의 아날로그 신호로 완전 복원될 수 있어, `실효적 (샘플링을 잘 해두었으면)` 등가라고 봄



### Audio Sampling

analog -&gt; audio sample

* `[샤논(Shannon)의 샘플링 원리], [샘플링 정리], [나이퀴스트(Nyquist)의 정리]`
  * 아날로그 신호를 디지털화하는 경우, 2배 이상의 주파수로 샘플링하면, 원래의 연속적인 아날로그 신호로 완전히 복원하는 것이 가능하다

### 

### Video Sampling 

analog -&gt; RGB

### 

### Reference

{% embed url="http://www.yes24.com/Product/Goods/2532229" %}

{% embed url="https://app.gitbook.com/@yoooonghyun/s/documents/media/media-sampling" %}





