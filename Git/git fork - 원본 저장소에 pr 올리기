## **git fork**

  다른 사람의 레포지토리에서 어떤 부분을 수정하거나 추가하고 싶을 때 `해당 레포지토리를 내 깃허브로 복제`하는 기능 

  fork한 저장소는 원본 레포지토리와 연결되어 있어서, 원본 레포지토리에 변화가 생기면(새로운 commit 등) 포크 해온 레포지토리에 반영 가능

이 때 fetch나 rebase의 과정이 필요하다.

## **clone vs fork**

**clone**

- 기존의 원본 저장소와 연결되지 않음
- 레포지토리의 커밋 등 로그를 보지 못함

**fork**

- 원본 저장소에 변경 사항을 적용하고 싶으면 해당 저장소에 pull request 해야함
- PR이 원본 저장소의 관리자에게 승인받으면 코드가 commit, merge되어 original에 반영

## **git fork**

1. 제출한 repo fork한 후

2. git clone <개인 repo url>

3.  PR 보낼 저장소 주소를 upstream이라는 이름으로 추가

- git remote add upstream <PR 보낼 원본 repository 주소>

4. upstream 원격 저장소들이 잘 추가되었는지 확인

- git remote -v

5. upstream 원격 저장소의 최신 상태를 반영

- git fetch upstream
- git rebase upstream/main

6. pr올릴 브랜치를 생성 후  merge 하기

- git switch -c new-branch
- new branch에 해당 내용 merge 하기
- add, commit
- git push origin <작업했던 내 브랜치 이름>
- 원본 저장소에서 Compare & pull request 버튼 클릭
- PR 작성

# 참고

- [https://velog.io/@imacoolgirlyo/Git-fork와-clone-의-차이점-5sjuhwfzgp](https://velog.io/@imacoolgirlyo/Git-fork%EC%99%80-clone-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-5sjuhwfzgp)