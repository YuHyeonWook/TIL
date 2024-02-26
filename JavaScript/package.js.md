# package.json

# **npm**(node package manager)

- npm(node package manager)은 자바스크립트 패키지 매니저이자 node.js를 위한 오픈소스 생태계이다.
- Node.js에서 사용할 수 있는 모듈들을 패키지화하여 모아둔 저장소 역할과 패키지 설치 및 관리를 위한 CLI(Command line interface)를 제공한다.
- 자신이 작성한 패키지를 공개할 수도 있고 필요한 패키지를 검색하여 재사용할 수도 있다.

## 구성요소

### name

- 패키지의 이름을 나타낸다.
- 패키지를 게시하려는 경우 package.json에서 가장 중요한 것은 이름과 버전 필드이므로 필수 항목이다.
- 이름과 버전은 고유한 것으로 가정되는 식별자를 구성한다.

규칙

- 이름은 214자 이하여야 한다. 여기에는 범위 지정 패키지의 범위가 포함된다.
- 범위가 지정된 패키지의 이름은 점 또는 밑줄로 시작할 수 있다. 범위가 없는 이름은 허용되지 않는다.
- 새 패키지는 이름에 대문자가 포함되어서는 안된다.
- 이름은 결국 URL, 명령줄의 인수 및 폴더 이름의 일부가 된다. 따라서 이름에는 URL이 아닌 문자를 포함할 수 없다.

```json
{
  "name": "@beomy/blog"
}
```

<br>

### version

- 패키지를 게시하려는 경우 package.json에서 가장 중요한 것은 이름과 버전 필드이므로 필수 항목이다.
- 이름과 버전은 고유한 것으로 가정되는 식별자를 구성한다.

```
{
  "version": "1.0.0"
}
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/52b1ebe7-d06c-4898-9190-968f5e0a2a3e)

- Major: API가 변경/삭제 되어 사용자가 Major 버전을 업데이트 할 경우 기존의 코드가 동작하지 않을 수 있을 때, Major 버전을 업데이트하여 배포합니다.
- Minor: 이전 버전과 호환되는 방식으로 API가 추가/변경 되었을 때 Minor 버전을 업데이트하여 배포합니다.
- Patch: 이전 버전과 호환되는 버그 수정을 할 경우 Patch 버전을 업데이트하여 배포합니다.

<br>

### description

- 패키지에 대한 설명을 입력을 할 수 있으며, 문자열로 입력해야한다. 이렇게 하면 **npm 검색에 나열되어 사람들이 패키지를 쉽게 찾을 수 있다.**

```json
{
  "description": "A packaged foo fooer for fooing foos"
}
```

<br>

### files

- files 항목은 프로젝트에 포함된 파일의 배열이다. 폴더 이름을 지정하면 폴더 안의 파일도 포함된다.
- 또한, npmignore 파일을 패키지의 루트 혹은 하위 폴더에 둘 수 있다. 이 파일에 기록된 파일들은 files의 배열로 지정되어 있었다고 해도 대상에서 제외된다. .npmignore 파일은 .gitignore 파일과 유사하다.

```json
{
  "files": ["dist/**/*", "lib/**/*"]
}
```

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/38126dc7-7255-4060-8a41-c304ad852b3d)

<br>

### main

- main 항목은 사용자의 프로그램 시작점이 되는 모듈의 ID이다. 예를들어 foo라는 패키지가 있다면 이 패키지를 사용자가 설치 한 뒤, requure(’foo’)를 실행했을 때 main으로 지정한 모듈의 exports객체가 반환된다.
- 모듈 id는 패키지 루트에 상대적인 경로를 지정해야 한다. 대부분의 모듈에 있어서 메인 스크립트를 갖는 것은 유용하지만 종종 그렇지 않을 수도 있다.

```json
{
  "main": "./sources/index.js"
}
```

`package.json`과 같이 작성된 패키지가 있다면,

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

<br>

### browser

- browser 항목은 모듈을 클라이언트 측(Client side)에서 사용하려는 경우 브라우저를 사용해야 한다. 이렇게 하면 Node.js 모듈에서 사용할 수 없는 기본형에 의존할 수 있음을 사용자에게 암시해준다. ex) , `window` 객체

```json
{
  "browser": "./sources/index.js"
}
```

<br>

### bin

- 많은 패키지는 경로에 설치되는 하나 이상의 실행 파일을 가지고 있다. npm에서는 이를 매우 쉽게 구현한다. (실제로 이 기능은 npm을 설치하는 데에도 사용된다.)
- 이 기능을 사용하려면 package.json파일에 bin 항목을 제공해야한다. 이 패키지가 전역으로 설치되면 해당 파일이 전역 bins 디렉터리 내에 링크되거나 bin 필드에 지정된 파일을 실행하는 cmd(Windows 명령 파일)가 생성되므로 이름 또는 name.cmd(Windows PowerShell의 경우)로 실행할 수 있습니다. 이 패키지가 다른 패키지에 종속성으로 설치되면 해당 패키지에 파일이 링크되어 npm 실행 스크립트로 직접 실행하거나 다른 스크립트에서 이름으로 호출할 때 사용할 수 있습니다.

예를 들어 myapp에는 다음과 같은 파일이 있을 수 있다:

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

<br>

### scripts

- scripts 항목은 패키지의 생명주기 중 다양한 타이밍에서 실행되는 scripts 명령들을 포함하고 있는 디렉토리이다. scripts항목 객체에서 키는 이벤트이고, 값은 이때 실행될 커맨드이다.
- 제사한 내용은 `[scripts](https://docs.npmjs.com/cli/v10/using-npm/scripts)` 를 참고해라.

<br>

### directories

- CommonJS packages 스펙에는 `directories` 개체를 사용하여 패키지 구성을 나타낼 수 있다. 아래와 같이 사용할 수 있습니다.

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

[npm-cli](https://github.com/npm/cli/blob/latest/package.json)에서 `directories` 필드가 설정되어 있는 것을 확인할 수 있다.

<br>

### repository

- 코드가 관리되는 저장소 위치를 지정한다. 만약 git 저장소가 github이라면 npm docs 명령으로 찾을 수 있다.

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

<br>

### config

- config객체는 패키지의 버전에 관계없이 패키지 스크립트에서 사용될 수 있는 설정 정보이다.

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

<br>

### dependencies

- 의존성을 규정하는 것은 패키지의 이름과 해당 패키지의 버전 범위를 지정한 객체를 통해 이루어진다. 버전 범위는 하나 혹은 여러개의 공백으로 분리된 설명자가 포함된 문자열이다. 의존성은 tarball 또는 git URL로 식별할 수 있다.
- 테스트 관련 모듈이나 트랜스 파일러 관련 모듈을 [dependencies](https://docs.npmjs.com/cli/v10/configuring-npm/package-json#dependencies) 개체에 추가하면 안된다. 운영이 아닌 개발 단계에서만 필요한 의존성 모듈들을 devDependencies에 설치해야 한다.

semver를 참고하면 버전 범위를 지정하는 방법에 대해 알 수 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cdf5fd00-85a4-4001-aa3d-4b52542685d0/51509245-62ef-4989-87a9-52a34232fa94/Untitled.png)

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

<br>

### Local Paths

- 버전 2.0.0부터 패키지가 포함된 로컬 디렉터리 경로를 제공할 수 있다. 로컬 경로는 다음 형식 중 하나를 사용하여 npm install -S 또는 npm install --save를 사용하여 저장할 수 있다

```
../foo/bar
~/foo/bar
./foo/bar
/foo/bar
```

```
// 이 경우 상대 경로로 정규화되어 package.json에 추가됩니다.

{
  "name": "baz",
  "의존성": {
    "bar": "file:../foo/bar"
  }
}
```

- 이 기능은 로컬 오프라인 개발 및 외부 서버를 사용하지 않으려는 곳에서 npm 설치가 필요한 테스트를 만드는 데 유용하지만 패키지를 public registry에 게시할 때는 사용해서는 안된다.

<br>

### devDependencies

- 누군가 자신의 프로그램에서 모듈을 다운로드하여 사용할 계획이라면 사용하는 외부 테스트 또는 문서 프레임워크를 다운로드하여 빌드하고 싶지 않거나 필요하지 않을 것이다.
- 이 경우 이러한 추가 항목을 devDependencies 객체에 추가하는 것이 좋은 방법이다.
- CoffeeScript 또는 다른 언어를 JavaScript로 컴파일하는 등 플랫폼에 구애받지 않는 빌드 단계의 경우 준비 스크립트를 사용하여 이 작업을 수행하고 필요한 패키지를 devDependency로 만든다

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

- prepare script는 사용자들이 js로 변환하지 않고도 사용할 수 있도록 퍼블리싱을 하기전에 실행될 것이다.

<br>

### bundledDependencies

- 패키지를 퍼블리싱할 때 번들되는 패키지 이름들의 목록이다.

<br>

### private

- 만약 private: true로 package.json에 설정 해두면, publish 명령을 거부하게 된다.
- 이 플래그는 개인적으로만 사용하는 저장소를 무심코 publish 해버리는 것을 방지한다. 만약 (내부 레지스트리 등) 특정 레지스트리 만에 출시하는 환경을 원한다면, 아래 publishConfig를 이용하여 publish시 registry 설정을 덮어 쓸 수 있다.

---

## 추가

### packageManager

- packageManager 항목은 패키지가 특정 패키지 매니저를 사용해야 할 경우 특정 패키지와 버전을 지정할 수 있는 항목이다.

```json
{
  "packageManager": "yarn@3.2.4"
}
```

<br>

### `types` (Typescript)

- `types` 필드는 타입스크립트의 `d.ts` 타입 정의 파일의 경로를 저장하는 필드입니다. `types` 필드 대신 `typings` 필드를 사용할 수 있습니다. 아래와 같이 사용할 수 있습니다.

```json
{
  "types": "./lib/index.d.ts"
}
```

- 타입 정의 파일의 이름이 `index.d.ts`이고 패키지 루트(`index.js`의 위치)에 있으면 생략 가능합니다.

<br>

### type

- `type` 필드는 `commonjs`(기본 값)와 `module` 중 하나를 사용할 수 있습니다. `type` 필드가 정의되어 있지 않다면 `commonjs`로 처리됩니다.

```json
{
  "type": "module"
}
```

- 파일의 확장자가 `.mjs`이거나 `type` 필드가 `module`일 경우 패키지는 ES Module를 사용하여 `import`나 `import()` 함수를 사용할 수 있게 됩니다. 파일 확장자가 `.cjs`이거나 `type` 필드가 `commonjs`일 경우(혹은 생략) `import`, `import()` 함수, `require()` 함수를 사용할 수 있습니다.

<br>

### module

- module 필드는 main 필드와 유사한 목적으로 사용되는 항목이다. ES6 호환 환경에서 **패키지를 사용할 때 진입되는 경로**이다.

```json
{
  "module": "./sources/index.mjs"
}
```

<br>

### exports

`main` 필드와 `exports` 필드를 사용하면 패키지의 진입점을 설정할 수 있습니다. `exports` 필드는 `main` 필드와 다르게 여러 개의 진입점을 설정할 수 있습니다. 아래와 같이 작성할 수 있습니다.

```json
{
  "exports": {
    ".": "./lib/index.js",
    "./lib": "./lib/index.js",
    "./feature": "./feature/index.js"
  }
}
```

Node 10 버전 이하에서는 `main` 필드를 사용해야 하고, 11 버전 이상에서는 `exports` 필드와 `main` 필드가 모두 정의되어 있는 경우 `exports` 필드가 우선합니다.

```jsx
{
  "name": "beomy-lib",
  "exports": {
    ".": "./lib/index.js",
    "./lib": "./lib/index.js",
    "./feature": "./feature/index.js"
  }
}
```

위의 코드에서는 `./feature/utils.js`가 `exports` 필드에 명시 되어있지 않기 때문에 `import util from 'beomy-lib/feature/utils.js'`가 불가능합니다. 이러한 경우 다른 파일들과 동일하게 `./feature/utils.js`를 `exports` 필드에 추가하거나 아래와 같이 작성하여 해결 할 수 있습니다.

```jsx
`{
  "name": "beomy-lib",
  "exports": {
    ".": "./lib/index.js",
    "./lib": "./lib/index.js",
    "./feature": "./feature/index.js",
    "./feature/*.js": "./feature/*.js"
  }
}``import BeomyLib from 'beomy-lib'
// Loads ./node_modules/beomy-lib/lib/index.js

import BeomyLib from 'beomy-lib/lib'
// Loads ./node_modules/beomy-lib/lib/index.js

import BeomyLib from 'beomy-lib/feature'
// Loads ./node_modules/beomy-lib/feature/index.js

import BeomyLib from 'beomy-lib/feature/utils.js'
// Loads ./node_modules/beomy-lib/feature/utils.js`;
```

<br>

### imports

`exports` 필드가 패키지 사용자에게 패키지를 진입할 수 있는 진입점을 제공하는 필드라면, `imports` 필드는 패키지를 개발하는 패키지 생성자에게 진입점을 제공하는 필드입니다. 아래와 같이 사용할 수 있습니다.

```jsx
{
  "imports": {
    "#dep": {
      "node": "dep-node-native",
      "default": "./dep-polyfill.js"
    }
  },
  "dependencies": {
    "dep-node-native": "^1.0.0"
  }
}
```

외부 패키지와 구분될 수 있도록 `#`으로 시작해야 합니다. 위의 코드와 같이 조건 별로 진입점을 다르게 제공할 수 있습니다. 패키지 생성자는 `import #dep`로 가져와 사용할 수 있습니다.

<br>

# 참고

https://beomy.github.io/tech/etc/package-json/

https://programmingsummaries.tistory.com/385

https://docs.npmjs.com/cli/v10/configuring-npm/package-json#config
