# useContext(컴포넌트 트리에 데이터 공급하기)

## Context

- Context는 리액트 컴포넌트 트리 전체를 대상으로 데이터를 공급하는 기능이다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/d8d54307-4bb9-46c1-96b6-a7a0a46d6b3d)

- Context를 사용하는 이유는 Props Drilling 문제를 해결하기 위해서 이다. Props Drilling란 원하는 목적지까지 데이터를 전달하기 위해서는 경로상에 있는 모든 컴포넌트에 일일이 Props를 전달해야한다. Props를 전달하는 과정이 마치 드릴로 땅을 파고 내려가는 것과 같다고 하여 Props Drilling 문제라고 한다.
  - Props Drilling는 컴포넌트 사이의 데이터 교환 구조를 파악하기 어렵게 만들고, Props를 수정하게 되면 그것을 공유하는 여러 컴포넌트를 모두 살펴 봐야해서 코드의 유지 보수를 어렵게 한다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/f95f2219-8531-4aa2-995d-60dea4306e54)

- 리액트에서 Context는 같은 문맥 아래에 있는 컴포넌트 그룹에 데이터를 공급하는 기능에 사용된다. Context를 이용하면 단계마다 일일이 Props를 전달하지 않고도 컴포넌트 트리 전역에 데이터를 공급할 수 있어 Props Drilling 문제를 간단히 해결할 수 있다.

## ContextAPI

- 리액트의 Context API 를 사용하면, 프로젝트 안에서 전역적으로 사용 할 수 있는 값을 관리 할 수 있다. 또한, ContextAPI는 context를 만들고 다루는 리액트 기능이다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/d11fa988-915a-4b47-9fb3-d6c92d536a04)

```jsx
const MyContext = React.createContext(defalutValue);
```

- 위와 같이 React.createContext를 이용하면 Context를 생성할 수 있다.
- Context에서 데이터를 공급하려면 Context.Provider 기능을 사용해야 한다.

```jsx
import React from "react";

const MyContext = React.createContext(defaultValue);

function App1() {
  const data = "data";
  return (
    <div>
      <Header />
      <MyContext.Provider value={data}>
        {" "}
        ⓐ
        <Body />
      </MyContext.Provider>
    </div>
  );
}
export default App;
```

- ⓐ MyContext.Provider를 App 컴포넌트의 자식으로 배치하여 Provider가 설정한 자식, 자손 컴포넌트들은 MyContext로 묶여 이 객체에서 공급하는 데이터를 사용할 수 있다. Provider 컴포넌트에 Props(value)를 전달해 MyContext가 공급할 값을 설정한다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/dc3f077a-90d8-4790-b6ce-5871019775d1)

- Provider 컴포넌트는 Props로 공급할 데이터를 받아 컴포넌트 트리에서 자신보다 하위에 있는 모든 컴포넌트에 데이터를 공급한다.

```jsx
import React from "react";

const MyContext = React.createContext(defaultValue);

function App1() {
  const data = "data";

  function Main() {
    const data = useContext(MyContext); ⓐ
  }
...
export default App;
```

- ⓐ useContext를 호출하고 인수로 값을 공급할 Context를 전달한다. useContext함수는 해당 Context가 공급하는 값을 반환하다. 반환한 값을 변수 data에 저장한다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/bbe9405c-7962-4bf1-8b73-413a462568e3)

- useContext를 이용하면 자신이 속한 그룹의 Context가 제공하는 값을 불러올 수 있다. Main 컴포넌트는 MyContext 그룹에 속하기 때문에 문제 오류 발생 하지 않는다.
  - useContext를 호출한 컴포넌트가 인수로 전달한 Context그룹에 속하지 않으면 오류가 발생한다.

```jsx
const MyContext = React.createContext(defalutValue);
```

- 위 코드로 Context 생성할 수 있다. `createContext` 의 파라미터에는 Context 의 기본값을 설정할 수 있다. 여기서 설정하는 값은 Context 를 쓸 때 값을 따로 지정하지 않을 경우 사용되는 기본 값이다.

```jsx
<MyContext.Provider value ={전역으로 전달하고자하는 값}>
  {/* context안에는 자식 컴포넌트들이 위치*/}
</MyContext.Provider>
```

- Context를 만들면, Context 안에 Provider 라는 컴포넌트가 들어있는데 이 컴포넌트를 통하여 Context 의 값을 정할 수 있다. 이 컴포넌트를 사용할 때, `value` 라는 값을 설정해주면 된다. 즉, Context Provider를 통한 데이터 공급하는 것이다.

## ContextAPI 짚고 넘어가야하는 부분

```jsx
<AppContext.Provider value={{ globalState, setGlobalState }}>
  <Routes>
    <Route path="/" element={<HomePage />} />
    <Route path="/about" element={<AboutPage />} />
  </Routes>
</AppContext.Provider>
```

- contextAPI는 Provider의 value값을 props로 내려주는 것이 아니고 하위 컴포넌트인 HomePage와 AboutPage가 AppContext.Provider를 구독(subscribe)하고 있기 때문에 AppContext.Provider의 value 값이 변경되면 하위 컴포넌트들이 상태가 자동으로 변경된다.
- 이렇게 작동하는 이유는 React의 Context API가 구독-발행(subscribe-publish) 모델을 사용하기 때문이다.
  1. `Provider` 컴포넌트는 context 값을 "발행(publish)"하는 역할을 합니다.
  2. 하위 컴포넌트에서 `useContext` 훅을 사용하면 해당 context를 "구독(subscribe)"하게 됩니다.
  3. `Provider`의 `value` prop 값이 변경되면, 구독 중인 하위 컴포넌트들에게 새로운 값이 자동으로 전파되어 반영됩니다.
