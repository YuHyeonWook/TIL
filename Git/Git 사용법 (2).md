# Git 사용법 (2)

## **작업을 커밋할 때 권장사항**

### **1. 하나의 커밋에는 한 단위의 작업을 넣도록 하자**

- 한 작업을 여러 버전에 걸쳐 커밋하지 않는다.
- 여러 작업을 한 버전에 커밋하지 않는다.

### **2. 커밋 메시지는 어떤 작업이 이뤄졌는지 알아볼 수 있도록 작성한다.**

<br/>

## **커밋 메시지 컨벤션**

널리 사용되는 커밋 메시지 작성방식

```yaml
type: subject

body (optional)
...
...
...

footer (optional)
```

### **예시**

```yaml
feat: 압축파일 미리보기 기능 추가

사용자의 편의를 위해 압축을 풀기 전에
다음과 같이 압축파일 미리보기를 할 수 있도록 함
 - 마우스 오른쪽 클릭
 - 윈도우 탐색기 또는 맥 파인더의 미리보기 창

Closes #125
```

### **Type**

| 타입     | 설명                                            |
| -------- | ----------------------------------------------- |
| feat     | 새로운 기능 추가                                |
| fix      | 버그 수정                                       |
| docs     | 문서 수정                                       |
| style    | 공백, 세미콜론 등 스타일 수정                   |
| refactor | 코드 리팩토링                                   |
| perf     | 성능 개선                                       |
| test     | 테스트 추가                                     |
| chore    | 빌드 과정 또는 보조 기능(문서 생성기능 등) 수정 |

### **Subject**

커밋의 작업 내용 간략히 설명

### **Body**

길게 설명할 필요가 있을 시 작성

### **Footer**

- **Breaking Point** 가 있을 때
- 특정 이슈에 대한 해결 작업일 때

<br/>

## **Gitmoji**

[😊 사이트 방문하기](https://gitmoji.dev/)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/6d673384-7065-447f-b8a7-a67c617442fb)

- 이렇게 꾸밀 수도 있다.

---

<br/>

## **내용 확인하며 hunk별로 스테이징하기**

```yaml
# **내용 확인하며 hunk별로 스테이징하기**

git add -p
# - 옵션 설명을 보려면 ?입력 후 엔터
# - y 또는 n로 각 헝크 선택
# - 일부만 스테이징하고 진행해보기
# - git stats와 소스트리로 확인함
```

<br/>

## **변경사항을 확인하고 커밋하기**

```yaml
# **변경사항을 확인하고 커밋하기**

git commit -v
# - j, k로 스크롤하며 내용 확인
# - git diff --staged와 비교
# - 커밋 후 남은 헝크를 다른 버전으로 커밋해보기
```

---

<br/>

## Stash

```yaml
# 작업하는것을 다른 공간에 치워둠
git stash
# - git stash save와 같음

# 원하는 시점에 브랜치를 다시 적용함
git stash pop

# 원하는 것만 stash 해보기
git stash -p

# 메시지와 함께 스태시
# ex) git stash -m 'Add Stash3'
git stash -m '메시지'

# 스태시 목록 보기
git stash list
# 리스트상의 번호로 apply, drop, pop 가능
# ex) git stash apply stash@{1}
```

## **Stash 사용법 정리**

| 명령어                         | 설명                                          | 비고                           |
| ------------------------------ | --------------------------------------------- | ------------------------------ |
| git stash                      | 현 작업들 치워두기                            | 끝에 save 생략                 |
| git stash apply                | 치워둔 마지막 항목(번호 없을 시) 적용         | 끝에 번호로 항목 지정 가능     |
| git stash drop                 | 치워둔 마지막 항목(번호 없을 시) 삭제         | 끝에 번호로 항목 지정 가능     |
| git stash pop                  | 치워둔 마지막 항목(번호 없을 시) 적용 및 삭제 | apply + drop                   |
| 💡 git stash branch (브랜치명) | 새 브랜치를 생성하여 pop                      | 충돌사항이 있는 상황 등에 유용 |
| git stash clear                | 치워둔 모든 항목들 비우기                     |                                |

---

<br/>

## 커밋 수정하기

```yaml
# 메시지 입력
# git commit -am 'wwww'
git commit -am '메시지'

# 마지막 커밋 수정함
git commit --amend

# 커밋 메시지 한 줄로 변경
# ex) git commit --amend -m 'Add members to Panthers and Pumas'
git commit --amend -m '메시지'
```

---

<br/>

## 과거의 커밋들을 수정, 삭제, 병합, 분할하기

### **git rebase i (대상 바로 이전 커밋)**

- 과거 커밋 내역을 다양한 방법으로 수정 가능
  ```yaml
  # git rebase i (대상 바로 이전 커밋)
  # - 수정이 필요한 커밋 이전 것을 선택하면 됨
  # - 과거 커밋 내역을 다양한 방법으로 수정 가능
  git rebase -i '수정이 필요한 커밋에서 이전 커밋 명'
  ```

| 명령어    | 설명               |
| --------- | ------------------ |
| p, pick   | 커밋 그대로 두기   |
| r, reword | 커밋 메시지 변경   |
| e, edit   | 수정을 위해 정지   |
| d, drop   | 커밋 삭제          |
| s, squash | 이전 커밋에 합치기 |

---

<br/>

## 관리되지 않는 파일들 삭제하기

```yaml
# Git에서 추적하지 않는 파일들 삭제함
# ex) git clean -n
git clean

# 삭제될 폴더와 파일들 보여줌
git clean -nd

# 폴더 포함해서 인터렉티브 모드 시작
git clean -di

# 폴더 포함해서 강제로 바로 지워버림
git clean -df
```

| 옵션 | 설명                                 |
| ---- | ------------------------------------ |
| -n   | 삭제될 파일들 보여주기               |
| -i   | 인터렉티브 모드 시작                 |
| -d   | 폴더 포함                            |
| -f   | 강제로 바로 지워버리기               |
| -x   | ⚠️ .gitignore에 등록된 파일들도 삭제 |

- 위의 옵션들을 조합하여 사용함

---

<br/>

## 커밋에 태그 달기

### **Git의 Tag**

- 특정 시점을 키워드로 저장하고 싶을 때
- 커밋에 버전 정보를 붙이고자 할 때

<br/>

### **태그 달아보기**

| 태그 종류   | 설명                                           |
| ----------- | ---------------------------------------------- |
| lightweight | 특정 커밋을 가리키는 용도                      |
| annotated   | 작성자 정보와 날짜, 메시지, GPG 서명 포함 가능 |

```yaml
# 마지막 커밋에 태그 달기 (lightweight)
git tag v2.0.0

# 현존하는 태그 확인
git tag

# 원하는 태그의 내용 확인
git show v2.0.0

# 태그 삭제
git tag -d v2.0.0

# 마지막 커밋에 태그 달기 (annotated)
git tag -a v2.0.0

# 입력 후 메시지 작성 또는
git tag v2.0.0 -m '자진모리 버전'
	# -m 태그가 -a 태그 암시
	# git show v2.0.0으로 확인

# 원하는 커밋에 태그 달기
git tag (태그명) (커밋 해시) -m (메시지)
# 원하는 커밋에 아래 태그들 추가
	# v1.0.0 (굿거리 버전)
	# v1.2.1 (휘모리 버전)

# 원하는 패턴으로 필터링하기
git tag -l 'v1.*'

# 원하는 버전으로 체크아웃
git checkout v1.2.1
	# switch로 이전 브랜치로 복귀
```

---

<br/>

### 원격의 태그 동기화

```yaml
# 특정 태그 원격에 올리기
# ex) git push origin v2.0.0
git push (원격명) (태그명)

# 특정 태그 원격에서 삭제
# ex) git push --delete origin v2.0.0
git push --delete (원격명) (태그명)

# 로컬의 모든 태그 원격에 올리기
git push --tags
```

<br/>

## **release**

- 다운로드 가능한 배포판 기능을 함
- 모든 파일을 github에 올릴 수 있음

### **릴리즈 만들기**

- GitHub에서 태그 목록으로
- 원하는 태그에서 `Create release` 누르기
- 제목과 내용(마크다운) 입력 후 `Publish release` 누르기

<br/>

# 참고

얄코, github 강의
