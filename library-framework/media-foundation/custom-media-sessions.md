# Custom Media Sessions

### How to create playback topology

### how all of these components actually pass data from one to another

## Topology

* Direct Show의 media graph에 해당
  * directly connected
* individual components do not know anything about each other
  * topology loader가 각 component의 스트림의 미디어 타입을 조회하고 세팅해주고, 논리적 파이프라인을 만들어줌
  * 결과적으로 component들은 서로를 전혀 모
  * data flow를 위해 MF는 media session이라는 별도의 객체를 
* solid arrow : sample flow, dashed line : media events

![](../../.gitbook/assets/image%20%283%29.png)

## Topology Builder

* Topology를 만들기 위해 사용하는 객
* 소스가 만들어지면, 혹은 소스부터 파이프라인을 만들기 시작
* Media Type 협상과정을 진행하며, 이 과정은 Direct Show와 크게 다를 것이 없음

## Media Session

* MFCreateMediaSession\(\)으로 만들어짐
  * created general purpose
  * handful scenario를 위해 custom session을 사용할 수도 있음
    * 다양하게 분리된 파일 간의 협업
    * custom DRM
    * unit test
    * ...
* **`IMFMediaSession`** 인터페이스를 구현하고 있음
* Topology Builder가 Topology를 만들고, 이를 Session에 붙여주는 형식으로 동작
* Session의 주요 역할의 간략한 요약 다음 코드를 참조

```cpp
HRESULT CSession::Invoke(IMFAsyncResult* pResult)
{
    HRESULT hr = S_OK;
    IUnknown *pUnkState;
    IAsyncState *pAsyncState;
    
    do 
    {
        // see if the event indicates a failure
        hr = pResult->GetState();
        BREAK_ON_FAIL(hr);
        
        // get the IAsnycState state from the result
        hr = pResult->GetState(&pUnkState);
        BREAK_ON_FAIL(hr);
        
        pAsyncState = pUnkState;
        BREAK_ON_NULL(pAsyncState, E_UNEXPECTED);
        
        // figure out the type of the operation from the state
        // and then proxy the call to the right function
        if (pAsyncState->EventType() == AsyncEventType_ByteStreamHandlerEvent)
        {
            hr = HandleByteStreamHandlerEvent(pResult);
        }
        else if (pAsnycState->EventType() == AsyncEventType_SinkStreamEvent)
        {
            hr = HandleSinkStreamEvent(pResult);
        }
        else if (pAsnycState->EventType() == AsnycEventType_SourceEvent)
        {
            hr = HandleSourceEvent(pResult);
        }
        else if (pAsnycState->EventType() == AsnycEventType_SourceStreamEvent)
        {
            hr = HandleSourceSteramEvent(pResult);
        }
        else if (pAsnycState->EventType() == AsnycEventType_SyncMftSampleRequest)
        {
            hr = HandleSyncronousMftRequest(pResult);
        }   
    } while (false);
    
    // if we got a failure, queue an error event
    if (FAILED(hr))
    {
        hr = m_pEventQueue->QueueEventParamVar(MEError, GUID_NULL, hr, NULL);
    }
    
    return hr;
}
```

* MF의 경우 위에서 data flow를 묘사했던 것처럼 MFT는 기본적으로 synchronous한 모델이였음
  * 이 경우, session의 mft task를 처리하는 handler가 blocking이 발생할 여지가 있음
  * 따라서 별도의 thread를 두어야 함
  * state로 관리하는 법도 있지만, complex, fragile하다고 함.
  * 또한 multi-thread로 구현된 MFT의 경우 지원이 힘들다고 함\(???\)
  * 다음은 예시코드

```cpp
HRESUlT DataFlowMFTtoSink {
    do {
        hr = ProcessOut();
        if (hr == NEED_MORE_INPUT) {
            WaitForSingleObject();
            ProcessInput();
        }
    } while(hr != S_OK;)
}
```

* 그래서 Windows 7부터 asynchronous MFT를 도입했지만, synchronous 모델이 기본이라고 함.
  * asynchronous MFT는 event를 발행하도록 구현되어 있음
  * 각기 need\_input과 have\_output 두 가지의 event를 발행
  * available sample, requested sample을 관리하면서 동작하도록 되어있음
  * 예시코드는 없음....... 어떻게 트리거된다는 것이

