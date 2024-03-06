# else if 문, else문피하기, **Early Return**

```jsx
const x = 1;
if (x >= 0) {
  console.log("x는 0과 같거나 크다");
} else if (x > 0) {
  console.log("x는 0보다 크다");
}

// 위와 똑같은 예
if (x >= 0) {
  console.log("x는 0과 같거나 크다");
} else {
  if (x > 0) {
    console.log("x는 0보다 크다");
  }
}
```

- else if문을 쓰기보다는 switch문을 쓰는 것이 더 좋다.

```jsx
// 올바른 예
if (x >= 0) {
  console.log("x는 0과 같거나 크다");
} 
if (x > 0) {
   console.log("x는 0보다 크다");
 }

```

- 명확하게 조건을 분리해라!!

## 정리

- 위 예시처럼 if문의 조건을 분리하고, if문이 많이 늘어날 경우 switch문을 사용하자.

# else 피하기

```jsx
function getActiveUserName(user)  {
  if(user.name) {
    return user.name;
  } else {
    return '이름없음';
  }
}
```

```jsx
// else문 안쓰는 예시
function getActiveUserName(user)  {
  if(user.name) {
    return user.name;
  }
    return '이름없음';
}
```

다른예시)

```jsx
// age가 20미만일 때 report() 함수를 실행하는 예시
// 나쁜 예
function getHelloCustomer(user) {
  if(user.age < 20) {
    report(user);
  } else { //  else 사용시 return '인녕하세요' 실행이 되지 않는다.
    return '안녕하세요';
  }
}
```

- if문에 조건을 만족, 불만족한 경우 ‘안녕하세요’를 반환하고 싶을 떄 else문을 쓰면 안녕하세요가 실행되지 않는다. 위 에시는 if else문을 하나의 역할이 아닌 2개의 역할을 하고 있다.
- 이처럼 우리가 원하는 결과를 나오지 않을 때 else문을 빼면 된다.

```jsx

// else 문 사용 안한 예
function getHelloCustomer(user) {
  if(user.age < 20) {
    report(user);
  }
 
  return '안녕하세요';
}
```

## 정리

- 항상 else문을 쓸 필요는 없다. 습관이 되지 말자.

# **Early Return**

- Early Return은 함수를 미리 종료시키고, 사고(사람이 생각)하기 편하다

```jsx
// 읽기 어려움
function loginService(isLogin, user) {
  if (!isLogin) {
    if (checkToken()) {
      if (!user.nickName) {
        return registerUser(user);
      } else {
        refreshToken();

        return "로그인 성공";
      }
    } else {
      throw new Error("No Token");
    }
  }
}

```

```jsx

// eary return 활용하는 예시
function loginService(isLogin, user) {
  if (isLogin) { // 로그인이 되어있으면 함수 종료
    return;
  }
  if (!checkToken) { // 토근이 없으면 에러를 발생시킴
    throw new Error("No Token");
  }
  if (!user.nickName) {
    return registerUser(user);
  }

  refreshToken();

  return "로그인 성공";
}
```

- Early Return을 활용하면 명시적으로 코드를 알 수 있다.

```jsx
function 오늘하루(condition, weather, isJob) {
  if (condition === "GOOD") {
    공부();
    게임();
    유투브보기();
  }

  if (weather === "GOOD") {
    운동();
    빨래();
  }

  if (isJob) === "GOOD") {
    야간업무();
    조기취침();
    유투브보기();
  }
}

// early return
function 오늘하루(condition, weather, isJob) {
  if (condition !== "GOOD") {
    return
  }
  공부();
  게임();
  유투브보기();
  if (weather !== "GOOD") {
    return
  }
  운동();
  빨래();

  if (isJob !== "GOOD") {
    return
  }
  야간업무();
  조기취침();
  유투브보기();

}
```

## 정리

- Early Return을 활용하면 명시적으로 코드를 알 수 있다.