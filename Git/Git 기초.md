# Git

- **Git은 프로젝트의 시간과 차원을 자유롭게 넘나들수 있도록 해줌**
  - 프로젝트의 버전을 과거로 되돌리거나 특정 내역을 취소할 수 있음
  - 프로젝트의 여러 모드를 쉽게 전환하고 관리할 수 있음
- 또한, **Git은 여러 사람들이 프로젝트에서 협업할 수 있도록 도와줌**

# Git설정 & 프로젝트 관리

## **Git 최초 설정**

- **Git 전역으로 사용자 이름과 이메일 주소를 설정해야함**
  - GitHub 계정과는 별개임

터미널 프로그램 (Git Bash, iTerm2)에서 아래 명령어 실행

```
# 유저 설정
git config --global user.name "(본인 이름)"
git config --global user.email "(본인 이메일)"

# 아래의 명령어들로 확인
git config --global user.name
git config --global user.email

# **기본 브랜치명 변경**
git config --global init.defaultBranch main
```

## **프로젝트 생성 & Git 관리 시작**

```
# 새로운 Git 저장소(repository)를 생성할 때 사용하는 Git 명령어
# 폴더에 숨김모드로 .git 폴더 생성됨
git init

# Git 프로젝트의 상태를 확인
# 현재 폴더의 상태를 보여줌
git status
```

## **Git의 관리에서 특정 파일/폴더를 배제해야 할 경우**

### **a. 포함할 필요가 없을 때**

- 자동으로 생성 또는 다운로드되는 파일들 (빌드 결과물, 라이브러리)

### **b. 포함하지 말아야 할 때**

- 보안상 민감한 정보를 담은 파일

## **.gitignore 형식**

https://git-scm.com/docs/gitignore 참조

```
# 이렇게 #를 사용해서 주석

# 모든 file.c
file.c

# 최상위 폴더의 file.c
/file.c

# 모든 .c 확장자 파일
*.c

# .c 확장자지만 무시하지 않을 파일
!not_ignore_this.c

# logs란 이름의 파일 또는 폴더와 그 내용들
logs

# logs란 이름의 폴더와 그 내용들
logs/

# logs 폴더 바로 안의 debug.log와 .c 파일들
logs/debug.log
logs/*.c

# logs 폴더 바로 안, 또는 그 안의 다른 폴더(들) 안의 debug.log
logs/**/debug.log
```

---

## **Git에 파일 반영하기**

```
## 버전에 파일 담기
git add filename.py

# add
git add [file name]

# 모든 파일 담기
**#** git status로 확인할 수 있다.
git add .

# git add 취소하기
git rm --cached <file>

## 버전으로 묶어주기
# vi 입력모드로 진입
# 저장소의 변경 내역을 저장함
git commit

# 커밋 메세지 한 번에 작성
git commit -m "[commit message]"

# 변경 사항이 있는 모든 파일 add 와 동시에 commit
git commit -am "[commit message]"

# 커밋 이력 확인
git log
```

**Vi 입력 모드로 진입**

| 작업                | Vi 명령어 | 상세                                         |
| ------------------- | --------- | -------------------------------------------- |
| 입력 시작           | i         | 명령어 입력 모드에서 텍스트 입력 모드로 전환 |
| 입력 종료           | ESC       | 텍스트 입력 모드에서 명령어 입력 모드로 전환 |
| 저장 없이 종료      | :q        |                                              |
| 저장 없이 강제 종료 | :q!       | 입력한 것이 있을 때 사용                     |
| 저장하고 종료       | :wq       | 입력한 것이 있을 때 사용                     |
| 위로 스크롤         | k         | git log등에서 내역이 길 때 사용              |
| 아래로 스크롤       | j         | git log등에서 내역이 길 때 사용              |

# Git에서 과거로 돌아가는 두 방식

- **reset** : 원하는 시점으로 돌아간 뒤 이후 내역들을 지움
- **revert** : 되돌리기 원하는 시점의 커밋을 거꾸로 실행함

```
# reset 사용해서 과거로 돌아가기
git reset --hard (돌아갈 커밋 해시)

# 뒤에 커밋 해시가 없으면 마지막 커밋을 가리킨다
git reset --hard
```

```
# revert로 과거의 커밋 되돌리기
git revert (되돌릴 커밋 해시)

# 커밋해버리지 않고 revert하기
git revert --no-commit (되돌릴  커밋 해시)
```

---

# **Branch**

### **Branch는 왜 필요한가?**

- Branch는 분기된 차원으로 프로젝트를 하나 이상의 모습으로 관리해야 할 때(실배포용, 테스트 서버용, 새로운 시도용 등)
- 여러 작업들이 각각 독립되어 진행될 때 각각의 차원에서 작업한 뒤 확정된 것을 메인 브랜치에 통합한다

## **Branch 생성/ 이동/ 삭제**

```bash
# 브랜치 생성
git branch (신규 브랜치 명)

# 브랜치 목록 확인
git branch

# 다른 브랜치로 이동
git switch (신규 브랜치 명)

# 브랜치 생성과 이동을 동시에 하기
git switch -c (신규 브랜치 명)

# 브랜치 삭제하기
# 지워질 브랜치에만 있는 내용의 커밋이 있을 경우(=다른 브랜치로 가져오지 않은 내용이 있는 경우)
# -d 대신 -D로 강제 삭제
git branch -d (삭제할 브랜치 명)

# 브랜치 이름 변경
git branch -m (기존 브랜치 명) (신규 브랜치 명)

# 여러 브랜치의 내역을 한번에 보기
git log --al --decorate --oneline --graph
```

## **Branch 합치기**

- Merge : 두 브랜치를 한 커밋에 이어붙이는 방식
  - 브랜치 사용 내역을 남길 필요가 있을 때
  - 다른 형태의 merge도 있음

!https://blog.kakaocdn.net/dn/dYgvmH/btrWg1B6a0L/HkC24hYXQd36K7FlTbU71K/img.jpg

!https://blog.kakaocdn.net/dn/b9ClaD/btrWggzpd01/APTOF9NynXws7jZlErGinK/img.jpg

### merge로 합치기

```bash
# 합쳐져서 주요 대상이 될 브랜치로 이동
# merge는 reset으로 되돌리기가 가능함. merge하기 전 해당 브랜치의 마지막 시점으로 reset
git switch main
git merge add-coach

# 병합된 브랜치는 삭제
git branch -d add-coach
```

- Rebase : 브랜치를 다른 브랜치에 이어붙이는 방식
  - 한 줄로 깔끔히 정리된 내욕을 유지하기 원할 때
  - 이미 팀원들과 공유한 커밋에 대해서는 사용하지 않는 것이 적합함

!https://blog.kakaocdn.net/dn/dYgvmH/btrWg1B6a0L/HkC24hYXQd36K7FlTbU71K/img.jpg

!https://blog.kakaocdn.net/dn/beuCaY/btrWedXuWgi/47vOlbOuY6ElhKxq9AqeeK/img.jpg

### Rebase로 합치기

```bash
# merge와 반대로 합쳐질 브랜치로 이동한다
git switch new-teams
git rebase main

# new-teams 브랜치가 main에 합쳐졌지만 아직 main은 new-teams 브랜치의 끝에 있지 않다.
# 따라서 main 브랜치로 이동 후 new-teams의 시점으로 fast-forward해준다
git merge new-teams

# 합친 브랜치 삭제
git branch -d new-teams
```

# **원격 저장소 사용하기**

- 여기서는 https 프로토콜 사용

### **git과 github 연동하기**

```bash
# remote repository 등록하기
git remote add [remote github repository address]

# 로컬의 git 저장소에 원격 저장소로의 연결 추가
# 원격 저장소 이름에 흔히 origin 사용함. 다른 것으로 수정 가능
git remote add origin (원격 저장소 주소)

# 브랜치 명을 main으로 변경함
git branch -M main

# 로컬 저장소의 커밋 내역을 원격으로 push(업로드) 할 것인지
# origin의 main branch로 push
git push -u origin main

# 원격 저장소 목록보기
git remote
git remote -v

# 원격 지우기 (GitHub repository가 지워지는 것이 아니라 로컬 프로젝트와의 연결만 삭제)
git remote remove (origin 등 원격 이름)
```

```bash
# Github에서 프로젝트 다운받기# 프로젝트를 다운받고자 하는 폴더에서 우클릭 - Git Bash here
git clone (원격 저장소 주소)
```

### **Push & Pull**

```bash
# 원격으로 커밋 밀어올리기 (push)
git push

# 원격으로 커밋 당겨오기 (pull)
# 동료가 github에 올린 프로젝트를 내가 pull로 다운받음
git pull
```

### pull 할 것이 있을 때 push를 해버리면?

```bash
# 우선 먼저 pull을 하고 push를 해준다

# 1-1. merge 방식
git pull --no-rebase

# 1-2. rebase 방식
# pull 상의 rebase는 협업 시에도 사용 OK
git pull --rebase

# 2. push
git push
```

### 협업 시 충돌이 발생하는 경우

```bash
# 이후는 merge/rebase 방식과 동일함.
# 둘 중에 하나 하면 됨
git pull --no-rebase
git pull --rebase

# 충돌 처리 후 git add .와 git commit 명령어 입력
git add .
git commit
```

### 로컬의 내역을 강제로 push 하기

```bash
# 로컬의 충돌 전으로 reset함
# 혼자할때 사용하기 (협업할때 쓰면 데이터 나갈 수 있음)
git push --force
```

### **원격의 Branch 다루기**

```bash
# 로컬에서 브랜치 만들어 원격에 push 해보기
git branch -c from-local

# git push 하면 신규 브랜치에서 어디로 push 할 지 정해져있지 않으니 명시해달라는 에러 발생
git push

# push 해 줄 브랜치를 명시해준다
# 아래와 동일한 코드
git push --set-upstream origin from-local
(or)
# 위 와 동일한 코드
git push -u origin from-local

# 로컬과 원격의 브랜치들 확인함
git branch --all
git branch -a
```

### 원격의 브랜치를 로컬로 받아오기

```bash
# 원격의 변경사항을 확인함
$ git fetch

# 브랜치 목록 확인
git branch -a

# 로컬에 같은 이름의 브랜치를 생성하여 연결하고 switch 함
# 원격에서 로컬로 from-remote 브랜치를 복사하고, 이후에도 로컬의 from-remote 브랜치와
# 원격의 from-remote 브랜치를 연동하겠다는 의미함
git switch -t origin/from-remote
```

### 원격의 브랜치 삭제

```bash
# 원격의 브랜치 삭제
git push (원격 이름) --delete (원격의 브랜치 명)

ex) git push origin --delete from-remote
```

---

# 참고

- 얄코, github 강의
- [https://github.com/JaeYeopHan/Minimal_Git_command?tab=readme-ov-file#remote-repository-등록하기](https://github.com/JaeYeopHan/Minimal_Git_command?tab=readme-ov-file#remote-repository-%EB%93%B1%EB%A1%9D%ED%95%98%EA%B8%B0)
