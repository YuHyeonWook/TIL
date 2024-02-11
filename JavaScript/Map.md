# Map

객체 - 키가 있는 컬렉션을 저장함

배열 - 순서가 있는 컬렉션을 저장함

현실 세계를 반영하기엔 이 두 자료구조 만으론 부족해서 맵(Map)과 셋(Set)이 등장하게 되었습니다.

<br>

## Map 자료형

키가 있는 데이터를 저장한다는 점에서 객체와 유사한다. 다만, 맵을 **키에 다양한 자료형**을 허용한다는 점에서 차이가 있다.

```jsx
// 2차원 key, value 형태의 배열
let map = new Map([
  ["a", 1],
  ["a1", 2],
  ["b", 3],
]);
// map 자료형 : {"a" => 1, "a1" => 2, "b" => 3}
```

```jsx
new Map()
# 맵을 만듬

map.set(key, value)
# key를 이용해 value를 저장

map.get(key)
# key에 해당하는 값을 반환함. key가 존재하지 않으면 undefined를 반환

map.has(key)
# key가 존재하면 true, 존재하지 않으면 false를 반환

map.delete(key)
# key에 해당하는 값을 삭제

map.clear()
# 맵 안의 모든 요소를 제거

map.size
# 요소의 개수를 반환
```

```jsx
let map = new Map();

map.set("1", "str1"); // 문자형 키
map.set(1, "num1"); // 숫자형 키
map.set(true, "bool1"); // 불린형 키

// 결과
// Map(3) {
//'1' => 'str1',
// 1 => 'num1',
// true => 'bool1'
// }
```

```jsx
// map.get(key)은 key를 반환함
alert(map.get(1)); // 'num1'
alert(map.get("1")); // 'str1'
alert(map.size); // 3
```

- Map은 객체와 달리 키를 문자형으로 변환하지 않음. key엔 자료형 제약이 없다.

```jsx
let map1 = new Map([
  ["a", 1],
  ["a", 2],
  ["b", 3],
]); // {"a" => 2, "b" => 3}

let object1 = {
  a: 1,
  a: 2,
  b: 3,
}; // {a: 2, b: 3}
```

- Map의 key에 중복값이 있으면 나중값으로 적용됨 ( 이는 객체도 똑같음)

> map[key]는 Map을 쓰는 바른 방법이 아님. map[key] = 2로 값을 설정하는 것 같이 map[key]를 사용할 수 있긴 함. 하지만 이 방법은 map을 일반 객체처럼 취급하게 된다. 따라서 여러 제약이 생겨 map을 사용할 땐 map 전용 메서드 set, get등을 사용해야만 한다.

<br>

## map은 key로 객체도 허용함

```jsx
let john = { name: "John" };

// 고객의 가게 방문 횟수를 세본다고 가정
let visitsCountMap = new Map();

// john을 맵의 키로 사용
visitsCountMap.set(john, 123);

alert(visitsCountMap.get(john)); // 123
```

- 객체를 키로 사용할 수 있다는 점은 map의 가장 중요한 기능 중 하나임. 객체에는 문자열 키를 사용할 수 있다. 하지만 객체 키는 사용 수 없다.

객체형 키를 객체에 쓰는 예시)

```jsx
let john = { name: "John" };
let visitsCountObj = {}; // 객체를 하나 만듭니다.

visitsCountObj[john] = 123; // 객체(john)를 키로 해서 객체에 값(123)을 저장해봅시다.

// 원하는 값(123)을 얻으려면 아래와 같이 키가 들어갈 자리에 `object Object`를 써줘야합니다.
alert(visitsCountObj["[object Object]"]); // 123
```

- visitsCountObj 는 객체이기 때문에 모든 키를 문자형으로 변환시킴. 이 과정에서 john은 문자형으로 변환되어 "[object Object]"가 됨

### 체이닝

- map.set을 호출할 때마다 맵 자신이 반환된다. 이를 이용하면 map.set을 ‘체이닝’할 수 있다.

```jsx
map.set("1", "str1").set(1, "num1").set(true, "bool1");
// Map(3) {'1' => 'str1', 1 => 'num1', true => 'bool1'}
```

<br>

## **맵의 요소에 반복 작업**

다음 세 가지 메서드를 사용해 맵의 각 요소에 반복 작업을 할 수 있다.

```jsx
map.keys()
# 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환합니다.

map.values()
# 각 요소의 값을 모은 이터러블 객체를 반환합니다.

map.entries()
# 요소의 [키, 값]을 한 쌍으로 하는 이터러블 객체를 반환합니다. 이 이터러블 객체는 for..of반복문의 기초로 쓰입니다.
```

```jsx
let recipeMap = new Map([
  ["cucumber", 500],
  ["tomatoes", 350],
  ["onion", 50],
]);

// 키(vegetable)를 대상으로 순회합니다.
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// 값(amount)을 대상으로 순회합니다.
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// [키, 값] 쌍을 대상으로 순회합니다.
for (let entry of recipeMap) {
  // recipeMap.entries()와 동일합니다.
  alert(entry); // cucumber,500 ...
}
```

[팁]

> 맵은 삽입 순서를 기억함(이터러블 객체) 맵은 값이 삽입된 순서대로 순회를 실시함. 객체가 프로퍼티 순서를 기억하지 못하는 것과는 다름

여기에 더하여 `맵`은 `배열`과 유사하게 내장 메서드 `forEach`도 지원함

### **객체 -> 맵 으로 바꾸기**

- 평범한 객체를 가지고 맵을 만들고 싶다면 내장 메서드Object.entries(obj)Visit Website를 활용해야 함. 이 메서드는 객체의 키-값 쌍을 요소([key, value])로 가지는 배열을 반환함.

```jsx
// 그냥 맵 만들기 (각 요소가 [키, 값] 쌍인 배열)
let map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

// 객체로 맵 만들기
let obj = {
  name: "John",
  age: 30,
};

let map2 = new Map(Object.entries(obj)); // 객체를 2차원의 키:밸류 형태로 만들고 맵으로 변환
// [ ["name","John"], ["age", 30] ]
alert(map2.get("name")); // John
```

- Object.entries를 사용해 객체 obj를 배열 [ ["name","John"], ["age", 30] ]로 바꾸고, 이 배열을 이용해 새로운 맵을 만들어봄

### **맵 -> 객체 로 바꾸기**

- Object.fromEntries를 사용하면 가능함. 이 메서드는 각 요소가 [키, 값] 쌍인 배열을 객체로 바꿔줌. 자료가맵에 저장되어있는데, 서드파티 코드에서 자료를 객체형태로 넘겨받길 원할 때 이 방법을 사용할 수 있다.

```jsx
let map = new Map();
map.set("banana", 1);
map.set("orange", 2);
map.set("meat", 4);

let obj = Object.fromEntries(map.entries()); // 맵을 일반 객체로 변환 (*)
// let obj = Object.fromEntries(map); // .entries()를 생략할 수 있음.
// 맵이 객체가 되었습니다!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```

</br>

# 참고

https://ko.javascript.info/map-set

[https://inpa.tistory.com/entry/JS-📚-자료형-Map-🚩-정리](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9E%90%EB%A3%8C%ED%98%95-Map-%F0%9F%9A%A9-%EC%A0%95%EB%A6%AC)
