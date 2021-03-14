# Control / Event Handling / Clock

## PID\(Plug-in Distribution\) interface

![](../../.gitbook/assets/image%20%2852%29.png)

## Filter Graph Manager

* PID interface를 이용하여 중앙관리 수행
  * PID interface란 반드시 필터그래프로 부터 요청해야 하는 인터페이스를 의미
  * 필터그래프의 동적 확장 및 중앙관리를 통해 시스템 보호
  * 필터의 PID interface 구현은 필터에서 구현하되, 요청은 필터그래프의 PID interface를 이용해 이뤄짐
* 파이프라인 내의 인터페이스 요청의 분배 및 제어는 Upstream order로 순차적으로 실행 됨

![](../../.gitbook/assets/image%20%2832%29.png)

* Filter Graph Manager Interface

![](../../.gitbook/assets/image%20%2839%29.png)

## Control Graph

* 필터의 3가지 상태
  * Stopped : 필터가 정지해있는 상태
  * Paused : 랜더필터를 제외하고는 running과 실질적으로 동일한 상태. 랜더 필터는 일시정지 됨
  * Running : 필터가 동작하고 있는 상태
* FGM의 상태변화는 upstream order로 이루어짐
  * Sample drop 방지 및 deadlocking 방지
* Stopped -&gt; Paused \(Running\)
  * Puased로 전환 시, 하위 필터부터 차례로 샘플을 받을 수 있는 상태로 전환
  * 스트리밍 스레드가 활성화되면 샘플의 이동 시작
  * 랜더러가 활성화되기 전까지는 샘플의 이동을 완료할 수 없음
* \(Runnning\)Paused -&gt; Stopped
  * 하위 필터부터 차례로 지니고 있던 샘플을 릴리즈 및 대기중이던 Receive\(\)를 반환시킴
  * 정지 전 상위필터로부터 전달된 샘플을 모두 거절
* 필터그래프의 3가지 상태
  * Run\(재생\) : 모든 필터그래프의 필터가 동작하는 상태
  * Pause\(일시정지\) : 모두 동작하지만 출력은 하지 않는 상태
  * Stop\(정지\) : 모두 정지한 상태
* 필터그래프의 그래프 제어
  * IMediaControl 인터페이스의 메서드는 IMediaFilter 인터페이스의 상응하는 메서드를 호출
  * Stop\(\)과 Run\(\) 사이에는 항상 Pause\(\)를 경유하여 이뤄

![](../../.gitbook/assets/image%20%2834%29.png)

* 미디어 검색 그래프 제
  * PID가 렌더 필터를 대상으로 IMediaSeeking 인터페이스 분배
  * 렌더 필터는 하위 필터의 IMediaSeeking 인터페이스 지원 여부를 확인 후, 지원 시 IMediaSeeking 호출을 하위 필터로 전파
  * 미디어 검색을 구현하는 필터를 만날 때까지 해당 호출이 전파됨
    * 푸쉬 : 소스 필터
    * 풀 : 파서 필터
  * 해당 필터에서 미디어 검색 처리 하위 필터로 신호 전
    * Flush 전파 및 스레드 핸들링

![](../../.gitbook/assets/image%20%2872%29.png)

![](../../.gitbook/assets/image%20%2849%29.png)

## Event Handling

* 필터그래프 매니저는 필터그래프 내에서 발생하는 이벤트를 자체 처리하거나 App에 전달
*  IMediaEventEX::SetNotifyWindow\(\)로 메세지 통지
  * param1 : 메세지를 처리할 창의 핸들
  * param2 : 이벤트 발생 알림 메세지
  * param3 : 이벤트 분기용 파라미터
* IMediaEvent::GetEvent\(\)로 message queue의 가능한 모든 메세지 추출 및 처리

![](../../.gitbook/assets/image%20%2843%29.png)

* Event Handling Example - EC\_COMPLETE
  * CBasePin::EndOfStream\(\)이 EOS 신호 생성 \(Pull 모드의 경우 CPullPin::EndOfStream\(\)\)
  * CBaseOutputPin::DeliverEndOfStream\(\)이 하위 필터로 신호 전파
  * 랜더 필터는 전달받은 EOS 신호를 Filter Graph Manager에게 EC\_COMPLETE 이벤트로 전

![](../../.gitbook/assets/image%20%2831%29.png)

## DirectShow의 Clock

* DirectShow에는 2가지 시간 개념이 존재
* 참조 시간 \(reference time\) : 항상 흘러가는 시간, 절대 시간\(absolute time\)
  * 보통 오디오 랜더러가 사운드 클락을 구현
  * 시스템 클락 컴포넌트를 구현하는 객체를 사용할 수도 있음
  * IReferenceClock::GetTime\(\) 함수를 통해 참조시간 값을 얻음
* 스트림 시간\(stream time\) : 시작과 일시정지, 초기화가 가능한 시간, 상대 시간\(relative time\)
* DirectShow의 기본 시간 단위 : 100 ns
* Media Sample의 두 가지 시간 정보 : Time Stamp, Media Time
  * Time Stamp : 스트림 출력 시간 \(PTS, Presentation Time Stamp\)
  * Media Time : 검색 가능한 단위의 시간, 패킷 시간, 디코딩 시간\(DTS, Decoding Time Stamp\)
  * 두 시간 정보는 모두 스트림 시간을 기준으로 사

