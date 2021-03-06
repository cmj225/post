# DPCM

## DPCM \(Differential Pulse-code modulation\)

[**DPCM**](https://en.wikipedia.org/wiki/Differential_pulse-code_modulation)이란 예측한 신호와 입력된 신호의 오차인 **`예측오차(Differential)`**만을 보내는 방법

* 인접 데이터의 short-term redundency를 제거하여 정보량을 줄인다.
* **`차분치의 진폭분포는 0주변에 집중된 지수분포`**로 그 값들이 0 주위로 집중기 때문에, 이를 이용해 신호를 표현함으로 보다 적은 정보량으로 신호를 표현 가능



### Audio Example

* 가장 단순한 예측 방법으로 현재의 값이 직전 값과 같다고 가정

|  | t0 | t1 | t2 | t3 | t4 | t5 | ... |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| PCM | 5 | 6 | 5 | 5 | 4 | 5 | ... |
| DPCM | +5 | +1 | -1 | 0 | -1 | +1 | ... |

### 

### Image Example        

![](../../../.gitbook/assets/image%20%2815%29.png)  ![](../../../.gitbook/assets/image%20%2812%29.png) 

* 일반적으로 이미 부호화된 주변의 화소\(좌측, 상단, zig-zag scanning\)를 가중평균하여 현재 부호화하려는  화소를 예측하는 방식을  사용 `(좌측 화소값 * 0.5 + 상단 화소값 * 0.5)`  

## Reference

{% embed url="http://www.yes24.com/Product/Goods/2532229" %}

