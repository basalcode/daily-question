실행 문맥(Execution Context)이란 무엇일까?
===
Javascript 핵심원리인 실행 문맥에 대해 알아보자.
---

### 1. 실행 컨텍스트 스택(Execution Context Stack)
*  ```Javascript
    //global execution context
    let textA = 'Hello, ';

    function funcA() {
        //funcA execution context
        let textB = 'World. ';

        function funcB() {
            //funcB execution context
            let textC = 'Bye!';

            console.log(textA + textB + textC);
        }

        funcB();
    } 
    funcA();
    ``` 
    위 코드의 실행 컨텍스트 스택은 프로그램의 시작과 종료, 함수의 호출과 반환의 과정에서 다음과 같이 변화한다.<br />
    |   1    |   2    |   3    |   4    |   5    |
    | :----: | :----: | :----: | :----: | :----: |
    | global | global | global | global | global |
    |        | funcA  | funcA  | funcA  |        |
    |        |        | funcB  |        |        |
    
### 2. 실행 컨텍스트(Execution Context)<br />
실행 컨텍스트에는 2 종류의 변수 객체(variable object)가 있다.<br />

| Execution Context |  Variable Object  |          Value          |
| :---------------: | :---------------: | :---------------------: |
|      global       |   Global Object   |      funcA, textA       |
|       funcA       | Activation Object | funcB, textB, arguments |
|       funcB       | Activation Object |    textC, arguments     |

* 전역 객체(Global Object)<br />
  * 전역 실행 컨텍스트가 가지는 변수 객체.<br />
  * 변수 및 함수 선언 등을 프로퍼티로 갖는다.<br />
  <br />
* 활성 객체(Activation Object)<br />
   *  함수 실행 컨텍스트가 가지는 변수 객체.<br />
   *  변수와 함수 선언 그리고 arguments object(parameter, argument)를 가지고 있다<br />
   <br />
* 스코프 체인(Scope Chain)<br />
스코프 체인은 현재 스코프보다 상위 스코프를 참조할 때 사용된다.<br />

| Execution Context | Scope Chain Index |     Reference Value     |
| :---------------: | :---------------: | :---------------------: |
|      global       |         0         |      Global Object      |
|       funcA       |         0         | funcA Activation Object |
|                   |         1         |      Global Object      |
|       funcB       |         0         | funcB Activation Object |
|                   |         1         | funcA Activation Object |
|                   |         2         |      Global Object      |

0번 인덱스(자기 자신의 변수 객체)에서 값 조회에 실패하면, 다음 인덱스(상위 스코프의 변수 객체)의 변수객체를 검색한다.<br />

* this<br />
    this의 값은 함수 선언시에 결정되는 것이 아닌, 함수를 호출하는 시점에 어디에 바인딩 될지 동적으로 결정된다.