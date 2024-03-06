## package.json

프로젝트에 대한 정보, 설정, 사용중인 패키지를 기록하는 파일이다.

## npm(node package manager)

npm(node package manager)은 자바스크립트 패키지 매니저이자 node.js를 위한 오픈소스 생태계이다.

Node.js에서 사용할 수 있는 모듈들을 패키지화하여 모아둔 저장소 역할과 패키지 설치 및 관리를 위한 CLI(Command line interface)를 제공한다.

## 구성요소

```json
{
  "name": "project-name",
  "version": "1.0.0",
  "keywords": [],
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "wook",
  "license": "MIT",
  "dependencies": {},
  "devDependencies": {}
}
```

### name

패키지의 이름을 나타낸다. URL이나 Command Line의 일부로 사용될 소문자로 표기된 214자 이내의 프로젝트(패키지) 이름으로, 간결하고 직관적인 이름으로 설정한다.

```json
{
  "name": "@beomy/blog"
}
```

### version

프로젝트의 버전을 나타낸다.

```
{
  "version": "1.0.0"
}
```

### description

**패키지에 대한 설명을 입력을 할 수** 있으며, 문자열로 입력해야한다. 이렇게 하면 npm 검색에 나열되어 사람들이 패키지를 쉽게 찾을 수 있다. (npm search 사용하여 검색함)

```json
{
  "description": "A packaged foo fooer for fooing foos"
}
```

### files

패키지가 의존성으로 설치될 때 같이 포함될 파일들의 배열이다. 생략하면 자동 제외로 설정된 파일을 제외한 모든 파일이 포함된다.

```json
{
  "files": ["dist/", "js/{src,dist}/", "scss/"]
}
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/d929f7e7-5119-4a21-9533-fd3b3f90c8ed)

### main

**패키지의 시작점이 되는 경로**를 지정한다.

패키지의 시작점이 되는 모듈의 id로, 패키지 진입점이 루트와 다른 경우에만 `main` 경로 설정이 필요하다.

```json
{
  "main": "./sources/index.js"
}
```

package.json과 같이 작성된 패키지가 있다면,

```json
{
  "name": "beomy-lib",
  "main": "lib/index.js"
}
```

`import BeomyLib from 'beomy-lib'`으로 패키지를 가져오면 `beomy-lib`의 `lib/index.js`를 가져오는 것과 동일하다.

```json
import BeomyLib from 'beomy-lib'
// Loads ./node_modules/beomy-lib/lib/index.js
```

### **scripts**

**프로젝트에 사용할 수 있는 npm 명령어를 정의**한다. 혹은 패키지 라이프 사이클에서 여러 번 실행되는 스크립트 명령을 포함한다.

제사한 내용은 `[scripts](https://docs.npmjs.com/cli/v10/using-npm/scripts)` 를 참고

```json
{
  "scripts": {
    "lint": "bash lint.sh",
    "dev": "webpack-dev-server",
    "prod": "webpack -p"
  }
}
```

```json
# `webpack -p` 와 동일
$ npm run prod
```

### author, contributors

**패키지의 제작자 정보를 지정**한다.

### **bugs**

**사용자들이 패키지에서 발견한 버그를 제보할 수 있는 이메일, url을 지정**한다.

```json
{
  "bugs": {
    "url": "https://github.com/owner/project/issues",
    "email": "aaa@gmail.com"
  }
}
```

### license

패키지 사용을 허용하는 방법과 제한 사항을 알 수 있도록 라이센스를 지정한다.

### keywords

프로젝트(패키지)의 키워드를 배열로 지정한다. 이 키워드들은 패키지를 검색하거나 분류하는 데 도움된다.

```json
{
  "keywords:": ["array", "string"]
}
```

### homepage

프로젝트 홈페이지로 연결되는 URL을 지정한다.

### **repository**

**코드가 관리되는 저장소 위치를 지정**한다. 만약 git 저장소가 github이라면 npm docs 명령으로 찾을 수 있다.

```json
"repository": {
    "type": "git",
    "url": "http://github.com/npm/npm.git"
}

"repository": {
    "type": "svn",
    "url": "http://v8.googlecode.com/svn/trunk/"
}
```

## **dependencies, devDependencies, peerDependencies**

프로젝트를 진행하면서 여러가지 패키지들을 사용(의존)하게 된다. package.json은 의존 중인 패키지들의 버전을 기록해준다. 이는 dependencies, devDependencies, peerDependencies을 사용하여 기록을 해준다.

### **Dependencies**

**프로젝트가 의존하고 있는 다른 패키지들을 명시하는 곳**이다. 혹은 **패키지의 배포 시 포함될 의존성 모듈을 지정**한다 라고 할 수 있다.

- 의존성을 규정하는 것은 패키지의 이름과 해당 패키지의 버전 범위를 지정한 객체를 통해 이루어진다.

```
"dependencies": {
  "foo": "1.0.0 - 2.9999.9999",
  "bar": ">=1.0.2 <2.1.2",
  "baz": ">1.0.2 <=2.3.4",
  "boo": "2.0.1",
  "qux": "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0",
  "asd": "http://asdf.com/asdf.tar.gz",
  "til": "~1.2",
  "elf": "~1.2.3",
  "two": "2.x",
  "thr": "3.3.x",
  "lat": "latest",
  "dyl": "file:../dyl"
}
```

```json
 "dependencies": {
    "@testing-library/jest-dom": "^5.17.0",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  }
```

### devDependencies

**devDependencies는 개발 과정에서만 사용될 의존성 모듈을 지정한다.**

devDependencies는 **실제로 배포할 때는 필요없는 테스트 도구나 웹팩, 바벨** 같은 것들을 넣어둔다.

```
{
  "name": "ethopia-waza",
  "설명": "유쾌한 과일 향이 나는 커피 품종",
  "version": "1.2.3",
  "devDependencies": {
    "coffee-script": "~1.6.3"
  },
  "스크립트": {
    "prepare": "coffee -o lib/ -c src/waza.coffee"
  },
  "main": "lib/waza.js"
}
```

### **peerDependencies**

호환되는 패키지 목록이 명시된다. 혹은 패키지의 호환성 모듈을 지정한다 라고 할 수 있다.

**패키지를 설치하는 사람에게 필요한 종속성이, 내 패키지에도 동일하게 있을 경우** 이 프로젝트에서 필요한 패키지이지만, 다른 패키지 또한 제공할 것으로 예상되는 패키지를 작성한다.

```
{
  "name": "bootstrap",
  "peerDependencies": {
    "jquery": "1.9.1 - 3",
    "popper.js": "^1.12.9"
  }
}
```

```
"name": "tea-latte",
"version": "1.3.5",
"peerDependencies": {
	"tea" : "2.x"
	}
```

- 위 같은 경우, 내 패키지 `tea-latte`는 `tea`라는 외부 패키지의 **2.x 버전대와 함께 설치되는 것이 보장된다**.
- 그럼 이 때 `npm install tea-latte`는 다음과 같은 의존성 그래프를 출력한다

```
├── tea-latte@1.3.5
└── tea@2.2.0
```

### dependencies와의 차이점

`dependencies` 내가 만든 모듈에서 사용하는 패키지들을 기록하고, `peerDependencies`는 내가 만든 모듈이 다른 모듈과 함께 동작할 수 있다는 호환성을 표시한다.

```
{
  "peerDependencies": {
    "react": "17.0.2",
    "react-dom": "17.0.2"
  }
// ...
}
```

### peerDependencies에 react와 react-dom을 작성하는 이유

- `React`는 UI 라이브러리로서 사용되고,`React-DOM`은 React로 작성된 컴포넌트를 실제 DOM에 렌더링하는 데 사용된다.
- 패키지를 만들어서 배포할 때, Peer Dependencies로 React와 React-DOM을 작성하면 해당 패키지를 사용하는 다른 프로젝트에서는 이 패키지와 함께 이 버전의 React와 이 버전의 React-DOM도 설치해야 한다는 것을 알 수 있다.
- 즉, React와 React-DOM의 버전 충돌을 방지하고, 호환성을 유지을 하고자 peerDependencies에 작성한다.

### bundledDependencies

패키지를 게시할 때 번들로 묶을 패키지 이름을 배열로 지정한다.

```
{
  "bundledDependencies": [
    "renderized",
    "super-streams"
  ]
}
```

### optionalDependencies

npm을 찾을 수 없거나 설치에 실패한 경우 계속 진행하려면 optionDependencies 객체에 넣을 수 있다.

dependencies 동일하게 배포 시 포함될 의존성 모듈을 지정하지만, 빌드 실패로 인해 설치 과정이 중단되지 않는다.

```
{
  "optionalDependencies": {
    "7zip-bin-mac": "^1.x.x",
    "7zip-bin-win": "^2.x.x"
  }
}
```

### private

개인 저장소의 우연한 발행을 방지하기 위해 npm에서 **해당 패키지의 비공개 여부를 지정**한다.

만약 private: true로 package.json에 설정 해두면, 패키지의 배포(publish) 명령을 거부하게 된다.

```
{
  "private": true
}
```

### directories

CommonJS packages 스펙에는 `directories` 개체를 사용하여 패키지 구성을 나타낸다. 아래와 같이 사용할 수 있습니다.

```json
{
  "directories": {
    "bin": "./bin",
    "doc": "./doc",
    "lib": "./lib",
    "man": "./man"
  }
}
```

- `directories.bin`: `bin` 항목과 동일한 기능을 하는 필드이다. `directories.bin`와 `bin` 하나의 항목만 설정되어야 한다.
- `directories.doc`: 패키지의 문서, 마크다운 파일들의 위치를 표시하는 항목이다.
- `directories.lib`: 패키지의 라이브러리의 위치를 표시하는 항목이다.
- `directories.man`: man문서들이 위치한 폴더를 가리킨다. man 배열을 만드는 것보다 간편하다.
- `directories.example` : 예제 파일들을 여기에 위치시킨다.

### config

- 패키지의 버전에 관계없이 패키지 스크립트에서 사용될 수 있는 설정 정보이다.
- 패키지 스크립트에서 사용되는 구성 매개변수를 설정할 수 있다.

```jsx
"name":"foo",
"config":{
"port":"8080"
}
```

"start" 명령을 실행할 때 npm_package_config_port 를 참조할 수 있게 된다. 다음 명령으로 사용자가 이를 덮어 쓸 수 있다.

```jsx
"name":"foo","config":{"port":"8080"}
```

### browser

- browser 항목은 모듈을 클라이언트 측(Client side)에서 사용하려는 경우 브라우저를 사용해야 한다. 이렇게 하면 Node.js 모듈에서 사용할 수 없는 기본형에 의존할 수 있음을 사용자에게 암시해준다. ex) , `window` 객체

```json
{
  "browser": "./sources/index.js"
}
```

### bin

패키지가 제공하는 실행 가능한 자바스크립트 파일을 명시한다.

```json
{
  "bin": {
    "myapp": "./cli.js"
  }
}
```

- 그래서 myapp을 설치할 때 cli,js 파일에 대한 심볼릭 링크가 /usr/local/bin/myapp에 만들어진다.

실행 파일이 하나이고 그 이름이 패키지 이름이어야 하는 경우에는 문자열로 지정하면 됩니다. 예시)

```json
{
  "name": "my-program",
  "version": "1.2.5",
  "bin": "./path/to/program"
}

는 다음과 같다.

{
  "name": "my-program",
  "version": "1.2.5",
  "bin": {
    "my-program": "./path/to/program"
  }
}
```

- 만약 하나의 실행 파일만 가지고 있다면, 실행 파일의 이름은 패지키의 이름과 같게 되고, 그렇지 않다면 각각의 실행 파일의 이름을 bin 항목에 지정해 주어야 한다.

### engines, os, cpu

- 패키지가 특정 환경에서만 동작하도록 제한하도록 한다.
- engines :  패키지가 호환되는 Node.js 버전을 지정한다. 예를 들어, `"engines": {"node": ">=14.0.0"}`은 패키지가 Node.js 14.0.0 버전 이상에서 동작하도록 한다.
- os : 패키지가 동작하는 운영체제를 지정한다.
- cpu : 허용되는 cpu 목록을 저장한다.

### package-lock.json 파일

- package-lock.json 파일은 dependencies나 devDependencies에 명시된 라이브러리를 설치할 때 필요한 부수 라이브러리의 버전을 관리한다. package.json 파일에 명시된 라이브러리를 설치하고 나면 자동으로 생성된다.
- package.json 파일과 다르게 개발자가 직접 package-lock.json 파일의 내용을 수정하지 않는다.

<br>

# 참고

https://beomy.github.io/tech/etc/package-json/

https://programmingsummaries.tistory.com/385

https://docs.npmjs.com/cli/v10/configuring-npm/package-json#config

https://www.zerocho.com/category/NodeJS/post/5825a3caaff5c70018279975

https://heropy.blog/2018/02/18/node-js-npm/
