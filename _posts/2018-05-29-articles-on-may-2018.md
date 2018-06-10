---
title: "2018년 5월, 읽고 공부한 것들"
tags: ["Readings"]
---

회사 위치가 바뀌면서 출퇴근 시간이 80분 가량으로 늘었다. 원래 좀 멍하니 보냈던 이 시간동안 폰으로 글을 읽기 시작했더니 꽤 많은 글을 읽게 됐다. React와 자바스크립트에 대한 글도 상당히 많이 읽었지만 기술적인 내용들은 가능하면 개별적인 글로 정리하기로 하고, 나머지 중 기록해둘 만한 글들을 정리해본다.

### 글이 내게 오는 과정

우선, 그동안의 패턴을 보니 읽을 글은 대략 이런 경로를 통해 얻는다.

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

---

### 개발문화/철학

- [Hype driven development](<https://blog.daftcode.pl/hype-driven-development-3469fc2e9b22>): 새롭거나 유명한 기술이 현재 자신과 팀의 상황에 맞는지에 대한 고찰과 분석 없이 도입되는 것을 경고하는 재밌는 글이다. 읽고 나서 번역하려고 했더니 '설레발 주도 개발'이라는 아주 멋진 제목으로 [번역된 글](https://lazygyu.net/blog/hype_driven_development)이 있었다. 
- [리모트 근무는 실화고 사무실은 먹는 것](https://medium.com/@sybae/리모트-근무는-실화고-사무실은-먹는것-0편-65d9aa8dced1): [세일즈부스트](https://medium.com/@blaswan/salesboost-recruit-2c1248aa394a)라는 기업에서 슬랙 봇 서비스인 [Standuply](https://standuply.com/)를 이용해서 어떻게 원격 근무 환경에서 효과적으로 컨텍스트를 공유하는지에 대한 글이다. 자율적인 원격 근무는 직원 입장에서 아주 훌륭한 근무형태로 여겨지지만, 실제로 실행해 보면 암묵적 의사소통의 부재로 인한 문제가 작지 않다. 최근 우리 팀도 이런 문제를 느껴 해결책을 고심하고 있었는데 여기서 소개된 슬랙 봇을 테스트해볼 예정이다.
- [Designing very large (JavaScript) applications](https://medium.com/@cramforce/designing-very-large-javascript-applications-6e013a3291a3): 구글에서 오래 프론트엔드 개발자로 일했던 [Malte Ubi](https://medium.com/@cramforce?source=post_header_lockup) 가 거대한 앱을 구축할 때 고려해야 할 점들에 대해 발표한 글이다. 원문은 컨퍼런스 발표 스크립트의 거의 무편집 버전이라, 구조화도 잘 안 되어있고 몇몇 부분은 이해하기 쉽지 않았지만 충분히 좋은 인사이트를 주는 좋은 글이었다. 고생해서 블로그에 [전문 번역](https://medium.com/steady-study/번역-아주-거대한-자바스크립트-어플리케이션을-구축하기-3aa37fc45122)했다.
- [인간답게 코드 리뷰하기](https://www.slideshare.net/codetemplate/2018-01code-review-95601233): 코드리뷰가 어려운 이유, 그리고 코드리뷰를 효과적으로 하는 8가지 방법에 대한 글([1부](https://mtlynch.io/human-code-reviews-1/), [2부](https://mtlynch.io/human-code-reviews-2/))이 정리된 슬라이드다. 개발팀에서 코드 리뷰가 잘 이뤄지지 않고 있다면 특히 추천.

- [The Mistakes I Made As a Beginner Programmer](https://medium.com/@samerbuna/the-mistakes-i-made-as-a-beginner-programmer-ac8b3e54c312): 필자가 초보 개발자 시절에 저질렀다고 하는 25가지 실수에 대한, 상당히 길지만 대충이라도 읽어볼 만한 글이다. 좋은 개발자가 되려면 어떤 태도를 가져야 하는가? 라는 질문에 대해 괜찮은 길을 제시해준다. 프로젝트 회고 등을 할 때 체크리스트로 써봐도 괜찮을 것 같다.


### UI/UX 디자인, CSS

- [Design better forms](https://uxdesign.cc/design-better-forms-96fadca0f49c): 입력 폼을 디자인할 때 흔히 하는 실수들과, 그걸 어떻게 고칠 수 있는지 보여주는 글이다. 블로그에 [요약 번역](https://spilist.github.io/2018/05/08/design-better-forms.html)했다.
- [Design better data tables](https://uxdesign.cc/design-better-data-tables-4ecc99d23356): 성공적인 데이터 테이블 UI의 요소들에 대해, 어떤 기능들이 어떨 때 필요한지 보여주는 글이다. 블로그에 [요약 번역](https://spilist.github.io/2018/05/10/design-better-data-tables.html)했다.
- [I Got Rejected by Apple Music… So I Redesigned It](https://medium.com/startup-grind/i-got-rejected-by-apple-music-so-i-redesigned-it-b7e2e4dc64bf): Apple Music의 인턴십에 지원했다가 떨어진 사람이 Apple Music 앱을 자기 나름대로 분석하여 다시 디자인한 과정을 적은 글이다. 글 내용 자체보다도 입사 실패의 다음 액션이 '자신만의 앱 재설계'로 삼고, 그 과정을 기록하는 태도가 멋지다. 참고로 이 사람은 결국 [입사에 성공](http://jasonyuan.design/about)했다.
- [Scroll to the future](https://evilmartians.com/chronicles/scroll-to-the-future-modern-javascript-css-scrolling-implementations): 스크롤과 관련된 여러가지 기능들은 대부분 ‘모든 브라우저에서 잘 작동’하게 하기 위해 자바스크립트로 작성되어 왔다. 이제 최신 CSS와 DOM API가 새 버전의 브라우저들에 지원되면서 자바스크립트로 만들어진 이런 기능들이 더 간편한 코드로, 더 좋은 성능으로 대체될 수 있는 가능성이 생겼다. 어떤 예시들이 있는지 블로그에 [요약 번역](https://spilist.github.io/2018/05/11/scroll-to-the-future.html)했다.
- [CSS at Scale: LinkedIn’s New Open Source Projects Take on Stylesheet Performance](https://engineering.linkedin.com/blog/2018/04/css-at-scale--linkedins-new-open-source-projects-take-on-stylesh): CSS 셀렉터의 성능 문제는 크게 신경쓸 필요가 없다고는 하지만, 사이트가 아주 거대해지면 이야기가 다르다. 이 글은 링크드인에서 너무 비대해진 CSS의 문제를 인지하고, 불필요한 CSS 클래스 정의를 최적화하면서 코드 분할을 적용함으로써 CSS 파일 번들의 크기를 90% 이상 줄인(156KB -> 9KB) 과정을 보여준다. 이정도로 최적화를 해낸 것도 놀랍지만, 자신들이 적용한 기술을 [CSS Blocks](http://css-blocks.com/) 와 [OptiCSS](https://github.com/linkedin/opticss) 라는 오픈소스 라이브러리로 공개한 것도 놀랍다.

### React

- [카카오페이지 웹 React 포팅 후기](https://medium.com/@ljs0705/카카오페이지-웹-react-포팅-후기-76402cc5e031): 정성들인 개발 후기를 읽는 건 언제나 즐겁다. 많은 유저가 사용하는 거대한 서비스를 React로 옭기면서 다양한 기술적 결정을 어떤 이유로 어떻게 결정했는지를 자세히 설명해주는 좋은 글이다. 이 글을 읽고 몇 가지 유용한 키워드와 라이브러리를 알게 됐다.
- [리액트 도움닫기 한국어 번역서를 출간하며](https://sujinlee.me/the-road-to-learn-react-korean/): [The Road to learn React](https://leanpub.com/the-road-to-learn-react)라는 리액트 튜토리얼 책을 번역한 과정에 대한 글이다. 번역에 참여하게 된 계기와 번역 자체 과정, 퇴고를 위해 어떻게 했는지 등 전체 과정이 잘 나와있어서 흥미롭게 읽었다. 참고로 책의 저자인 Robin Wieruch는 [모두에게 리액트를 배울 수 있는 기회를 주고자 이 책을 오픈 소스로 출판했다.](https://www.robinwieruch.de/giving-back-by-learning-react/)
- [Performance-tuning a React application - A Case Study](https://codeburst.io/performance-tuning-a-react-application-f480f46dc1a2): [Tello](https://tello.tv/)라는 웹앱의 성능을 프로파일링하고, 압축, 캐싱, 동적 이미지 크롭, 레이지 로딩, 코드 분할 기법을 활용하여 최적화한 과정을 자세히 적은 글이다. 서버사이드 렌더링을 비롯한 어떤 기법들은 왜 사용하지 않았는지 등도 적혀 있어 유용했다. 정말 여러가지를 배울 수 있었던 글이다.

### 함수형 프로그래밍

- [Goodbye, Object Oriented Programming](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53): 객체 지향 프로그래밍의 장점으로 꼽히는 상속(inheritance), 캡슐화(encapsulation), 다형성(polymorphism)이 복잡한 어플리케이션에서 어떤 문제를 가지고 있는지 보여주고, 결론적으로 함수형 프로그래밍 쓰라는 영업글이다. OOP 단점이 잘 드러난 글이긴 하나, 내용과는 별개로 이런 형식의 글을 그다지 좋아하진 않는다. 모든 도구는 상황에 맞는 쓰임새가 있는 건데 이런 글은 '무조건 OOP가 구리고 FP가 좋다'는 식으로 생각하게 유도하는 느낌이라서다. 모든 상황에 들어맞는 [만병통치약은 없다](http://www.cs.nott.ac.uk/~pszcah/G51ISS/Documents/NoSilverBullet.html).
- [Learning functional programming and compositional software techniques in JavaScript ES6+ 시리즈](https://medium.com/javascript-scene/composing-software-an-introduction-27b72500d6ea): 함수형 프로그래밍을 주로 하던 개발자가 ES6 이후의 자바스크립트에 입문하고자 할 때 필요한 지식을 여러 글에 걸쳐 설명해주는 시리즈다. 기초 지식과 고급 개념이 섞여있긴 하지만 자바스크립트 개발자라면 시간을 들여 읽을 만하다.

### 블록체인

- [문돌이도 이해하는 스팀 디앱 (DApp)의 세계](https://steemit.com/kr/@project7/dapp): 비트코인 붐 이후로 블록체인 기술이 여기저기서 많이 들린다. 디앱(DApp, Decentralized Application)은 블록체인을 이용해서 만들어진 탈중앙화된 앱을 지칭한다. 많은 디앱들이 (게임 플랫폼 [스팀Steam](https://store.steampowered.com)이 아닌) [스팀Steem](https://steem.io)에 올라오는데, 그 생태계에 대해 설명해준 글이다.
- [Why Everyone Missed the Most Important Invention in the Last 500 Years](https://hackernoon.com/why-everyone-missed-the-most-important-invention-in-the-last-500-years-c90b0151c169): 지난 500년간 있었던 발명 중 가장 중요한 발명이 [삼식부기(Triple-entry accounting)](https://blockinpress.com/archives/3330)라고 주장하는, 좀 방정맞게 쓰여졌지만 재밌었던 글이다. 내맘대로 요약해보면 대강 이렇다.
  - 5000년 전 '누가 나에게 얼마를 빌렸다'고 기록하는 단식부기를 통해 '거래', 즉 경제활동이 시작되었다. 
  - 600년 전, 사람들은 점점 더 멀리 있는 사람들 - 때론 얼굴 한 번 못 본 사람과도 거래를 시작했고, 기록이 기록으로 옮겨가면서 생기는 오류를 복식부기를 통해 줄일 수 있었다. 
  - 그리고 2005년, 암호학자 [Ian Grigg](https://twitter.com/iang_fc?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)이 거래의 정당성을 탈중화된 제 3자가 담보하는 삼식부기 시스템을 선보였고, 그로부터 몇 년 후 비트코인이 등장했다. 
  - 삼식부기 시스템은 정말 많은 것들을 바꿔나갈 것이다. 선거도 그 좋은 예다.

### 기타 읽을거리

- [이 세대의 공부](https://brunch.co.kr/@yoojs8512/81): 중국의 대표적인 유료 구독 지식 플랫폼인 논리사유에서, 대표인 뤄전위가 자신의 200회에 걸친 방송을 마무리하면서 논한 '이 세대의 공부'에 대한 훌륭한 글이다. 뤄전위가 '지적 초조함'을 해결하기 위해 제시한 다섯가지 방법은 다음과 같다.
  - 첫째, 책이 아닌 뛰어난 사람을 쫓아 공부하라는 겁니다.
  - 둘째, 신 개념을 장악해 스스로의 지식 창고를 만들어야 합니다. 새로운 정보를 어디에 둬야할지를 알 수 있기 때문입니다.
  - 셋째, 봉합입니다. 정보는 스쳐지나갈 뿐입니다. 기억할 방법이 없죠. 이를 봉합하기 위해 한 문장이라도 표현해야 합니다.
  - 넷째, 파편화입니다. 파편화된 시간 속에서 공부법을 찾아야만 합니다.
  - 다섯째, 당연히 목표가 가장 중요합니다. 확실한 목표가 있어야만 나아갈 수 있고 상과를 거둘 수 있습니다. 
- [Stop Trying To Memorize — A Good Book Will Change You](https://medium.com/swlh/stop-trying-to-memorize-a-good-book-will-change-you-2bebafb22203): 위에서 나온 '지적 초조함'을 해소하는 또다른 방법, 어쩌면 위 글과 반대되는 것 같지만, 실제로는 보완해주는 방법을 알려주는 글이다. 좋은 글을 읽고 좋은 경험을 하면 자연스럽게 세상을 보는 모델이 달라질 것이므로, 읽은 것을 모두 기록하고 기억하려고 강박적으로 행동할 필요가 없다는 것.
- [Fake Experts Abound. Here’s How to Find (and Be) a Real One.](https://mobile.nytimes.com/2018/04/20/your-money/experts-david-baker.html): 사실 이 링크는 요즘 읽고 있는 [The Business of Expertise](https://www.amazon.com/Business-Expertise-Entrepreneurial-Experts-Convert/dp/1605440604)라는 책의 영업글이다. 서론 부분에 대강 이런 말이 나오는데, 사실상 여기에 꽂혀서 책을 샀다. "지식은 패턴 인식에 기반하고, 패턴을 인지하려면 유사한 시나리오에 여러 번 노출되어야 하며, 그러려면 좋은 포지션을 잡아야 한다. 이게 전문성을 기르는 핵심이다." 기술서적이 아니라서인지 단어가 너무 어려워서 수월하게 읽지는 못하고 있지만, 좋은 인사이트를 주는 책이다. 이거 읽느라 다른 글을 못읽고 있어 좀 아쉬울 뿐.
- [5 Essential Investments Every Human Being Should Make In Themselves](https://medium.com/the-mission/5-essential-investments-every-human-being-should-make-in-themselves-121771565384): 몸의 건강, 마음의 건강, 새로운 지식에 대한 공부, 전문성 기르기, 집/옷/차 등 물리적 환경. 이 다섯 가지에 충분히 돈과 시간을 투자해야 장기적으로 행복한 삶을 살 수 있다는 글이다.
- [사이드 프로젝트, 10년간의 기록](https://medium.com/@jungil.han/사이드-프로젝트-10년의-기록-파트-1-63bc25f8dcfc): [한로니 님](https://medium.com/@jungil.han?source=post_header_lockup)이 10년간 사이드 프로젝트 25개를 개발하신 경험을 공유한 첫 번째 글이다. (2012년까지가 1부고 아직 2부가 안나왔다.) 사이드 프로젝트를 개발한다는 건 나를 포함하여 개발자의 로망 같은 것이다. 나는 로망을 실현하신 분들을 보면 예전엔 멋지다, 부럽다고 생각했는데 지금은 '나도 해야지'로 바뀌게 된 게 재밌다.
- [우리는 왜 관리역량을 과소평가하는가?](http://m.hbrkorea.com/magazine/article/view/7_1/page/1/article_no/1047): 기존의 MBA에서는 기업이 내부 관리역량을 높여서 경쟁에서 이기려 해서는 안된다고 가르친다. 관리 프로세스는 쉽게 모방할 수 있기 때문에, 운영을 탁월하게 하는 게 중요하다는 것. 그러나 실제로는 1) 탁월한 프로세스를 쉽게 모방하기 어렵기 때문에, 2) 프로세스의 질적 차이가 시간이 지나도 줄어들지 않으며, 3) 효과적 관리 프로세스가 전략적 성공과 높은 상관관계가 있다. 이 글은 관리역량의 중요성과 함께 네 가지 영역 - 운영 관리, 성과 모니터링, 목표 설정, 인재 관리 영역에서의 핵심 관리 측면이 무엇인지 보여준다.