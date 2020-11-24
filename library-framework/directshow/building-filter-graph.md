# Building Filter Graph

## Intelligent Connect

### Building Filter Graph

* Mechanism the Filter Graph Manager uses to build filter graph
* 주요 기술은 다음과 같이 분류할 수 있음
  * 핀 간 수동 연결
  * 필터 추가 : 다운스트림 필터 탐색 및 추가
  * 핀 간 자동연결 : 다운스트림 필터 추가 + 핀 간 수동 연결
  * 핀 랜더링 : 핀으로 부터 랜더링을 시작하여 랜더러까지 파이프라인 연결
  * 필터 랜더링 : 필터의 모든 핀의 핀 랜더링 수행
  * 널 랜더링 : 소스필터를 추가 후 필터 랜더링
  * 필터 추가 후 랜더링 : 소스필터 추가 후, 추가되어 있는 필터를 이용해 파이프라인 랜더링

![](../../.gitbook/assets/image%20%2827%29.png)

* 소스필터 탐색 및 추가
  * 파일을 파싱할 수 있는 소스필터를 레지스트리를 탐색하여 추가
    * 레지스트리에 protocol이나 extension에 맞게 필터에 대한 CLSID가 기재되어 있어, COM을 이용해 필터를 얻을 수 있음
* 하위 필터 검색 및 추가
  * 필터 내 존재하는 필터의 입력핀과 연결 시도
  * 연결 실패 시, 필터의 출력 핀의 미디어타입을 입력으로 지원하는 필터를 레지스트리에서 검색
    * Filter Graph Manager는 Filter Mapper 객체를 사용하여 registry 검색
    * 필터 카테고리, 미디어타입, merit 등을 비교하여 우선순위에 맞게 필터 인스턴스를 만들 수 있는 객체를 가져옴
  * 필터 추가 및 연결 재시

### 필터 간 연결 절

* 필터의 핀 열거 및 연결 시도
  * `IBaseFilter::EnumPins()`로 연결할 두 필터의 핀을 열거
  * `IEnumPins::Next()`로 IPin 인터페이스를 연결할 출력/입력 핀을 얻음
  * 입력 핀을 인자로 출력 핀의 `IPin::Connect()`함수를 호출하여 연결 시도
* 미디어 협상
  * `CBasePin::Connect()`함수는 `CBasePin::AgreeMediaType()`을 호출하 미디어협상을 진행하합고, 합치하는 미디어타입을 찾게 되면 `CBasePin::AttempConnection()`을 호출하여 연결을 시도
  * `CBasePin::AttemptConnection()`은 핀의 방향 확인, 미디어 타입 세팅, 핀간 연결 정보 생성 등의 과정을 거친 후, `CBasePin::CompleteConnect()`를 호출하여 미디어협상을 완료하고 버퍼 협상 단계로 진입
* 버퍼 협상
  * Upstream 필터의 출력핀의 `CBaseOutputPin::DecideAllocator()`가 호출되어 버퍼 협상이 시작됨
  * DownStream의 `IMemInputPin::GetAllocatorRequirements()`로 Allocator 요구사항 요청 및 `IMemInputPin::GetAllocator()`를 이용해  Downstream에서 제공하는 Allocator를 얻어 옴
  * 요구사항 및 할당자를 확인하여 출력핀에서 사용할 수 있는 요구사항에 맞는 경우, `CBaseOutputPin::DecideBufferSize()`, `IMemInputPin::NotifyAllocator()` 등을 호출하여 Allocator를 설정하고 공지하여 버퍼협상을 마무리
  * 위 단계에서 버퍼 협상에 실패할 경우, `CBaseOutputPin::InitAllocator()`를 호출해 스스로 Allocator를 만들고, `CBaseOutputPin::DecideBufferSize()`로 자신에게 Allocator를 설정한 뒤, `IMemInputPin::NotifyAllocator()`을 호출하여 Downstream Filter의 Pin에 Allocator를 공지하여 버퍼협상 시
  * 즉, 가능한 downstream이 원하는 버퍼의 요구사항에 맞게 Allocator를 지원할 수 있는지 확인하고, 불가한 경우 upstream이 제시할 수 있는 버퍼형태가 downstream에서 지원가능한지 파악하는 과정을 거쳐 buffer pool이 만드는 과정이 `버퍼협상` 

![](../../.gitbook/assets/image%20%2828%29.png)

