# map 함수를 이용한 컴포넌트 반복

## 자바스크립트 배열의 map() 함수

- 자바스크립트 배열 객체의 내장 함수인 map 함수를 사용하여 반복되는 컴포넌트를 렌더링할 수 있다.

```jsx
let numbers = [1, 2, 3, 4, 5];

let processed = numbers.map((el) => el * el);

console.log(processed); // (5) [1, 4, 9, 16, 25]
```

## 데이터 배열을 컴포넌트 배열로 변환하기

```jsx
const EventPractice = () => {
  const names = ["눈", "얼음", "바람", "사람"];
  const nameList = names.map((el) => <li>{el}</li>);
  return <ul>{nameList}</ul>;
};
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/12c114e6-b61c-4ff7-9997-5c29f185b3e4)

- 문자열로 구성된 배열 값을 사용하여 <li></li> jsx 코드로 된 배열을 새로 생성한 후 nameList에 담는다.

```jsx
EventPractice.js:6 Warning: Each child in a list should have a unique "key" prop.

Check the render method of `EventPractice`. See https://reactjs.org/link/warning-keys for more information.
    at li
    at EventPractice
    at App
```

- 브라우저에 원하는 대로 렌더링이 되었지만, 개발자 도구의 출력결과 ‘key’ prop이 없다는 경고 메시지를 표시하고 있다. key란 무엇인지 밑에서 확인해보자.

## key

- 리액트에서 key는 컴포넌트 배열을 렌더링했을 때 어떤 원소에 변동이 있었는지 알아내려고 사용한다.
- 유동적인 데이터를 다룰 때는 원소를 새로 생성, 제거, 수정할 수 있다.
  - key가 없을 때 Virtual DOM을 비교하는 과정에서 리스트를 순차적으로 비교하면서 변화를 감지함.
  - key가 있다면 이 값을 사용하여 어떤 변화가 일어났는지 빠르게 알아낼 수 있다.

### key설정

- key 값을 설정할 때는 map 함수의 인자로 전달되는 함수 내부에서 컴포넌트 props를 설정하듯이 설정하면됨. key값은 언제나 유일해야함.
  - 따라서 데이터가 가진 교유값을 key값으로 설정해야 한다.

key값을 설정한 예시)

```jsx
const articleList = articles.map(article => (
  <Article
      title={article.title}
      writer={article.writer}
      key={article.id}
  />
);
```

고유 번호가 없는 컴포넌트에서는 map함수에 전달되는 콜백 함수의 인수인 index 값을 사용하면 된다.

```jsx
const EventPractice = () => {
  const names = ["눈", "얼음", "바람", "사람"];
  const nameList = names.map((el, idx) => <li key={idx}>{el}</li>);
  return <ul>{nameList}</ul>;
};
```

- 이렇게 바꿔주면 경고 메시지 발생 하지 않음.
- 따라서 고유한 값이 없을 때만 index 값을 key로 사용해야한다. index를 key로 사용하면 배열이 변경될 때 효율저그올 리렌더링하지 못한다.

## 응용

- 세 가지 상태를 사용한다. 하나는 데이터 배열, 두번째 텍스트를 입력할 수 있는 input의 상태이다. 세번째는 데이터 배열에서 새로운 항목을 추가할때 사용할 고유 id를 위한 상태이다.

```jsx
import React, { useState } from "react";

const EventPractice = () => {
  const [names, setNames] = useState([
    { id: 1, text: "눈" },
    { id: 2, text: "얼음" },
    { id: 3, text: "바람" },
    { id: 4, text: "사람" },
  ]);
  const [inputText, setInputText] = useState("");
  const [nextId, setNextId] = useState(5); // 새로운 항목을 추가할 때 사용할 id

  const nameList = names.map((el) => <li key={el.id}>{el.text}</li>);
  return <ul>{nameList}</ul>;
};
export default EventPractice;
```

- map 함수를 활용하여 key 값을 index 대신 el.id값으로 지정해줌.
- 브라우저에 동일한 결과가 나타남.

### 데이터 추가 기능 구현

```jsx
import React, { useState } from "react";

const EventPractice = () => {
  const [names, setNames] = useState([
    { id: 1, text: "눈사람" },
    { id: 2, text: "얼음" },
    { id: 3, text: "눈" },
    { id: 4, text: "바람" },
  ]);
  const [inputText, setInputText] = useState("");
  const [nextId, setNextId] = useState(5); // 새로운 항목을 추가할 때 사용할 id

  const onChange = (e) => setInputText(e.target.value);
  const onClick = () => {
    const nextNames = names.concat({
      id: nextId, // nextId 값을 id로 설정하고
      text: inputText,
    });
    setNextId(nextId + 1); // nextId 값에 1을 더해 준다.
    setNames(nextNames); // names 값을 업데이트한다.
    setInputText(""); // inputText를 비운다.
  };

  const namesList = names.map((name) => <li key={name.id}>{name.text}</li>);
  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{namesList}</ul>
    </>
  );
};
export default EventPractice;
```

### 데이터 제거 기능 구현

```jsx
const numbers = [1, 2, 3, 4, 5, 6];
const biggerThanThree = numbers.filter((number) => number > 3);
// 결과: [4, 5, 6]
```

- 불변성을 유지하면서 배열의 특정 항목을 지울 때는 배열의 내장 함수 filter를 사용한다.
- filter 함수를 응용하여 특정 배열에서 특정 원소만 제외시킬 수 있다.
