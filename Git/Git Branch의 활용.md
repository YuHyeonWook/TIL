# Git Branch의 활용

## Git에서 `merge`가 이뤄지는 두 방식 **Fastforward**와 **3-way-merge**

### **Fastforward**

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/9c472cff-a5d9-44f6-8f67-0ce773962665)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/13c97ca5-28e7-4555-889c-29cbac6be931)


- A와 B를 병합할때 굳이 다른 커밋을 만들지 않고, A 브랜치를 오른쪽 그림 처럼 옮김
- 즉, 커밋 하나를 새로 만들지 않고 ‘빨리 감기'를 해버린 것 이다.
- 단점 : 어떤 브랜치를 사용했고 언제 병합했는 기록이 남지 않음

  ```yaml
  # 병합 두 가지 방법

  git merge (병합할 브랜치명)

  # ff는 **Fastforward 이다.**
  git merge --no-ff (병합할 브랜치명)
  ```

### **3-way-merge**

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/a8eeb33f-490f-471d-b2ef-75f6a4a77752)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/e3833394-3b65-4284-ba8d-2fdafeb87790)


- A와 B의 공통 조상인 빨간색 밑줄인 커밋의 내용과 A와 B를 대조해서 3-way가 되는 것이다.

<br/>

## Branch

```yaml
# 다른 브랜치의 원하는 커밋 가져오기
git cherry-pick (체리의 해시)
	# fruit 브랜치의 Cherry와는 별개의 커밋

# 다른 브랜치에서 파생된 브랜치 옮겨붙이기
git rebase --onto (도착 브랜치) (출발 브랜치) (이동할 브랜치)
# ex) git rebase --onto main fruit citrus
# ex) git rebase --onto main에 다가 fruit에 있는 citrus를 옮겨붙임

# 다른 커밋들을 하나로 묶어 가져오기
git merge --squash (대상 브랜치)
	# 변경사항들 스테이지 되어 있음
	# git commit 후 메시지 입력

```

<br/>


### **일반 merge와** merge --squash**의 차이 정리**

- 일반 merge와 **merge --squash**는, 실행 후 코드의 상태는 같지만 내역 면에서 큰 차이가 있다.
  - 일반 merge : A와 B 두 브랜치를 한 곳으로 이어붙임
  - merge --squash : B 브랜치의 마디들을 복사해다가 한 마디로 모아 A 브랜치에 붙임 (staged 상태로)



<br/>

## 협업을 위한 브랜치 활용

### **Gitflow**

- 협업을 위한 브랜칭 전략임

Gitflow 그림)

![image](https://github.com/YuHyeonWook/TIL/assets/110236953/4ba3203a-666c-44ec-a738-74ac942dc89c)

<br/>

### **사용되는 브랜치들**

| 브랜치  | 용도                            |
| ------- | ------------------------------- |
| main    | 제품 출시/배포                  |
| develop | 다음 출시/배포를 위한 개발 진행 |
| release | 출시/배포 전 테스트 진행(QA)    |
| feature | 기능 개발                       |
| hotfix  | 긴급한 버그 수정                |
