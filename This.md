Javascript의 this는 무엇이 다를까?
===
this의 바인딩에 대해 알아보자.
---

### 1. 상황별 this가 가리키는 대상
* 함수 
    ```Javascript
    function printThis() {
        console.log(this);
    }

    printThis(); // Window
    ```
    this는 함수를 호출한 스코프에 바인딩 된다.<br />
    

* 객체의 메서드
    ```Javascript
    let obj = {
        literal: function () {
            console.log(this); // 함수를 호출한 obj에 바인딩 된다.
        },
        arrow: () => {
            console.log(this);
        }
    }

    obj.literal(); // Object
    obj.arrow(); // Window
    ```
    화살표함수는 자신을 호출한 스코프의 this 값을 상속 받는다.<br />
    화살표함수는 때에 따라 메소드에 사용하기 적합하지 않을 수 있다.<br />

* 생성자
    ```Javascript
    function Student(name) {
        this.name = name;
    }

    let studentA = new Student('alex');
    
    console.log(studentA.name);
    ```
    new를 사용한 생성자 함수의 경우 this가 생성하는 객체에 바인딩 된다.<br />


* 이벤트 핸들러
    ```Javascript
    let button = document.createElement('button');

    button.innerText = 'Click me!'

    document.body.appendChild(button);

    button.addEventListener('click', function (event) {
        console.log(this); // Button Element
    });
    ```
    이 경우에도 화살표함수로 작성을 하면 this는 Window를 가리킨다.<br />

### 2. this 바인딩하기
* apply, call, bind
    ```Javascript
   function printThis() {
        console.log(this);
    }

    let obj = { text: 'hello' }

    printThis(); // Window
    printThis.apply(obj); // obj Object
    printThis.call(obj); // obj Object
    
    let bindedPrintThis = printThis.bind(obj);
    bindedPrintThis(); // obj Object
    ```
    사용법의 차이를 제외하면 this를 바인딩하는 역할은 동일하다.<br />