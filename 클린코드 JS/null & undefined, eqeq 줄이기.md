# null & undefined, **eqeq 줄이기**

- null과 undefined 두 타입 모두 값이 ‘없음’을 의미한다.
  - 둘 다 데이터 타입이자 변수의 값이다.
- 또한, 자바스크립트에서 변수를 선언하면 초기값으로 undefined를 할당하게 되고, null은 ‘비어있음'을 명시적으로 나타내고 싶을 때 사용하는 것이다.

undefined & null 예시)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/15286033-a3f1-477b-b9b3-fe4478df0df5)

## 요약

- undefined & null은 값이 없거나 정의되지 않음
  - undefined의 숫자형은 NaN이고, type은 undefined이다.
  - null의 숫자형 0이고, type은 object이다.
- undefined & null의 쓰임을 조심하자

## eqeq 줄이기 (동등 연산자 ==)

### **equality (==)**

- **동등 연산자는** 형변환(type casting)이 일어난다.

```
console.log(1 == 1); // true
console.log(1 == "1"); // true

//Strict equality(===)
console.log(1 === 1); // true
console.log(1 === "1"); // false

const ticketNum = document.querySelector("#ticketNum");
console.log(ticketNum.value); // '0'
console.log(ticketNum.value > 1000); // false
console.log(ticketNum.value === 0); // false

console.log(ticketNum.value == 0); // 위험 협업시 알아듣기 어렵다.

// 옳은 예
console.log(Number(ticketNum.value) === 0); // true
console.log(ticketNum.valueAsNumber == 0); // true
```

- 옳은 예처럼 형변환을 명시적으로 해서 안전하게 검사 해야한다.
