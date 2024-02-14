# 레이아웃 (float&flex)

## css 레이아웃이란

css를 이용해서 단순한 문서 형태인 HTML을 보기 좋게 배치하고 재배열 하는 것이고, 관련 기능, 완성된 배열 등을 포괄적으로 지칭함

## 기본 선택자

기본 선택자 이외에 `전체 선택자`, `그룹선택자`, `가상 클래스 선택자`가 있다.

### 전체 선택자

```jsx
* {
   property : property value
}
```

### 그룹 선택자

그룹 선택자는 `여러 선택자를 그룹으로 묶는 기능`이다.

보통 그룹 선택자는 중복된 속성을 여러번 반복해서 줄 경우, 선택자를 묶어서 한번에 처리함으로써 코드를 줄여주는 역할을 합니다.

```jsx
/* 동일한 속성을 반복적으로 사용 */
h2 {
	color : blue;
}
p {
	color : blue;
}
div {
	color : blue;
}
```

```jsx
/* 그룹 선택자를 이용해서 한번에 처리 */
h2, p, div {
	color : blue
}
```

### 가상 클래스 선택자

선택자 뒤에 `:가상 이벤트` 를 붙이면 특정 이벤트마다 적용 할 스타일을 설정 할 수 있으며, 이를 `가상 클래스`라 합니다.

가상 클래스 선택자의 종류는 많지만, 오늘은 그 중 사용 빈도가 높은 아래 4개를 먼저 배우고 나머지는 이후에 차차 더 알아보도록 하겠습니다.

```jsx
# 첫번째 자식
first-child

# 마지막 자식
last-child

# 홀수번째 자식
nth-child(n)

# 마우스를 요소에 올렸을 때
hover
```

<br>

**가상클래스 선택자 사용방법**

가상 클래스는 선택자 뒤에 콜론을 찍은 후 적어주시면 됩니다.

`선택자:가상클래스{ 속성 : 속성값 }` 이런식으로 적어주시면 되며, 아래 예시를 통해 조금 더 자세히 알아보도록 하겠습니다.

```jsx
.some-box:hover{ background-color: red; }
.container-boxs:first-child{ margin-left: 0; }
.container-boxs:last-child{ margin-right: 0; }
.contentsBox:nth-child(n){ color: red; }
```

<br>

## **float 레이아웃**

전통적으로 레이아웃을 구성할때 사용하던 방법입니다.

하지만 float 레이아웃은 PC로만 인터넷에 접속할 수 있던 시절에 고안되었기 때문에,
반응형 웹에는 적합하지 않습니다.

> ❗️ **반응형 웹이란?**
> 모바일, 태블릿, 데스크탑 PC 등 **접속하는 기기의 너비에 맞추어** 레이아웃이 변하는 웹페이지

### float

HTML 요소를 일반적인 흐름(normal flow)으로부터 벗어나서 특정한 컨테이너의 좌측 혹은 우측을 감싸는 형태로 강제 배치할 수 있도록 도와주는 속성입니다.

- **float: none (기본값)**
- **float: left**
- **float: right**

### clear

float가 적용된 요소에 추가로 줄 수 있는 속성으로, float의 영향력을 해당 요소에 한해 해제합니다.

- **clear: none (기본값)**
- **clear: left**
- **clear: right**
- **clear: both**

<br>

## flex 레이아웃

**flex는 레이아웃 배치 전용 기능**으로 고안되었기 때문에 float에 비해 **훨씬 편리**합니다.
그렇기 때문에 flex가 등장한 이후부터 레이아웃에 있어서 float는 찬밥신세가 되었다고 볼 수 있습니다.

자, 이제 flex를 사용해볼까요?

Flex 레이아웃을 만들기 위한 기본적인 HTML 구조는 다음과 같습니다.

```jsx
<div class="container">
  <div class="item">박스1</div>
  <div class="item">박스2</div>
  <div class="item">박스3</div>
</div>
```

위의 코드에서 부모요소는 **container**, 자식요소는 **item** 입니다.

우리는 이제부터 부모요소를 **`Flex Container`** , 자식요소를 **`Flex item`** 이라고 부르겠습니다.

컨테이너는 Flex의 영향을 받는 전체 공간이고, 이 공간 내에 아이템들이 배치된다고 보시면 됩니다.

<br>

### flex의 속성

flex에 적용할 수 있는 속성은 크게 두개로 나뉩니다.

- **컨테이너에 적용**하는 속성
- **아이템에 적용**하는 속성

### 컨테이너에 적용하는 속성들

**display : flex**

**flex-direction (배치 방향 설정)**

- **`row`** (행) : 중심축을 가로 방향으로 배치합니다.
- **`column`** (열) : 중심축을 세로 방향으로 배치합니다.

```jsx
# 요소들을 텍스트의 방향과 동일하게 정렬합니다.
flex-direction: row

# 요소들을 텍스트의 반대 방향으로 정렬합니다.
flex-direction: row-reverse;

# 요소들을 위에서 아래로 정렬합니다.
flex-direction: column

# 요소들을 아래에서 위로 정렬합니다.
flex-direction: column-reverse
```

<br>

**justify-content (메인축 방향 정렬)**

- 메인축은 flex-direction방향과 동일합니다.
- 메인축 방향으로 어떻게 정렬할지 결정합니다

```jsx
# 요소들을 컨테이너의 왼쪽으로 정렬합니다.
justify-content: flex-start

# 요소들을 컨테이너의 오른쪽으로 정렬합니다.
justify-content: flex-end

# 요소들을 컨테이너의 가운데로 정렬합니다.
justify-content: center

# 요소들 사이에 동일한 간격을 둡니다.
justify-content: space-between

# 요소들 주위에 동일한 간격을 둡니다.
justify-content: space-around
```

<br>

**align-items (교차축 방향 정렬)**

- 교차축 방향, 즉 메인축의 수직 방향으로 어떻게 정렬할지 결정합니다.

```jsx
# 요소들을 컨테이너의 꼭대기로 정렬합니다.
align-items: flex-start;

# 요소들을 컨테이너의 바닥으로 정렬합니다.
align-items: flex-end

# 요소들을 컨테이너의 세로선 상의 가운데로 정렬합니다.
align-items: center

# 요소들을 컨테이너의 시작 위치에 정렬합니다.
align-items: baseline

# 요소들을 컨테이너에 맞도록 늘립니다.
align-items: stretch

```

align-self는 개별 요소에 적용할 수 있는 또 다른 속성임. 이 속성은 **`align-items`**가 사용하는 값들을 인자로 받으며, 그 값들은 지정한 요소에만 적용됩니다.

```jsx
# 요소들을 컨테이너의 꼭대기로 정렬합니다.
align-self: flex-start;

# 요소들을 컨테이너의 바닥으로 정렬합니다.
align-self: flex-end

# 요소들을 컨테이너의 세로선 상의 가운데로 정렬합니다.
align-self: center

# 요소들을 컨테이너의 시작 위치에 정렬합니다.
align-self: baseline

# 요소들을 컨테이너에 맞도록 늘립니다.
align-self: stretch

```

<br>

align-content : 여러 줄 사이의 간격을 지정함

```jsx
# 여러 줄들을 컨테이너의 꼭대기에 정렬합니다.
align-content: flex-start

# 여러 줄들을 컨테이너의 바닥에 정렬합니다.
align-content: flex-end

# 여러 줄들을 세로선 상의 가운데에 정렬합니다.
align-content: center

# 여러 줄들 사이에 동일한 간격을 둡니다.
align-content: space-between

# 여러 줄들 주위에 동일한 간격을 둡니다.
align-content: space-around

# 여러 줄들을 컨테이너에 맞도록 늘립니다.
align-content: stretch
```

<br>

flex-wrap : 요소들을 정렬하는 기능

```jsx
# 요소들을 여러 줄에 걸쳐 정렬합니다.
flex-wrap : wrap

# 모든 요소들을 한 줄에 정렬합니다.
flex-wrap : nowrap

# 요소들을 여러 줄에 걸쳐 반대로 정렬합니다.
flex-wrap : wrap-reverse
```

<br>

flex-flow → flex-direction && flex-wrap

```jsx
# 요소들을 가로선 상의 여러줄에 걸쳐 정렬하기 위해
flex-flow: row wrap

flex-flow: row-reverse nowrap;

flex-flow: column wrap-reverse;

flex-flow: column wrap;
```
