# **truthy & falsy, 단축평가**

- **truthy & falsy에 대해 알아보자.**

```jsx
if ("string".length) {
}

if (10) {
}

if (boolean) {
}
```

- 위 처럼 if문이 boolean 에 만족(true)하면 {}내부가 실행된다. 밑에도 똑같다.

```jsx
// truthy
true;
{};
[];
42;
("0");
("false");
new Date();
3.14 - 3.14;
Infinity - Infinity;
```

- 위 예시는 다 truthy로 평가된다.

```jsx
// falsy
false;
null;
undefined;
0;
0n;
NaN;
("");
```

- 위 예시도 falsy로 평가된다.

## 정리

- 간단한 조건문 로직은 truthy, falsy를 활용해라 ex) null과 undefined

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/97c4d37e-c871-4a4b-be8e-cb7f305a0990)


- undefined를 활용함

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/0b67f314-801d-474d-af6f-c3d44ec337fd)


- 함수 호출에 null 활용함

# 단축평가

```scss
true && true && "도달O"; // '도달O'
true && false && "도달X"; // false

false || false || "도달O"; // '도달 O'
false || true || "도달X"; // true
```

```scss
function fetchDate() {
  if (state.data) {
    return state.data;
  } else {
    return "Fetching....";
  }
}

return state.data ? state.data : "Fetching..."; // 삼항 연산자 이용

return state.data || "Fetching..."; // 단축 평가 이용
```

- 위는 삼항 연산자도 가능하지만,  or 연산자(단축 평가)로 평가가 가능하다.

```scss
// 안 좋은 예
function favoriteDog(someDog) {
  let favoriteDog;
  if(someDog) {
    favoditeDog = someDog;
  } else {
    favoriteDog='냐옹'
  }
  return favoriteDog + '입니다';
})
favoriteDog() // => 냐옹 입니다
favoriteDog('포메') // => 포메 입니다.

// 좋은 예
function favoriteDog(someDog) {
  return (someDog || '냐옹') + '입니다';
}

favoriteDog() // => 냐옹 입니다
favoriteDog('뽀삐') // => 뽀삐 입니
```

- 단축 평가로 코드를 줄을 수 있고, 가독성도 좋다.

다른예시

```scss
// 안 좋은 예
const getActiveUserName = (user, isLogin) {
  if(isLogin) {
    if(user){
      if(user.name){
        return user.name;
      } else {
        return '이름없음';
      }
    }
  }
}

// 좋은 예
const getActiveUserName = (user, isLogin) {
  if(isLogin && user) {
    if(user.name) {
      return user.name;
    } else {
      return '이름없음';
    }
  }
}

// 더 좋은 예
const getActiveUserName = (user, isLogin) {
  if(isLogin && user) {
    return user.name || '이름없음
  }
```

- 위 예시는 if else 문을 단축 평가를 || 사용하면 더 줄일 수 있다.

## 정리

- 논리 연산자를 활용하여 단축 평가를 하자. &&, ||