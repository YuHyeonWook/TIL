# Git **diff, Git blame, Git bisect**

## Git **diff**

- 워킹 디렉토리의 변경사항 확인

```jsx
# 워킹 디렉토리의 변경사항 확인
git diff

# 파일명만 확인
git diff --name-only

# 스테이지의 확인
git diff --staged
	# --cached와 같음

# 커밋간의 차이 확인
# ex) git diff HEAD~~ HEAD10
	# 지난 커밋과 10개 전 차이를 확인함
git diff (커밋1) (커밋2)
	# 커밋 해시 또는 HEAD 번호로
	# 현재 커밋과 비교하려면 이전 커밋만 명시

# 브랜치간의 차이 확인함
git diff (브랜치1) (브랜치2)
```

<br/>

## git blame

- 각 라인의 작성자를 확인함

```jsx
# 각 라인의 작성자를 확인함
git blame

# 파일의 부분별로 작성자 확인하기
git blame (파일명)

# 특정 부분 지정해서 작성자 확인하기
git blame -L (시작줄) (끝줄, 또는 +줄수) (파일명)
```

- **VS Code의 GitLens 확장 사용하면 편함**

<br/>

## **git bisect**

- 이진 탐색 알고리즘으로 문제의 발생 시점을 찾아냄

```jsx
# 이진 탐색 알고리즘으로 문제의 발생 시점을 찾아냄
git bisect

# 이진 탐색 시작
git bisect start

# 오류발생 지점임을 표시
git bisect bad

# 의심 지점으로 이동
git checkout (해당 커밋 해시)

# 오류 발생 않을 시 양호함 표시
git bisect good
# ♻️ 원인을 찾을 때까지 반복
	# git bisect good/bad

# 이진 탐색 종료
git bisect reset
```
