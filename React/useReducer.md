# useReducer

# **useReducer**

- **useReducer**는 상태 변화 로직을 분리한다.
  - state 관리를 컴포넌트 내부가 아닌 외부에서 할 수 있게 만든다. 그래서 useState와 달리 state를 관리하는 상태 변화 코드를 컴포넌트와 분리할 수 있다. 파일로도 분리가 가능하여 컴포넌트 내부가 훨씬 간결해 진다.
- **useReducer는 useState처럼 리액트 컴포넌트에서 state(상태) 관리를 돕는 리액트 Hooks**이다.
  - useReducer는 컴포넌트의 상태 변화 로직을 컴포넌트에서 분리시킬 수 있어 컴포넌트를 가볍게 작성할 수 있도록 도와줌
- useReducer는 현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션(action) 값을 전달받아 새로운 상태를 반환하는 함수이다. useReducer 에서 새로운 상태를 만들 때는 반드시 불변성을 지켜 주어야 한다.

```
function reducer(state, action) {
	return { ... }; // 불변성을 지키면서 업데이트한 새로운 상태를 반환합니다.
}
```

- 액션 값은 주로 다음과 같은 형태로 이루어져 있다.

```
{
  type: 'INCREMENT',
  // 다른 값들이 필요하다면 추가로 들어감
}
```

## **useReducer 형태**

```
const [state, dispatch] = useReducer(reducer, initialState);
 //  [state 변수, 상태변화 촉발 함수]  = 생성자(상태 변화 함수, 초깃값)
```

- state : 앞으로 컴포넌트에서 사용 할 수 있는 상태
- dispatch :
  - dispatch를 호출할 때 전달해줬던 action객체를 전달받음
  - 액션을 발생시키는 함수(액션 = 상태 변화 )
- reducer : 상태 변화를 처리 해주는 함수
- initialState : state의 초기 상태
- action 은 업데이트를 위한 정보 type 값을 지닌 객체 형태로 사용함

즉, dispatch에서 상태 변화가 일어나면, reducer가 처리함

<aside>
👉 useReducer를 호출해도 useState처럼 State를 만들 수 있다.

</aside>

### 상태 변화 코드란?

상태 변화 코드란 state값을 변경하는 코드이다. 밑의 Comp 컴포넌트의 함수 onIncrease와 onDecrease는 각각 변수 count의 값을 늘리거나 줄이므로 상태 변화 코드라고 할 수 있다.

```jsx
function Comp() {
  const [count, setCount] = useState(0)

  const onIcrease = () => { // 상태 변화 코드 (+1
    setCount(count + 1);
  };
  const onDecrease = () => { // 상태 변화 코드 (-1
    setCount(count - 1);
  };

	return (
		...
	);
}

export default Comp;
```

- 상태 변화 코드를 컴포넌트에서 분리한다는 말은 컴포넌트 내부에 작성했던 상태 변화 코드를 외부에 작성한다는 의미이다.
  - 컴포넌트 안에 상태 변화 코드 둘다 선언했기 떄문에 useState를 이용해 state를 만들면 상태 변화 코드를 분리할 수 없다.

이처럼 useState를 이용해 state를 생성하면 상태 변화 코드는 반드시 컴포넌트 안에 작성해야 함. 반면 함수 useReducer를 사용하면 상태 변화 코드를 **컴포넌트 밖**으로 분리할 수 있다.

### 상태 변화 코드 분리 이유

- 하나의 컴포넌트 안에 너무 많은 상태 변화 코드가 있으면 가독성을 헤쳐 유지 보수를 어렵게 만든다.

### useReducer 사용법

useReducer를 사용해 상태 변화 코드를 컴포넌트와 분리하는 예시)

```jsx
function Comp() {
  return (
    <div>
      <h4>테스트 컴포넌트</h4>
      <div>
        <bold>0</bold>
      </div>
      <div>
        <button>+</button>
        <button>-</button>
      </div>
    </div>
  );
}
export default Comp;
```

useReducer 적용 예시)

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "INCREASE":
      return state + action.data;
    case "DECREASE":
      return state - action.data;
    default:
      return state;
  }
}

function Comp() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h4>테스트 컴포넌트</h4>
      <div>
        <bold>{count}</bold>
      </div>
      <div>
        <button onClick={() => dispatch({ type: "INCREASE", data: 1 })}>
          {" "}
          ⓐ +
        </button>
        <button onClick={() => dispatch({ type: "DECREASE", data: 1 })}>
          -
        </button>
      </div>
    </div>
  );
}
export default Comp;
```

- ⓐ + 버튼을 클릭하면 카운트 값을 1 늘린다. 상태 변화가 필요할 때 이를 촉발하는 함수 dispatch를 호출함.
  - 이때 함수 dispatch에서는 인수로 객체를 전달하는데 이 객체는 state의 변경 정보를 담고 있다.
  - 이 객체를 **action 객체**라고 함
- - 버튼을 클릭했을 때, 함수 dispatch는 2개의 프로퍼티로 이루어진 action 객체를 인수로 전달함.
    - 두 프로퍼티 중 type은 어떤 상황이 발생했는지를 나타낸다.
    - - 버튼을 클릭했으므로 type 프로퍼티에는 증가를 의미하는 INCREASE를 값으로 설정함.
- data 프로퍼티는 상태 변화에 필요한 값은 1로 설정함.
  - - 버튼을 클릭하면 카운트를 1만큼 늘리므로 data 프로퍼티의 값은 1로 설정함.
- - 버튼 누르면 dispatch 함수 호출하고, 인수로 전달하는 action 객체의 type 프로퍼티에는 감소를 의미하는 DECREASE를 , data 프로퍼티에는 state 값을 1만큼 줄이도록 설정함

<aside>
💡 정리하면 useReducer가 반환하는 함수 dispatch를 호출하면 useReducer는 함수 reducer를 호출하고 이 함수가 반환하는 값이 state를 업데이트 한다.

</aside>

reducer 함수 예시)

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case "INIT":
    case "CREATE":
    case "REMOVE":
    case "EDIT":
    default:
      return state;
  }
};
```

- **state** : **상태 변화 일어나기 직전의 state 값**
- **action** : **상태 변화를 일으키는 객체**

## useReducer vs useState **- 뭐 쓸까?**

```jsx
const [value, setValue] = useState(true);
```

- 어떨 때 useReducer 를 쓰고 어떨 때 useState를 써야 할까?
- **useState**는 컴포넌트에서 관리하는 값이 딱 하나고, 그 값이 **단순한 숫자, 문자열 , boolean 값**일 때 **사용**함
- **useReducer** : 컴포넌트에서 관리하는 **값이 여러개가 되어서 상태의 구조가 복잡할 떄 사용**함
- 예를들어 setter 를 한 함수에서 여러번 사용해야 하는 일이 발생한다면

```jsx
setUsers((users) => users.concat(user));
setInputs({
  username: "",
  email: "",
});
```

- 그 때부터 **useState**를 쓸까? 고민하게된다.  **useReducer** 를 썼을때 편해질 것 같으면 **useReducer** 를 쓰고, 딱히 그럴 것 같지 않으면 **useState**를 유지하면 된다.

# 참고

- https://react.vlpt.us/basic/20-useReducer.html
