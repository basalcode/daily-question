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

        let weeks: ReadonlyArray<string> = ['Mon', 'Tue', 'Wed', 'Tur', 'Fri', 'Sat', 'Sun'];
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

* 클래스 타입 (Class Types)
    ```Typescript
    interface ClockInterface {
        currentTime: Date;
        setTime(d: Date): void;
    }

    class Clock implements ClockInterface {
        currentTime: Date = new Date();
        setTime(d: Date) {
            this.currentTime = d;
        }
        constructor(h: number, m: number) { }
    }
    ```
    인터페이스를 사용해 클래스를 구현할 수 있다.

* 인터페이스 확장 (Extend Interface)
    ```Typescript
    interface Shape {
        color: string;
    }

    interface PenStroke {
        penWidth: number;
    }

    interface Square extends Shape, PenStroke {
        sideLength: number;
    }

    let square = {} as Square;
    square.color = "blue";
    square.sideLength = 10;
    square.penWidth = 5.0;
    ```
### 3. 함수
* 함수의 타이핑 (Typing the function)
    ```Typescript
    function add(x: number, y: number): number {
        return x + y;
    }

    let sub = function(x: number, y: number): number {
        return x - y;
    }
    ```

* 함수 타입 작성하기 (Writing the function type)
    ```Typescript
    let add: (baseValue: number, increment: number) => number =
    function (x: number, y: number): number {
        return x + y;
    }
    ```

* 타입 추론 (Inferring the Type)
    ```Typescript
    let add = function(x: number, y: number): number {
        return x + y;
    }

    let sub: (x: number, y: number) => number = function(x, y) {
        return x - y;
    }
    ```
    `=`를 기준으로 좌항 또는 우항 한쪽에만 타입이 부여되어있어도 타입 추론이 가능하다.<br />
    `contextual typing` 이라고 한다.<br />

* 선택적 매개변수와 기본 매개변수 (Optional and Default Parameter)
    ```Typescript
    function introduce(name: string, age?: number) {
        console.log(`Hello, I'm ${name}.`);
        if (age) console.log(`I'm ${age}.`);
    }
    ```
    `매개변수명?`을 사용하면 선택적으로 값을 받을 수 있다.<br />
    ```Typescript
    function introduce(name: string, age: number = 20) {
        console.log(`Hello, I'm ${name}.`);
        console.log(`I'm ${age}.`);
    }
    ```
    매개변수에 기본 값을 지정하는 것도 가능하다.<br />

* 나머지 매개변수(Rest Parameter)
    ```Typescript
    function printScores(name: string, ...scores: number[]) {
        console.log(`name: ${name}.`);
        console.log(`score: ${scores.join(' ')}`);
    }

    printScores('alex', 1, 2, 3, 4, 5);
    ```

* 오버로드 (Overloads)
    ```Typescript
    function introduce(person: {name: string}): void;
    function introduce(person: {name: string; age: number}): void;
    function introduce(person: {name: string; age: number; isStudent: boolean}): void;
    function introduce(person: any): void {
        let { name, age, isStudent } = person;

        if (name) console.log(`I'm ${name}.`);
        if (age) console.log(`I'm ${age}.`);
        if (isStudent) console.log(`I'm a student.`);
    }

    introduce({name: 'alex'});
    introduce({name: 'alex', age: 20});
    introduce({name: 'alex', age: 20, isStudent: true});
    ```
    함수명과 매개변수의 개수가 같아야 사용할 수 있다.<br />
    함수의 오버로드 선언을먼저 해주고 마지막에 함수를 정의해준다.<br />

### 4. 리터럴 타입
* 문자열 리터럴 타입
    ```Typescript
    type Position = 'static' | 'relative' | 'absolute' | 'fixed' | 'sticky';

    function(position: Position): void {
        // 로직
    }
    ```
* 숫자형 리터럴 타입
    ```Typescript
    interface Dice{
        number: 1 | 2 | 3 | 4 | 5 | 6;
    }
    ```
    Enum 과 유사한 역할을 할 수 있다.<br />