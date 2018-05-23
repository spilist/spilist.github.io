---
title:  "레거시 React 앱에 Prettier + ESLint/StyleLint 적용하기"
tags: [JavaScript, React, Prettier, ESLint, StyleLint]
---

개요

- lint에 대한 소개
  - https://velopert.com/3671
- 우리의 상황
  - 레거시 React 앱이 있었다
  - 스타일 가이드는 위키로 존재했으나 사람들이 크게 신경쓰지 않았다
  - 개발자가 점점 많아지면서 스타일을 일치시키고 코드 리뷰의 효율을 올릴 필요가 생겼다
  - eslint, stylelint 도입
  - 수동으로 고치다 보니 귀찮음
  - prettier 세팅하면서 강제 포맷팅
- 당신의 레거시 앱에 처음으로 Prettier, ESLint, StyleLint를 적용한다고 가정하고 과정 설명해줌.
  - ESLint 설치. airbnb rule 적용
    - 본인이 사용하는 editor에 플러그인 추가 (atom 예시)
  - StyleLint 설치. 우리는 sass를 사용하므로 extend.
    - 본인이 사용하는 editor에 플러그인 추가 (atom 예시)
  - Prettier 설치. eslint rule로 적용되게 함.
    - 본인이 사용하는 editor에 플러그인 추가 (atom 예시)
    - atom plugin option에서 eslint, stylelint integration.
    - auto format on save.
  - 팀에 적용하기.
    - package.json 커맨드로 만들기. https://yarnpkg.com/lang/en/docs/cli/run/
    - 전체 auto fix를 돌리고, 모두의 에디터에 linter와 prettier 설치하게 하기.



https://github.com/airbnb/javascript

https://prettier.io/docs/en/install.html

https://github.com/stylelint/stylelint

https://github.com/stylelint/stylelint-config-standard

https://github.com/kristerkari/stylelint-scss

https://github.com/kristerkari/stylelint-config-recommended-scss

https://git.elicer.io/elice/module-run