---
title: "정리: 5월에 읽고 공부한 글들"
tags: ["Readings"]
---

회사 위치가 바뀌면서 출퇴근 시간이 80분 가량으로 늘었다. 원래 좀 멍하니 보냈던 이 시간동안 폰으로 글을 읽기 시작했더니 꽤 많은 글을 읽게 됐다. 그동안의 패턴을 보니 읽을 글은 대략 이런 경로를 통해 얻는다.

- Medium Weekly Digest
  - 매주 금요일에 내가 팔로우한 사람이나 내가 관심 표명한 주제, 글 등에 기반하여 읽을 글들을 보내준다.
  - 여기서 좋은 글을 읽으면 그 글을 쓴 사람이나 그룹의 글을 앞뒤로 더 찾아서 읽는다.
  - 요즘 미디엄에서 가장 많은 글을 읽다 보니 점점 더 큐레이션이 잘 되는 느낌이다.
- [Outsider 님의 기술 뉴스](https://blog.outsider.ne.kr/category/Newsletter)
  - 2주에 한 번씩, 웹개발이나 프로그래밍 전반에 관련된 글, 그밖에 읽을 만한 흥미로운 글들을 본인의 코멘트와 함께 올려주신다. 
  - 관심사가 비슷해서인지 올려주시는 글 중 재밌게, 유용하게 읽은 글이 많다.
- [jhrogue 님의 기술 뉴스](http://jhrogue.blogspot.com/search/label/B%EA%B8%89%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8)
  - 이 분도 1~2주에 한 번씩 읽을 만한 글들을 올려주신다.
  - 별다른 설명 없이 딱 링크만 올리시는데다가 관심분야가 살짝 달라서 생각보다는 읽을 글을 많이 건지지는 못한다.
- Facebook
  - 개발자 페친이 많다 보니 각종 스타트업이나 기술 소식을 페북을 통해서도 알게 되는 경우가 종종 있다.
- 문제해결 과정에서의 구글링
  - 회사에서 개발하면서 겪는 각종 문제를 해결하다 보면 공식 문서를 파고들거나 개념을 설명해주는 글도 많이 읽게 된다.

카테고리별로 분류하면서 코멘트를 좀 남겨보자.

----

###UI/UX 디자인

월 초에 의욕이 넘쳐서 읽는 것들을 많이 번역했는데 우연히도 거의 디자인 쪽이었다.

- [Design better forms](https://uxdesign.cc/design-better-forms-96fadca0f49c): 입력 폼을 디자인할 때 흔히 하는 실수들과, 그걸 어떻게 고칠 수 있는지 보여주는 글이다. 블로그에 [요약 번역](https://spilist.github.io/2018/05/08/design-better-forms.html)했다.
- [Design better data tables](https://uxdesign.cc/design-better-data-tables-4ecc99d23356): 성공적인 데이터 테이블 UI의 요소들에 대해, 어떤 기능들이 어떨 때 필요한지 보여주는 글이다. 블로그에 [요약 번역](https://spilist.github.io/2018/05/10/design-better-data-tables.html)했다.

### CSS

- [Scroll to the future](https://evilmartians.com/chronicles/scroll-to-the-future-modern-javascript-css-scrolling-implementations): 스크롤과 관련된 여러가지 기능들은 대부분 ‘모든 브라우저에서 잘 작동’하게 하기 위해 자바스크립트로 작성되어 왔다. 한편 웹의 스탠다드는 빠르게 발전하고 있으며, 최신 CSS와 DOM API가 새 버전의 브라우저들에 지원되면서 자바스크립트로 만들어진 이런 기능들이 더 간편한 코드로, 더 좋은 성능으로 대체될 수 있는 가능성이 생겼다. (글이 작성된 시점인 2018년 4월 12일 기준으로) 어떤 기능들은 브라우저에서 바로 지원되고 어떤 기능들은 polyfill을 써야만 지원되지만, 적어도 자바스크립트로 모든 기능을 구현하는 게 유일한 해답이 아니라는 것은 확실하다. 어떤 예시들이 있는지 블로그에 [요약 번역](https://spilist.github.io/2018/05/11/scroll-to-the-future.html)했다.

### JavaScript

- 실행 컨텍스트와 scope: 블로그 정리글. bind를 잊어서 에러가 나는 경우도 많고, React에서 bind를 어떻게 하느냐가 성능에 영향을 준다는 말도 많이 봐서 이것저것 읽어보고 정리했다.