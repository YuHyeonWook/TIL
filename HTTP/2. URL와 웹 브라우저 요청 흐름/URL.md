# URI

## URI? URL? URN?

**: URI는 로케이터(locator), 이름(name)또는 둘 다 추가로 분류될 수 있다.**
![image](https://github.com/YuHyeonWook/-TIL-/assets/110236953/40b29bc1-42f4-4171-9f10-16c3820f279d)
![image](https://github.com/YuHyeonWook/-TIL-/assets/110236953/641d842b-4554-4599-930b-740385fefb22)
![image](https://github.com/YuHyeonWook/-TIL-/assets/110236953/aab76e96-2ecb-4c3f-b5ed-47be010c0917)

- URL은 우리가 흔히 웹브라우저에서 사용하는 주소
- URN은 위 그림과 같이 이름을 부여하는 것인데, 이름만 가지고는 주소를 찾아갈 수 없기에 실제로 사용하기는 힘들다.
---
## URI
- **U**niform : 리소스를 식별하는 통일된 방식
- **R**esource : 자원, URI로 식별할 수 있는 모든 것(제한이 없다.)
- **I**dentifier : 다른 항목과 구분하는데 필요한 정보

## URL, URN

- URL - Locator : 리소스가 있는 위치를 지정한다.
- URN - Name : 리소스에 이름을 부여한다.
- 위치는 변할 수 있지만, 이름은 변하지 않는다.
- URN 만으로 리소스를 찾을 수 있는 방법이 보편화되지 않았다.

## URL 분석

**scheme://[userinfo@]host[:port][/port][/path][?query][#fragment]**

- 문법 예시: **https://google.com/search?q=hello&hl=ko**
- 프로토콜: `https`
- 호스트명: `google.com`
- 포트번호: `443`
- 패스: `/search`
- 쿼리 파라미터: `q=hello&hl=ko`

### scheme

- 주로 프로토콜이 사용된다.
- 프로토콜이란 어떤 방식으로 자원에 접근할 것인지 정해놓은 규칙이다.
    - ex: http, https, ftp 등
- http는 80 포트, https는 443포트를 주로 사용하며 생략 가능하다.
- https는 http에 보안사용을 추가한 것(HTTP Secure)

### userinfo

- URL에 사용자정보를 포함해서 인증할 때 사용한다.
- 하지만 **거의 사용하지 않는다.**

### host

- 호스트명
- 도메인명 또는 IP주소를 직접 입력한다.

### PORT

- 접속 포트
- 일반적으로 생략가능하며, 생략시 http는 80, https는 443이다.

### path

- 리소스 경로, 계층적 구조로 되어있다.
    - /home/file1.jpg
    - /members
    - /members/100, /item/iphone12

### query

- **key=value 형태**이다
- ?로 시작하며 &로 추가가 가능하다
    - ?keyA=valueA&keyB=valueB
- query parameter, query string등으로 불린다. 웹서버에 제공하는 파라미터로 문자형태.

### fragment

- html 내부 북마크 등에 사용한다.
- 서버에 전송하는 정보가 아니다.
