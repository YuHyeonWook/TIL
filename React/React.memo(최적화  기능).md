# React.memo(최적화 기능)

컴포넌트 트리)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/7620559a-7688-41c3-9576-1e769f0a9c60)

- 위 사진에서 부모 컴포넌트가 리렌더 되면 자식 컴포넌트(CountView, TextView) 또한 리렌더가 되기 때문에 성능 낭비가 발생함
- 위와 같이 prop의 변화가 없어도 리렌더 되는 성능의 낭비를 방지하기 위해 각각의 자식 컴포넌트에 업데이트 조건을 부여하는 것이 **React.memo** 이다.
  - CountView 컴포넌트는 자신이 받는 prop인 count가 바뀔 때만 리렌더가 발생하도록, TextView 컴포넌트는 자신이 받는 prop인 text가 바뀔 때만 리렌더가 발생하도록 **React.memo을 사용하여 조건을 부여**해줄 수 있다.

## React.memo

- React.memo를 이용하면 메모이제이션 기법으로 컴포넌트가 불필요하게 리렌더되는 상황을 방지할 수 있고, 브라우저의 연산량을 줄여 주어 성능 최적화에 도움이 된다.
- React.memo는 고차 컴포넌트이다.
- 또한, Props가 메모이제이션의 기준이된다. 즉, React.memo가 반환하는 컴포넌트는 부모 컴포넌트에서 전달된 Props가 변경되지 않는 한 리렌더되지 않는다.

사용방법

- 강화하고 싶은(메모이제이션을 적용하고 싶은) 컴포넌트를 React.memo로 감싸면 된다.

```jsx
const memoizedComp = React.memo(Comp);
// const memoizedComp = React.memo(메모이제이션하려는 컴포넌트)
```

함수 컴포넌트를 선언과 동시에 메모이제이션 예시)

```jsx
const CompA = React.memo(() => {
  console.log("컴포넌트가 호출되었습니다.");
  return <div>CompA</div>;
});
```

<br>

```jsx
const Comp = ({ a, b, c }) => {
  console.log("컴포넌트가 호출되었다.");
  return <div>Comp</div>;
};

function areEqual(prevProps, nextProps) { ⓐ
  if (prevProps.a === nextProps.a) {
    return true;
  } else {
    return false;
  }
}
const MemoizedComp = React.memo(Comp, areEqual); ⓑ

```

- React.memo는 Props의 변경 여부를 기준으로 컴포넌트의 리렌더 여부를 결정하기 때문에 Props로 전달되는 값이 많을 때는 판별 함수를 인수로 전달해 Props의 특정 값만으로 리렌더 여부를 판단할 수 있다.
- ⓐ 판별 함수로 사용할 함수 areEqual을 만듬. 판별 함수에는 두 개의 매개변수가 제공된다. prevProps에는 이전 Props의 값, nextProps에는 새롭게 바뀐 Props의 값이 각각 저장된다. 판별 함수가 true를 반환하면 리렌더되지 않고, 판별 함수가 false를 반환하면 리렌더된다.
- ⓑ Comp 컴포넌트를 메모이제이션하기 위해 React.memo를 호출하고 인수를 전달함. 두 번째 인수로 판별 함수 areEqual을 전달한다. 그 결과로 반환되는 MemoizedComp는 전달되는 Props의 값 중 a가 변경될 때만 리렌더된다.

```

const MyComponent = React.memo(function MyComponent(props) {
  /* props를 사용하여 렌더링 */
});
```

- 위는 React.memo 함수 안에 매개변수로 컴포넌트를 전달하면 새 컴포넌트를 MyComponenet에 할당함
- 또한, React.memo는 똑같은 prop을 받으면 똑같은 것을 반환한다.

- React.memo에서 props가 갖는 복잡한 객체에 대하여 얕은 비교만을 수행하는 것이 기본 동작이다. 다른 비교 동작을 원한다면, 두 번째 인자로 별도의 비교 함수를 제공하면 된다.

```
function MyComponent(props) {
  /* props를 사용하여 렌더링 */
}
function areEqual(prevProps, nextProps) {
  /*
  nextProps가 prevProps와 동일한 값을 가지면 true를 반환하고, 그렇지 않다면 false를 반환
  */
}
export default React.memo(MyComponent, areEqual);
```

- prevProps, nextProps에 동일한 값을 가지면 true 그렇지 않으면 false 반환함
- 즉, React.memo가 두 번째 인수로 받는 것은 비교 함수이며 해당 비교 함수가 반환하는 값이 true이면 리 렌더링을 하지 않고, false이면 리렌더링을 하게 된다.

# 참고

- 리액트 공식 문서, https://ko.legacy.reactjs.org/docs/react-api.html#reactmemo
- 한입 크기 리액트
