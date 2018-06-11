---
title: "디버그를 디버깅하기: 디버그라는 단어의 함정"
tags: ["Software Development", "Debugging", "Problem Solving"]
---





![The very first recorded computer bug](https://cdn0.tnwcdn.com/wp-content/blogs.dir/1/files/2013/09/bug.jpg)

- 문제 해결(디버깅) 템플릿 겸 체크리스트
- 디버그의 어원
  - https://en.m.wikipedia.org/wiki/Software_bug
  - https://thenextweb.com/shareables/2013/09/18/the-very-first-computer-bug/
  - 벌레가 낌. 벌레를 제거
  - 벌레가 끼지 않게 하는 환경
  - 벌레가 꼈을 때 알 수 있게 함
  - 벌레를 자동으로 주기적으로 청소
- 디버그라는 단어에서 연상되는 것은 버그를 제거하는 것. 실제로 많은 개발자들이 그냥 버그를 없애는 데 집중한다. 
- 정훈님의 말. 
  - 훌륭한 개발자는 버그를 만났을 때 그걸 단지 빠르게 고치는 게 아니라, 버그가 생길 수밖에 없었던 근본적 원인을 생각해보고 개선하는 기회로 삼는다.
- 훌륭한 개발자는 저 과정이 자동으로 될 수 있겠지만 나같은 평범한 개발자는 분석적으로 접근해야 함
- 디버그를 5단계로 나눈다.
  - 현상
  - 재현 조건
  - 문제 원인
  - 해결 방법
  - 환경 개선
- 버그의 시초와, 내가 실제로 겪은 버그로 예시. 
- 체크리스트.
- 버그에서 환경 개선으로 가려면 패턴을 찾는 훈련이 필요. 이건 다음 글에서.