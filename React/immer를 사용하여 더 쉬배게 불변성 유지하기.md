# **immer를 사용하여 더 쉽게 불변성 유지하기**

- react의 불변성을 유지하기 위해서는 스프레드 연산자와 배열의 내장 함수(map(), filter())를 사용하면 간단하게 배열 혹은 객체를 복사하고 새로운 값을 덮어 쓸 수 있다.
- 지만 객체의 구조가 엄청나게 깊어지면 불변성을 유지하면서 이를 업데이트하는 것이 매우 힘들다.

```scss
const object = {
  somewhere: {
    deep: {
      inside: 3,
      array: [1, 2, 3, 4]
  },
    bar: 2
},
  foo: 1
};

// somewhere.deep.inside 값을 4로 바꾸기
let nextObject = {
...object,
  somewhere: {
  ...object.somewhere,
    deep: {
    ...object.somewhere.deep,
      inside: 4
  }
}
};

// somewhere.deep.array에 5 추가하기
let nextObject = {
...object,
  somewhere: {
  ...object.somewhere,
    deep: {
    ...object.somewhere.deep,
      array: object.somewhere.deep.array.concat(5)
  }
}
};
```

- 값 하나를 업데이트하기 위해 코드를 열 줄 정도 작성해야 합니다. 이렇게 스프레드 연산자를 자주 사용한 것은 기존에 가지고 있던 다른 값은 유지하면서 원하는 값을 새로 지정하기 위해서이다.
- 간혹 실제 프로젝트에서 스프레드 연산자를 여러 번 사용하는 것은 꽤 번거로운 작업이다. 가독성 또한 좋지 않다.

> 이러한 상황에 **immer라는 라이브러리를 사용하면, 구조가 복잡한 객체도 매우 쉽고 짧은 코드를 사용하여 불변성을 유지하면서 업데이트**해 줄 수 있습니다.

## 1. immer를 사용하지 않고 불변성 유지

- immer를 사용하지 않고 불변성을 유지하면서 값을 업데이트하는 컴포넌트를 작성한 예시)

```jsx
import { useRef, useCallback, useState } from "react";

const App = () => {
  const nextId = useRef(1);
  const [form, setForm] = useState({ name: "", username: "" });
  const [data, setData] = useState({
    array: [],
    uselessValue: null,
  });

  // input 수정을 위한 함수
  const onChange = useCallback(
    (e) => {
      const { name, value } = e.target;
      setForm({
        ...form,
        [name]: [value],
      });
    },
    [form]
  );

  // form 등록을 위한 함수
  const onSubmit = useCallback(
    (e) => {
      e.preventDefault();
      const info = {
        id: nextId.current,
        name: form.name,
        username: form.username,
      };

      // array에 새 항목 등록
      setData({
        ...data,
        array: data.array.concat(info),
      });

      // form 초기화
      setForm({
        name: "",
        username: "",
      });
      nextId.current += 1;
    },
    [data, form.name, form.username]
  );

  // 항목을 삭제하는 함수
  const onRemove = useCallback(
    (id) => {
      setData({
        ...data,
        array: data.array.filter((info) => info.id !== id),
      });
    },
    [data]
  );

  return (
    <div>
      <form onSubmit={onSubmit}>
        <input
          name="username"
          placeholder="아이디"
          value={form.username}
          onChange={onChange}
        />
        <input
          name="name"
          placeholder="이름"
          value={form.name}
          onChange={onChange}
        />
        <button type="submit">등록</button>
      </form>
      <div>
        <ul>
          {data.array.map((info) => (
            <li key={info.id} onClick={() => onRemove(info.id)}>
              {info.username} ({info.name})
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
};

export default App;
```

![316.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/453bbb12-72a8-4458-b38a-360fc17a5910/316.jpg)

- 폼에서 아이디/이름을 입력하면 하단 리스트에 추가되고, 리스트 항목을 클릭하면 삭제되는 간단한 컴포넌트이다. 이렇게 스프레드 연산자와 배열 내장 함수를 사용하여 불변성을 유지하는 것은 어렵지 않지만, 상태가 복잡해진다면 조금 귀찮은 작업이 될 수 있다.

## 2. immer 사용

- immer를 사용하면 불변성을 유지하는 작업을 매우 간단하게 처리할 수 있습니다

```jsx
// 예시 코드
import produce from "immer";
const nextState = produce(originalState, (draft) => {
  // 바꾸고 싶은 값 바꾸기
  draft.somewhere.deep.inside = 5;
});
```

- produce라는 함수는 두 가지 파라미터를 받습니다. **첫 번째 파라미터는 수정하고 싶은 상태**이고, **두 번째 파라미터는 상태를 어떻게 업데이트할지 정의하는 함수**입니다.
  - 두 번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면, produce 함수가 불변성 유지를 대신해 주면서 새로운 상태를 생성해 줍니다.
- immer라이브러리의 핵심은 ‘불변성에 신경 쓰지 않는 것처럼 코드를 작성하되 불변성 관리는 제대로 해 주는 것’입니다. 단순히 깊은 곳에 위치하는 값을 바꾸는 것 외에 배열을 처리할 때도 매우 쉽고 편합니다.
- react의 불변성을 유지하기 위해서는 스프레드 연산자와 배열의 내장 함수(map(), filter())를 사용하면 간단하게 배열 혹은 객체를 복사하고 새로운 값을 덮어 쓸 수 있다.
- 지만 객체의 구조가 엄청나게 깊어지면 불변성을 유지하면서 이를 업데이트하는 것이 매우 힘들다.

```scss
const object = {
  somewhere: {
    deep: {
      inside: 3,
      array: [1, 2, 3, 4]
  },
    bar: 2
},
  foo: 1
};

// somewhere.deep.inside 값을 4로 바꾸기
let nextObject = {
...object,
  somewhere: {
  ...object.somewhere,
    deep: {
    ...object.somewhere.deep,
      inside: 4
  }
}
};

// somewhere.deep.array에 5 추가하기
let nextObject = {
...object,
  somewhere: {
  ...object.somewhere,
    deep: {
    ...object.somewhere.deep,
      array: object.somewhere.deep.array.concat(5)
  }
}
};
```

- 값 하나를 업데이트하기 위해 코드를 열 줄 정도 작성해야 합니다. 이렇게 스프레드 연산자를 자주 사용한 것은 기존에 가지고 있던 다른 값은 유지하면서 원하는 값을 새로 지정하기 위해서이다.
- 간혹 실제 프로젝트에서 스프레드 연산자를 여러 번 사용하는 것은 꽤 번거로운 작업이다. 가독성 또한 좋지 않다.

> 이러한 상황에 **immer라는 라이브러리를 사용하면, 구조가 복잡한 객체도 매우 쉽고 짧은 코드를 사용하여 불변성을 유지하면서 업데이트**해 줄 수 있습니다.

## 1. immer를 사용하지 않고 불변성 유지

- immer를 사용하지 않고 불변성을 유지하면서 값을 업데이트하는 컴포넌트를 작성한 예시)

```jsx
import { useRef, useCallback, useState } from "react";

const App = () => {
  const nextId = useRef(1);
  const [form, setForm] = useState({ name: "", username: "" });
  const [data, setData] = useState({
    array: [],
    uselessValue: null,
  });

  // input 수정을 위한 함수
  const onChange = useCallback(
    (e) => {
      const { name, value } = e.target;
      setForm({
        ...form,
        [name]: [value],
      });
    },
    [form]
  );

  // form 등록을 위한 함수
  const onSubmit = useCallback(
    (e) => {
      e.preventDefault();
      const info = {
        id: nextId.current,
        name: form.name,
        username: form.username,
      };

      // array에 새 항목 등록
      setData({
        ...data,
        array: data.array.concat(info),
      });

      // form 초기화
      setForm({
        name: "",
        username: "",
      });
      nextId.current += 1;
    },
    [data, form.name, form.username]
  );

  // 항목을 삭제하는 함수
  const onRemove = useCallback(
    (id) => {
      setData({
        ...data,
        array: data.array.filter((info) => info.id !== id),
      });
    },
    [data]
  );

  return (
    <div>
      <form onSubmit={onSubmit}>
        <input
          name="username"
          placeholder="아이디"
          value={form.username}
          onChange={onChange}
        />
        <input
          name="name"
          placeholder="이름"
          value={form.name}
          onChange={onChange}
        />
        <button type="submit">등록</button>
      </form>
      <div>
        <ul>
          {data.array.map((info) => (
            <li key={info.id} onClick={() => onRemove(info.id)}>
              {info.username} ({info.name})
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
};

export default App;
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/d42c8a4d-fae1-4d97-9252-bef79dc5d743)

- 폼에서 아이디/이름을 입력하면 하단 리스트에 추가되고, 리스트 항목을 클릭하면 삭제되는 간단한 컴포넌트이다. 이렇게 스프레드 연산자와 배열 내장 함수를 사용하여 불변성을 유지하는 것은 어렵지 않지만, 상태가 복잡해진다면 조금 귀찮은 작업이 될 수 있다.

## 2. immer 사용

- immer를 사용하면 불변성을 유지하는 작업을 매우 간단하게 처리할 수 있습니다

```jsx
// 예시 코드
import produce from "immer";
const nextState = produce(originalState, (draft) => {
  // 바꾸고 싶은 값 바꾸기
  draft.somewhere.deep.inside = 5;
});
```

- produce라는 함수는 두 가지 파라미터를 받습니다. **첫 번째 파라미터는 수정하고 싶은 상태**이고, **두 번째 파라미터는 상태를 어떻게 업데이트할지 정의하는 함수**입니다.
  - 두 번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면, produce 함수가 불변성 유지를 대신해 주면서 새로운 상태를 생성해 줍니다.
- immer라이브러리의 핵심은 ‘불변성에 신경 쓰지 않는 것처럼 코드를 작성하되 불변성 관리는 제대로 해 주는 것’입니다. 단순히 깊은 곳에 위치하는 값을 바꾸는 것 외에 배열을 처리할 때도 매우 쉽고 편합니다.
