# interface와 type차이점

```jsx
interface PeopleInterface {
  name: string
  age: number
}

const me1: PeopleInterface = {
  name: 'yc',
  age: 34,
}

type PeopleType = {
  name: string
  age: number
}

const me2: PeopleType = {
  name: 'yc',
  age: 31,
}
```

- `interface`는 `type`과 마찬가지로 객체의 타입의 이름을 지정한다.

### `interface`와`type`차이점

1. 확장하는 방법
2. 선언적 확장
3. **interface는 객체에만 정의가 가능하고, type은 객체 뿐만 아니라 다양한 형태의 타입을 정의**할 수 있다.
4. computed value 사용 여부

### 1. 확장하는 방법

```jsx
interface PeopleInterface {
  name: string
  age: number
}

interface StudentInterface extends PeopleInterface {
  school: string
}

interface TestInterface extends PeopleInterface {
	dd : boolean
}

type PeopleType = {
  name: string
  age: number
}

type StudentType = PeopleType & {
  school: string
}
```

- 확장하는 방법에 차이점이 있다.

### 2. 선언적 확장

```jsx
interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}
// 같은 interface 명으로 Window를 다시 만든다면, 자동으로 확장이 된다.
const src = 'const a = "Hello World"'
window.ts.transpileModule(src, {})

---

type Window = {
  title: string
}

type Window = {
  ts: TypeScriptAPI
}

// Error: Duplicate identifier 'Window'.
// 타입은 안된다.
```

- `interface`에서 할 수 있는 대부분의 기능들은 `type`에서 가능하다. 하지만 `type`은 새로운 속성을 추가하기 위해서 다시 같은 이름으로 선언할 수 없지만, `interface`는 항상 선언적 확장이 가능하다는 것이다.

### 3. **interface는 객체에만 정의가 가능하고, type은 객체 뿐만 아니라 다양한 형태의 타입을 정의**할 수 있다.

```jsx
// PersonInterface 인터페이스 정의
interface PersonInterface {
  name: string;
  age: number;
  email?: string; // 선택적 속성
}

// PersonType 타입 정의
type PersonType = {
  name: string,
  age: number,
  email?: string, // 선택적 속성
};

// PersonInterface를 따르는 객체 생성
let person1: PersonInterface = {
  name: "John",
  age: 30,
  email: "john@example.com",
};

// PersonType을 따르는 객체 생성
let person2: PersonType = {
  name: "Alice",
  age: 25,
};

// 함수 매개변수로 인터페이스와 타입 활용
function greetInterface(person: PersonInterface) {
  console.log(`Hello, ${person.name}!`);
}

function greetType(person: PersonType) {
  console.log(`Hello, ${person.name}!`);
}

// greet 함수 호출
greetInterface(person1); // 출력: Hello, John!
greetType(person2); // 출력: Hello, Alice!
```

- `type`은 객체 뿐만 아니라 다양한 형태의 타입을 정의할 수 있다. 이를 예를 들면, 원시 타입(primitive types)이나 유니온 타입(union types), 튜플 타입(tuple types), 함수 타입(function types) 등을 정의할 때 사용할 수 있다.
  **1) 원시 타입 (Primitive Types):**
  ```tsx
  type ID = number;
  type Username = string;
  type Status = "active" | "inactive";
  ```
  **2) 유니온 타입 (Union Types):**
  ```tsx
  type Result = string | number;
  type Option = "yes" | "no" | "maybe";
  ```
  **3) 튜플 타입 (Tuple Types):**
  ```tsx
  type Coordinate = [number, number];
  let point: Coordinate = [10, 20];
  ```
  **4) 함수 타입 (Function Types):**
  ```tsx
  type AddFunc = (x: number, y: number) => number;
  let add: AddFunc = (a, b) => a + b;
  ```

### 4. **computed value의 사용 여부**

- `type`은 **computed value의 사용**이 가능하지만, `interface`는 불가능하다

```tsx
type names = "firstName" | "lastName";

type NameTypes = {
  [key in names]: string;
};

const yc: NameTypes = { firstName: "hi", lastName: "yc" };
```

- `type`인 `NameTypes`는 `names` 타입에 대해 computed property를 사용하여 `firstName`과 `lastName`라는 속성을 갖는 객체를 정의한다. `names`에 정의된 각 문자열에 대해 동적으로 속성을 만들어낸다.

```tsx
interface NameInterface {
  // 오류 발생
  [key in names]: string;
}
```

- 반면에 `interface`인 `NameInterface`에서는 동일한 방식으로 computed property를 사용할 수 없다. TypeScript는 interface에서 computed property를 사용하는 것을 허용하지 않는다.

※ "computed property"는 객체의 속성명을 동적으로 생성하는 것을 의미하고, "computed value"는 동적으로 계산된 값을 의미한다.

## 결론

프로젝트 전반에서 type을 쓸지 interface를 쓸지 통일이 필요하다. 그러나 객체, 타입간의 합성(TypeScript에서 두 개 이상의 타입을 조합하여 새로운 타입을 만드는 것)등을 고려해 보았을 때 interface를 쓰는 것이 더 나을 수 있다.

※ interface 확장 예시

```jsx
// 공통된 속성을 포함하는 Animal 인터페이스 정의
interface Animal {
  name: string;
  age: number;
}

// Animal을 확장하여 Mammal 인터페이스 정의
interface Mammal extends Animal {
  furColor: string;
}

// Animal을 확장하여 Bird 인터페이스 정의
interface Bird extends Animal {
  wingspan: number;
}

// 객체 생성 예시
const dog: Mammal = {
  name: "Max",
  age: 5,
  furColor: "brown",
};

const sparrow: Bird = {
  name: "Sparrow",
  age: 2,
  wingspan: 20,
};
```
