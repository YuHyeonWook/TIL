# class

```jsx
// 익명 클래스 표현식
const Person = class {};

// 기명 클래스 표현식
const Person = class MyClass {};
```

- class는 함수이면서, 익명 클래스와 기명 클래스로 표현할 수 있다.

### 클래스와 생성자 함수의 정의 방식 비교

```jsx
// 클래스 선언문
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name; // name 프로퍼티는 public하다.
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }

  // 정적 메서드
  static sayHello() {
    console.log("Hello!");
  }
}

// 인스턴스 생성
const me = new Person("Lee");

// 인스턴스의 프로퍼티 참조
console.log(me.name); // Lee
// 프로토타입 메서드 호출
me.sayHi(); // Hi! My name is Lee
// 정적 메서드 호출
Person.sayHello(); // Hello!
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/3dc8f80f-96fb-48e6-9348-31ce2015f623)

## 클래스 호이스팅

```jsx
// 클래스 선언문
class Person {}

console.log(typeof Person); // function
```

```jsx
console.log(Person);
// ReferenceError: Cannot access 'Person' before initialization

// 클래스 선언문
class Person {}
```

```jsx
const Person = "";

{
  // 호이스팅이 발생하지 않는다면 ''이 출력되어야 한다.
  console.log(Person);
  // ReferenceError: Cannot access 'Person' before initialization
}
```

- 클래스는 함수로 평가되고, 클래스 정의 이전에 참조할 수 없다. 따라서 클래스 선언문은 마치 호이스팅이 발생하지 않는 것처럼 보이나 그렇지는 않다. 변수 선언, 함수 정의와 마찬가지로 호이스팅이 발생한다.
- 클래스는 let, const 키워드로 선언한 변수처럼 동일하게 호이스팅된다. 클래스 선언문 이전에 일시적 사각지대 (TDZ)에 빠지게 되어 호이스팅이 발생하지 않는 것처럼 동작함.

<aside>
💡 var, let, const, function,  class 키워드들은 선언된 모든 식별자는 호이스팅된다. 모든 선언문은 런타입 이전에 먼저 실행되기 때문이다.

</aside>

## 인스턴스 생성

```jsx
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); // Person {}
```

- 클래스는 생성자 함수이며 new 연산자와 함꼐 호출되어 인스턴스를 생성한다. new연산자 없이 호출하면 타입 에러가 발생한다.

```jsx
class Person {}

// 클래스를 new 연산자 없이 호출하면 타입 에러가 발생한다.
const me = Person();
// TypeError: Class constructor Person cannot be invoked without 'new'
```

## 메서드

- 클래스 몸체에는 0개 이상의 메서드만 선언할 수 있다. 클래스 몸체에서 정의할 수 있는 메서드는 constructor(생성자), 프로토타입 메서드, 정적 메서드의 세 가지가 있다.

### constructor

- constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메서드이다.

```jsx
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }
}

// 클래스는 함수다.
console.log(typeof Person); // function
console.dir(Person);
```

- **클래스는 인스턴스를 생성하기 위한 생성자 함수**이다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/54f69cdd-4778-47d1-bc77-4aa3d45fdb0f)

- 또한 클래스는 함수와 동일하게 프로토타입과 연결되어 있고, 자신의 스코프 체인을 구성한다.
- 모든 함수 객체가 가지고 있는 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor 프로퍼티는 클래스 자신을 가리키고 있다. 이는 클래스가 인스턴스를 생성하는 생성자 함수라는 것을 의미한다. 즉, **new 연산자와 함께 클래스를 호출하면 클래스는 인스턴스를 생성**한다.

### constructor는 생성자 함수와 유사하지만 몇 가지 차이

1. constructor는 클래스 내에 최대 한 개만 존재할 수 있다.

```jsx
class Person {
  constructor() {}
  constructor() {}
}
// SyntaxError: A class may only have one constructor
```

또한 constructor을 생략할 수 있다.

1. **constructor 내부에서 this에 인스턴스 프로퍼티**를 추가하면 초기화된 인스턴스를 생성할 수 있다.

```jsx
class Person {
  constructor() {
    // 고정값으로 인스턴스 초기화
    this.name = "Lee";
    this.address = "Seoul";
  }
}

// 인스턴스 프로퍼티가 추가된다.
const me = new Person();
console.log(me); // Person {name: "Lee", address: "Seoul"}
```

- 인스턴스를 생성할 때 클래스 외부에서 인스턴스 프로퍼티의 초깃값을 전달하려면 constructor에 매개변수를 선언하고 인스턴스를 생성할 때 초깃값을 전달하면 된다. 밑에 처럼

```jsx
class Person {
  constructor(name, addres) {
    // 고정값으로 인스턴스 초기화
    this.name = name;
    this.address = addres;
  }
}

// 인스턴스 프로퍼티가 추가된다.
const me = new Person("Lee", "Seoul");
console.log(me); // Person {name: "Lee", address: "Seoul"}
```

1. constructor 내부에 return문을 생략한다.

- this가 아닌 다른 객체를 명시적으로 반환하면 this는 인스턴스가 반환되지 못하고 return 문을 명시한 객체가 반환된다.

```jsx
class Person {
  constructor(name) {
    this.name = name;

    // 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
    return {};
  }
}

// constructor에서 명시적으로 반환한 빈 객체가 반환된다.
const me = new Person("Lee");
console.log(me); // {}
```

```jsx
class Person {
  constructor(name) {
    this.name = name;

    // 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.
    return 100;
  }
}

const me = new Person("Lee");
console.log(me); // Person { name: "Lee" }
```

- 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.
- 이처럼 constructor 내부에서 명시적으로 this가 아닌 다른 값을 반환하는 것은 클래스의 기본 동작을 훼손하는 것이다.

### 프로토타입 메서드

```jsx
// 생성자 함수
function Person(name) {
  this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHi = function () {
  console.log(`Hi! My name is ${this.name}`);
};

const me = new Person("Lee");
me.sayHi(); // Hi! My name is Lee
```

- 생성자 함수를 사용하여 인스턴스를 생성하는 경우 프로토타입 메서드를 생성하기 위해서는 명시적으로 프로토 타입에 메세더를 추가하면 된다.

```jsx
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
}

const me = new Person("Lee");
me.sayHi(); // Hi! My name is Lee
```

- 생성자 함수에 의한 객체 생성 방식과 다르게 클래스의 prototype 프로퍼티에 메서드를 추가하지 않아도 기본적으로 프로토타입 메서드가 된다.

### 정적 메서드

- 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드를 말한다.

```jsx
// 생성자 함수
function Person(name) {
  this.name = name;
}

// 정적 메서드
Person.sayHi = function () {
  console.log("Hi!");
};

// 정적 메서드 호출
Person.sayHi(); // Hi!
```

```jsx
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }

  // 정적 메서드
  static sayHi() {
    console.log("Hi!");
  }
}
```

- 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드(클래스 메서드)가 된다.

```jsx
// 정적 메서드는 클래스로 호출한다.
// 정적 메서드는 인스턴스 없이도 호출할 수 있다.
Person.sayHi(); // Hi!
```

- 정적 메서드는 프로토타입 메서드 처럼 인스턴스로 호출하지 않고 클래스로 호출한다. 따라서 정적 메서드는 인스턴스로 호출 할 수 없다.

```jsx
// 인스턴스 생성
const me = new Person("Lee");
me.sayHi(); // TypeError: me.sayHi is not a function
```

### 정적 메서드와 프로토타입 메서드의 차이

1. 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.

```jsx
class Square {
  // 정적 메서드
  static area(width, height) {
    return width * height;
  }
}

console.log(Square.area(10, 10)); // 100
```

- 정적 메서드 area는 인스턴스 프로퍼티를 참조하지 않는다. 참조해야한다면 정적 메서드 대신 프로토타입 메서드를 사용해야 한다.

```jsx
class Square {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  // 프로토타입 메서드
  area() {
    return this.width * this.height; // 프로토타입 메서드 내부 this
  }
}

const square = new Square(10, 10); // 프로토타입 메서드를 호출한 인스턴스
console.log(square.area()); // 100
```

- 프로토타입 메서드는 인스턴스로 호출해야 하므로 프로토타입 메서드 내부의 this는 프로토타입 메서드를 호출한 인스턴스를 가리킨다.
- 위 예제인 **프로토타입 메서드**는 **프로토타입 메서드 내부 this는 square 객체를 가리킨다**. 반면 **정적 메서드**는 클래스로 호출해야 하므로 **정적 메서드 내부 this는 인스턴스가 아닌 클래스를 가리킨다.** 즉, 프로토타입과 정적 메서드 내부의 this 바인딩이 다르다.
  - 따라서, 메서드 내부에서 인스턴스 프로퍼티를 참조할 필요가 있다면 this를 사용해야 하며, 이러한 경우 프로토타입 메서드로 정의해야 한다.

## 클래스의 인스턴스 생성 과정

```jsx
class Person {
  // 생성자
  constructor(name) {
    // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
    console.log(this); // Person {}
    console.log(Object.getPrototypeOf(this) === Person.prototype); // true

    // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
    this.name = name;

    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
  }
}
```

1. 암묵적으로 인스턴스가 생성되고 this에 바인딩
2. this에 바인딩되어 있는 인스턴스를 초기화
3. 인스턴스 반환

## 프로퍼티

### 인스턴스 프로퍼티

```jsx
class Person {
  constructor(name) {
    // 인스턴스 프로퍼티
    this.name = name;
  }
}

const me = new Person("Lee");
console.log(me); // Person {name: "Lee"}
```

### 접근자 프로퍼티(getter, setter)

```jsx
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }

  // setter 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(" ");
  }
}

const me = new Person("Ungmo", "Lee");

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
console.log(`${me.firstName} ${me.lastName}`); // Ungmo Lee

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
me.fullName = "Heegun Lee";
console.log(me); // {firstName: "Heegun", lastName: "Lee"}

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(me.fullName); // Heegun Lee

// fullName은 접근자 프로퍼티다.
// 접근자 프로퍼티는 get, set, enumerable, configurable 프로퍼티 어트리뷰트를 갖는다.
console.log(Object.getOwnPropertyDescriptor(Person.prototype, "fullName"));
// {get: ƒ, set: ƒ, enumerable: false, configurable: true}
```

- 접근자 프로퍼티는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수이다. 즉, getter 함수와 setter 함수로 구성되어 있다.
- getter와 setter는 인서턴스 프로퍼티처럼 사용된다. getter의 경우 반환되는 것이고, setter의 경우 프로퍼티 처럼 값을 할당하는 형식으로 사용한다.
  - setter는 단 하나의 값만 할당받기 떄문에 단 하나의 매개변수만 선언할 수 있다.

## 상속에 의한 클래스 확장

### extends 키워드

- 상속을 통해 클래스를 확장하려면 extends 키워드를 사용한다..

```jsx
// 수퍼(베이스/부모)클래스
class Base {}

// 서브(파생/자식)클래스
class Derived extends Base {}
```

### super 키워드

- super 키워드는 함수처럼 호출할 수도 있고, this와 같이 식별자 처럼 참조할 수 있다.
- 또한, super 키워드는 부모의 클래스를 호출하는 것이다.

super 동작

- super를 호출하면 부모클래스의 constructor를 호출한다.
- super를 참조하면 부모클래스의 메서드를 호출할 수 있다.

<br>
# 참고
- 모던 자바스크립트 딥다이브
