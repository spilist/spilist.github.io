---
title: "요약 번역: 2018년에 JavaScript 앱 테스트하기"
tags: [JavaScript, Testing, React, Angularjs, Web Development]
---

원문: https://medium.com/welldone-software/an-overview-of-javascript-testing-in-2018-f68950900bc3

### 한줄 요약: 유닛 테스트와 통합 테스트에는 `Jest`를 쓰고 UI 테스트에는 `TestCafe`를 써라.



#### 테스트의 종류

테스트 종류에 대해 더 자세히 알려면 이 링크들을 참고하라. [[1]](http://stackoverflow.com/questions/520064/what-is-unit-test-integration-test-smoke-test-regression-test), [[2]](https://www.sitepoint.com/javascript-testing-unit-functional-integration/), [[3]](https://codeutopia.net/blog/2015/04/11/what-are-unit-testing-integration-testing-and-functional-testing/)

일반적으로 웹사이트에서 중요시되는 테스트는 다음과 같다.

- 유닛 테스트: 개별 함수 또는 클래스에 적절한 인풋을 넣었을 때 예상대로 아웃풋이 나오는지 확인.
- 통합 테스트: 사이드 이펙트를 포함하여, 프로세스나 컴포넌트가 예상대로 동작하는지 확인.
- UI 테스트(= 기능 테스트): 내부 구조는 알 필요 없이, 웹브라우저를 통해 제품 자체에서 유저 시나리오가 예상대로 동작하는지 확인.



####테스팅 툴의 종류

1. Provide a **testing structure** ([Mocha](https://mochajs.org/), [Jasmine](http://jasmine.github.io/), [Jest](https://facebook.github.io/jest/), [Cucumber](https://github.com/cucumber/cucumber-jshttps://github.com/cucumber/cucumber-js))
2. Provide **assertions functions** ([Chai](http://chaijs.com/), [Jasmine](http://jasmine.github.io/), [Jest](https://facebook.github.io/jest/), [Unexpected](http://unexpected.js.org/))
3. Generate, **display, and watch** test results ([Mocha](https://mochajs.org/), [Jasmine](http://jasmine.github.io/), [Jest](https://facebook.github.io/jest/), [Karma](https://karma-runner.github.io/))
4. Generate and compare **snapshots** of component and data structures to make sure changes from previous runs are intended ([Jest](https://facebook.github.io/jest/), [Ava](https://github.com/avajs/ava))
5. Provide **mocks, spies, and stubs** ([Sinon](http://sinonjs.org/), [Jasmine](http://jasmine.github.io/), [enzyme](http://airbnb.io/enzyme/docs/api/), [Jest](https://facebook.github.io/jest/), [testdouble](https://github.com/testdouble/testdouble.js))
6. Generate **code coverage** reports ([Istanbul](https://gotwarlost.github.io/istanbul/), [Jest](https://facebook.github.io/jest/), [Blanket](http://blanketjs.org/))
7. Provide a **browser or browser-like environment** with a control on their scenarios execution ([Protractor](http://www.protractortest.org/)**,** [Nightwatch](http://nightwatchjs.org/), [Phantom](http://phantomjs.org/)**,** [Casper](http://casperjs.org/))



#### 합치면

- 두 가지 프로세스를 통해 테스트하길 권한다.
  - 유닛 테스트와 통합 테스트를 위한 것 하나
  - UI 테스트를 위한 것 하나
- 이유는 UI 테스트에는 시간이 더 오래 걸리기 때문. 
  - 특히 여러 브라우저를 테스트하고, 외부 서비스도 사용하는 경우가 많아서 돈도 들어갈 수 있음. 
  - feature branch 머지 직전에만 한다거나 등 더 적게 하길 원하게 될 것임.

##### 유닛 테스트

Should cover all small pure units of the application- utils, services and helpers. Provide all these units with simple and edge case inputs and make sure their outputs are as expected **using the assertion functions (3)**. Also make sure to use a **coverage reporting tool (6)** to know what units are covered.

##### 통합 테스트

Integration tests should cover important cross-module processes. Comparing to unit tests, you would probably use **spies (5)** to ensure expected side effects instead of just asserting the output and **stubs (5)** to mock and modify the parts of the process that are not in the specific test.

Also, as opposed to unit tests, **a browser or browser-like environment** **(7)**could help with processes that are dependent on the `**window**` and when part of the process is to render certain components or interact with them.

**Component snapshot tests** **(4)** fall into this category as well. They provide us with a way to test how processes affect selected components without actually render them or using a browser or browser-like environment.

##### UI 테스트

Sometimes the quick and effective unit and integration tests are not enough.

UI tests are always running inside **a browser or browser-like environment****(7)** that were discussed earlier.

They simulate user behavior on these environments (clicking, typing, scrolling etc…) and make sure these scenarios actually work from the point of view of an end user.

It is important to remember that these tests are the hardest to set up. Imagine yourself creating an environment to run a test on different machines, devices, browser types and versions. This is why there are [many services](https://www.keycdn.com/blog/browser-compatibility-testing-tools/) that provide this service for you. [And even more can be found here.](https://www.guru99.com/top-10-cross-browser-testing-tools.html)



#### 유닛, 통합 테스트 프레임워크 선택하기

> \* In short, if you want to “just get started” or looking for a fast framework for large projects, go with **Jest**.
>
> \* If you want a very flexible and extendable configuration, go with **Mocha**.
>
> \* If you are looking for simplicity go with **Ava**.
>
> \* If you want to be really low-level, go with **tape**.



#### UI 테스트 툴 선택하기

> \* In short, if you want to “just get started” with a reliable and simple to set-up cross-browser all-in one tool, go with **TestCafe**.
>
> \* If you want to go with the flow and have maximum community support, **WebdriverIO** is the way to go.
>
> \* If you don’t care about cross-browser support, use **Puppeteer**.
>
> \* If your application has no complex user interactions and graphics, like a system full of forms and navigations, use cross browser headless tools like **Casper.**



---

##### Hwidong's insight

- 이미 나 복귀하기 전에 프론트엔드 팀에서 고민 많이 한 것 같다. (이미 Jest, TestCafe 쓰기로 함)
- TestCafe로 테스팅 구조를 열심히 만들고 있었는데 하면 할수록 모르는게 너무 많아서 다시 공부하다가 이 글 읽게 되었다.
- 정말 이제 시작만 하면 된다. 그런데 원래 이번주에 세팅하고 싶었지만 눈에 띄는 버그들을 핫픽스하고, 프리티어 세팅하고 등등 하다보니 이미 금요일이다.. 그리고 다음주에는 스프린트 개발을 좀 해야 한다. 어떻게든 둘다 하고싶다.