# **Props - 컴포넌트에 값 전달하기**

- 리액트에서의 **props**는 **부모가 자식 컴포넌트에 단일 객체 형태로 값을 전달**할 수 있다.
  - Props는 Properties의 줄임말로 속성이라는 뜻이다.
  - 어떠한 값을 컴포넌트에게 전달해줘야 할 때, props 를 사용함
- 리액트에서는 보통 재사용하려는 요소를 **컴포넌트**로 만듬.
  - 예를 들어 게시판 페이지를 리액트로 만든다고 가정해보자. 사용자가 게시판에서 작성한 글은 게시물 리스트에서 하나의 항목으로 표시됨. 그런데 이 리스트에 존재하는 여러 게시물 항목은 내용은 각각 다르지만, 모두 동일한 구조이다.
  - 리액트에서는 내용은 다르지만 구조가 같은 요소를 주로 컴포넌트로 만듬
  - 여러 게시물 리스트를 페이지에 표시할 때는 이 컴포넌트를 반복해 렌더링하고, 게시물 각각의 내용은 Props로 전달함.

![al

- 위 그림의 감정 일기장은 일기 리스트를 보여주는데, 각각의 일기 항목은 **컴포넌트**로 구성되어 있다. 현재 감정 일기장에는 일기 컴포넌트가 2개 있는 셈이다.
- 2개의 일기 컴포넌트는 요소의 크기나 배열 등은 모두 같지만, 일기 내용, 작성일자, 감정 상태를 표현하는 이미지는 다르다. 이렇듯 리액트에서는 컴포넌트의 공통 기능이 아닌 **세부 기능을 표현할 때 Props를 사용함.**
- 다음 그림과 같이 App인 부모가 Props로 작성일, 일기내용, 감정 상태를 전달 하면, 일기 컴포넌트는 전달된 Props를 토대로 일기 리스트를 페이지에 렌더링함.

<br>

## **Props로 값 전달하기**

- Props는 **부모만이 자식 컴포넌트에 전달**할 수 있다. 그 반대는 성립하지 않는다.
  - Body 컴포넌트에 Props를 전달하려면 부모인 App 컴포넌트에서 전달해야 함

App.js)

```jsx
(...)

function App() {
  const name = "이정환";
  return (
    <div className="App">
      <Header />
      <Body name={name} /> ①
      <Footer />
    </div>
  );
}

export default App;
```

- **①** Props를 전달하려는 자식 컴포넌트 태그에서 이름={값} 형식으로 작성하면 됨

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/adb31974-882b-40c0-aca6-5ab10780bed8/Untitled.png)

- 위 그림은 App 컴포넌트가 Body에 Props 전달함

<br>

## **Props로 여러 개의 값 전달하기**

```jsx
(...)

function App() {
  const name = "이정환";
  return (
    <div className="App">
      <Header />
      <Body name={name} location={"부천시"} /> ①
      <Footer />
    </div>
  );
}

export default App;
```

- **①** App컴포넌트에서 Body 컴포넌트에 Props로 2개의 값 name, location을 전달함.
- 변수를 미리 선언하지 않아도 location={"부천시"} 처럼 객체 Props에 프로퍼티를 추가해 전달 할 수 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/c856804d-3e73-4c65-a744-0d91995abc08/Untitled.png)

```jsx
function Body(props) {
  console.log(props); // ①
  return (
    <div className="body">
      ② {props.name}은 {props.location}에 거주합니다
    </div>
  );
}
export default Body;
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/dc0ddca8-c865-4c0b-9134-fef468ab3e14/Untitled.png)

- Props로 전달한 2개의 값을 확인할 수 있다.

<br>

### 데이터 흐름은 단방향

리액트는 데이터를 항상 부모에서 자식 아래로 전달하는 단방향 데이터 흘러서 데이터를 관리하기에 좋다. 하지만, state를 변경하는 이벤트는 자식에서 부모를 향해 역방향으로 전달된다.

![20240213_233621.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/1d9edc6f-88da-4bef-a281-f46708811dde/20240213_233621.jpg)

![20240213_233426.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/5f4b5443-e0ed-4db1-9536-6419f164571c/20240213_233426.jpg)

위의 그림에서 controller 컴포넌트에 있는 버튼 요소를 클릭할 때마다 App 컴포넌트의 state를 엡데이트 하는 이벤트가 발생함. App컴포넌트는 자신이 관리하는 setState를 변경하는 함수를 props로 전달해 자식이 부모의 state를 대신 업데이트하게함

따라서, 데이터는 위에서 아래로, 이벤트는 아래에서 위로 향하도록 설계되어야함

<br>

## **스프레드 연산자로 여러 개의 값 쉽게 전달하기**

- 반대로 부모 컴포넌트에서 Props로 전달할 값이 많으면, 값을 일일이 명시해야 하므로 불편할 뿐만 아니라 가독성도 떨어짐
- 이때 Props로 값을 하나의 객체로 만든 다음, 스프레드 연산자를 활용해 전달하면 훨씬 간결하게 코드를 작성할 수 있다.

```jsx
(...)

function App() {
  const BodyProps = { ①
    name: "이정환",
    location: "부천시",
  };

  return (
    <div className="App">
      <Header />
      <Body {...BodyProps} /> ②
      <Footer />
    </div>
  );
}
export default App;
```

- **①** Body 컴포넌트에 Props로 전달할 값을 객체 BodyProps로 만듬.
- **②** 스프레드 연산자로 객체 BodyProps 각각의 프로퍼티를 Props 값으로 전달함.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/6e3f482c-d9ad-4d16-8fcb

<br>

## **Props로 컴포넌트 전달하기 (props.children)**

- 지금까지 컴포넌트 간에 Props로 문자열이나 숫자 같은 자바스크립트 값을 전달해 보았다. 그런데 Props로는 자바스크립트 값뿐만 아니라 컴포넌트도 전달할 수 있다.

```jsx
(...)
function ChildComp() { ①
  return <div>child component</div>;
}

function App() {
  return (
    <div className="App">
      <Header />
      <Body>
        <ChildComp /> ②
      </Body>
      <Footer />
    </div>
  );
}

export default App;
```

- ① 새로운 컴포넌트 ChildComp를 만듬
- ② ChildComp를 Body 컴포넌트의 자식 요소로 배치함
- Body 컴포넌트의 자식 요소로 ChildComp를 배치함.
- 리액트에서는 자식 컴포넌트에 또 다른 컴포넌트를 배치하면, 배치된 컴포넌트는 자동으로 Props의 children 프로퍼티에 저장되어 전달됨

```jsx
function Body({ children }) { ①
  console.log(children);
  return <div className="body">{children}</div>; ③
}
export default Body;
```

- ① App에서 Body 컴포넌트의 자식으로 배치한 ChildComp는 children 프로퍼티로 전달되어 매개 변수 children에 저장됨
- ③ children을 자바스크립트 표현식을 사용하듯 렌더링함
- Props의 children 프로퍼티로 전달되는 자식 컴포넌트는 값으로 취급하므로 JSX의 자바스크립트 표현식으로 사용할 수 있다.
- children에는 컴포넌트 ChildComp가 저장되어 있기 때문에 해당 컴포넌트를 렌더링함

저장하고 결과를 콘솔과 페이지에서 확인)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/7b871df3-4a85-41b6-b6d0-542420c1eaa6/Untitled.png)

- 컴포넌트를 개발자 도구의 콘솔에서 출력하면 객체 형식의 값을 출력함. 앞서 JSX에서는 자바스크립트 표현식이 객체를 평가할 경우 오류가 발생한다고 했지만, 이 객체는 리액트 컴포넌트를 표현한 것이므로 오류가 발생하지 않는다.
