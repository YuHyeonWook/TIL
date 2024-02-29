# strict mode

```jsx
function foo() {
  x = 10;
}
foo();

console.log(x); // ?

// 결괏값
// 10
```

위 예제는 전역 스코프에 x변수의 선언이 존재하지 않기 때문에 ReferenceError를 발생시킬 것 같지만 자바스크립트 엔진은 암묵적으로 전역 객체에 x 프로퍼티를 동적 생성하기 때문에 전역 객체의 x 프로퍼티는 마치 전역 변수처럼 사용할 수 있다.

이러한 현상을 **암묵적 전역**(implicit global)이라고 한다.

<aside>
💡 개발자의 의도와는 상관없이 발생한 암묵적 전역은 오류를 발생시키는 원인이 될 가능성이 크기 때문에 var, let, const 키워드를 사용하여 변수를 선언한 다음 사용해야 한다.

</aside>

오타나 문법 지식의 미비로 인한 실수는 언제나 발생한다 이것을 지원하는 ES5부터 strict mode(엄격 모드)가 추가되었다.

strict mode는 자바스크립트 언어의 문법을 엄격히 적용하여 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.

⇒ ESLint 도구를 사용하면 strict mode와 유사한 효과를 얻을 수 있다.

## **strict mode의 적용**

strict mode를 적용하려면 전역의 선두 또는 함수 몸체의 선두에 ’use strict’ 를 추가한다. 전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

전역 선두에 선언)

```jsx
"use strict";

function foo() {
  x = 10; // ReferenceError: x is not defined
}
foo();
```

함수 몸체 선두에 선언)

```jsx
function foo() {
  "use strict";

  x = 10; // ReferenceError: x is not defined
}
foo();
```

’use strict’ 를 선두에 위치하지 않으면 제대로 동작하지 않는다.

<br>

# 참고

- 모던 js 딥다이브
