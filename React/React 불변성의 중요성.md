# React 불변성의 중요성

- 리액트 컴포넌트에서 상태를 업데이트할 때 불변성을 지키는 것은 매우 중요합니다.

```jsx
const onToggle = useCallback((id) => {
  setTodos((todos) =>
    todos.map((todo) =>
      todo.id === id ? { ...todo, checked: !todo.checked } : todo
    )
  );
}, []);
```

- 위는 map()을 사용하여 불변성을 유지하고 있다.
- 기존 데이터를 수정할 때 직접 수정하지 않고, 새로운 배열을 만든 다음에 새로운 객체를 만들어서 필요한 부분을 교체해 주는 방식이다.

> 이렇게 기존의 값을 직접 수정하지 않으면서 새로운 값을 만들어 내는 것을 ‘불변성을 지킨다’고 합니다.

불변성을 어떻게 지키는지 예시)

```jsx
const array = [1, 2, 3, 4, 5];

const nextArrayBad = array; // 배열을 복사하는 것이 아니라 똑같은 배열을 가리킵니다.
nextArrayBad[0] = 100;
console.log(array === nextArrayBad); // 완전히 같은 배열이기 때문에 true

const nextArrayGood = [...array]; // 배열 내부의 값을 모두 복사합니다.
nextArrayGood[0] = 100;
console.log(array === nextArrayGood); // 다른 배열이기 때문에 false

const object = {
  foo: "bar",
  value: 1,
};

const nextObjectBad = object; // 객체가 복사되지 않고, 똑같은 객체를 가리킵니다.
nextObjectBad.value = nextObjectBad.value + 1;
console.log(object === nextObjectBad); // 같은 객체이기 때문에 true

const nextObjectGood = {
  ...object, // 기존에 있던 내용을 모두 복사해서 넣습니다.
  value: object.value + 1, // 새로운 값을 덮어 씁니다.
};
console.log(object === nextObjectGood); // 다른 객체이기 때문에 false
```

- **불변성이 지켜지지 않으면 객체 내부의 값이 새로워져도 바뀐 것을 감지하지 못함.** 그러면 React.memo에서 서로 비교하여 최적화하는 것이 불가능하다
- **스프레드(... 문법)를 사용하여 객체나 배열 내부의 값을 복사할 때는 얕은 복사**(shallow copy)를 하게 됩니다. 즉, 내부의 값이 완전히 새로 복사되는 것이 아니라 **가장 바깥쪽에 있는 값만 복사**됩니다. 따라서 내부의 값이 객체 혹은 배열이라면 내부의 값 또한 따로 복사해 주어야 합니다.

얕은 복사 예시)

```
const todos = [{ id: 1, checked: true }, { id: 2, checked: true }];
const nextTodos = [...todos];

nextTodos[0].checked = false;
console.log(todos[0] === nextTodos[0]); // 아직까지는 똑같은 객체를 가리키고 있기 때문에 true
// {id: 1, checked: false} === {id: 1, checked: false}
// 결괏값 : true

```

- **얕은 복사는** 새로운 배열에서 객체의 값을 변경하면 원본 배열의 객체 값도 변경됩니다.
- 위 코드와 아래 코드 비교해보기.

```

const todos = [{ id: 1, checked: true }, { id: 2, checked: true }];
const nextTodos = [...todos];

nextTodos[0] = {
  ...nextTodos[0],
  checked: false
};
console.log(todos[0] === nextTodos[0]); // 새로운 객체를 할당해 주었기에 false
```

- 위 코드가 `false`가 출력되는 이유는 `nextTodos[0]`에 새로운 객체를 할당했기 때문입니다. 이렇게 새로운 객체를 할당하면 기존 객체와는 다른 메모리 공간에 저장되므로, 두 객체의 참조값이 다르게 됩니다.

> react에선 기존 객체나 배열을 직접 수정하지 않고, 새로운 객체나 배열을 생성하여 업데이트하는 방식으로 상태를 관리합니다. 이렇게 하면 불필요한 렌더링을 방지하고 성능을 최적화할 수 있습니다.

- 또한, 배열 혹은 객체의 구조가 정말 복잡해진다면 불변성을 유지하면서 업데이트하는 것도 까다로워집니다. 만약 복잡한 상황일 경우 immer 라이브러리를 사용하면 편하게 작업할 수 있습니다.
