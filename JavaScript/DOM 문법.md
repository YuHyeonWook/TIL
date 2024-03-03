# DOM(Document Object Model)문법

# DOM

- HTML문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 **프로퍼티와 메서드를 제공하는 트리 자료구조**이다. \*\*\*\*혹은 HTML을 JS로 조작할 수 있다.

## **브라우저 DOM 종류**

- 브라우저는 HTML 문서를 로드한 후, 해당 문서에 대한 모델을 메모리에 생성한다.
  이때 모델은 객체의 트리로 구성되는데, 이것을 DOM tree라 한다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/71c49c14-5a59-41db-93d8-2682c92ae64c)

### **문서 노드(Document Node)**

- 트리의 최상위에 존재하며 각각 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다.즉, **DOM tree에 접근하기 위한 시작점**(entry point)이다.

### **요소 노드(Element Node)**

- 요소 노드는 HTML 엘리먼트를 표현한다. 어트리뷰트, 텍스트 노드에 접근하려면 먼저 요소 노드를 찾아 접근해야 한다. 모든 요소 노드는 요소별 특성을 표현하기 위해 HTMLElement 객체를 상속한 객체로 구성된다.
- html 태그 id 값을 가져온다.

```jsx
document.getElementById(id); // -> id 어트리뷰트 값으로 요소 노드를 한 개 선택
```

### **어트리뷰트 노드(Attribute Node)**

- 어트리뷰트 노드는 HTML 요소의 어트리뷰트를 표현한다. 어트리뷰트 노드는 해당 어트리뷰트가 지정된 요소의 자식이 아니라 해당 요소의 일부로 표현된다. 따라서 해당 요소 노드를 찾아 접근하면 어트리뷰트를 참조, 수정할 수 있다.

```jsx
document.querySelector("h1").id = "heading"; // -> id 어트리뷰트의 값을 변경
```

### **텍스트 노드(Text Node)**

- 텍스트 노드는 HTML 요소의 텍스트를 표현한다. 텍스트 노드는 요소 노드의 자식이며 자신의 자식 노드를 가질 수 없다. 즉, 텍스트 노드는 DOM tree의 최종 하단이다. 요소의 텍스트는 텍스트 노드에 저장되어 있다.

> <> ~ </> 꺽쇠 한쌍이 노드 객체 한 개이다.

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/3da583a8-7d35-445a-babd-fc593ad9b507)

## **자바스크립트 브라우저 DOM 문법**

### **DOM 요소 선택**

- document.getElementById("id명") : 해당 id명을 가진 요소 하나를 반환한다.
- document.querySelector("선택자"): 해당 선택자를 만족하는 요소 하나를 반환
- document.getElementsByClassName("class명")[순서]: 해당 class명을 가진 모든 요소들을 배열에 담아 인덱스에 맞는 요소를 반환
- document.getElementsByTagName("태그명")[순서]: **해당 태그명**을 가진모든 요소들을 배열에 담아 인덱스에 맞는 요소를 반환
- document.querySelectorAll("선택자명")[순서]: 해당 선택자를 만족하는**모든 요소들**을 배열에 인덱스에 맞는 요소를 반환

```jsx
const selectedItem = document.getElementsByTagName("li"); // 모든 <li> 요소를 선택함.

for (let i = 0; i < selectedItem.length; i++) {
  console.log(selectedItem[i]); // 태그 배열들을 순회함
}
```

```jsx
document.getElementById("idname"); // id값 가져옴
document.getElementsByClassName("classname")[0]; // 선택된 요소중 첫번째 요소 => 인덱스 0
document.getElementsByTagName("button")[0];

// <div>태그들을 모두 가져오고 그중 첫번째 div태그에서, 클래스가 button인것들중에 첫번째 선택
document.getElementsByClassName("div")[0].getElementsByClassName("button")[0];

document.querySelector("#idname"); // 선택쿼리문 선택
document.querySelector("#idname, .classname"); // 여러 속성 선택 가능 !!
document.querySelectorAll(".classname")[0];
```

```jsx
<div id="login-form">
  <input type="text" placeholder="what is your name?" />
  <button>Log In</button>
</div>;

const $loginForm = document.querySelector("#login-form");
const $loginInput = $loginForm.querySelector("input");
const $loginButton = $loginForm.querySelector("button");
console.log($loginButton); // button
```

### **요소 배열 순회**

- getElementsByClassName 메소드의 반환값은 HTMLCollection이다.

```jsx
const elems = document.getElementsByClassName("red");

// 유사 배열 객체인 HTMLCollection을 배열로 복사&변환한다.
// 배열로 변환된 HTMLCollection은 더 이상 live하지 않다.
// 배열값들을 복사를 해도, dom에 레퍼런스로 연결되어있기 때문에 문제없다.
console.log([...elems]); // [li#one.red, li#two.red, li#three.red]

[...elems].forEach((elem) => (elem.className = "blue"));
```

- HTMLCollection으로 반환된 리스트는 실시간 유사배열이다. 실시간으로 Node의 상태 변경을 반영하기 때문에 loop가 필요한 경우 주의가 필요하다. (중간에 배열 값을 떼거나 변경하면 자동으로 인덱스 정렬을 한다.)

### **HTMLCollection vs NodeList**

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/df0312bb-419b-4d73-a33e-352238a596d6)

### **DOM 요소 탐색**

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/01a2e57a-f388-4c78-ba01-7f72a04bed28)

```
parentNode: 부모 노드를 탐색

parentElement: 부모 노드 탐색

childNodes: 하위 모든 노드 객체를 NodeList로 반환

children: 하위 모든 노드 객체를 HTMLCollection으로 반환

firstChild: 직계 자식 객체 중에서 가장 첫번째 노드 객체를 반환

lastChild: 직계 자식 객체 중에서 가장 마지막 노드 객체를 반환

firstElementChild: 직계 자식 객체 중에서 가장 첫번째 노드 객체를 반환

lastElementChild: 직계 자식 객체 중에서 가장 마지막 노드 객체를 반환

hasChildNodes(): 자식 노드 객체의 존재 여부를 boolean으로 반환

children.length: 자식 노드 객체 수 반환

childElementCount: 자식 노드 객체 수 반환

previousSibling: 같은 부모를 가진 노드 객체 중에서 이전 노드 반환

nextSibling: 같은 부모를 가진 노드 객체 중에서 다음 노드 반환

previousElementSibling: 같은 부모를 가진 노드 객체 중에서 이전 노드 반환

nextElementSibling: 같은 부모를 가진 노드 객체 중에서 다음 노드 반환

```

```jsx
<html>
  <head></head>
  <body>
    <ul id="languages">
      <li class="html">HTML</li>
      <li class="css">CSS</li>
      <li class="js">JS</li>
    </ul>
    <script>
      const $el = document.querySelector('.css');
      console.log($el.previousSibling); // 이전 노드 반환
      console.log($el.nextSibling); // 다음 노드 반환
      console.log($el.previousElementSibling); // 이전 노드 반환
      console.log($el.nextElementSibling); // 다음 노드 반환
    </script>
  </body>
</html>
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/4485dc0b-ed60-4bfc-85e6-3efc414ac473)

### **DOM 요소 속성 조정**

- hasAttribute(attribute): 지정한 어트리뷰트를 가지고 있는지 검사한다.
- getAttribute(attribute): 어트리뷰트의 값을 취득한다.
- setAttribute(attribute, value): 어트리뷰트와 어트리뷰트 값을 설정한다.
- removeAttribute(attribute): 지정한 어트리뷰트를 제거한다.
- .attributes: 속성들을 모아서 배열로 반환

```jsx
<!DOCTYPE html>
<html>
  <body>
  <input type="text">
  <script>
     const input = document.querySelector('input[type=text]');
     console.log(input);

     if (!input.hasAttribute('value')) {  // value 어트리뷰트가 존재하지 않으면
       // value 어트리뷰트를 추가하고 값으로 'hello!'를 설정
       input.setAttribute('value', 'hello!');
     }

     // value 어트리뷰트 값을 취득
     console.log(input.getAttribute('value')); // hello!

     // value 어트리뷰트를 제거
     input.removeAttribute('value');

  </script>
  </body>
</html>
```

- element.id: id 어트리뷰트의 값을 취득 또는 변경한다. id 어트리뷰트가 존재하지 않으면 id 어트리뷰트를 생성하고 지정된 값을 설정한다.
- element.style.property: 해당 요소에 적용된 css속성의 값을 나타낸다.
- element.attribute: 해당 요소의 속성을 나타낸다.

```jsx
<form>
  <input type="password" name="input"/>
</form>

input {
  display: block;
  background-color: red;
  width: 200px;
  height: 10px;
}

const input = document.querySelector("input");

input.style.display = "none";
input.style.width = "100px";
input.name = "output";
input.id = "input_id";
input.style['font-size'] = '2rem';

//주의할 점은 css 속성 값을 따옴표로 감싸서 문자열의 형태로 대입해야 된다는 것입니다.
```

### **DOM 클래스 속성 조정**

- element.className: class 어트리뷰트의 값을 취득, 변경한다. class 어트리뷰트가 존재하지 않으면 class 어트리뷰트를 생성하고 지정된 값을 설정한다.
- element.classList: 클래스명으로 css 스타일을 조정하는 경우 classList에서 제공하는 메서드로 클래스명을 간편하게 조정 할 수 있다. add, remove, item, toggle, contains, replace 메소드를 제공한다.

```jsx
<p id="a1"class="document, aa, bb, cc, dd"></p>

<script>
    let a = document.querySelector("#a1");
    console.log(a.className) // "document, aa, bb, cc, dd"

    let arr = a.className.split(", "); // [ 'document', 'aa', 'bb', 'cc', 'dd' ]
</script>
```

```
add(): 클래스 목록에 추가할 문자열을 1개 이상 인수로 전달한다.

remove(): 클래스 목록에서 제거할 문자열을 1개 이상 인수로 전달한다.

item(): 클래스 목록에서, 인수로 전달한 정수 인덱스에 위치한 문자열을 반환한다.

contains(): 인수로 전달한 문자열이 클래스 목록에 존재하는 지 판단하여 boolean을 반환한다.

replace(): 첫번째 인수로 전달한 문자열을 클래스 목록에서 찾은 후, 두번째 인수를 대입한다.

toggle(): 첫번째 인수로 전달한 문자열이 클래스 목록에 있으면 삭제를, 없으면 추가한다.

toggle(true/false): 첫번째 인수가 클래스 목록에 이미 존재하는지 파악하지 않고, true는 첫번째 인수를 클래스 목록에 강제 추가, false는 첫번째 인수를 클래스 목록에서 강제 삭제한다.
```

```jsx
const element = document.createElement("tagName");

const addClass = element.classList.add("className"); // Class 추가
const removeClass = element.classList.remove("className"); // Class 삭제
const toggleClass = element.classList.toggle("className"); // Class 토글
// class가 존재한다면 제거하고 존재하지 않으면 class를 추가한다.
```

### **DOM 노드 조회**

- 노드(Node) : HTML 페이지의 각 요소(html, head, body . . . 등)
- 요소 노드(Element Node) : HTML 태그
- 텍스트 노드(Text Node) : 요소 노드 안에 있는 글자

```
nodeName: 노드의 이름을 나타내는 문자열 반환

nodeValue: 특정 노드에 첫번째 하위 텍스트 노드의 값(텍스트)을 조회/수정한다.

nodeType: 노드 고유의 타입을 조회. 수정X
```

```jsx
<!DOCTYPE html>
<html lang="ko">

<head>
	<meta charset="UTF-8">
	<title>JavaScript Node Access</title>
</head>

<body>
	<h1>nodeName 프로퍼티</h1>
	<p id="document"></p>
	<p id="html"></p>
	<h1 id="heading">nodeValue 프로퍼티</h1>
	<p id="text1">텍스트</p>

	<script>
		// 문서의 첫 번째 자식 노드는 <!DOCTYPE html>이며, 두 번째 자식 노드는 <html>입니다.
		console.log(document.childNodes[1].nodeName)

		// 문서의 두번째 자식노드 html 의 첫 자식은 head 노드.
		console.log(document.childNodes[1].childNodes[0].nodeName)

		// 문서의 두번째 자식노드 html 의 세번째 자식노드 body의 첫 자식노드 h1의 첫 자식 노드 text노드
		console.log(document.childNodes[1].childNodes[2].childNodes[0].nodeName)

		// 아이디가 "heading"인 요소의 첫 번째 자식 노드(텍스트노드)의 노드값을 선택함.
		console.log(document.getElementById("heading").firstChild.nodeValue)
	</script>
</body>

</html>
```

### **DOM 쓰기**

- 요소에 접근하면 요소의 여러 가지 속성에 접근하여 변경할 수 있다.

```
element.innerHTML: 해당 요소의 모든 자식 요소를 포함하는 모든 콘텐츠를 하나의 문자열로 취득할 수 있다. 이 문자열은 마크업을 포함한다.

element.outerHTML: outerHTML에서 지정한 요소 태그도 포함하여 전체 태그 값을 가져오고 선택한 엘리먼트를 포함해서 처리한다.

document.write()
document.writeln()
: 인자로 전달한 내용을 DOM에 그릴 수 있다. ln은 개행문자 포함해서 출력

textContent: 요소의 텍스트 콘텐츠를 취득 또는 변경한다.
이때 마크업은 무시된다.

element.insertAdjacentHTML: innerHTML로 기존 요소를 수정할 때 원본이 불필요하게 지워졌다가 다시 할당되는 것을 방지한다.
```

```jsx
<div id="test">TEST</div>

<script type="text/javascript">
	alert(document.getElementById('test').innerHTML);
	//결과는 TEST

	alert(document.getElementById('test').outerHTML);
	//결과는 <div id="test">TEST</div>

</script>
```

```jsx
const one = document.getElementById("one");

// 마크업이 포함된 콘텐츠 취득
console.log(one.innerHTML); // Seoul

// 마크업이 포함된 콘텐츠 변경
one.innerHTML += '<em class="blue">, Korea</em>';

// 마크업이 포함된 콘텐츠 취득
console.log(one.innerHTML); // Seoul <em class="blue">, Korea</em>
```

### **DOM 추가 / 삭제**

- innerHTML 프로퍼티를 사용하지 않고, 새로운 콘텐츠를 추가할 수 있는 방법은 DOM을 직접 조작하는 것이다.

```
createElement(tagName): 태그이름을 인자로 전달하여요소를 생성한다.

createTextNode(text): 텍스트를 인자로 전달하여 텍스트 노드를 생성한다.

appendChild(Node): 인자로 전달한 노드를 마지막 자식 요소로DOM 트리에 추가한다.

removeChild(Node): 인자로 전달한 노드를DOM 트리에서 제거한다.

replaceChild(after, before): 두번째 인수를 첫번째 인수로 덮어씌우는데, 두번째 인수는 이 메서드를 호출한 노드 객체의 자식 객체여야 한다.

.remove(): 현재 엘리먼트를 삭제. 삭제할 엘리먼트의 참조만 있으면 됨.

insertBefore(newNode, childNode): 첫번째 인수로 전달받은 노드를, 두번째 인수로 전달한 노드의 바로 앞에 삽입한다. 단, 두번째 인수는 이 메서드를 호출한 노드 객체의 자식 노드여야 한다.

cloneNode(): 현재 노드를 복사해 반환합니다. 파라미터로 true/false 를 인자로 보낼 수 있습니다.
true 면 노드가 담고 있는 텍스트 등 안의 태그 내용까지 복사됩니다. false 면 노드 외형만 복사합니다.
```

**HTML 생성**

```jsx
// HTML 도큐먼트 생성
let newdoc = document.implementation.createHTMLDocument("HTML Document");

// div 태그 안에 내용을 만들어 넣음.
let div = newdoc.createElement("div");
div.innerHTML = "<span>HTML 문서 샘플</span>";
newdoc.body.appendChild(div); // 도큐먼트 바디(body)에 자식으로 붙임

//HTML 도큐먼트를 붙여넣을 아이프레임 참조 얻기
targetdoc = document.getElementById("newframe").contentDocument;
// 붙여넣을 새 노드를 복사해옴
let newnode = targetdoc.importNode(newdoc.documentElement, true);
// 아이프레임 도큐먼트를 새 노드로 대체
targetdoc.replaceChild(newnode, targetdoc.documentElement);
```

**엘리먼트 생성**

```jsx
let div = document.createElement("div"); //div 태그 생성
let span = document.createElement("span"); //span 태그 생성
span.textContent = "HTML 문서 샘플"; //span태그 안에 텍스트 넣음

div.appendChild(span); // span태그를 div 자식으로서 상속
document.body.appendChild(div); // div태그를 body 자식으로서 상속 -> 태그 추가
```

**엘리먼트 삭제**

```jsx
document.getElementById("delid").remove(); //선택한 태그 자기자신 삭제

let parent = document.getElementById("parentdiv");
let child = document.getElementById("childspan");
parent.removeChild(child); //부모요소.removeChild(자식요소); 형식으로 부모 안에 있는 자식 삭제
```

**엘리먼트 삽입, 이동**

```jsx
<!DOCTYPE html>
<html>
<head>
  <title>Elemetnt Insert</title>
</head>
<body>
  <ul id="friends">
    <li class="animal">라이언</li>
    <li class="fruit">어피치</li>
    <li class="animal">프로도</li>
    <li class="alien">콘
      <ul class="keyword">
        <li>3세</li>
        <li>숏다리</li>
        <li>초록괴수</li>
      </ul>
    </li>
  </ul>
  <ul class="icons">
    <li>
      <span>스몰</span>
      <span>미디엄</span>
      <span>빅</span>
    </li>
  </ul>
  <ul id="newfriends">
  </ul>
</body>
</html>
```

<br>

# 참고

- https://poiemaweb.com/js-dom
- https://ko.javascript.info/modifying-document
- https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-DOM-%EB%AC%B8%EB%B2%95-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC?category=889100
- https://tcpschool.com/javascript/js_dom_element#google_vignette
