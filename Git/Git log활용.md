# Git log 활용

**옵션들을 활용한 다양한 사용법**

```jsx
# 각 커밋마다의 변경사항 함께 보기
git log -p

# 최근 n개 커밋만 보기
git log -(갯수)

# 통계와 함께 보기
git log --stat
	# 더 간략히: --shortstat

# 한 줄로 보기
git log --oneline
	# --pretty=oneline --abbrev-commit의 줄임

# 변경사항 내 단어 검색
git log -S (검색어)
	# (검색어)로 검색함

# 커밋 메시지로 검색
git log --grep (검색어)

# 자주 사용되는 그래프 로그 보기 - (sourcetree로 보는게 더 편함)
git log --all --decorate --oneline --graph
# --all : 모든 브랜치 보기
# --graph : 그래프 표현
# --decorate : 브랜치, 태그 등 모든 레퍼런스 표시
	# --decorate=no
	# --decorate=short : 기본
	# --decorate=full
```

<br/>

<aside>
📌 참고 : [https://git-scm.com/book/ko/v2/Git의-기초-커밋-히스토리-조회하기#limit_options](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%BB%A4%EB%B0%8B-%ED%9E%88%EC%8A%A4%ED%86%A0%EB%A6%AC-%EC%A1%B0%ED%9A%8C%ED%95%98%EA%B8%B0#limit_options)

</aside>
