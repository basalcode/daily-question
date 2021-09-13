Javascript의 V8 엔진은 어떻게 작동할까 ?
===
javascript의 작동 방식에 대해 알아보자.
---

### 1. V8 엔진 알아보기
* 런타임 구성<br />
  * 메모리 힙(Memory Heap)
    * 변수 객체(Variable Object)가 할당되는 공간이다.
  * 콜 스택(Call Stack)
    * 실행 컨텍스트(Execution Context)를 처리하는 공간이다.
  * 태스크 큐(Event Loop)
    * 각종 이벤트를 큐 방식으로 처리한다.
    * DOM, Network, Timer 등의 이벤트를 처리하는 큐를 가지고 있다.
  * Web API
    * DOM, Ajax, Timeout 등의 Api들을 가지고 있다.
  * Garbage Collector
    * 한정적인 메모리를 효율적으로 관리하기 위해 사용하지 않는 메모리를 해제한다.
    * Mark and Sweep 알고리즘을 사용한다.
