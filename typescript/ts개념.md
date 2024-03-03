# TS 개념

- 타입스크립트는 타입을 위한 구문이 있는 자바스크립트 즉, 타입스크립트는 기본적으로 자바스크립트이다.

타입스크립트 적용)

```jsx
const hello: string = "world";
function add(x: number, y: number): number {
  return x + y;
}

interface Person {
  name: string;
  age: number;
}
const person: Person = {
  name: "zero",
  age: 28,
};
```

- 타입을 위한 구문은 변수나 매개변수, 반환값 같은 값에 타입을 부여하였다.
- 타입은 데이터의 형태를 의미한다. 여기서 데이터의 형태란 자바스크립트에서 배운 문자열, 숫자, 객체 등의 자료형이다.
- 위 코드는 hello 변수가 string(문자열) 타입이고, 함수 add의 매개변수인 x와 y가 number(숫자) 타입이며, 함수 add의 반환값이 number 타입임을 표기한 것이다.
- 자바스크립트에 있는 타입만 표기할 수 있는 건 아니다. person 변수는 **Person이라는 타입**이다.

<br>

# 참고

- 타입스크립트 교과서
