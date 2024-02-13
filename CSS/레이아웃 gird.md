# grid 레이아웃

## grid 레이아웃이란?

Flex와 Grid는 현대 웹 레이아웃의 양대산맥이며, 서로 다른 특징을 가지고 있다.

<br>

## flex vs grid

flex는 **`1차원적인 구조`** 를 가지고 있다. row 혹은 column 중 택1 하여 배치 방향을 결정할 수 있다.

반면 grid는 **`2차원적인 구조`** 를 가지고 있다. row와 column 방향의 배치 방식을 동시에 설정할 수 있다.

<br>

## flex와 grid의 차이점

**flex**

- 비교적 작은 단위의 레이아웃 구성에 적합함
- 작업 유동성이 높기 때문에, 디자인이나 기획이 확실하게 잡히지 않아 변경 가능성이 있는 경우에 적합함

**Grid**

- 큰 규모의 레이아웃 구성에 적합함
- 레이아웃 구조가 확실하게 잡혀있는 경우, 효율적으로 반응형 디자인을 구현할 수 있다.
- 단 그리드는 상대적으로 최신 기술이기 때문에 모든 브라우저에서 지원하지 않는다.

<br>

## grid 속성

display: grid를 이용해 grid가 적용된 요소는 다음과 같은 구조로 변경됨.

```
# 그리드 컨테이너(Container)를 정의
display

# grid가 적용된 요소
grid-container

# grid가 적용된 요소의 자식 요소들
grid-item

# grid-item 사이의 경계를 의미합니다.
grid-line

# 해당 grid-line이 몇번째 line인지를 의미합니다.
grid-number
```

```
# 그리드 아이템(Item)의 행 시작 위치 지정
grid-row-start

# 그리드 아이템의 행 끝 위치 지정
grid-row-end

# grid-row-xxx의 단축 속성(행 시작/끝 위치)
grid-row

# 그리드 아이템의 열 시작 위치 지정
grid-column-start

# 그리드 아이템의 열 끝 위치 지정
grid-column-end

# grid-column-xxx의 단축 속성(열 시작/끝 위치)
grid-column

# 영역(Area) 이름을 설정하거나, grid-row와 grid-column의 단축 속성
grid-area
```

<br>

## gird-template

grid의 행&열의 개수 및 크기를 지정할 수 있다.

```
#	영역(Area) 이름을 참조해 템플릿 생성
grid-template-areas

# 명시적 행(Track)의 크기를 정의
grid-template-rows : 1fr 2fr 200px

# columns는 열의 템플릿 지정함
grid-template-columns : 1fr 2fr 200px
```

<br>

### 단위: fr

이 때 사용되는 **`fr`** 이란 **fraction(분수)의 약자임**
분수라는 이름의 뜻으로 유추할 수 있듯 **grid-template에서 사용할 수 있는 비율 단위이다.**

https://dingco.s3.ap-northeast-2.amazonaws.com/2022-08-05/c28bce52-2675-4624-94b4-659609112b53/origin/f0e41b50-a1a0-4c17-9269-fecce9cb9dd1

<br>

### repeat()

grid-template에는 **`repeat()`** 이라는 반복 함수도 써줄 수 있습니다.

repeat(a, b)라고 입력하면, **b규격의 grid-template을 a개 생성한다**는 의미가 됩니다.

```
grid-template-columns: repeat(4, 1fr);
grid-template-columns: 1fr 1fr 1fr 1fr;
```

<br>

## grid-column & grid-row

**`grid-column`** 과 **`grid-row`** 는 grid-item에 줄 수 있는 속성임
각각의 **grid-item이 열과 행 방향으로 얼마만큼의 영역을 차지할 지 정의함.**
이 때, 그 값에는 시작점이 되는 grid-number와 종료지점이 되는 grid-number를 입력할 수 있다.

```
grid-column: 1 / 4;
grid-row: 2 / 3;
```
