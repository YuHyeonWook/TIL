# **형변환 주의하기, isNaN**

## **형변환 주의하기**

- 느슨한 검사는 암묵적 형변환이 일어난다.
- 밑의 예시는 암묵적인 변환이다.

```jsx
// 암묵적인 변환
console.log("1" == 1); // true
console.log(1 == true); // true
console.log(0 == false); // true

console.log(11 + " 문자와 결합"); // '11 문자와 결합'
console.log(!!"문자열"); // true
console.log(!!""); // false

// 명시적 변환
parseInt("9.999", 10); // 9 (10진수)
```

- parseInt(’’, 진수)를 쓸때 기본적으로 10진수를 넣어주자.

```jsx
// 명시적 변환 (옳은 예)

console.log(String(11 + " 문자와 결합")); // '11 문자와 결합'
console.log(Boolean(!!"문자열")); // true
console.log(Boolean(!!"")); // false

Number("11"); // 11
```

- 사용자가 아닌 자바스크립트 엔진이 평가시에는 암묵적 형변환이 일어난다. 그래서 **우리는 타입 변환시 명시적 변환**을 해주어야 한다.

## **isNaN**

```jsx
console.log(Number.MAX_SAFE_INTEGER); //9007199254740991
console.log(Number.isInteger); //ƒ isInteger() {}

is Not A Number => 숫자가 아니다.
isNaN(123) // false => 숫자가 맞다.
typeof 123 === 'number' // true

isNaN(123+'테스트') // true => 숫자가 아니다.
Number.isNaN(123+ '테스트') // false => 숫자가 맞다.
```

- isNaN는 느슨한 검사이다.
- Number.isNaN 는 엄격한 검사이다. 그래서 **동적인 언어 js를 사용할때 Number.isNaN 안전한 검사를 사용**해라
