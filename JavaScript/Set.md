# **셋(Set)**

- 셋(Set)은 **중복**을 허용하지 않는 값을 모아놓은 특별한 컬렉션임.
- set에 키가 없는 값이 저장됨

```jsx
let sett = new Set(["bananas", "oranges", "bananas", "apples", "bananas"]);
// Set(3) {'bananas', 'oranges', 'apples'}
```

```jsx
new Set(iterable)
# 셋을 만듭니다. 이터러블 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어줍니다.

set.add(value)
# 값을 추가하고 셋 자신을 반환합니다.

set.delete(value)
# 값을 제거합니다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 true, 아니면 false를 반환합니다.

set.has(value)
# 셋 내에 값이 존재하면 true, 아니면 false를 반환합니다.

set.clear()
# 셋을 비웁니다.

set.size
# 셋에 몇 개의 값이 있는지 세줍니다.

```

방문자 방명록을 만든다고 가정

한 방문자가 여러 번 방문해도 방문자를 중복해서 기록하지 않겠다고 결정 내린 상황임 즉, 한 방문자는 '단 한 번만 기록’되어야 함

이때 적합한 자료구조가 바로 `셋`임

```jsx
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// 어떤 고객(john, mary)은 여러 번 방문할 수 있습니다.
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// 셋에는 유일무이한 값만 저장됩니다.
alert(set.size); // 3

for (let user of set) {
  alert(user.name); // // John, Pete, Mary 순으로 출력됩니다.
}
```

- `셋` 대신 배열을 사용하여 방문자 정보를 저장한 후, 중복 값 여부는 배열 메서드인 [arr.find](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/find)를 이용해 확인할 수도 있다.
  - 하지만 `arr.find`는 배열 내 요소 전체를 뒤져 중복 값을 찾기 때문에, 셋보다 성능 면에서 떨어진다.
  - 반면, `셋`은 값의 유일무이함을 확인하는데 최적화되어있다.

<br>

# **Set의 값의 반복 작업**

for..of나 forEach를 사용하면 셋의 값을 대상으로 반복 작업을 수행할 수 있다.

```jsx
let set = new Set(["oranges", "apples", "bananas"]); // {"oranges", "apples", "bananas"}

for (let value of set) alert(value);

// forEach를 사용해도 동일하게 동작합니다.
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```

- forEach에 쓰인 콜백 함수는 세 개의 인수를 받는데,첫 번째는 값, 두 번째도 같은 값인 valueAgain을 받고 있다. 세 번째는 목표하는 객체(셋)이고요.
  - 즉, 동일한 값이 인수에 두 번 등장하고 있다.이렇게 구현된 이유는맵과의 호환성때문임.
  - 맵의 forEach에 쓰인 콜백이 세 개의 인수를 받을 때를 위해서죠.이상해 보이겠지만 이렇게 구현해 놓았기 때문에 맵을 셋으로 혹은 셋을 맵으로 교체하기가 쉽다.

셋에도 맵과 마찬가지로 반복 작업을 위한 메서드가 있습니다.

```jsx
set.keys()
# 셋 내의 모든 값을 포함하는 이터러블 객체를 반환합니다.

set.values()
# set.keys와 동일한 작업을 합니다. 맵과의 호환성을 위해 만들어진 메서드입니다.

set.entries()
# 셋 내의 각 값을 이용해 만든 [value, value] 배열을 포함하는 이터러블 객체를 반환합니다. 맵과의 호환성을 위해 만들어졌습니다.

```

<br>

# 참고

https://ko.javascript.info/map-set

[https://inpa.tistory.com/entry/JS-📚-자료형-Set-🚩-정리?category=889099](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9E%90%EB%A3%8C%ED%98%95-Set-%F0%9F%9A%A9-%EC%A0%95%EB%A6%AC?category=889099)
