---
title: "내맘대로 정리한 Chrome Developer Summit 2020"
tags: ["Conference"]
---

[Chrome Developer Summit 2020](https://www.youtube.com/playlist?list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR) 에서 내가 몰랐던 거나 메모할 만한 것만 정리해본다. 나중에 검색할 수 있게.



#### CSS, UX

- [ Extending CSS with Houdini](https://www.youtube.com/watch?v=5eBar5TI71M&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=4)
  - [https://houdini.how/](https://houdini.how/) → worklet library
  - houdini.. 후디니.. 처음 들어봤다. 직접 CSS 속성을 만들어낼 수 있음. 어떤 worklet은 애니메이션 파일을 import하는 것과 비슷한 효과를 낼 수도 있을듯.
- 좋은 Form design에 대한 영상들. 매우 실전적인 팁들이 들어있어서 좋았다. 디자인 시스템 구현할 때라든가, 핵심 유저 퍼널 개선할 때라든가, 따로 한번 정리할 가치도 있어 보임.
  - [Sign-up form best practices](https://www.youtube.com/watch?v=Ev2mCzJZLtY&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=27)
    - [https://web.dev/sign-up-form-best-practices/](https://web.dev/sign-up-form-best-practices/)
  - [SMS OTP form best practices](https://www.youtube.com/watch?v=sU4MpWYrGSI&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=28)
    - [https://web.dev/sms-otp-form/](https://web.dev/sms-otp-form/)
  - [Payment and address form best practices](https://www.youtube.com/watch?v=xfGKmvvyhdM&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=35)
    - [https://web.dev/payment-and-address-form-best-practices/](https://web.dev/payment-and-address-form-best-practices/)

#### Core Web Vitals

- [State of speed tooling](https://www.youtube.com/watch?v=_G3X_IsozKk&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=18)

  - Lighthouse에서 Field Data와 Lab Data 두 개에 대한 측정을 지원한다고 한다.
    - Field Data: 몇주간 실제 방문한 유저에게 측정된 데이터
    - Lab Data: 특정 데모그래픽을 가진 유저베이스를 찍어서 측정한 데이터
  - 써드파티 리소스 용량이 꽤 클 수 있는데 이걸 facade 패턴 이용해서 레이지로드할 수 있음.
    - [https://web.dev/third-party-facades/](https://web.dev/third-party-facades/)
    - 실제 유튜브 영상 대신 프리뷰 이미지만 올려두는 식 (3KB VS 540KB)
  - **Core Web Vitals**는 구글이 웹페이지 퍼포먼스 메트릭으로 밀고 있는 3가지 기준이다. 요거 향상시키는 팁들이 이후 영상에서 나옴.
    - LCP(Largest Contentful Paint): **Loading** 상태에 대한 측정
    - FID(First Input Delay), TBT(Total Blocking Time): **Interactivity**에 대한 측정
    - CLS(Cumulative Layout Shift): **Visual Stability**에 대한 측정
    - -> 주요 리액트 프레임워크에서도 CWV 분석을 위한 도구를 내장하고 있다.
      - [https://create-react-app.dev/docs/measuring-performance](https://create-react-app.dev/docs/measuring-performance)

- [Fixing common Web Vitals issues](https://www.youtube.com/watch?v=IB3e8SAdBaE&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=19)

  - CLS 계산하고 리포트하는 방법 보여줌. DevTools의 "Layout Shift Regions" 이용해서 어디가 언제 shifting되는지 시각화할 수 있음.
  - [Search Console](https://search.google.com/search-console/about) 은 지난 28일간 성능 측정 데이터를 URL group 기준으로 보여주는데, 여기서 CLS 이슈를 확인할 수도 있음.
  - 성능 측정에는 구글이 수집한 실제 유저의 방문 데이터를 기반으로 한 [CrUX](https://developers.google.com/web/tools/chrome-user-experience-report) 를 쓸 수도 있고, RUM(Real User Metric)을 직접 수집할 수도 있음

- [UX patterns optimized for Core Web Vitals](https://www.youtube.com/watch?v=EUxrBG_98hQ&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=20)

  - 요약하면 "유저를 놀라게 하지 마세요"
  - Insert new content carefully
    - 페이지 로드 후에 배너나 광고 등을 띄우는 걸로 메인 컨텐츠를 아래로 밀지 마라. [https://web.dev/optimize-cls/](https://web.dev/optimize-cls/)
      - 대신 광고나 배너의 height를 fix해두고 placeholder를 배치했다가 교체하라. 만약 광고할게 없으면 in-house 광고라도 넣어라.
      - 배너 height이 제각각이라서 fix할 수 없다면?
        - 웬만하면 통일할 것.
        - 적어도 min-height를 두면 CLS 정도가 작아진다.
    - 무한스크롤로 인해 푸터가 자꾸 아래로 밀리게 하지 마라. [https://addyosmani.com/blog/infinite-scroll-without-layout-shifts/](https://addyosmani.com/blog/infinite-scroll-without-layout-shifts/)
      - 최하단에 placeholder 등을 이용해 충분한 height를 줘서 컨텐츠가 더 로드될 공간을 확보하라.
  - Give instant feedback
    - 유저 클릭으로 인해 컨텐츠가 생겨날 때는 로딩 끝날 때까지 기다려서 한번에 움직이지 말고, 먼저 placeholder를 보여준 다음 변경하라.
  - Match visuals to reality
    - Javascript 로딩 중에는 버튼 등의 상태를 disabled로 둬라. 즉 클릭 가능할 때 클릭할 수 있게 해라.

- [Optimize for interactivity using Web Vitals (FID/TBT)](https://www.youtube.com/watch?v=WxYpdw5ELrU&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=29)

  - [https://web.dev/fid/](https://web.dev/fid/)
  - 핵심은 유저가 인풋을 넣을 수 있는 (= 메인 쓰레드가 일할 수 있는) 시간을 주라는 것.
  - 특별한 얘기가 많진 않았다. 실제로 FID를 측정하고 향상시키는 건 위 글 참조. 
  - 영상은 실제로 Mercado Libre라는 남미의 쇼핑 사이트의 FID를 개선하는 과정을 보여줘서 참고가 되긴 했음.
    - [https://web.dev/how-mercadolibre-optimized-web-vitals/](https://web.dev/how-mercadolibre-optimized-web-vitals/)

  

#### Performance

- [Transitioning to modern JavaScript](https://www.youtube.com/watch?v=cLxNdLK--yI&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=6)
  - [https://web.dev/publish-modern-javascript/](https://web.dev/publish-modern-javascript/ ) 
  - 우리가 일상적으로 쓰는 대부분의 기능이 이제 대부분의 modern browser에서 지원되고 있다. 따라서 IE11 등을 신경쓰지 않아도 된다면 (e.g., 모바일 앱의 웹뷰로만 페이지를 serving) transpile target을 ES2015로 두고 하위 버전 polyfill을 하지 않음으로써 훨씬 적은 패키지 용량을 달성할 수 있다.
    - 예를 들어, typescript를 쓴다면 `tsconfig.json`에서 target을 `ES2015` 로 두는 식.
  -  [https://estimator.dev/]( https://estimator.dev/) 에서 나의 배포된 웹사이트 성능을 확인할 수 있다.
    - 현재 [캐시노트 웹](https://app.cashnote.kr)으로 확인해보니 압축 안된거 기준 4mb -> 3.5MB 로 12% 번들 용량 크기를 줄일 수 있다고 한다.
    - 캐시노트 2.0에서 참고해야겠다.
- [Beyond fast with new performance features](https://www.youtube.com/watch?v=Z6wjUOSh9Tk&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=23)
  - [https://web.dev/content-visibility/](https://web.dev/content-visibility/)
    - `content-visibility: auto` 쓰면, 뷰포트에 안보이는 children DOM 렌더링을 스킵함.
    - `contain-intrinsic-size: 0 500px` 따위로 height 지정은 해줘야 함. 뷰포트 계산은 해야 하니.
    - 아직 iOS Safari에서는 안되지만 Chrome 85에서는 지원됨. 지원 안해도 break되지는 않으므로 그냥 이득. -> 적용해보자!
  - [Font metrics override descriptors](https://gist.github.com/xiaochengh/da1fa52648d6184fd8022d7134c168c1)
    - 폰트 로드 안돼서 fallback font 갈 때 폰트 자체의 크기나 자간 따위가 달라서 컨텐츠 height / width가 너무 달라지는 거 방지 가능.
  - [Back/forward cache](Back/forward cache)
    - 인메모리 캐시로 페이지 스냅샷을 저장해둠으로써, 페이지 이동 후 이전 페이지에 백버튼 따위로 돌아왔을 때 빠르게 페이지를 표시한다.
      - Chrome 87부터 모든 안드로이드 유저에게 cross-site navigation할 때 제공됨.
      - 데탑 크롬에서 쓰고싶으면 [플래그 켜라](https://www.chromium.org/developers/how-tos/run-chromium-with-flags).
    - 이를 위해서는 `unload` 이벤트를 절대 사용하면 안 된다. 대신 `pagehide` 이벤트를 써라.
    - `beforeunload` 이벤트도 conditional하게 써라. 핸들러를 전역 바인딩하고 그 안에서 조건을 타는 대신 조건에 맞을 때만 이벤트 listner 바인드.
    - window를 열고 싶으면 `opener` 대신 `postMessage` 써라.
    - ongoing connection이 있다면 캐싱 안되니까, navigate away할 때는 커넥션 끊어라.
    - 페이지뷰 이벤트가 제대로 안 잡힐 수 있으니 [이거](https://web.dev/bfcache/#how-bfcache-affects-analytics-and-performance-measurement) 참고해서 변경해라.
    - CWV에도 임팩트 있으니까 코드로 리포트하길.
  - [portals](https://github.com/WICG/portals/blob/master/README.md)
    - iframe처럼, 특정 페이지를 프리뷰해서 보이게 할 수 있는 새로운 html 태그.
      - -> 아직은 쓸 수 있는 곳이 별로 없음 [https://caniuse.com/?search=portal](https://caniuse.com/?search=portal)
    - 잘 쓰면 다음 페이지로의 네비게이션을 훨씬 빠르게 할 수 있음.
    - 나중에 좀 더 널리 지원되면 다시 보자.
  - [https://github.com/GoogleChromeLabs/quicklink](https://github.com/GoogleChromeLabs/quicklink)
    - 뷰포트 안의 `<link />` 들을 프리로드해서 더 빠르게 이동하게 한다.
      - -> SPA에서는 어렵다. html이 실제로 generate되는 SSR에서는 가능함. (nextjs에서는 [그렇게](https://nextjs.org/docs/api-reference/next/link) 하고 있다.)
- [Love your cache: Optimize for the second load](https://www.youtube.com/watch?v=tprJYFkv4LU&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=30)
  - [https://web.dev/love-your-cache/](https://web.dev/love-your-cache/)
  - 전반적으로 Cache-Control 헤더 의미도 알려주고, 캐싱의 장단점이나 트렌드도 케이스별로 알려줘서 좋은 영상이었음.
  - 일단 first load를 빠르게 하는 게 중요함. CWV 잘 써라.
  - **cache never**: 요즘은 CDN이 워낙 잘 되어있음. 기본적으로는 no-cache 전략이 안전함.
    - `Cache-Control: max-age=0,must-revalidate,public`
    - ETag 쓰면 validate가 빨라짐
  - **cache forever**: 그러나 안 바뀌는 게 확실한 파일들은 캐싱 안할 이유가 없음. generated hash를 가진 빌드 결과물들 같은.
    - `Cache-Control: max-age=31536000,immutable`

#### SEO

- SEO 토픽은 회사에서 비로그인 상태의 데스크톱 웹을 더 밀게 되면 다시 보자.
- [3x3 SEO tips for JavaScript web apps](https://www.youtube.com/watch?v=y1UzfahXfao&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=40)
  - [https://developers.google.com/search/docs/guides/javascript-seo-basics](https://developers.google.com/search/docs/guides/javascript-seo-basics)
  - 구글 서치엔진이 Javascript를 읽을 수 있기 때문에, 예전처럼 꼭 SPA가 SEO에 불리한 것은 아니지만 그래도 몇가지를 지키면 훨씬 좋아진다.
  - 팁 1. 정확한 메타데이터(title, description)를 제공하라 ([https://www.npmjs.com/package/react-helmet](https://www.npmjs.com/package/react-helmet))
  - 팁 2. 에러 페이지는 indexing되지 않게 하라
    - `<meta name="robots" content="noindex" />`
  - 팁 3. 여러 URL이 같은 결과물을 보여준다면 전부 한 URL을 쓰도록 canonical을 설정하라.
    - `<link rel="canonical" content={...} />`
  - 팁 4. sturctured data를 이용해서 rich result를 보여줘라. (아래 영상)
  - 팁 5. url에 `#` 쓰지 마라. 크롤러가 못 읽음.
- [Structured Data for Developers](https://www.youtube.com/watch?v=bUwmHX_EPmw&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=12)
  - [https://developers.google.com/search/docs/guides/search-gallery](https://developers.google.com/search/docs/guides/search-gallery)
  - 구글 검색 결과를 단순히 웹페이지 링크가 아니라 더 rich하게 보여줄 수 있다.
- [Core Web Vitals and SEO](https://www.youtube.com/watch?v=ggpZA5U2rZk&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=22)
  - Good "SEO signals"는 좋은 CWV를 포함한다.
  - Search Console 써서 퍼포먼스 올려라. 그러면 검색순위 좋아짐 ^^

#### Privacy

- Privacy 쪽은 잘 몰랐는데 덕분에 어느정도 알게 됐다.
  - 핵심은 각 서비스가 브라우저 내에 passive하게 제공되는 broad한 정보(e.g., 쿠키, User agent string)를 모아서 개별 유저를 uniquely identify하는 대신, 서비스가 Privacy budget 내에서 정확히 필요한 정보만 active하게 요청하라는 것.
  - 모였을 때 유저를 uniquely identify할 수 있는 정보를 많이 획득할수록 privacy budget이 차게 됨. 
- 영상들
  - [Enable and debug cross-origin isolated](https://www.youtube.com/watch?v=D5DLVo_TlEA&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=24)
  - [Introducing the Privacy Budget](https://www.youtube.com/watch?v=0STgfjSA6T8&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=25)
  - [A more private way to measure ad conversions](https://www.youtube.com/watch?v=jcDfOoWwZcM&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=26)
  - [Patterns for privacy](https://www.youtube.com/watch?v=-U42RRPrOrM&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=36)

#### 그 외

- [Superpowers for next gen web apps: Machine learning](https://www.youtube.com/watch?v=dDIk1Tmnj9A&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=39)
  - [https://www.tensorflow.org/js](https://www.tensorflow.org/js)
  - 당장은 쓸일 없겠지만 재밌게 봤다. 일단 초반에 ML의 아주 기초적인 컨셉들을 아주 간단하게 설명하는 게 맘에 들었다.
  - TensorflowJS로, 웹에서 다른 플러그인 따위 설치할 필요 없이 강력한 ML 피처들을 쓸 수 있는 게 장점이라고 한다.
  - 클라이언트 사이드에서 실행하므로, train 데이터를 어딘가로 보낼 필요 없기 때문에 Privacy, Lower latency, Lower cost가 보장된다.

- [What's new in DevTools](https://www.youtube.com/watch?v=QsOF9SJJdAA&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=3) (Chrome 87)
  - [https://developers.google.com/web/tools/chrome-devtools/blog](https://developers.google.com/web/tools/chrome-devtools/blog)
  - CSS grid 사이즈 디버깅, i18n 변경, 일정 시간 idle인 상태 시뮬레이트, 로컬 폰트 disable해서 웹폰트 적용되는지 여부 확인, animation style 수정
  - 특정 컨테이너만 선택해서 스크린샷 찍기 가능 :thumbsup:
  - 색맹 유저에게 화면이 어떻게 보이는지 시뮬레이트, 그리고 색맹 유저에게 잘 보일 수 있게 바로 색깔 제안
- [Making the web more visual with Web Stories](https://www.youtube.com/watch?v=mp6IUgUXJds&list=PLNYkxOF6rcIDzLmWaDwfHVZJl1Q5RFgOR&index=13)
  - [https://stories.google/](https://stories.google/)
  - 구글이 제공하는 브랜딩 웹페이지 제작 툴로 보인다. 회사 마케팅 팀에게 토스함.
- PWA, Service Worker
  - 영상이 상당히 많았는데 내가 제대로 써본적이 없고, 회사에서 당장 쓸 일도 별로 없어 보여서 대충 듣고 넘겼다.
  - 나중에 더 공격적인 성능 향상을 꾀해야 하거나 해서 요게 필요해지면 그때 다시 공부해봐도 될듯. 어차피 기술 발전도 빠른 분야라.