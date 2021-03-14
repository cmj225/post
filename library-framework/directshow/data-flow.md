# Data Flow

## Push Mode / Pull Mode

* `Push Mode`는 Upstream 필터가 thread를 가지고 Allocator에서 버퍼가 허용하는 만큼 데이터를 Downstream으로 pushing
* `Pull Mode`의 경우, Downstream 필터가 thread를 가지고 필요에 따라 Upstream에 task를 요청하여 버퍼를 pulling
* DirectShow의 경우, 기본적인 thread model은 각 스트림별로 threading하여 synchronous하게 동작하는 형태이지만, 핀 구현에 따라 threading model을 조절하여 asynchronous하게 동작하도록 할 수도 있음\(MSDN에서 권고하고 있지는 않음\)
* DirectShow의 경우 기본적으로 Push Mode로 동작하도록 설계되었고, Pull Mode의 경우 파서필터 등의 특정 필터에게만 IAsyncReader 인터페이스를 통해 지원할 수 있도록 함
* `Push/Pull Model에 대한 정리는 다른 doc을 통해 자세히 정해둠`
* ![](../../.gitbook/assets/image%20%2826%29.png)

## Allocator

* DirectShow의 버퍼 관리자
* 각 핀들은 Allocator를 통해 필요한 버퍼를 요청하여 버퍼를 얻는다\(sync-blocking\)
* 미리 버퍼를 할당해두고 요청 시 포인터만 전달해 처리 속도 향상
* 각 필터의 특성을 반영해 버퍼의 크기 및 개수 조정
* 버퍼는 reference count로 관리되며, 사용이 끝난 버퍼는 할당자로 회수 

![](../../.gitbook/assets/image%20%2854%29.png)

* 버퍼의 공유 \(buffer share\)

  * 멀티미디어 데이터의 특성 상 불필요한 복사를 줄여 성능의 향상을 꾀할 수 있음
  * Inplace 변환 필터\(추가적인 버퍼가 필요 없는 버퍼\)의 경우 재협상 과정을 통해 버퍼를 공

![](../../.gitbook/assets/image%20%2867%29.png)

## 

