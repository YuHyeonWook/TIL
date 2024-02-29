# Promise

# Promise(JS의 비동기 담당 객체)

- Javascript 에서는 대부분의 작업들이 비동기로 이루어진다.
- 콜백 함수로 처리하면 되는 문제였지만 요즘에는 프론트엔드의 규모가 커지면서 코드의 복잡도가 높아지는 상황이 발생하였다. 이에 콜백이 중첩되는 경우가 따라서 발생하였고, 이를 해결할 방안으로 등장한 것이 Promise 패턴이다.
- Promise 패턴을 사용하면 비동기 작업들을 순차적으로 진행하거나, 병렬로 진행하는 등의 컨트롤이 보다 수월해진다.
- promise는 비동기 처리를 목적으로 제공되는 **자바스크립트 내장 객체**이다.

## **프로미스 객체 생성**

```jsx
const promise = new Promise(실행 함수);
```

- 프로미스 객체를 생성하여 변수인 promise에 저장함
- 프로미스 객체를 만들 때 인수로 실행 함수(executor)를 전달함.
  - 실행 함수 : 비동기 작업을 수행하는 함수이다.
  - 이 함수는 프로미스 객체를 생성과 동시에 실행되며 2개의 매개변수를 제공받는다.

```jsx
const myPromise = new Promise((resolve, reject) => {
  // 비동기 작업 수행
  const data = fetch("서버로부터 요청할 URL");

  if (data) resolve(data); // 만일 요청이 성공하여 데이터가 있다면
  else reject("Error"); // 만일 요청이 실패하여 데이터가 없다면
});
```

- Promise 객체를 생성하려면 new 키워드와 Promise 생성자 함수를 사용하면 된다. 이때 Promise 생성자 안에 두개의 매개변수를 가진 콜백 함수를 넣게 되는데, 첫 번째 인수는 작업이 성공했을 때 성공(resolve)임을 알려주는 객체이고, 두 번째 인수는 작업이 실패했을 때 실패(reject)임을 알려주는 오류 객체이다.

### 프로미스 객체 처리

- Promise 객체는 비동기 작업이 완료된 이후에 다음 작업을 연결시켜 진행할 수 있다. 작업 결과 따라.then() 과.catch() 메서드 체이닝을 통해 성공과 실패에 대한 후속 처리를 진행할 수 있다.

```jsx
myPromise
  .then((value) => {
    // 성공적으로 수행했을 때 실행될 코드
    console.log("Data: ", value); // 위에서 return resolve(data)의 data값이 출력된다
  })
  .catch((error) => {
    // 실패했을 때 실행될 코드
    console.error(error); // 위에서 return reject("Error")의 "Error"가 출력된다
  })
  .finally(() => {
    // 성공하든 실패하든 무조건 실행될 코드
  });
```

- 처리를 성공하면 resolve(data) 를 호출하게 되고, .then() 으로 이어져then 메서드의 콜백 함수에서 성공에 대한 처리를 진행한다.
- 처리가 실패하면 프로미스 객체 내부에서 reject("Error") 를 호출하게 되고, .catch() 로 이어져 catch 메서드의 콜백 함수에서 성공에 대한 처리를 진행한다.

### 프로미스 함수 등록

- 다음과 같이 별도로 함수로 감싸서 사용하는 것이 일반적이다.

```jsx
// 프로미스 객체를 반환하는 함수 생성
function myPromise() {
  return new Promise((resolve, reject) => {
    if (/* 성공 조건 */) {
      resolve(/* 결과 값 */);
    } else {
      reject(/* 에러 값 */);
    }
  });
}

// 프로미스 객체를 반환하는 함수 사용
myPromise()
    .then((result) => {
      // 성공 시 실행할 콜백 함수
    })
    .catch((error) => {
      // 실패 시 실행할 콜백 함수
    });
```

- 위 예제는 함수를 만들고 해당 하는 함수를 호출해서 프로미스 생성자를 return하여 **생성된 프로미스 객체를 함수 반환값으로 얻어 사용하는 기법**이다.
- 이렇게 프로미스 객체를 함수로 만드는 이유는 다음 3가지 정도가 있다.
  - 재사용성 : 프로미스 객체를 함수로 만들면 필요할 때마다 호출하여 사용함으로써, 반복되는 비동기 작업을 효율적으로 처리할 수 있다.
  - 가독성 : 프로미스 객체를 함수로 만들면 코드의 구조가 명확해져, 비동기 작업의 정의와 사용을 분리하여 코드의 가독성을 높일 수 있다.
  - 확장성 : 프로미스 객체를 함수로 만들면 인자를 전달하여 동적으로 비동기 작업을 수행할 수 있다. 또한 여러 개의 프로미스 객체를 반환하는 함수들을 연결하여 복잡한 비동기 로직을 구현할 수 있다.
- 이러한 점으로 인해 실무에서는 프로미스 객체를 사용할 일이 있다면 함수로 감싸서 사용한다. js의 fetch() 메서드는 fetch() 메서드 내에서 프로미스 객체를 생성하여 서버로부터 데이터를 가져오면 resolve()하여 .then()으로 처리한다.

```jsx
// GET 요청 예시
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json()) // 응답 객체에서 JSON 데이터를 추출한다.
  .then((data) => console.log(data)); // JSON 데이터를 콘솔에 출력한다.
```

## **프로미스 3가지 상태**

Promise 비동기 작업을 진행 단계에 따라 3가지 상태로 나누어 관리함

- Pending(대기) : 처리가 완료되지 않은 상태 (처리 진행중)
- Fulfilled(이행) : 성공적으로 처리가 완료된 상태
- Eejected(거부) : 처리가 실패로 끝난 상태

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/f6b03d4a-e8b8-4f43-a6a2-c6db7003d960)

### **Pending 상태**

- 대기(Pending) 상태란, 말 그대로 아직 비동기 처리 로직이 완료 되지 않은 상태이다

```jsx
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("처리 완료");
  }, 5000);
});
console.log(promise); // Pending (대기) 상태
```

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/8ffbe9b5-9cf3-424b-b015-efa0f30d2597)

### **Fulfilled 상태**

- 이행(fulfilled) 상태란, 비동기 처리 로직이 성공적으로 완료 됬다는 것을 표현하기 위한 상태라고 보면 된다.
- 위의 프로미스 코드를 실행하고 5초 동안 기다리다가 다시 콘솔을 출력하면. 아래와 같이 이행(fulfilled) 상태로 변하게 된다.

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/dc46138a-a327-4725-a632-74af1405bbee)

- 5초가 지나 resolve() 수행되면서 프로미스 성공을 알리는 개체를 호출하였으니 이행 상태로 변한 것이다.

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/29a3604b-65c5-4c57-9325-7439d0795f2b)

- 이행 상태로 변한 프로미스 객체는 바로 체이닝된 .then() 메서드를 호출하여 처리 결과 값을 받을 수 있다.

```jsx
promise.then((data) => {
  console.log("프로미스가 이행 상태가 되면서 처리에 대한 결과를 수행");
});
```

### **Rejected 상태**

- reject()를 호출하면 프로미스 객체가 실패(rejected) 상태가 된다.

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/c64be41e-523c-4789-9c08-717d9bf39525)

```jsx
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("처리 실패");
  }, 5000);
});
```

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/ddb1a804-24c4-42d8-b876-a9b4e32b40dc)

- 실패 상태로 변한 프로미스 객체는 바로 체이닝된.catch() 메서드를 호출하여 처리 실패에 대한 행동을 수행하게 된다.

```jsx
promise.catch((error) => {
  console.log(error);
  console.log("실패에 대한 후속 조치...");
});
```

유튜브 영상 시청하는 상황 Promise 객체의 3가지 예시)

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/d9210d90-3215-41f7-bc80-b6fe7aba56c7)

- 시청자가 특정 영상을 시청하기 위해 클릭하면 해당 영상을 불러오고, 영상 로딩 작업은 비동기적으로 동작함
  - 즉, 영상이 로딩되기까지 사용자는 다른 영상을 탐색하거나 댓글을 다는 등의 행동을 할 수 있다.
- 영상 로딩 과정에서 영상이 로딩 중인 상태를 ‘대기 상태’라고 할 수 있다. 그리고 정상적으로 영상이 로딩되었다면 이를 ‘해결’이라고 할 수 있으며, 이 상태를 ‘성공 상태’라고 말할 수 있다. 만약 영상이 모종의 이유로 로딩되지 못했다면 이를 ‘거부’라고 할 수 있으며, 이 상태는 ‘실패 상태’라고 말할 수 있음

## **프로미스 핸들러**

- 프로미스가 생성되면, 성공/ 실패 결과를 .then / .catch / .finally 핸들러를 통해 받아 다음 후속 작업을 수행할 수 있다. 프로미스 핸들러는 프로미스의 상태에 따라 실행되는 콜백 함수라고 생각하면 된다.
  - .then() : 프로미스가 이행(fulfilled)되었을 때 실행할 콜백 함수를 등록하고, 새로운 프로미스를 반환
  - .catch() : 프로미스가 거부(rejected)되었을 때 실행할 콜백 함수를 등록하고, 새로운 프로미스를 반환
  - .finally() : 프로미스가 이행되거나 거부될 때 상관없이 실행할 콜백 함수를 등록하고, 새로운 프로미스를 반환
- 마치 try - catch - finally 구조와 유사하다.

### **프로미스 체이닝**

- 프로미스 체이닝이란 프로미스 핸들러를 연달아 연결하는 것을 말한다. 이는 여러 개의 비동기 작업을 순차적으로 수행할 수 있다는 특징이 있다.
- 프로미스는 then, catch, finally 후속 처리 메서드를 통해 콜백 헬을 해결한다.

```
function doSomething() {
  return new Promise((resolve, reject) => {
      resolve(100)
  });
}

doSomething()
    .then((value1) => {
        const data1 = value1 + 50;
        return data1
    })
    .then((value2) => {
        const data2 = value2 + 50;
        return data2
    })
    .then((value3) => {
        const data3 = value3 + 50;
        return data3
    })
    .then((value4) => {
        console.log(value4); // 250 출력
    })
```

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/a88f73df-0288-4e25-b7a3-5fb93613a145)

- 위 doSomething 함수를 호출하여 프로미스를 생성하고, then 메서드를 통해 이행 핸들러를 연결하는 과정이다. 각 이행 핸들러는 이전 프로미스의 값에 50을 더한 값을 반환하고, 마지막 이행 핸들러는 최종값을 콘솔에 출력한다.
- 이러한 체이닝이 가능한 이유는 then 핸들러에서 값을 리턴하면, 그 반환값은 자동으로 프로미스 객체로 감싸져 반환된다. 그리고 다음 then 핸들러에서 반환된 프로미스 객체를 받아 처리한다. 이의 프로미스 상태의 흐름도를 표현하면 아래와 같다.

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/c91e9d24-d5cb-464f-a999-df3a978f972a)

<br>

```
function doSomething(arg) {
  return new Promise((resolve, reject) => {
      resolve(arg)
  });
}

doSomething('100A')
    .then((value1) => {
        const data1 = value1 + 50; // 숫자에 문자를 연산

        if (isNaN(data1))
            throw new Error('값이 넘버가 아닙니다')

        return data1
    })
    .then((value2) => {
        const data2 = value2 + 50;
        return data2
    })
    .catch((err) => {
        console.error(err);
    }
```

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/4b8435d8-70d1-4c16-b364-2a70b9662454)

- 만일 연결된 이행 핸들러에서 중간에 오류가 있는 처리를 행한다면 예외처리를 함으로써 catch 핸들러에 점프하도록 설정할 수 있다.

```
new Promise((resolve, reject) => {
  throw new Error("에러 발생!");
})
    .catch(function(error) {
      console.log("에러가 잘 처리되었습니다. 정상적으로 실행이 이어집니다.");
    })
    .then(() => {
        console.log("다음 핸들러가 실행됩니다.")
    })
    .then(() => {
        console.log("다음 핸들러가 또 실행됩니다.")
    });

```

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/174c26e4-0751-46b8-9c52-ed2071155cb3)

- catch 핸들러 다음으로 then 핸들러가 이어서 체이닝 되어 있다면, 에러가 처리되고 가까운 then 핸들러로 제어 흐름이 넘어가 실행이 이어지게 된다.

## **프로미스 정적 메서드**

- 프로미스 객체는 생성자 함수 외에도 여러 가지 정적 메서드(static method)를 제공한다. 정적 메서드는 객체를 초기화 & 생성하지 않고도 바로 사용할 수 있기 때문에 비동기 처리를 보다 효율적이고 간편하게 구현할 수 있도록 도와준다.

### **Promise.resolve()**

```jsx
// 프로미스 생성자를 사용하여 프로미스 객체를 반환하는 함수
function getPromiseNumber() {
  return new Promise((resolve, reject) => {
    const num = Math.floor(Math.random() * 10); // 0 ~ 9 사이의 정수
    resolve(num); // 프로미스 이행
  });
}

// Promise {<fulfilled>: 3}
```

- Promise.resolve() 정적 메서드로 한번에 호출할 수 있도록 편의 기능을 제공해준다.
- 프로미스 정적 메서드를 이용하면 프로미스 객체와 전혀 연관없는 함수 내에서 필요에 따라 **프로미스 객체를 반환하여 핸들러를 이용**할 수 있도록 응용이 가능하다. 이 방법은 비동기 작업을 수행하지 않는 함수에서도 프로미스의 장점을 활용하고 싶은 경우에 유용하다.

```jsx
// 프로미스 객체와 전혀 연관없는 함수
function getRandomNumber() {
  const num = Math.floor(Math.random() * 10); // 0 ~ 9 사이의 정수
  return num;
}

// Promise.resolve() 를 사용하여 프로미스 객체를 반환하는 함수
function getPromiseNumber() {
  const num = getRandomNumber(); // 일반 값
  return Promise.resolve(num); // 프로미스 객체
}

// 핸들러를 이용하여 프로미스 객체의 값을 처리하는 함수
getPromiseNumber()
  .then((value) => {
    console.log(`랜덤 숫자: ${value}`);
  })
  .catch((error) => {
    console.error(error);
  });
```

### **Promise.reject()**

- 주어진 사유로 거부하는 Promise 객체를 반환한다

```jsx
// 주어진 사유로 거부되는 프로미스 생성
const p = Promise.reject(new Error("error"));

// 거부 사유를 출력
p.catch((error) => console.error(error)); // Error: error
```

### **Promise.all()**

- 배열, Map, Set에 포함된 여러개의 프로미스 요소들을 한꺼번에 비동기 작업을 처리해야 할때 유용한 프로미스 정적 메소드이다.
- 모든 프로미스 비동기 처리가 이행(fulfilled) 될때까지 기다려서, 모든 프로미스가 완료되면 그때 then 핸들러가 실행하는 형태이다. 가장 대표적인 사용 예시로 여러 개의 API 요청을 보내고 모든 응답을 받아야 하는 경우에 사용할 수 있다.

```jsx
// 1. 서버 요청 API 프로미스 객체 생성 (fetch)
const api_1 = fetch("https://jsonplaceholder.typicode.com/users");
const api_2 = fetch("https://jsonplaceholder.typicode.com/users");
const api_3 = fetch("https://jsonplaceholder.typicode.com/users");

// 2. 프로미스 객체들을 묶어 배열로 구성
const promises = [api_1, api_2, api_3];

// 3. Promise.all() 메서드 인자로 프로미스 배열을 넣어, 모든 프로미스가 이행될 때까지 기다리고, 결과값을 출력
Promise.all(promises)
  .then((results) => {
    // results는 이행된 프로미스들의 값들을 담은 배열.
    // results의 순서는 promises의 순서와 일치.
    console.log(results); // [users1, users2, users3]
  })
  .catch((error) => {
    // 어느 하나라도 프로미스가 거부되면 오류를 출력
    console.error(error);
  });
```

### **Promise.allSettled()**

- Promise.all() 메서드의 상위 버전으로, 주어진 모든 프로미스가 처리되면 모든 프로미스 각각의 상태와 값 (또는 거부 사유)을 모아놓은 배열을 반환한다.

```jsx
// 1초 후에 1을 반환하는 프로미스
const p1 = new Promise((resolve) => setTimeout(() => resolve(1), 1000));

// 2초 후에 에러를 발생시키는 프로미스
const p2 = new Promise((resolve, reject) =>
  setTimeout(() => reject(new Error("error")), 2000)
);

// 3초 후에 3을 반환하는 프로미스
const p3 = new Promise((resolve) => setTimeout(() => resolve(3), 3000));

// 세 개의 프로미스의 상태와 값 또는 사유를 출력
Promise.allSettled([p1, p2, p3]).then((result) => console.log(result));
```

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/ce0bbd63-e879-4e82-a569-2fb94777ebcb)

### **Promise.any()**

- Promise.all() 메서드의 반대 버전으로, Promise.all()이 주어진 모든 프로미스가 **모두 완료**해야만 결과를 도출한다면,
- Promise.any()는 주어진 모든 프로미스 중 **하나라도 완료(이행)**되면 바로 반환하는 정적 메서드이다.

```jsx
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise1 failed");
  }, 3000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise2 succeeded");
  }, 2000);
});

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise3 failed");
  }, 1000);
});

// promise1, promise2, promise3은 각각 3초, 2초, 1초 후에 거부되거나 이행
Promise.any([promise1, promise2, promise3])
  .then((value) => {
    console.log(value); // "promise2 succeeded"
  })
  .catch((error) => {
    console.error(error);
  });

// 결괏값 :
// promise2 succeeded
```

- 위 코드는 Promise.any() 메서드의 결과로 promise2의 처리가 가장 먼저 도출됨을 볼 수 있다. 첫번째로 이행(fulfilled) 된 프로미스만을 취급하기 때문에 나머지 promise1과 promise3의 거부(rejected)는 무시되게 된다.

```jsx
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise1 failed");
  }, 3000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("promise2 succeeded");
  }, 2000);
});

const promise4 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("promise4 failed");
  }, 4000);
});

Promise.any([promise1, promise3, promise4])
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.error(error); // AggregateError: All promises were rejected
    console.error(error.errors); // ["promise3 failed", "promise1 failed", "promise4 failed"]
  });
```

- 만약 요청된 모든 프로미스가 거부(rejected)되면, AggregateError 객체를 사유로 하는 거부 프로미스를 반환한다.

### **Promise.race()**

```jsx
new Promise((resolve, reject) => {
  throw new Error("에러 발생!");
})
  .catch(function (error) {
    console.log("에러가 잘 처리되었습니다. 정상적으로 실행이 이어집니다.");
  })
  .then(() => {
    console.log("다음 핸들러가 실행됩니다.");
  })
  .then(() => {
    console.log("다음 핸들러가 또 실행됩니다.");
  });
```

- Promise.race()는 Promise.any() 와 같이 여러 개의 프로미스 중 가장 먼저 처리된 프로미스의 결과값을 반환한다. 하지만 차이점이 존재한다.
- Promise.any()는 가장 먼저 fulfilled(이행) 상태가 된 프로미스만을 반환하거나, 혹은 전부 rejected(실패) 상태가 된 프로미스(AggregateError)를 반환한다.
- 반면 Promise.race()는 fulfilled(이행), rejected(실패) 여부 상관없이 무조건 처리가 끝난 프로미스 결과값을 반환하다.

<aside>
💡 마치 프로미스 참가자들이 레이싱(race) 경주를 하는것을 떠올리면 된다.

</aside>

Promise.any 예시)

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/bda7cb19-25b6-4ddf-aabd-8d588fa94db8)

Promise.race 예시)

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/456d1750-d683-4b91-8abc-d1a756946850)

## **Promise 내부 동작 과정**

- Callback Queue의 종류에는 (Macro)Task Queue, MicroTask Queue 2가지가 있다
  - 그중 자바스크립트 Promise 객체의 콜백이 쌓이는 곳이 바로 MicroTask Queue이다. 그리고 MicroTask Queue는 그 어떤 곳보다 가장 먼저 우선으로 콜백이 처리되게 된다.

![image](https://github.com/KDT1-FE/KDT8-M1/assets/110236953/59a32584-a36b-4f95-a25a-929abf040f76)

```
console.log('Start!');

setTimeout(() => {
	console.log('Timeout!');
}, 0);

Promise.resolve('Promise!').then(res => console.log(res));

console.log('End!');
```

1. Call Stack에console.log('Start!') 코드 부분이 쌓인 뒤 실행 되어 콘솔창에 "Start!" 가 출력
2. setTimeout 코드가 콜 스택에 적재되고 실행되면, 그 안의 콜백 함수가 이벤트 루프에 의해 Web API로 옮겨지고 타이머가 작동하게 된다. (0초라서 사실상 바로 타이머는 종료된다)
3. 타이머가 종료됨에 따라setTimeout 의 콜백 함수는 MacroTask Queue에 이벤트 루프에 의해 적재되게 된다.
4. Promise 코드가 콜스택에 적재 되어 실행되고then 핸들러의 콜백 함수가 이벤트 루프에 의해 MicroTask Queue에 적재되게 된다.
5. console.log('End!') 코드가 실행되고 "End!" 텍스트가 콘솔창에 출력된다.
6. 모든 메인 스레드의 자바스크립트 코드가 실행이되어 더이상 Call Stack엔 실행할 스택이 없어 비워지게 된다.
7. 그러면 이벤트 핸들러가 이를 감지하여, Callback Queue에 남아있는 콜백 함수들을 빼와 Call Stack에 적재하게 된다
8. 이때 2종류의 Queue 중 MicroTask Queue에 남아있는 콜백이 우선적으로 처리된다. (만일 콟개이 여러개가 있다면 전부 처리된다)
9. MicroTask Queue가 비어지면, 이제 이벤트 루프는 MacroTask Queue에 있는 콜백 함수를 Call Stack에 적재해 실행되게 된다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/12a05be2-c55d-4e99-8b30-2cd382d89004)

## **프로미스 정적 메서드**

- **Promise.resolve()** : 비동기 작업의 상태를 **성공**으로 바꾸는 함수
- **Promise.reject()** : 비동기 작업의 상태를 **실패**로 바꾸는 함수
    <aside>
    📢 앞서 살펴 보았듯이 프로미스는 비동기 작업의 상태를 대기(Pending), 성공(Fulfilled), 실패(Rejected)로 나누어 관리함. 실행 함수가 제공받는 2개의 매개변수는 대기 상태의 비동기 작업을 성공 또는 실패 상태로 변경하는 역할을 함
    
    </aside>

실행 함수에서 매개변수로 제공된 resolve를 호출하여 작업 상태를 성공 상태로 변경하는 예시)

```
const promise = new Promise(function (resolve, reject) {
  setTimeout(() => {
    resolve("성공");
  }, 500);
});
```

- 위 예제는 0.5초 기다린 후 resolve를 호출하여 인수로 전달한 값 “성공”은 비동기 작업의 결괏값이 된다.
- 이 결괏값을 비동기 작업이 아닌 곳에서 이용하려면 프로미스 객체의 **then 메서드**를 이용하면 된다. then 메서드는 인수로 전달한 콜백 함수의 비동기 작업이 성공했을 때 실행한다.

<br>

# 참고

모던 js 딥다이브
[https://inpa.tistory.com/entry/🔄-자바스크립트-이벤트-루프-구조-동작-원리#promise*내부*동작\_과정](https://inpa.tistory.com/entry/%F0%9F%94%84-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-%EA%B5%AC%EC%A1%B0-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC#promise_%EB%82%B4%EB%B6%80_%EB%8F%99%EC%9E%91_%EA%B3%BC%EC%A0%95)

한입 크기 리액트
