타입스크립트의 타입은 뭐가 있을까?
===
타입스크립트의 타입을 알아보자.
---

### 1. 기본 타입
* boolean
    ```Typescript
        let isTrue = false;
    ```

* number
    ```Typescript
        let decimal: number = 7;
        let hex: number = 0xf0a5;
        let binary: number = 0b1011;
        let octal: number = 0o744;
    ```

* string
    ```Typescript
        let text: string = 'Hello, World!';
    ```
    `(백틱), ""(큰따옴표)를 이용한 표현도 JS와 동일하게 가능하다.

* array
    ```Typescript
        let odds: number[] = [1, 3, 5, 7, 9];
        let evens: Array<number> = [2, 4, 6, 8, 10];
    ```

* tuple
    ```Typescript
        let fruit: [string, number] = ['사과', 3000];
    ```
    요소의 값과 개수가 고정되어있는 배열이다.<br />

* enum
    ```Typescript
        enum Language { Korean = 1, English, Japanese }
    ```
    중복되는 값이 없는 집합(set) 자료형이다.<br />
    요소별로 인덱스를 부여할 수 있다.

* any
    ```Typescript
        let someValue: any = 4;
        someValue.split();
    ```
    타입을 특정할 수 없는 경우, 컴파일 타임에 타입 검사를 통과할 수 있게 해준다.<br />
    따라서, 위의 코드의 경우 컴파일 타임에 애러가 발생하지 않는다.<br />
* void
    ```Typescript
        function warnUser(): void {
            console.log('Hello, World!');        
        }
    ```
    리턴 값이 없는 함수 에 사용할 수 있다.<br />
    void에 undefined는 할당 할 수 있지만 null은 할당할 수 없다.<br />

* null and undefined<br />
    Javascript와 동일하다.

* never
    ```Typescript
        function error(): never {

        }
    ```
    항상 오류를 발생시키거나 값을 절대 반환하지 않는 타입으로 쓰인다.<br />
    모든 타입에 never를 할당 할 수 있지만 그 반대는 불가능하다.<br />

* object
    ```Typescript
        let student: object = { age: 20, name: 'alex' }
    ```

* type assertions(타입 단언)
    ```Typescript
        let length = (<string>someValue).length
        let length = (someValue as string).length
    ```
    형변환과 유사해 보이지만, 컴파일 타임에 특별한 검사를 수행하지 않는다.<br />
    컴파일러는 개발자가 특정 검사를 수행했다고 판단한다.<br /> 
    JSX 문법에서는 as를 이용한 타입단언만 사용할 수 있다.<br />

2. 인터페이스
* 덕 타이핑(Duck typing) 또는 구조적 서브타이핑(Structural subtyping)
    ```Typescript
    interface Student {
        name: string;
        address: string;
        age?: number;
        readonly phone: string;
    }

    function introduce(student: Student): void {
        const { name, address, age } = student;

        console.log(`Hi, I'm ${name}.`);
        console.log(`I live in ${name}.`);
        if (age) console.log(`I'm ${age}.`);
    }

    let studentA: Student {
        name: 'Alex',
        address: 'Seoul',
        age: 20, // 생략할 수 있다.
        phone: 01012345678, // 수정할 수 없다.
    }

    introduce(studentA);
    ```
    object의 프로퍼티에 타입을 정하고 싶을 때 interface를 사용하면 된다.<br />
    `프로퍼티?`를 사용하면 프로퍼티를 생략할 수 있다.<br />
    `readonly` 수정할 수 없다.<br />
