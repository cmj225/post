# Data Flow

## Push Mode / Pull Mode

* `Push Mode`는 Upstream 필터가 thread를 가지고 Allocator에서 버퍼가 허용하는 만큼 데이터를 Downstream으로 pushing
* `Pull Mode`의 경우, Downstream 필터가 thread를 가지고 필요에 따라 Upstream에 task를 요청하여 버퍼를 pulling
* DirectShow의 경우, 기본적인 thread model은 각 스트림별로 threading하여 synchronous하게 동작하는 형태이지만, 핀 구현에 따라 threading model을 조절하여 asynchronous하게 동작하도록 할 수도 있음\(MSDN에서 권고하고 있지는 않음\)
* DirectShow의 경우 기본적으로 Push Mode로 동작하도록 설계되었고, Pull Mode의 경우 파서필터 등의 특정 필터에게만 IAsyncReader 인터페이스를 통해 지원할 수 있도록 함
* `Push/Pull Model에 대한 정리는 다른 doc을 통해 자세히 정래해둠`
* ![](../../.gitbook/assets/image%20%2826%29.png)

