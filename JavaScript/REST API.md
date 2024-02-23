# **REST API**

# **REST API**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/e6567b52-2af6-447a-a30b-4c61b46483b4/Untitled.png)

- REST(Representational State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미함
- 즉, HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미한다.
- CRUD Operation
  - Create : 데이터 생성(POST)
  - Read : 데이터 조회(GET)
  - Update : 데이터 수정(PUT, PATCH)
  - Delete : 데이터 삭제(DELETE)

## **REST 구성 요소**

REST는 다음과 같은 3가지 구성 요소로 이루어져 있다.

1. **자원(Resource) :** 자원은 **URI(Uniform Resource Identifier)**로 표현되며, REST에서는 모든 것이 자원이다. 자원은 단순한 데이터일 수도 있고, 복잡한 데이터 구조일 수도 있다. 예를 들어, 웹 사이트에서 사용자, 게시물, 댓글 등 모든 것이 자원이 될 수 있다.
2. **행위(Verb) :** 자원에 대해 수행할 수 있는 작업을 의미한다. REST에서는 HTTP 메서드를 사용하여 행위를 표현한다. 일반적으로 사용되는 HTTP 메서드는 `GET`, `POST`, `PUT`, `DELETE` 등이 있다. 예를 들어, GET 메서드는 자원을 조회하고, POST 메서드는 자원을 생성하며, PUT 메서드는 자원을 수정하고, DELETE 메서드는 자원을 삭제한다.
3. **표현(Representation) :** 자원에 대한 표현 방법을 의미한다. REST에서는 `XML`, `JSON` 등의 데이터 형식을 사용하여 자원을 표현한다. 클라이언트는 서버에서 전송된 자원의 표현 방식을 해석하여 처리할 수 있다.

## **REST의 특징**

1. **클라이언트-서버(Client-Server) 구조:** REST는 클라이언트와 서버 간의 역할 분리를 지향한다. 클라이언트는 서버에게 요청을 보내고, 서버는 요청에 대한 응답을 제공한다. 이를 통해 시스템의 확장성과 유연성을 높일 수 있다.
2. **상태 없음(Stateless):** REST는 상태를 유지하지 않는 구조를 가진다. 클라이언트와 서버 간의 통신에서 상태를 저장하지 않고, 각각의 요청은 서로 독립적이다. 이를 통해 서버의 부하를 줄이고, 서버의 확장성을 높일 수 있다.
3. **인터페이스 일관성(Interface Uniformity):** REST는 HTTP 프로토콜의 인터페이스 일관성을 따른다. HTTP Method를 사용하여 자원에 대한 CRUD(Create, Read, Update, Delete) 작업을 수행하며, URI를 사용하여 자원을 식별한다. 이를 통해 클라이언트와 서버 간의 인터페이스를 일관성 있게 유지할 수 있다.
4. **캐시 처리 가능(Cacheable):** REST는 HTTP의 캐시 기능을 이용하여 클라이언트에서 서버로부터 전송받은 응답을 캐시할 수 있다. 이를 통해 클라이언트의 요청에 대한 응답 시간을 줄이고, 네트워크 대역폭을 절약할 수 있다.
5. **계층형 구조(Layered System):** REST는 다중 계층으로 구성될 수 있다. 클라이언트는 서버와 직접 통신하지 않고, 중간에 다른 계층(로드 밸런서, 캐시 등)을 거쳐 요청을 전송할 수 있다. 이를 통해 시스템의 확장성과 보안성을 높일 수 있다.

## REST의 장단점

### 장점

- **확장성:** REST는 클라이언트와 서버 간의 역할 분리, 자체 표현 구조, 상태 없음 등의 특징으로 확장성이 높다. 새로운 기능을 추가하거나 시스템을 확장하더라도, 기존의 시스템에 영향을 주지 않다.
- **다양한 클라이언트 지원:** REST는 HTTP 프로토콜을 사용하므로, 웹 브라우저, 모바일 앱 등 다양한 클라이언트에서 사용할 수 있다.
- **캐시 처리 가능:** REST는 HTTP의 캐시 기능을 이용하여 클라이언트에서 서버로부터 전송받은 응답을 캐시할 수 있다. 이를 통해 클라이언트의 요청에 대한 응답 시간을 줄이고, 네트워크 대역폭을 절약할 수 있다.
- **보안성:** REST는 HTTPS와 같은 보안 프로토콜을 사용할 수 있으며, 인증과 권한 부여를 위한 다양한 메커니즘을 제공한다.
- **상호 운용성:** REST는 다른 시스템과의 통합이 용이하며, 다양한 데이터 포맷(JSON, XML 등)을 지원한다.

### 단점

- **업무 로직에 대한 표준이 없음:** REST는 인터페이스 일관성만을 정의하고 있기 때문에, 업무 로직에 대한 표준이 없다. 이로 인해, 각각의 개발자나 조직에서 업무 로직을 자유롭게 정의할 수 있지만, 이는 유지보수나 통합 등의 과정에서 문제를 발생시킬 수 있다.
- **URL 길이 제한:** REST는 URI를 사용하여 자원을 식별하기 때문에, URL의 길이가 제한될 수 있다. 이는 대규모 시스템에서 자원을 식별하기 어려울 수 있다.
- **다양한 클라이언트 지원에 대한 보안 이슈:** REST는 다양한 클라이언트를 지원하기 때문에, 클라이언트 측에서의 보안 이슈가 발생할 수 있다.
- **대규모 시스템에서의 관리 어려움:** REST는 상태를 유지하지 않는 구조이기 때문에, 대규모 시스템에서의 관리가 어려울 수 있다.

---

## **REST API란?**

API(Application Programming Interface)란 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것이다.

REST API란 REST의 원리를 따르는 API를 의미합니다.

### **REST API 설계 예시**

**1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.**

```jsx
Bad Example - http://khj93.com/Running/

Good Example - http://khj93.com/run/
```

**2. 마지막에 슬래시 (/)를 포함하지 않는다.**

```jsx
Bad Example - http://khj93.com/test/ 

Good Example - http://khj93.com/test
```

**3. 언더바 대신 하이폰을 사용한다.**

```jsx
Bad Example - http://khj93.com/test_blog

Good Example - http://khj93.com/test-blog
```

**4. 파일확장자는 URI에 포함하지 않는다.**

```jsx
Bad Example - http://khj93.com/photo.jpg  

Good Example - http://khj93.com/photo
```

**5. 행위를 포함하지 않는다**

```jsx
Bad Example - http://khj93.com/delete-post/1 
 
Good Example - http://khj93.com/post/1
```

---

## **RESTful이란?**

!https://blog.kakaocdn.net/dn/Prbbr/btqUOBFqxzH/zhpIrKuFxPKI9QvRzmiBe1/img.png

RESTful이란 REST의 원리를 따르는 시스템을 의미한다다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아니다.

REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며 모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있다.

# 참고

[https://khj93.tistory.com/entry/네트워크-REST-API란-REST-RESTful이란](https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80)

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
