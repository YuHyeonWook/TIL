# var를 지양, 함수 스코프와 블록 스코프

## var를 지양하자

- let & const 사용 권장함
- var는 함수 스코프이고, 재선언과 재할당이 가능하고 반면에 let & const 블록 스코프이다. let은 재할당은 가능하지만 재선언은 되지 않는다. const는 재선언과 재할당이 불가능하다.

```
var name = "이름";
console.log(name);
var name = "이름2";
console.log(name);
```

```
console.log(name2); // undefined
var name2 = "hello";
console.log(name2);
```

- 호이스팅으로 인해, 변수 선언이 먼저 가기 때문에 아래와 같이 undefined가 나온다.

```
let name = "이름";
name = "이름2";
```

- let (변수 선언 및 재할당 가능)

```
const name = "이름;
```

- const (변수 선언시 할당해주어야 한다)

---

## 함수 스코프와 블록 스코프

- var는 Function 단위이므로 지역에서 할당한 변수가 전역까지 오염된다.

```jsx
var global = "전역";

if (global === "전역") {
  var global = "지역";

  console.log(global); //지역
}
console.log(global); // 지역
```

```jsx
let global = "전역";

if (global === "전역") {
  var global = "지역";

  console.log(global); //지역
}
console.log(global); // 지역
```

- let는 block 단위이므로 전역에 오염되지 않는다.

const & let 사용

```jsx
const global = "전역";

{
  let global = "지역";

  console.log(global); // 지역
}
console.log(global); // 전역
```

- 안전하게 코드를 사용하기 위해 let과 const를 사용하는 것이 좋다.
- 또한, let 보다는 **const 를 쓰는 것**이 **좋다**. 그 이유는 밑에서 보자

```jsx
const person = {
  // 선언과 할당 이루어짐
  name: "wook",
  age: 22,
};
person = {
  // 재할당 에러 발생
  name: "gim",
  age: 20,
};
```

- 밑에 처럼 다시 객체에 재할당을 하게 되면 에러가 발생한다.

```jsx
const person = {
  // 선언과 할당 이루어짐
  name: "wook",
  age: 22,
};
person.name = "lee";
person.age = 30;

console.log(person); // { name: 'lee', age: 30 }
```

위 처럼 객체의 프로퍼티에 할당을 하면 객체의 프로퍼티 값이 변경됨
