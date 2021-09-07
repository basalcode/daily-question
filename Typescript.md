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

        let weeks: ReadonlyArray<string> = ['Mon', 'Tue', 'Wed', 'Tur', "Fri', 'Sat', 'Sun'];
    ```
    `ReadonlyArray`는 값을 변경할 수 없다.<br /> 
    값을 변경하는 메소드 또한 지원하지 않음.<br /> 

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

### 2. 인터페이스
#### object의 프로퍼티에 타입을 정하고 싶을 때 사용한다.

* 덕 타이핑(Duck typing) 또는 구조적 서브타이핑(Structural subtyping)
    ```Typescript
        interface Vehicle {
            name: string,
            speed: number
        }

        function run(vehicle: Vehicle): void {
            let { name, speed } = vehicle;

            console.log(`${name} is running at ${speed}km/h.`);
        }

        let car = {
            name: 'car',
            model: 'ferrari',
            speed: 100
        }

        run(car);
    ```
    전달된 인자가 더 많은 프로퍼티를 가지고 있지만 애러가 나지 않는다.<br />

* 타입 
    ```Typescript
    interface Student {
        name: string;
        address?: string;
        readonly age: number;
    }

    function introduce(student: Student): void {
        const { name, address, age } = student;

        console.log(`Hi, I'm ${name}.`);
        if (address) console.log(`I live in ${address}.`);
        console.log(`I'm ${age}.`);
    }

    let studentA: Student {
        name: 'Alex',
        address: 'Seoul', // 생략할 수 있다.
        age: 20, // 수정할 수 없다.
    }

    introduce(studentA);
    ```
    `프로퍼티명?`를 사용하면 프로퍼티를 생략할 수 있다.<br />
    `readonly`를 사용한 프로퍼티는 수정할 수 없다.<br />

* 초과 프로퍼티 검사 (Excess Property Checks)
    ```Typescript
    interface Fruit {
        name: string,
        price: number,
    }

    let fruitA {
        name: 'apple',
        price: 3000,
        color: 'red'
    }

    let fruitB: Fruit {
        name: 'banana',
        price: 2500,
        color: 'yellow' // 초과프로퍼티 검사로 인해 애러가 발생한다.
    }
    ```
    인터페이스로 지정된 것보다 더 많은 프로퍼티를 사용할 수 없다.<br />

* 함수 타입 (Functional Types)
    ```Typescript
    interface SearchFunc {
        (source: string, subString: string): boolean;
    }

    let mySearch: SearchFunc = function (src: string, sub: string) {
        let result = source.search(subString);

        return result > - 1;
    };
    ```
    인터페이스를 함수의 형식을 지정하는데 사용할 수 있다.<br />

* 인덱서블 타입 (Indexable Types)
    ```Typescript
    interface StringArray {
        [index: number]: string;
    }
    let myArray: StringArray = ['Bob', 'Fred'];

    interface Dictionary {
        [key: string]: number | string;
        length: number;
        name: string;
        isOn: true; // 애러
    }
    ```
    인덱서블 타입을 사용하면 배열뿐 아니라 객체의 키와 값에 대한 타입도 정할 수 있다.<br />