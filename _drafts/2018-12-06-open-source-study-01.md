---
title: "오픈소스 스터디 기록"
tags: ["Open Source", "Study", "AWS Codedeploy Agent"]
---

8월 3일부터 전 직장 동료이자 절친인 [김정훈님](https://wonderer80.github.io/), [이지민님](http://americanopeople.tistory.com/)과 함께 매주 수요일 저녁에 스터디를 하고 있다. 첫 10주동안에는 [제랄드 와인버그](https://en.wikipedia.org/wiki/Gerald_Weinberg) 옹의 [Quality Software Management](https://www.amazon.com/Quality-Software-Management-Systems-Thinking/dp/0932633722)라는 고전을 함께 읽으며 토론하는 스터디였다. 그 다음 6주는 오픈소스 스터디였는데, [AWS CodeDeploy](https://aws.amazon.com/ko/codedeploy/)라는 아마존의 코드 배포 서비스의 버그 하나를 분석해서 [Pull Request](https://github.com/aws/aws-codedeploy-agent/pull/199)를 올리는 데 성공했다.

스터디 참여자 모두 오픈소스 프로젝트를 사용만 해봤지, 소스코드를 깊게 파보거나 제대로 기여를 해본 경험은 없었다. 그래서인지 6주라는 길다면 긴 시간동안 겨우 버그 하나밖에 고치진 못했지만, 스터디 과정 자체가 꽤 흥미로웠기 때문에 기록으로 남긴다.

### 시작하기까지 ###

QSM Volume 1-1 스터디를 끝내고 회고를 하며 다음 스터디는 어떤 주제로 할지 논의했다. 여러가지 후보가 있었는데:

1. QSM, 또는 와인버그의 다른 책을 비슷한 방식으로 이어서 읽기
2. 백엔드 기술 전문성을 높이는 활동 (2년 뒤 취업준비할 때 나의 선택의 폭 넓히기)
3. 공동으로 글쓰기 (팀블로그)
4. 공동으로 스택오버플로우 답변달기
5. 퍼실리테이션, 팀빌딩 액티비티 실습
6. 오픈소스 프로젝트 만들어서 개밥먹기로 학습
7. 강의자료, 학습자료 만들기
8. **기존의 오픈소스 프로젝트 코드 분석해서 코멘트 남기고 PR 올려보기. + 이슈 답변 달아주기**

카페에서 즐겁게 얘기만 하다 보니 정확히 여기서 어떻게 오픈소스로 결정됐는지는 기억나지 않지만, 책으로 스터디를 해봤으니 다른 쪽으로 스터디를 해보자는 것에는 빠르게 합의했던 것 같다. 특히 모두 백엔드 개발자였기에, 백엔드 프로그래밍과 관련된 것으로 해보고 싶었다.

### 대상 프로젝트 선정 ###

각자 몇가지 github 저장소를 후보로 가져왔다. [elasticsearch](https://github.com/elastic/elasticsearch), [AWS code deploy agent](https://github.com/aws/aws-codedeploy-agent), [rspec](https://github.com/rspec/rspec) , [redis](https://github.com/antirez/redis), [git](https://github.com/git/git), [pytest](https://github.com/pytest-dev/pytest), [redash](https://github.com/getredash/redash), [django oscar](https://github.com/django-oscar/django-oscar). 스터디 참여자들이 주로 다뤄왔던 언어가 Ruby였던 관계로, C로 구현된 프로젝트는 모두 순식간에 제외되었다. 그래도 여전히 후보가 많아서 선택하기 어려웠는데, 선택의 폭을 좁혀준 것은 이 기준이었다. `커밋 수가 가장 적은 프로젝트`. 

우리는 실제 문제를 푸는 데 기여하고 싶었고, 너무 많은 시간을 투자하기는 원치 않았기에, 레거시가 적고 파악해야 하는 코드의 양이 적은 프로젝트를 선택하고자 했다. `AWS code deploy agent`는 커밋 수도 적고 역사도 깊지 않았으며, 최근까지도 활발하게 개발이 이루어지고 있었다. 소스코드도 Ruby로 되어있었고 우리 모두 AWS에 관심이 있었으니 훌륭한 선택이라고 생각했다.

### 스터디 환경 셋업 ###

