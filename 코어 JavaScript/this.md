# this

# 상황에 따라 달라지는 this

- this는 기본적으로 실행 컨텍스트가 생성될 때 함께 결정된다.
- 실행컨텍스트는 함수를 호출할 때 생성되므로, 바꿔 말하면 t**his는 함수를 호출할 때 결정된다.**

## 1) 전역공간에서 this

- 전역 공간에서 this는 전역 객체를 가리킨다.
- 브라우저 환경에서 전역객체는 **window**이고, Node.js에서는 global이다.

전역변수와 전역객체 1)

```jsx
var a = 1;
console.log(a);        // 1
console.log(window.a); // 1
console.log(this.a);   // 1
```

- 전역공간에서 선언한 변수 a에 1을 할당했을 뿐인데 window.a와 this.a 모두 1이 출력된다.
- 이에 대한 이유는 **자바스크립트의 모든 변수는 특정 객체의 프로퍼티로서 동작한다.**
- 특정 객체란 실행 컨텍스트의 LexicalEnvironment(이하 L.E라 한다)이다.
- 실행 컨텍스트는 변수를 수집해서 L.E의 프로퍼티로 저장한다. 이후 어떤 변수를 호출하면 L.E를 조회해서 일치하는 프로퍼티가 있을 경우 그 값을 반환한다.
- 전역 컨텍스트의 경우 L.E는 전역객체를 그대로 참조한다.

전역변수와 전역객체 선언 2)

```jsx
var a = 1;
window.b = 2;
console.log(a, window.a, this.a); // 1 1 1
console.log(b, window.b, this.b); // 2 2 2
```

- 전역 공간에서 var로 변수를 선언하는 대신 window의 프로퍼티에 직접 할당하더라도 결과적으로  var로 선언한 것과 똑같이 동작한다.
- 그런데 전역변수 선언과 전역객체의 프로퍼티 할당 사이에 전혀 다른 경우도 있다. 바로 ‘삭제’ 명령에 해당한다.

전역변수와 전역객체 삭제 3)

```jsx
전역변수
var a = 1;
delete window.a;    // false
console.log(a, window.a, this.a);   /// 1 1 1
```

```jsx
var b = 2;
delete window.b;  //false
console.log(b, window.b, this.b); // 2 2 2
```

```jsx
전역객체
window.c = 3;
delete window.c; // true
console.log(c, window.c, this.c);  // Uncaught ReferenceError: c is not defined
```

```jsx
window.d = 4;
delete d; // true
console.log(d, window.d, this.d);  // Uncaught ReferenceError: d is not defined
```

- 전역객체의 프로퍼티로 할당한 경우 → 삭제가 되고,
- 전역변수로 선언한 경우 → 삭제가 되지 않는다.
    - 전역변수를 선언하면  js엔진이 이를 자동으로 전역객체의 프로퍼티로 할당하면서 추가적으로 해당 프로퍼티의 configurable 속성(변경 및 삭제 가능성)을 false로 정의하는것이다.

## 2) **메서드로서 호출할 때 그 메서드 내부에서의 this**

### **함수 vs 메서드**

- **함수**로서 호출하는 경우
- **메서드**로서 호출하는 경우

→ **함수의 호출**과 **메서드의 호출** **차이**는 **독립성**에 있다.

- 함수 : 그 자체로 독립적인 기능을 수행함
- 메서드 : 자신을 호출한 대상 객체에 관한 동작을 수행함

함수로서 호출 예시 )

```
function b() {
    function c() {
        console.log(this)
    }
    c();
}
b();

결과
Window {…}
```

- b() 호출하면 전역 객체인 window출력 됨
    - 또한, c()를 호출하면 window 객체가 출력됨
- 이에 함수로서 호출했을때는 this는 전역객체를 가리킨다라고 암기해야함

함수로서 호출, 메서드로서 호출)

```
var func = function (x) {
	console.log(this, x);
};
func(1); // window { ... } 1

var obj = {
	method: func
};
obj.method(2); // { method: f } 2
obj['method'](2); // { method: f } 2
```

- 점 표기법이든 대괄호 표기법이든, 어떤 함수를 호출할 때 그 함수 이름(프로퍼티명) 앞에 **객체가 명시돼 있는 경우**에는 **메서드로 호출한 것**이고,
- 그렇지 않은 모든 경우에는 **함수로 호출한 것**이다.

### 메서드 내부에서의 this

- 메서드 내부에서의 this에는 **호출한 주체**에 대한 정보가 담긴다.
- **호출 주체**는 함수명(프로퍼티명) 앞의 객체이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/4e604554-835e-4fbf-bdc5-c6f810485fd4/Untitled.png)

- 위 사진에서 a.b()에서 a는 this, b()는 메서드이다.
- 또한, a.b.c()는 a.b가 this 이고, c()가 메서드이다.

객체.메서드() ,대괄호 표기법 예시)

```
var obj = {
    methodA : function () {console.log(this);},
    inner : {
        methodB: function () { console.log(this); }
    }
}
obj.methodA();// {inner: {…}, methodA: ƒ}
obj['methodA'](); // {inner: {…}, methodA: ƒ}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/58f0461b-c18b-4fab-8b84-16971c0654f1/Untitled.png)

- .은 대괄호 표기법으로 표현할 수 있다.
- person[’info’] 가 this이고, [’getName’]();가 메서드명이다.

## 3) 함수로서 호출할 때 그 함수 내부에서의 this

### **함수 내부에서의 this**

- 어떤 함수를 함수로서 호출할 경우에는 this가 지정되지 않기 때문에 **this는 전역 객체**를 바라본다.
- 즉, **함수로서의 호출한 경우 전역객체를 바로봄**

### **메서드의 내부 함수에서의 this**

내부함수에서의 this)

```
var obj1 = {
	outer: function() {
		console.log(this); // obj1 {outer: ƒ}
		var innerFunc = function (){
			console.log(this); // Window {…}
		}
		innerFunc(); // 함수로서 호출

		var obj2 = {
			innerMethod: innerFunc // obj2 {innerMethod: ƒ}
		};
		obj2.innerMethod(); // 메서드로서 호출
	}
};
obj1.outer(); // 메서드로서 호출
```

### **메서드의 내부 함수에서의 this를 우회하는 방법**

- 우회를 하면 this에 대한 구분은 명확히 할 수 있다.

내부 함수에서의 this를 우회하는 방법- self 이용함)

```
var obj = {
	outer: function() {
		console.log(this);  // {outer: ƒ}
		var innerFunc1 = function (){
			console.log(this); // Window {...}
		}
	};
	innerFunc1();

	var self = this;
	var innerFunc2 = function() {
		console.log(self); // {outer: ƒ}
	};
};
obj.outer();
```

- 위는 변수를 활용하는 방법이다.
- self는 상위 스코프의 this를 저장해서 내부함수에서 활용하려는 수단이다.

→ 변수명은 무엇으로 정해도 무관.

### this를 바인딩하지 않는 함수

- this를 바인딩 하지 않는 **화살표 함수**(arrow function)이다.
    
    ```
    var obj = {
    	outer: function() {
    			console.log(this);  // {outer: ƒ}
    			var innerFunc = () => {
    						console.log(this); // {outer: ƒ}
    			};
    			innerFunc();
    		}
    };
    obj.outer();
    ```
    
- 그 밖에도 **call, apply 등의 메서드를 활용**해 함수를 호출할 때 명시적으로 this를 지정하는 방법이 있다.

<aside>
💡 메서드 내부함수에서 this를 호출하면 전역객체를 가리킨다. 이것을 조작(우회)하기 위해서 self, ES5(apply, call), ES6의 화살표 함수를 사용함

</aside>

## 4) 콜백 함수 호출 시 그 함수 내부에서의 this

**콜백 함수** : 함수 A의 제어권을 다른 함수(또는 메서드) B에게 넘겨주는 경우 함수 A를 **콜백 함수**라고 한다.

- 이때 함수 A는 함수 B의 내부 로직에 따라 실행되며, this 역시 함수 B 내부로직에서 정한 규칙에 따라 값이 결정된다.

```jsx
setTimeout(function () {
	console.log(this); 
}, 300)
```

- setTimeout함수는 300ms 만큼 시간 지연을한 뒤 **콜백 함수**를 실행하라는 명령이다. 0.3초 뒤 전역객체가 출력됨

```
[1,2,3,4,5].forEach(function (x) {
    console.log(this, x); 
});
// window 1
// window 2 
....
// window 5
```

- forEach 메서드는 배열의 각 요소를 앞에서부터 차례로 하나씩 꺼내어 그 값을 콜백 함수의 첫 번째 인자로 삼아 함수를 실행하는 명령이다. 전역객체와 배열의 각 요소가 총 5회 출력된다.

## 5) 생성자 함수 내부에서의 this(new 연산자 사용함)

- 생성자 함수 : 어떤 공통된 성질을 지니는 객체들을 생성하는 데 사용하는 함수이다.
- 프로그래밍적으로 ‘생성자’는 구체적인 인스턴스를 만들기 위한 일종의 틀이다.
- new 명령어와 함께 함수를 호출하면 해당 함수가 생성자로서 동작하게 된다.

생성자 함수)

```
var Cat = function (name, age) {
	this.bark = '야옹'
	this.name = name;
	this.age = age;
};

var choco = new Cat("초코", 7);
var nabi = new Cat("나비", 5);
console.log(choco, nabi); 

// Cat {bark: '야옹', name: '초코', age: 7}
// Cat {bark: '야옹', name: '나비', age: 5}
```

생성함수 호출 시(new 연산자 사용) 예시)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/f72ab282-9f71-4761-8ac3-124809b14cc8/Untitled.png)

---

# 명시적으로 this를 바인딩 하는 방법

## **call 메서드**

```
Function.prototype.call(thisArg[, arg1[, arg2[, ...]]])
```

- 메서드의 호출 주체인 함수를 즉시 실행하도록 하는 명령이다.
    - call 메서드의 **첫 번째 인자를 this로 바인딩**하고, **이후의 인자들을 호출할 함수의 매개변수**로 한다.

call 메서드(1) )

```
var func = function (a, b, c) {
	console.log(this, a ,b ,c);
};
func(1, 2, 3); // window{ ... } 1 2 3
func.call({x: 1}, 4, 5, 6); // {x: 1} 4 5 6
```

call 메서드(2) )

```
var obj = {
	a: 1,
	method: function (x, y) {
		console.log(this.a, x, y);
	}
};
obj.method(2, 3); // 1 2 3
obj.method.call({ a: 4 }, 5, 6); // 4 5 6
```

## apply 메서드

```
Function.prototype.apply(thisArg[, argsArray])
```

- apply 메서드는 call 메서드와 기능적으로 완전히 동일함
- apply 메서드는 두 번째 인자를 배열로 받아 그 배열의 요소들을 호출할 함수의 매개변수로 지정함

apply 메서드)

```
var func = function (a, b, c) {
	console.log(this, a ,b ,c);
};
func.apply({x: 1}, [4, 5, 6]); // { x: 1 } 4 5 6

var obj = {
	a: 1,
	method: function (x, y) {
		console.log(this.a, x, y);
	}
};
obj.method.apply({ a: 4 }, [5, 6]); // 4 5 6
```

## call / apply 메서드의 활용

### 유사 배열 객체에 배열 메서드를 적용

- 객체에는 배열 메서드를 직접 적용할 수 없다.
- 유사 배열 객체 : “**키가 0 또는 양의 정수인 프로퍼티**가 존재하고 length **프로퍼티의 값이 0 또는 양의 정수**인 객체”인 유사 배열 객체의 경우 call 또는 apply 메서드를 이용해 배열 메서드를 차용(빌리다)할 수 있다.
    
    ```
    var obj = {
    0: 'a',
    1: 'b',
    2 : 'c',
    length : 3
    
    }
    Array.prototype.push.call(obj, 'd');
    console.log(obj); // {0: 'a', 1: 'b', 2: 'c', 3: 'd', length: 4}
    
    var arr = Array.prototype.slice.call(obj);
    console.log(arr); // ['a', 'b', 'c', 'd']
    ```
    
- 배열 메서드인 push를 객체 obj에 적용해 프로퍼티 3에 ‘d’를 추가함
- slice 메서드를 적용해 객체를 배열로 전환하고, call 메서드를 이용하여 원본인 유사 배열 객체의 얕은 복사를 수행한 것이다.

### Array.from 메서드

- 유사 배열 객체 또는 순회 가능한 모든 종류의 데이터 타입을 배열로 전환하는 Array.from 메서드이다.

```
var obj = {
	0: 'a',
	1: 'b',
	2: 'c',
	length: 3
};
var arr = Array.from(obj);
console.log(arr);  // ['a', 'b', 'c']
```

### 생성자 내부에서 다른 생성자를 호출

- 생성자 내부에 다른 생성자와 공통된 내용이 있을 경우 call 또는 apply를 이용해 다른 생성자를 호출하면 간단하게 반복을 줄일 수 있다.

call/apply 메서드의 활용 - 생성자 내부에서 다른 생성자를 호출)

```
function Person(name, gender) {
	this.name = name;
	this.gender = gender;
}

function Student(name, gender, school) {
	Person.call(this, name, gender);
	this.school = school;
}
function Employee(name, gender, company) {
	Person.apply(this, [name, gender]);
	this.company = company;
}
var by = new Student('보영', 'female', '단국대');
var jn = new Employee('재난', 'male', '구골');
```

- Employee, Student 객체 생성자 함수 내부에서 Person 객체 생성자 함수를 호출해서 인스턴스의 속송을 정의하여 반복을 줄였다.

### 여러 인수를 묶어 하나의 배열로 전달하고 싶을때 - apply 활용

- 여러 개의 인수를 받는 메서드에게 하나의 배열로 인수들을 전달하고 싶을 때 apply 메서드를 사용하는 것이 좋다.

call/apply 메서드의 활용 - 최대/최솟값을 구하는 코드 ) 

```
var number = [10,21,3,15,44];
var max = Math.max.apply(null, numbers);
var min = Math.min.apply(null, numbers);
console.log(max, min) // 43 3
```

### 스프레드 연산자

call/apply 메서드의 활용2 - ES6의 스프레드 연산자 활용

- 스프레드 연산자를 이용하면 apply를 적용하는 것보다 더욱 간편하게 작성할 수 있다.

```
const numbers = [10,21,3,15,44];
const max = Math.max(...numbers);
const min = Math.min(...nubmers);
console.log(max, min) // 44 3
```

## bind 메서드

```
Function.prototype.bind(thisArg[, arg1, [arg2[, ...]])
```

- bind 메서드 : call과 비슷하지만 즉시 호출하지는 않고 넘겨 받은 this 및 인수들을 바탕으로 새로운 함수를 반환하기만 하는 메서드이다.
- bind 메서드는 두가지 목적으로 나뉜다.
    - 함수에 this를 미리 적용하는 것
    - 부분 적용 함수를 구현하는 것

bind 메서드 - this 지정과 부분 적용 함수 구현 )

```
var func = function (a, b, c, d){
	console.log(this, a, b, c,d);
};
func(1, 2, 3, 4);  // window{ ... } 1 2 3 4

var bindFunc1 = func.bind({x: 1});
bindFunc1(5, 6, 7, 8);  // { x: 1 } 5 6 7 8

var bindFunc2 = func.bind({ x: 1 }, 4, 5);
bindFunc2(6, 7);  // { x: 1 } 4 5 6 7
bindFunc2(8, 9);  // { x: 1 } 4 5 8 9
```

### name 프로퍼티

- bind 메서드를 적용해서 새로 만든 함수는 한 가지 독특한 성질을 가진다.

bind 메서드 - name 프로퍼티 )

```
var func = function (a, b, c, d){
	console.log(this, a, b, c,d);
};
var bindFunc = func.bind({ x: 1 }, 4, 5);
console.log(func.name);  // func
console.log(bindFunc.name);  // bound func
```

- 어떤 함수의 name 프로퍼티가 ‘bound xxx;라면 이는 곧 함수명이 xxx인 원본 함수에 bind 메서드를 적용한 새로운 함수라는 의미이다.
- 기존의 call 이나 apply 보다 코드를 추적하기에 더 수월해진다.

# 정리

명시적 this 바인딩 없을 때

- 전역공간에서의 this는 전역객체(브라우저에서는 window)를 참조한다.
- 어떤 함수를 메서드로서 호출한 경우 this는 메서드 호출 주체(메서드명 앞의 객체)를 참조한다.
- 어떤 함수를 함수로서 호출한 경우 this는 전역객체를 참조한다. 메서드의 내부함수에서도 전역객체를 참조한다.
- 생성자 함수에서의 this는 생성될 인스턴스를 참조한다.

다음은 명시적 this 바인딩이다.

- call, apply 메서드는 this를 명시적으로 지정하면서 함수 또는 메서드를 호출한다.
- bind 메서드는 this 및 함수에 넘길 인수를 일부 지정해서 새로운 함수를 만든다.

---

# 참고

정재남, 코어 자바스크립