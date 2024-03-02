# first-last, **접두사-접미사,** 매개변수의 순서가 경계

# first-last

- first-last는 포함된 양 끝을 의미한다.
- ~ 부터 ~ 까지

```jsx
const students = ["현욱", "기철", "수철"];

function getStudents(first, last) {
  // ...some code
}

getStudents(students[0], students[2]);
// getStudents('현욱', '수철');
```

# **접두사(Prefix)-접미사(Suffix)의 중요성**

- 프로그래밍에서 사용한 접두사와 접미사가 있다. ex) 리액트 훅, 리덕스,
- 팀 내에서 접두사와 접미사의 약속을 개인적으로 만들어두거나 이미 만들어졌을 때 직관적으로 볼 수 있어서 개발하는데 유용하다.

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/343dce68-db17-404a-b8e7-35c8c2b50567)

- 접미사는 단어의 뒷쪽에 붙는 것이다.
- 밑에서는 프로그래밍과 관련한 접두사와 접미사의 사용 예시를 보자

JS의 prefix getter, setter 예시

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/1dd026b1-d673-4deb-b1d5-52bcbb37f5c1)

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/c2adc913-0303-40a3-b5bd-377ec371f1c6)

리액트 훅을 예시

```jsx
useState
useEffect
useContext
...
useReducer
```

- use가 붙은 것은 hook이라는 약속이다.

jQuery prefix ‘$’ 예시

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/1bbf7216-2d9e-4ddc-9004-6f6ddef5f109)

## 정리

- 접두사와 접미사를 활용하면 코드를 읽는 일관성을 가질 수 있다.

# 매개변수의 순서가 경계이다.

- 호출할때 함수의 네이밍과 인자의 순서의 연관성을 고려해야한다.
- 매개변수의 순서에 따라 함수의 역할을 추론할 수 있다.

```jsx
function someFunc(someArg1, someArg2, someArg1, someArg2) {}

function getFunc(someArg3, someArg4) {
  // 많이 쓰는 매개변수 일 경우 이렇게 들고온다.
  someFunc(undefined, undefined, someArg3, someArg4);
}

function someFunc2({ someArg1, someArg2, someArg1, someArg2 }) {}

getRandomNumber(1, 50);
getDates("2021-01-01", "2021-12-31");
shuffleArray(1, 5);
```

- 유지보수에 취약하지 않은 함수를 만들기 위해서는 규칙이 있다.

1. 매개변수를 2개가 넘지 않도록 만든다.

```jsx
function getFunc(someArg, someArg2) {
...
}
```

2. arguments, rest parameter(나머지 매개변수, …)를 고려해야한다.

```jsx
function foo(param, ...rest) {
  console.log(param); // 1
  console.log(rest); // [ 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
```

```jsx
function bar(param1, param2, ...rest) {
  console.log(param1); // 1
  console.log(param2); // 2
  console.log(rest); // [ 3, 4, 5 ]
}

bar(1, 2, 3, 4, 5);
```

3. 매개변수를 객체에 담아서 넘긴다.

```jsx
function someFunc2({ someArg1, someArg2, someArg3, someArg4 }) {
...
}
```

4. 이미 만든 함수가 있다면 랩핑하는 함수를 만든다.

```jsx
// 기존 함수
function greet(name) {
  return `Hello, ${name}!`;
}

// 랩핑 함수
function greetWithLogging(name) {
  console.log("greetWithLogging function was called");
  const result = greet(name);
  console.log("greet function was called");
  return result;
}

console.log(greetWithLogging("John")); // "Hello, John!"

// greetWithLogging function was called
// greet function was called
// Hello, John!
```

- 래핑된 함수는 기존 함수의 기능을 확장하거나 수정할 수 있다. 위 코드에서는 greetWithLogging함수는 greet 함수를 랩핑한다.

<br>

# 참고

- 클린코드 js
