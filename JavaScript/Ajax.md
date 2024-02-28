# Ajax

## Ajax(Asynchronous javascript and XML)란

- 자바스크립트를 사용하여 브라우저가 서버에게 **비동기 방식으로 데이터를 요청**하고, → 서버가 응답한 데이터를 수신하여 **웹페이지를 동적으로 갱신하는 프로그래밍 방식**을 말한다.
- Ajax는 브라우저에서 제공하는 Web API인 XMLHttpRequest 객체를 기반으로 동작한다.
- XMLHttpRequest는 **HTTP 비동기 통신을 위한 메서드와 프로퍼티를 제공**한다.

이전의 브라우저는 화면이 전환되면 서버로부터 새로운 HTML을 전송받아 웹페이지 전체를 처음부터 다시 렌더링한다. 이러한 전통적인 방식은 다음과 같은 단점이 있다.

![alt text](image.png)

- 위와 같은 단점들로 Ajax의 등장은 전통적인 패러다임을 획기적으로 전환했다. 이를 통해 브라우저에서도 데스크탑 애플리케이션과 유사한 빠른 동작이 가능해졌다.
- 또한, Ajax는 전통적인 방식과의 장점이 있다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/c1f780cc-b06e-4b0a-b59b-c47213424496)

## JSON(javascript object notation\_

- JSON은 클라이언트와 서버 간의 http 통신을 위한 텍스트 데이터 포맷이다. 자바스크립트에 종속되지 않는 언어 독립형 데이터 포맷으로, 대부분의 프로그래밍 언어에서 사용할 수 있다.

### JSON 표기 방식

- JSON은 자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트이다.

```jsx
{
    "name": "Lee",
    "age": 20,
    "alive": true,
    "hobby": ["traveling", "tennis"]
  }
```

- JSON의 키는 반드시 큰따옴표(작은 따옴표 사용불가) 로 묶어야한다. 같은 객체 리터럴과 같은 표기법을 그대로 사용할 수 있다. 하지만 문자열도 큰따옴표로 묶어야한다.

### JSON.stringify

- **JSON.stringify 메서드는 객체를 → JSON 포맷의 문자열로 변환**한다. 클라이언트가 서버로 객체를 전송하려면 객체를 문자열화해야 하는데 이를 **직렬화**라고 한다.

```jsx
const obj = {
  name: "Lee",
  age: 20,
  alive: true,
  hobby: ["traveling", "tennis"],
};

// 객체를 JSON 포맷의 문자열로 변환한다.
const json = JSON.stringify(obj);
console.log(typeof json, json);
// string {"name":"Lee","age":20,"alive":true,"hobby":["traveling","tennis"]}

// 객체를 JSON 포맷의 문자열로 변환하면서 들여쓰기 한다.
const prettyJson = JSON.stringify(obj, null, 2);
console.log(typeof prettyJson, prettyJson);
/*
string {
  "name": "Lee",
  "age": 20,
  "alive": true,
  "hobby": [
    "traveling",
    "tennis"
  ]
}
*/

// replacer 함수. 값의 타입이 Number이면 필터링되어 반환되지 않는다.
function filter(key, value) {
  // undefined: 반환하지 않음
  return typeof value === "number" ? undefined : value;
}

// JSON.stringify 메서드에 두 번째 인수로 replacer 함수를 전달한다.
const strFilteredObject = JSON.stringify(obj, filter, 2);
console.log(typeof strFilteredObject, strFilteredObject);
/*
string {
  "name": "Lee",
  "alive": true,
  "hobby": [
    "traveling",
    "tennis"
  ]
}
*/
```

배열을 JSON 포맷의 문자열로 변환 예시)

```jsx
const todos = [
  { id: 1, content: "HTML", completed: false },
  { id: 2, content: "CSS", completed: true },
  { id: 3, content: "Javascript", completed: false },
];

// 배열을 JSON 포맷의 문자열로 변환한다.
const json = JSON.stringify(todos, null, 2);
console.log(typeof json, json);
/*
string [
  {
    "id": 1,
    "content": "HTML",
    "completed": false
  },
  {
    "id": 2,
    "content": "CSS",
    "completed": true
  },
  {
    "id": 3,
    "content": "Javascript",
    "completed": false
  }
]
*/
```

- JSON.stringify 메서드는 객체뿐만 아니라 배열도 JSON 포맷의 문자열로 반환한다.

### JSON.parse

- J**SON.parse메서드는 JSON포맷의 문자열을→ 객체로 변환**한다. 서버로부터 클라이언트에게 전송된 JSON 데이터는 문자열이다. 이 문자열을 객체로서 사용하려면 JSON 포맷의 문자열을 객체화해야 하는데 이를 **역직렬화**라고 한다.

```jsx
const obj = {
  name: "Lee",
  age: 20,
  alive: true,
  hobby: ["traveling", "tennis"],
};

// 객체를 JSON 포맷의 문자열로 변환한다.
const json = JSON.stringify(obj);

// JSON 포맷의 문자열을 객체로 변환한다.
const parsed = JSON.parse(json);
console.log(typeof parsed, parsed);
// object {name: "Lee", age: 20, alive: true, hobby: ["traveling", "tennis"]}
```

문자열로 변환되는 경우 배열 객체로 변환하는 예시)

```jsx
const todos = [
  { id: 1, content: "HTML", completed: false },
  { id: 2, content: "CSS", completed: true },
  { id: 3, content: "Javascript", completed: false },
];

// 배열을 JSON 포맷의 문자열로 변환한다.
const json = JSON.stringify(todos);

// JSON 포맷의 문자열을 배열로 변환한다. 배열의 요소까지 객체로 변환된다.
const parsed = JSON.parse(json);
console.log(typeof parsed, parsed);
/*
 object [
  { id: 1, content: 'HTML', completed: false },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'Javascript', completed: false }
]
*/
```

- 배열이 JSON 포맷의 문자열로 변환되어 있는 경우 JSON.parse는 문자열을 배열 객체로 변환한다. 배열의 요소가 객체인 경우 배열의 요소까지 객체로 변환한다.

<br>

# 참고

- 모던 js 딥다이브
