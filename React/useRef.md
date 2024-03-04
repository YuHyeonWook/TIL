# useRef

- 리액트의 Ref를 이용하면 **돔(DOM)**요소들을 직접 조작할 수 있다. Ref는 Reference의 줄임말로 **참조**라는 뜻이다.
- js의 Document.querySelector()와 유사하다.
  ![image](https://github.com/YuHyeonWook/TIL/assets/110236953/cfef361f-cf73-4537-8861-e08e554432d6)

  - Ref 객체의 `.current` 값은 우리가 원하는 DOM 을 가르키게 된다.

### **useRef 사용하기**

- useRef 리액트 함수를 이용해 Ref 객체를 생성한다.

```jsx
import { useState } from "react";

function Body() {
  const [text, setText] = useState("");

  const handleOnChange = (e) => {
    setText(e.target.value);
  };

  const handleOnClick = () => {
    alert(text);
  };

  return (
    <div>
      <input value={text} onChange={handleOnChange} />
      <button onClick={handleOnClick}>작성 완료</button>
    </div>
  );
}
export default Body;
```

- State 변수 text로 관리하는 텍스트 입력 폼 하나와 버튼 하나를 생성함. 버튼을 클릭하면 이벤트 핸들러 handleOnClick이 실행되어 입력 폼에서 작성한 텍스트를 메시지 대화상자에 표시됨

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/a24aae8e-0bdd-4e4a-98f6-2d9c072d0ae3)

```jsx
import { useRef, useState } from "react";

function Body() {
  const [text, setText] = useState("");
  const textRef = useRef();

  const handleOnChange = (e) => {
    setText(e.target.value);
  };
  const handleOnClick = () => {
    alert(text);
  };

  return (
    <div>
      <input ref={textRef} value={text} onChange={handleOnChange} /> ③
      <button onClick={handleOnClick}>작성 완료</button>
    </div>
  );
}
export default Body;
```

- useRef는 인수로 전달한 값을 초깃값으로 하는 Ref 객체를 생성함. 생성한 Ref를 상수 textRef에 저장함
- ③ input 태그에서 ref={textRef} 명령으로 textRef가 돔 입력 폼에 접근하도록 설정함. 이제 textRef를 이용하면 입력 폼을 직접 조작할 수 있다.

### **useRef로 입력 폼 초기화하기**

- 예를들어 웹 서비스의 로그인 페이지는 대부분 사용자가 ID와 패스워드를 입력하고, 로그인 버튼을 클릭하면 패스워드가 올바른지 점검한 후 패스워드 입력 폼에서 작성한 값을 초기화한다.
- 이러한 것을 Ref를 이용하면 동작을 수행할 수 있게된다.

이번에는 useRef를 이용해 텍스트 입력 폼을 초기화하는 법을 알아보자

```jsx
import { useRef, useState } from "react";

function Body() {
  (...)
  const handleOnClick = () => {
    alert(text);
    textRef.current.value = "";
  };
  (...)
}
export default Body;
```

- 버튼을 클릭해 이벤트 핸들러 handleOnClick을 실행함. 대화상자에서 <확인> 버튼을 클릭 하면, textRef.current(textRef가 현재 참조하고 있는 돔 요소)의 value 값을 공백 문자열로 초기화됨

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/f7920756-7007-4eb2-bb66-cea860f91f70)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/7eee5323-6672-42e6-a16f-2170536a7bc4)

- 텍스트 입력 폼에서 입력한 문자열이 사라지고 빈 공백만 남는다. 이렇듯 Ref를 이용하면 돔 요소를 원하는 형태로 조작할 수 있다.

### **useRef로 포커스하기**

- 웹 서비스에서는 사용자가 특정 폼에 내용을 입력하지 않거나 내용이 정한 길이보다 짧으면 해당 폼을 포커스(focus)하여 사용자의 추가 입력을 유도할 수 있다. 리액트의 Ref 기능을 이용하면 특정 요소에 포커스 기능을 지정할 수 있다.

```jsx
import { useRef, useState } from "react";

function Body() {
  const [text, setText] = useState("");
  const textRef = useRef();

  const handleOnChange = (e) => {
    setText(e.target.value);
  };

  const handleOnClick = () => {
    if (text.length < 5) {
      textRef.current.focus(); ①
    } else {
      alert(text);
      setText(""); ②
    }
  };

  return (
    <div>
      <input ref={textRef} value={text} onChange={handleOnChange} />
      <button onClick={handleOnClick}>작성 완료</button>
    </div>
  );
}
export default Body;
```

- 텍스트 입력 폼에서 사용자가 문자를 다섯 글자 미만으로 입력하면 이 요소에 포커스한 상태로 사용자가 입력을 추가할 때까지 대기함.
- ① 현재 input 태그로 지정한 폼에 입력한 텍스트가 다섯 글자보다 적다면 textRef.current가 참조하는 입력 폼에 포커스를 실행한다. focus()는 현재 돔 요소에 포커스를 지정하는 메서드이다.
- ② 텍스트 폼에 입력한 값을 초기화하기 위해 set 함수 setText를 호출하고, 인수로 빈 문자열을 전달한다. Ref를 사용하지 않고도 set 함수로 입력 폼을 초기화할 수 있다.

다섯 글자 미만 문자열에 대한 포커스 기능 그림 예시)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/dd2a652b-109f-4607-9cb1-1904b652349a)

- 다섯 글자 미만의 문자열을 입력하니 포커스 기능이 동작하면서 입력 폼을 초기화하지 않고 사용자의 입력을 기다리게 된다.

<br>

# 참고

- 한입 크기 리액트
- 리액트를 다루는 기술
