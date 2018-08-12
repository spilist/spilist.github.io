---
layout: page
title: Portfolio
permalink: /about/portfolio
---

**배휘동** | bae.hwidong@gmail.com| [Medium Blog](https://medium.com/steady-study) | [LinkedIn](https://linkedin.com/in/hwidongbae) | [GitHub](http://github.com/spilist)

최종 업데이트: 2018.08.12

<br>

### 맞춤 세무사 찾기 (2018년)

[한국신용데이터](http://kcd.co.kr/)에서 의뢰받아 외주로 만든, [캐시노트](http://cashnote.kr/)에 연결된 세무대리인을 지역/관심업종 기반으로 검색하고 연결하는 모바일 웹 서비스. [사이트 링크](https://tax.cashnote.kr/)

* [React](https://github.com/facebook/react)([create-react-app](https://github.com/facebook/create-react-app))에 [ducks 스타일의 Redux](https://github.com/erikras/ducks-modular-redux)와 [CSS module](https://github.com/css-modules/css-modules)을 적용하여 구현했다. 재사용되는 컴포넌트들은 따로 빼서 모듈화했다.
* 레거시 없는 상태에서 만들기 시작하는 것의 즐거움을 제대로 느꼈다. (그러나 이 때 만든 것들이 나중에 다시 보니 어느새 레거시가 되어있어서 다시 리팩토링했다.)
* 기획과 스펙이 아주 깔끔하여 8일만에 완성되었다. 훌륭한 기획자가 있는 팀은 이렇게나 다르다는 걸 느꼈다. 특히 [MVP](https://en.wikipedia.org/wiki/Minimum_viable_product)의 Minumum에 대한 의미를 정확히 알고, 일정에 맞춰 스펙을 쳐낼 수 있는 능력을 가진 팀이었다. 생산성 높게 진행되어 서로가 만족한 프로젝트였다.
  ![image-20180714234348052]({{ "portfolio/image-20180714234348052.png" | absolute_url }} )

<br>

### Elice (2016년 말 ~ 현재)

웹 프론트엔드 팀 리더로 일했다.

* 온라인 소프트웨어 교육 플랫폼 '[엘리스](https://academy.elice.io/)'의 제품 기획 및 웹 프론트엔드 부문 개발 총괄을 맡았다. 프론트엔드는 [React](https://github.com/facebook/react) / [Flux](https://facebook.github.io/flux/)로 이루어져 있었고 Flux는 차차 [Redux](https://github.com/reduxjs/redux)로 포팅되었다. 몇 개 프로젝트를 제외한 엘리스 제품 거의 모든 부분의 기획과 개발에 참여했다.

* 엘리스에서 나의 프로그래밍 전문성을 웹 프론트엔드, 특히 자바스크립트에 더 집중해서 공부하고 키워냈다. 구체적으로 배우고 실행한 것들은 다음과 같다.

  * React와 Redux를 사용한 [SPA](https://en.wikipedia.org/wiki/Single-page_application) 개발 방법을 익혔다. [Webpack](https://webpack.js.org/), [Babel](https://babeljs.io/), [Gulp](https://gulpjs.com/) 등 SPA의 기반 기술들에 대해 이해했으며 [ES6](http://es6-features.org/#Constants) 이후의 자바스크립트 활용법에 대해서도 익숙해졌다.
  * 자주 사용되는 디자인 컴포넌트들을 팀원들과 함께 패키지화하여 `elice-blocks` 로 만들었다. 초반에는 외부 공개를 염두에 두고 각종 컴포넌트를 전부 직접 만들었고, 나중에는 [antd](https://ant.design/)를 wrapping해서 쓰는 등 생산성에 더 염두를 두었다. 엘리스 웹이 `elice-blocks` 라는 외부 패키지를 가져다 쓰게 되면서, 거기서 오는 문제점을 해결하는 법 또한 부수적으로 알게 됐다.
  * 엘리스에서 진행하는 라이브 수업을 위해, [Azure Media Service](https://azure.microsoft.com/ko-kr/services/media-services/)를 통한 비디오 스트리밍을 [Azure Media Player](http://ampdemo.azureedge.net/azuremediaplayer.html)로 라이브로 제공하는 작업을 했다. 동영상과 스트리밍에 대한 이해가 높아졌다.
  * [Intercom](https://www.intercom.com/)으로 유저 피드백을 받고 [Sentry](https://sentry.io/)로 에러 로깅을 했다.
  * 앱 번들 용량을 줄이기 위해 [번들 크기를 분석](https://www.npmjs.com/package/webpack-bundle-analyzer)한 뒤, 대용량 패키지의 지연 로딩을 도입하도록 팀원에게 위임했다. 용량은 실제로 40% 정도 줄었으나 이후 지연 로딩에서 비롯된 버그가 끊임없이 쏟아져나와 고생했다.
  * [eslint](https://eslint.org/)와 [stylelint](https://github.com/stylelint/stylelint)를 [prettier](https://github.com/prettier/prettier)에 통합하여 자동 포맷팅하도록 세팅했다. 이로써 코딩 시간을 단축하고, 더 좋은 프랙티스를 자연스럽게 익히게 하고, 팀원들끼리 더 유의미하게 코드 리뷰를 할 수 있도록 했다.
  * 최근에는 [Jest](https://jestjs.io/docs/en/getting-started), [Enzyme](https://airbnb.io/enzyme/docs/api/), 각종 mocking 패키지를 이용해 [TDD](https://en.wikipedia.org/wiki/Test-driven_development)로 프론트엔드를 개발하기 시작했고, TDD를 팀에 소개하는 세션을 진행했다.

* 정말 여러가지를 배우고, 시도하고, 해냈지만 내가 좋은 팀 리더였다고 말하긴 어렵다.

  * 프론트엔드 팀 리더로 입사하긴 했으나 React와 SPA기반 기술에 대한 이해가 부족한 상태였기 때문에 나는 오랫동안 일반 개발자처럼 일했다. 그래서 엘리스 웹은 메인 아키텍트가 없는 상태로 개발이 오래 진행됐다.
  * 새로운 무언가를 도입할 때도 기존 코드가 정리되지 않은 채 엉성하게 도입되었고, 주니어는 오래된 나쁜 예시를 보며 따라했다. 기능 구현에 바빠 코드 리뷰도 제대로 되지 않았다. 정신을 차리고 보니 이미 테스트 코드도 없이 레거시가 엄청나게 쌓여있는 상태였다.
  * 쌓인 기술 부채를 해결하기 위해, 병가에서 복귀한 뒤로 나 자신이 아키텍트로서, 좋은 프로그래머로서 역량을 갖추고 팀원들을 이끌 수 있도록 공부를 계속했다. 그리고 prettier 도입, redux 구조 정리, TDD 소개 등 개발 환경과 문화를 점진적으로 개선하는 작업을 진행하고 있다. 그러면서 동시에 제품 릴리즈 일정을 맞추는 것은 결코 쉽지 않은 여정이었다. 그래도 지금은 많은 부분이 개선되었고 계속 개선되고 있다.

* 직원 수가 적었던 때부터 대표와 함께 하루 10시간 넘게 동고동락하며 좋은 조직문화를 만들고 관리 프로세스를 만들기 위해 노력했다. 여러가지 도구를 쓰다가 결국 [Jira](https://jira.atlassian.com/)와 [Confluence](https://confluence.atlassian.com/)에 정착했는데 아주 만족스럽진 않다. 덕분에 간단하게나마 [칸반](https://ko.atlassian.com/agile/kanban)과 [스크럼](https://www.scrum.org/resources/what-is-scrum) 프로세스에 대해 이해하게 됐다.

  ![image-20180714234704826]({{ "portfolio/image-20180714234704826.png" | absolute_url }} )


<br>

### Cultureland-OCR (2016년 가을)

모바일 컬처랜드 문화상품권 번호 추출 쉘 스크립트. [Gist 링크](https://gist.github.com/spilist/4dfa257e81bcef84a1320d4b4197b9ce)

* 당시 내가 다니던 NBT에서는 '식권대장'이라는 서비스를 통해 식대를 지급하고 있었다. 이 서비스와 제휴되지 않은 식당에서 식사를 할 경우 모바일 컬처랜드 문화상품권을 받을 수 있었는데, 많은 직원들이 문화상품권을 몇십 개씩 휴대폰에 모아뒀다가 몇 시간씩 들여 컬처랜드 웹사이트에서 노가다로 번호를 입력하곤 했다. 나는 이게 무척 귀찮아서 일부라도 자동화하고 싶었다.
* [Teserract](https://github.com/tesseract-ocr/tesseract)라는 이미지 인식 프로그램을 이용하면 문화상품권 번호를 쉽게 인식할 수 있음을 확인했다. 그리고 컬처랜드 모바일 상품권 충전 페이지의 DOM 형태를 보고, 충전 페이지의 번호 입력 칸에 개발자 콘솔을 통해 번호를 입력할 수 있겠다고 생각했다.
* 이미지가 있는 디렉토리에서 실행하면 `번호 추출 + 개발자 콘솔에서 번호 입력하는 코드 생성 + 추출 끝난 이미지 옮기기` 를 해주는 쉘 스크립트를 개발하여 사내에 배포했다.
* 결과적으로 몇 시간 걸리던 작업을 몇 분만에 해결할 수 있게 만들었지만 쉘 스크립트와 개발자 콘솔이라는 장벽이 커서였는지, 개발팀 이외에는 별로 사용하지 않아서 아쉬웠다.

<br>

### [NBT](http://nbt.com/) (2016년 초 ~ 2016년 말)

서버 엔지니어로 일하면서 백엔드 API 와 웹 프론트 뷰를 개발하고, 서버 성능을 향상시켰다.

* NBT의 대표 서비스였던 모바일 리워드 앱 '[캐시슬라이드](http://site.cashslide.co.kr/)'의 백엔드 API 를 Ruby / Rails로 개발하고 유지보수했다.
* 코드 리뷰와 페어 프로그래밍을 적극적으로 하여 개발문화를 개선하는 데 기여했다. 서버 팀 전체가 [Ruby 스타일 가이드](https://github.com/rubocop-hq/ruby-style-guide)를 함께 보며 더 좋은 프랙티스를 익히게 되는 것을 주도했다. 내가 리뷰할 때 Ruby 스타일 가이드를 기반으로 더 좋은 개발 방식을 자주 제시하다 보니, 루비 스타일을 잡아주던 [Rubocop](https://github.com/rubocop-hq/rubocop) 에서 따온 '휘보콥'이라는 별명을 얻었다.
* '개발팀의 개발 프로세스에 성능에 대한 고려가 녹아들도록 하기'라는 사내 프로젝트를 진행하여 [Ruby Profiler](https://github.com/ruby-prof/ruby-prof)와 [New Relic](https://newrelic.com/)의 사용법에 대해 서버 팀에 전파했다. 또한 개인 작업을 통해 병목 API 를 분리하고 개선하여 피크 타임의 서버 평균 응답시간을 40% 이상 줄였다.
  ![image-20180714205132317]({{ "portfolio/image-20180714205132317.png" | absolute_url }} )
  ![image-20180714205143245]({{ "portfolio/image-20180714205143245.png" | absolute_url }} )
* 이후 애드네트워크 '애디슨'을 개발하는 팀으로 옮겨 백엔드 API 및 프론트 뷰 웹개발을 했다. 모바일 광고 시스템이 어떤 식으로 돌아가는지 배우고, 로그를 체계적으로 남기고 분석하는 방법에 대해 여러모로 고민했다.
* NBT 개발팀은 스크럼과 칸반을 비롯한 개발문화와 조직문화를 갖추고 계속 발전시키고자 노력하는 조직이었다. 프로젝트 관리 도구와 협업 도구에 대해 많이 배웠다. 어느 정도 규모가 있는 조직에서 개발자 및 다른 구성원들과 어떻게 협업해야 하는지에 대해서도 많이 경험했다.

<br>

### Smashy Toys (2015년)

모바일 아케이드 리듬액션 게임. [플레이 스토어 링크](https://play.google.com/store/apps/details?id=com.morogoro.smashytoysspace), [GitHub 링크](https://github.com/spilist/shoong)

* 기획자 겸 디자이너 친구 한 명, 개발자 친구 한 명과 함께 셋이서 '모로고로'라는 팀을 만들어 모바일 게임을 개발했다. 이슈 관리는 [Trello](https://trello.com/)로 했다.
* 그동안 경험해왔던 웹개발과는 전혀 다른 영역이어서 재밌게 배운 게 많았다. 스토리텔링, 재미요소 측정, 유저 테스팅, 사용자 랭킹, 광고 붙이고 집행하기, 로컬라이제이션, 버그가 있는 버전을 배포한 뒤 핫픽스가 승인되어 재배포되기를 전전긍긍하며 기다리기 등등. '슈퍼마리오 브라더스' 같은 고전게임의 '느낌'에서 오는 재미를 살리기 위해 게임 영상을 수십번 유투브로 돌려보곤 했다.
* C# / [Unity3d](https://unity3d.com/)로 만들었고, 코드의 퀄리티나 방법론보다는 작업 결과물의 퀄리티만 높이려고 노력했다. (어리석었다.)
* 안드로이드로 베타 버전을 만들어 출시한 뒤 인디게임답게 유저들의 반응은 없다시피 했고, 번아웃되어있었던 팀은 자연스럽게 와해됐다. 이후 퍼블리셔가 붙어서 게임 홍보를 도와주겠다고 했고, 우리는 재결합해서 게임의 완성도를 높여 iOS를 포함하여 재출시했다. 그러나 퍼블리셔는 약속과 달리 흐지부지 일을 진행했으며, 우리도 게임을 완성한 것에 만족하며 그렇게 대강 마무리됐다.
  ![image-20180714194058169]({{ "portfolio/image-20180714194058169.png" | absolute_url }} )

<br>

### Havit (2014년 ~ 2015년)

좋은 습관을 만들어 유지하고 싶은 사람들을 연결해줌으로써 서로 격려할 수 있는 SNS. [개인 백업용 사이트 링크](https://havit-personal.herokuapp.com/), [GitHub 링크](https://github.com/spilist/havit)

* 창업팀 EverMentors의 대표를 맡았던 친구가 군대에 가고 내가 대표를 이어받았다. [린 스타트업](http://theleanstartup.com/) 방법론에 대해 공부하면서 우리가 원래 풀고자 하는 문제와 방향을 완전히 재정의했다.
* 잠재고객들과 문제 인터뷰를 진행한 후, 습관 형성을 돕는 '계획 실천 도우미'라는 서비스를 만들었다. 웹사이트 없이 개인코칭 방식으로 목표 설정과 계획 실천 체크, 회고를 함께 하는 방식으로 운영했다. 첫 2 주 무료 후 유료 전환 의사를 물어봤고, 유료 고객 6명과 함께 3개월간 진행하며 가설 검증 후 재실험을 반복했다.
  진행하면서 실천을 지속하는 데에 함께 실천하는 사람들과의 사회적 연결이 중요하다는 가설을 세우고 개인 코칭에서 페이스북 그룹 형태로 바꿔보았고, 더 효과가 좋음을 확인했다. 3개월간의 실험을 바탕으로 Havit 서비스를 만들기로 결정하고, 개발했다.
* Ruby / Rails로 백엔드, jQuery / Bootstrap으로 프론트엔드를 구현했다. 애자일 프로세스를 일부 도입하여 백로그를 만들고, 스토리 포인트를 책정하고, 인수 테스트를 만들고, 매일 배포했다.
  * [CodeShip](https://codeship.com/)으로 CI/CD 연결을 하여, [heroku](https://www.heroku.com/)에 배포하고 [CloudFlare](https://www.cloudflare.com/)로 CDN에 올려서 서비스했다.
  * 헤로쿠가 아시아에 서버가 없어서 CDN을 거치지 않으면 무척 느렸다. 로딩 속도에 네트워크 병목이 끼치는 영향을 크게 실감했다.
* 프로토타입이 만들어진 이후부터 지인들에게 홍보하여 몇 분이 열심히 써주셔서 무척 기뻤다. 이 때, 유저의 목소리를 듣고 피드백을 반영한다는 것이 정말 즐거움을 깨달았다.
  ![image-20180714191331188]({{ "portfolio/image-20180714191331188.png" | absolute_url }} )
  ![스크린샷 2018-07-14 오후 7.19.09]({{ "portfolio/스크린샷 2018-07-14 오후 7.19.09.jpg" | absolute_url }} )
* 작은 팀, 짧은 기간이었지만 스타트업 팀의 대표로서 팀을 운영한다는 것이 어떤 것인지도 살짝 배울 수 있었다.

<br>

### CPS Seat Picker (2013년 3월)

연구실 사람들을 위한 랜덤 자리배정 웹 어플리케이션. [GitHub 링크](https://github.com/spilist/cps_seat_picker)

* 연구실에서 주기적으로 자리를 바꿨었는데, 다음 바꿀 시기가 와서 내가 랜덤으로 자리 정해주는 웹사이트를 만들어보겠다고 나섰다.
* 웹 어플리케이션의 전체 제작 과정을 경험해보고 싶었고, 구상-기획-디자인-구현-배포-홍보-유지보수 까지를 해보자는 마음으로 만들었다.
* 각 stakeholder별 요구사항을 정리하고 [Balsamiq](https://balsamiq.com/)으로 UI 디자인을 했다.
  ![CPS Seat Picker -2013.03.02-]({{ "portfolio/CPS Seat Picker -2013.03.02-.png" | absolute_url }})
* 스토리 카드에 필요한 기능을 적고, 작업 크기를 추정하고, 쪼갰다. 기능을 어떻게 구현할지도 같이 적었다.
  ![C670F7B1-CB0B-40BA-AC05-795A5C8C6911]({{ "portfolio/C670F7B1-CB0B-40BA-AC05-795A5C8C6911.png" | absolute_url }} )
  ![84EA9142-05F7-4F2A-A5B9-35A58C025E9F]({{ "portfolio/84EA9142-05F7-4F2A-A5B9-35A58C025E9F.png" | absolute_url }} )
* PHP로 프레임워크 없이 웹서버를 세팅하고, jQuery 와 Bootstrap으로 구현했다.
  ![스크린샷 2013-03-05 오후 8.31.09]({{ "portfolio/스크린샷 2013-03-05 오후 8.31.09.png" | absolute_url }})

<br>

### DreamNote (2012년 ~ 2014년)

중고등학교 학생들이 자신의 꿈을 찾고 이뤄나가는 과정을 체계적으로 기록할 수 있는 템플릿 겸 SNS.

* 교내 창업동아리인 KLC에서 EverMentors라는 팀이 파생되었다. 여기에 메인 개발자(사실상 혼자)로 참여했고, 팀원들과 함께 웹 개발을 처음부터 공부해나가며 오랫동안 기획하고 개발했다.
* 개발 기록과 기능 개발 도중의 스크린샷은 많은데 정작 전체 웹사이트 스크린샷은 남아있지 않아서 아쉽다.
  ![E9C9EDF1-18B0-4525-8379-5B7E23B35D0F]({{ "portfolio/E9C9EDF1-18B0-4525-8379-5B7E23B35D0F.png" | absolute_url }} )
  ![00-첫 화면]({{ "portfolio/00-첫 화면.png" | absolute_url }} )
* 여러가지를 시도했었지만 최종적으로는 PHP / [CodeIgniter](https://codeigniter.com/)로 백엔드, jQuery / Boostrap으로 프론트엔드를 구현했다.
  * 처음에는 PHP만으로 개발했다. 중복 코드가 너무 많아져서 방법을 찾아보다가 `template`이라는 걸 알게 됐다. 그러다가 더 많은 것들이 미리 세팅되어있는 `프레임워크` 라는 것도 있다는 걸 알았다. 그래서 PHP 프레임워크 중 CodeIgniter를 공부해서 적용했다.
  * 순수 자바스크립트만 써오다가 jQuery의 존재에 대해 알게 되고 신세계를 경험했다.
  * CSS도 쌩으로 그냥 만들다가 Bootstrap을 알게 되고 정말 감사해가며 썼다.
* 이 때 워낙 jQuery와 CSS로 삽질을 많이 해서 '내가 원하는 화면을 구현'하는 능력이 많이 길러진 것 같다.

<br>

### UseTimeLogger (2011년 말)

안드로이드 스마트폰에서 유저의 앱별 사용량을 측정하는 연구용 어플리케이션.

* 처음으로 해본 외주. 연구용 앱이고 사실상 백그라운드 서비스라서 UI는 전혀 신경쓰지 않고 만들었다.

* 안드로이드 공식 API 문서를 수도없이 보면서 만들었는데 정작 다 만들고 나니 시간이 별로 오래 걸리지 않아서, 로그를 엑셀 파일로 추출하고 통계로 정리해주는 프로그램을 추가로 만들어줬다. 이 프로그램은 Python으로 구현했다.

  ![image-20180714174815328]({{ "portfolio/image-20180714174815328.png" | absolute_url }} )

<br>

### ITOM (2010년 여름)

TV 임베디드 운영체제에 들어가는 태스크 최적화 프로그램.

* LG전자 소프트웨어 센터 인턴십에서 동료 인턴과 함께, 리눅스의 `htop` 을 수정하여 만들었다.

* Interactive Task Optimization Manager의 약자였는데, `I`는 당시 애플 기기들의 붐으로 `i` 를 앞에 붙이는 게 유행이어서 우리도 붙였던 걸로 기억한다.

* 당시 만든 매뉴얼 일부.
  ![image-20180714175927197]({{ "portfolio/image-20180714175927197.png" | absolute_url }} )

* 실행 화면.
  ![image-20180714180004396]({{ "portfolio/image-20180714180004396.png" | absolute_url }} )
