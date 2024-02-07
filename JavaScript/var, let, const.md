# var, let, const

**var : 재선언과 재할당이 가능**

**let : 재할당은 가능하지만 재선언 불가능**

- var, let은 재할당이 가능한 변수이다.

**const :** **재선언과 재할당 불가능한 상수**

- const는 변수를 선언할 시 값을 반드시 할당하여 정의해야 함

</br>

**var : 함수 레벨 스코프**

- **var**는 함수 내부에 선언된 변수만 지역 변수로 인정하는 **함수 레벨 스코프**

**let, const : 블록 레벨 스코프**

- **let, const**는 **모든 블록** 내부에서 선언된 변수까지 지역변수로 인정하는 **블록 레벨 스코프**
- 세 가지 모두 최상위로 호이스팅 되지만, `var` 변수만 `undefined(정의되지 않음)`으로 초기화되고 `let`과 `const` 변수는 초기화되지 않는다.

</br>

## var

- `var` 선언은 전역 범위 혹은 함수 범위로 지정됨.

**전역 범위**

- var변수가 함수 외부에서 선언될 때의 범위는 전역임. 즉, var를 사용하여 선언된 모든 변수를 전체 윈도우 상에서 사용할 수 있다.

**함수 범위**

- 함수 내에서 선언될 때 함수 범위로 지정되지만 해당 함수 내에서만 사용할 수 있다.

```jsx
var greeter = "hey hi";

function newFunction() {
  var hello = "hello";
}
```

- `hello`가 함수 범위이고, `greeter`는 함수 밖에 존재하므로 전역 범위임

```jsx
var tester = "hey hi";

function newFunction() {
  var hello = "hello";
}
console.log(hello); // error: hello is not defined
```

- `hello`는 `newFunction()` 함수 밖에서 사용할 수 없기 때문에 에러가 발생함

```jsx
var greeter = "hey hi";
var greeter = "say Hello instead";
```

```jsx
var greeter = "hey hi";
greeter = "say Hello instead";
```

- 이처럼 var는 재할당을 할 수 있다.

### **var의 호이스팅**

- 호이스팅이란 변수와 함수 선언이 맨 위로 이동되는 자바스크립트 매커니즘이다.

```jsx
console.log(greeter); // undefined
var greeter = "say hello";
greeter; // 'say hello'
```

- 위 코드를 js는 밑에 처럼 해석함

```jsx
var greeter;
console.log(greeter); // greeter is undefined
greeter = "say hello";
```

- `var`변수는 범위 내에서 맨 위로 올려지고, 값은 `undefined(정의되지 않음)`으로 초기화됨

### **var의 문제점**

```jsx
var greeter = "hey hi";
var times = 4;

if (times > 3) {
  var greeter = "say Hello instead";
}

console.log(greeter); // "say Hello instead"
```

- `time > 3`가 `true`를 반환하기 때문에 `greeter`는 `"say Hello instead"`로 재정의가 됨.
- 의도적으로 재정의한 것이라면 괜찮겠지만, 변수 greeter가 이미 정의되어 있다는 사실을 인식하지 못한 경우에는 문제가 된다.

</br>

## let

### 블록 범위 let

- 블록은 중괄호 {}을 의미한다. 중괄호 안에 있는 것은 모두 블록 범위이다.
- let으로 선언된 변수는 해당 블록 내에서만 사용가능하다.

```jsx
let greeting = "say Hi";
let times = 4;

if (times > 3) {
  let hello = "say Hello instead";
  console.log(hello); // "say Hello instead"
}
console.log(hello); // hello is not defined
```

- 중괄호로 감싸진 hello 변수가 정의된 블록 외부에서 hello를 사용했더니 에러가 반환됨

### let은 재할당은 되지만, 재선언 불가능

재할당)

```jsx
let greeting = "say Hi";
greeting = "say Hello instead";

greeting; // say Hello instead
```

재선언)

```jsx
let greeting = "say Hi";
let greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared
```

하지만, 동일한 변수가 다른 범위 내에서 정의되면 성립된다.

```jsx
let greeting = "say Hi";
if (true) {
  let greeting = "say Hello instead";
  console.log(greeting); // "say Hello instead"
}
console.log(greeting); // "say Hi"
```

### **let의 호이스팅**

```jsx
console.log(a); // ReferenceError: a is not defined
let a = 10;
```

- **let도 var와 같이 선언부가 위로 끌어올려지지만, undefined로 초기화 되지 않고, 에러가 발생**함.
  - 마치 호이스팅 발생하지 않는 것처럼 보인다. 이는 let,const의 호이스팅 과정이 var와 다르게 진행되기 때문임

let과 const 로 변수를 선언한 경우

- 변수 선언과 초기화는 코드 실행과정에서 변수 선언문을 만났을 때 수행한다.

```jsx
let a; // 선언만 하고 정의는 하지 않음.
console.log(a); // ReferenceError: a is not defined
a = 10;

a; // 10
```

또 다른 let, const 호이스팅 발생 예시)

```
let a = 10;  // 전역변수 a선언

if(true){
    console.log(a); // 10
}
```

- 이 코드는 전역변수로 선언된 a의 값 10을 if문 블럭에서 참조하여 출력함

```
let a = 10;  // 전역변수 a선언

if(true){
    console.log(a);  // ReferenceError: a is not defined
    let a = 20;  // 지역변수 a 선언
}
```

- 이 경우 블록 내의 지역변수 a가 호이스팅 되면서 TDZ(Temporal Dead Zone)이 만들어지면서 에러가 발생하였다.
  - 이는 let과 const는 선언과 초기화 사이에 TDZ가 막고 있어서 선언만 되고, 초기화는 되지 않아 에러가 발생하는 것이다.
  - 변수의 선언과 초기화 사이에 일시적으로 변수 값을 참조할 수 없는 구간을 TDZ라고 한다.

</br>

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/666aadcb-f6b0-4bf2-ab8b-47c13d05a370)

- var : 선언 및 초기화 ⇒ 할당
- let, const : 선언 ⇒ TDZ ⇒ 초기화 ⇒ 할당

</br>

## const

: const로 선언된 변수는 일정한 상수 값을 유지한다.

### **블록 범위 const**

- `let` 선언처럼 `const` 선언도 선언된 블록 범위 내에서만 접근 가능함.

### **const는 재할당, 재선언 불가능**

- `const`로 선언된 변수의 값이 해당 범위 내에서 동일하게 유지됨. 재할당하거나 다시 선언할 수가 없다.

```jsx
const greeting = "say Hi";
greeting = "say Hello instead"; // error: Assignment to constant variable.
```

```jsx
const greeting = "say Hi";
const greeting = "say Hello instead"; // error: Identifier 'greeting' has already been declared
```

모든 const 선언은 선언하는 당시에 초기화 되어야 함

const 객체의 경우 객체의 프로퍼티를 재할당 할 수 있다.

```jsx
const greeting = {
  message: "say Hi",
  times: 4,
};
```

아래와 같이 작업은 불가

```jsx
greeting = {
  words: "Hello",
  number: "five",
}; // error:  Assignment to constant variable.
```

```jsx
greeting.message = "say Hello instead";
// 'say Hello instead'
```

객체의 프로퍼티로 접근해서 재할당가능함

### **const의 호이스팅**

```jsx
console.log(b); // ReferenceError: b is not defined
const b = 10;
```

- `let`과 마찬가지로 `const` 선언부를 맨 위로 끌어올려지지만, 초기화는 일어나지 않아 에러가 발생함
  - 즉, 선언과 초기화 사이에 TDZ가 막고 있어 선언만 되고 초기화는 되지 않아서 에러가 발생함

</br>

# 참고

https://www.freecodecamp.org/korean/news/var-let-constyi-caijeomeun/
