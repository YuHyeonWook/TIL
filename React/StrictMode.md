# StrictMode

- `<StrictMode>`는 개발 중에 컴포넌트에서 일반적인 버그를 빠르게 찾을 수 있도록 한다.

```jsx
const root = createRoot(document.getElementById("root"));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

## 1. Strict Mode는 다음과 같은 개발 전용 동작을 활성화함.

- Strict Mode는 `<StrictMode>` 컴포넌트 내부의 모든 컴포넌트 트리에 대해 추가적인 개발 전용 검사를 활성화한다. 이러한 검사는 개발 프로세스 초기에 컴포넌트에서 일반적인 버그를 찾는 데 도움이 된다.

Strict Mode에서는 개발 시 다음과 같은 검사를 가능하게 한다.

1. 순수하지 않은 렌더링으로 인해 발생하는 버그를 찾기 위해 컴포넌트가 [추가로 다시 렌더링](https://ko.react.dev/reference/react/StrictMode#fixing-bugs-found-by-double-rendering-in-development)된다.
2. Effect 클린업이 누락되어 발생하는 버그를 찾기 위해 컴포넌트가 [추가로 Effect를 다시 실행](https://ko.react.dev/reference/react/StrictMode#fixing-bugs-found-by-re-running-effects-in-development)한다.
3. [더 이상 사용되지 않는 API의 사용 여부를 확인](https://ko.react.dev/reference/react/StrictMode#fixing-deprecation-warnings-enabled-by-strict-mode)하기 위해 컴포넌트를 검사한다.

<aside>
💡 공식문서에는 Strict Mode로 래핑하는 것을 권장한다.

</aside>

### **개발 중 이중 렌더링으로 발견한 버그 수정**

- 리액트 컴포넌트 안에서 함수가 순수한 경우 두 번 실행하여도 동작이 변경되지 않는다. 순수 함수는 항상 같은 결과를 생성하기 때문이다. 그러나 함수가 순수하지 않다면 (예: 받은 데이터를 변경하는 함수) 두 번 실행된다. (이것이 순수하지 않은 이유이다) 이는 버그를 조기에 발견하고 수정하는 데 도움이 된다.

## 2. 예제: **순수하지 않은 함수의 사용**

1)**`StrictMode`를 사용하지 않은 경우**

```jsx
import React, { useState, useEffect } from "react";
import { createRoot } from "react-dom/client";

const App = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Effect ran");
    // 순수하지 않은 함수: 외부 변수를 변경
    window.someValue = count;

    return () => {
      console.log("Cleanup");
    };
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

const root = createRoot(document.getElementById("root"));
root.render(<App />);

// 결괏값
// Effect ran
```

2. **`StrictMode`를 사용한 경우**

```jsx
import React, { useState, useEffect, StrictMode } from "react";
import { createRoot } from "react-dom/client";

const App = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Effect ran");
    // 순수하지 않은 함수: 외부 변수를 변경
    window.someValue = count;

    return () => {
      console.log("Cleanup");
    };
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

const root = createRoot(document.getElementById("root"));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);

// 결괏값
// Effect ran
// Cleanup
// Effect ran
```

- **`StrictMode`**로 래핑된 컴포넌트는 개발 모드에서 두 번 렌더링된다. 이는 순수하지 않은 함수가 문제를 일으킬 수 있음을 나타낸다.

# 참고문헌

- https://ko.react.dev/reference/react/StrictMode#fixing-deprecation-warnings-enabled-by-strict-mode
