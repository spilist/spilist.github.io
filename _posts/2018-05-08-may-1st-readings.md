---
title:  "기술 뉴스 #1 - UI/UX (2018.05.08)"
tags: 기술뉴스
---





[(영어) 미래를 향해 스크롤하기](https://evilmartians.com/chronicles/scroll-to-the-future-modern-javascript-css-scrolling-implementations): 스크롤과 관련된 여러가지 기능들은 대부분 '모든 브라우저에서 잘 작동'하게 하기 위해 자바스크립트로 작성되어 왔다. 한편 웹의 스탠다드는 빠르게 발전하고 있으며, 최신 CSS와 DOM API가 새 버전의 브라우저들에 지원되면서 자바스크립트로 만들어진 이런 기능들이 더 간편한 코드로, 더 좋은 성능으로 대체될 수 있는 가능성이 생겼다. (글이 작성된 시점인 2018년 4월 12일 기준으로) 어떤 기능들은 브라우저에서 바로 지원되고 어떤 기능들은 polyfill을 써야만 지원되지만, 적어도 자바스크립트로 모든 기능을 구현하는 게 유일한 해답이 아니라는 것은 확실하다. 어떤 예시들이 있는지 일부만 요약 정리해봤다.

- 모달과 스크롤

  - 모달이 열리면 뒤쪽의 메인 컨텐츠는 스크롤되지 않기를 기대한다. 이를 구현하는 가장 쉬운 방법은 이렇다.

     ```css
      body {
        overflow: hidden;
      }
     ```

    그러나 이렇게 하면 윈도우에서 스크롤바가 사라지면서 페이지의 폭이 바뀌기 때문에, 100% width를 가진 컨텐츠는 모달이 열리면서 순간적으로 보기싫게 움직인다(jitter).

    ![Jitter when a scrollbar disappears](https://cdn.evilmartians.com/front/posts/scroll-to-the-future-modern-javascript-css-scrolling-implementations/jitter-083fbef.gif)

  - 따라서 스크롤바가 없어지더라도 기존 페이지의 width를 보존해주고 싶은데, 문제는 브라우저마다 스크롤바 스타일이 다 다르고 width도 다르다는 것이다. 스크롤바 width를 동적으로 계산하는 방법도 있지만 DOM을 조작해야 해서 좋지 않은 방법이다.

  - 다른 방법은 항상 스크롤바가 유지되게 하는 것이다.

    ```css
    html {
        overflow-y: scroll;
    }
    ```

    그러나 이렇게 하면 jitter가 사라지는 대신, "눈에는 보이지만 움직일 수 없는" 스크롤바가 보여서 좋은 디자인은 아니다.

  - 더 좋은 방법은 스크롤바는 유지하되 눈에만 안보이게 하는 것이다.

    ```css
    // Chrome, Safari, Opera
    .container::-webkit-scrollbar {
        display: none;
    }
    
    // IE, Edge
    .container {
        -ms-overflow-style: none;
    }
    ```

    단, 현재까지는 파이어폭스는 방법이 없다. 보다시피 모든 상황에 들어맞는 해결책은 없으며 적당히 장단점을 고려하여 취할 수밖에 없다.

- 부드럽게 움직이기

  - 스크롤이 발생하는 아주 일반적 케이스 중 하나가 랜딩 페이지에서 원하는 섹션으로 이동시키는 것이다. 대개 이건 anchor 링크를 이용한다.

    ```html
    <a href="#section">Section</a>
    ```

    이 링크를 클릭하면 해당 섹션으로 *점프하게* 되는데, 대신 부드럽게 스크롤되게 하기 위한 Javascript 해결책은 무수히 많다.

  - 요즘에는 이 기능을 `Element.scrollIntoView()` DOM API를 이용해 구현 가능하다.

    ```javascript
    elem.scrollIntoView({ behavior: 'smooth' });
    ```

    그러나 아직 이 API에 대한 [브라우저 지원은 미비](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView#Browser_compatibility)하고, 여전히 Javascript 코드이다.

  - 다행히 현재는 working draft 상태이긴 하지만 [새로운 CSS 속성](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior)을 사용하면 전체 페이지에서 스크롤 동작을 바꿀 수 있다.

    ```css
    html {
        scroll-behavior: smooth;
    }
    ```

    ![Scrolling smoothly](https://cdn.evilmartians.com/front/posts/scroll-to-the-future-modern-javascript-css-scrolling-implementations/smooth-39c1d26.gif)

    [이 코드펜](https://codepen.io/askd/full/WdXOYW)에서 직접 확인해보라. 글을 쓰는 지금은 크롬/파이어폭스/오페라만 지원하지만 이 방식이 훨씬 아름다우며, "[점진적 개선](https://en.wikipedia.org/wiki/Progressive_enhancement)" 마인드셋과 잘 맞기 때문에 곧 모든 브라우저에 적용되길 기대한다.

- 달라붙게 하기

  - 스크롤과 관련된 또다른 일반적 작업은 스크롤 방향에 따라 요소가 달라붙게 하는 것이다.![A sticky element](https://cdn.evilmartians.com/front/posts/scroll-to-the-future-modern-javascript-css-scrolling-implementations/sticky-207e351.gif)

    예전에는 이걸 구현하기 위해 복잡한 스크롤 핸들러가 필요했고, Javascript로 구현하기 위해 `Element.getBoundingClientRect()`를 [사용](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)하면 성능 문제도 있었다.

  - 얼마 전부터 이를 대체할 수 있는  `position: sticky` 가 CSS로 구현되었다. 개발자가 offset만 명시하면 나머지는 브라우저가 알아서 처리해준다.

    ```css
    .element {
        position: sticky;
        top: 50px;
    }
    ```

    [이 코드펜](https://codepen.io/askd/full/ppGQya)에서 직접 확인해보라. 현재 이 기능은 IE 11을 제외하면 모바일을 포함한 [거의 모든 브라우저](https://caniuse.com/#feat=css-sticky)에서 지원된다. 아직 Javascript로 이를 구현하고 있다면 CSS로 바꿀 때가 됐다.

- 스크롤 이벤트 핸들러 최적화하기

  - 스크롤은 Javascript 이벤트이고, addEventListener로 스크롤 이벤트에 bound하여 특정 동작을 처리하는 경우가 많다. 그런데 사람들이 스크롤을 워낙 많이 하기 때문에 자연스럽게 성능 문제가 생긴다.

  - 이 때 사용할 수 있는 기술이 스로틀링이다.

    ```javascript
    window.addEventListener('scroll', throttle(() => {
      const scrollTop = window.scrollY;
      /* doSomething with scrollTop */
    }));
    
    function throttle(action, wait = 1000) {
      let time = Date.now();
      return function() {
        if ((time + wait - Date.now()) < 0) {
            action();
            time = Date.now();
        }
      }
    }
    
    // smoother version
    function throttle(action) {
      let isRunning = false;
      return function() {
        if (isRunning) return;
        isRunning = true;
        window.requestAnimationFrame(() => {
          action();
          isRunning = false;
        });
      }
    }
    ```

    물론 Lodash 등에서 나온 [구현](https://lodash.com/docs/4.17.5#throttle)을 사용할 수도 있다. 

  - 무엇을 선택하는가가 중요한 건 아니고, 중요한 건 스크롤 이벤트 핸들러를 최적화할 필요가 있다는 것이다.

- 뷰포트에 존재하는지 확인하기

  - 이미지의 *레이지 로딩이나 *무한 스크롤* 기능을 만드려면 요소가 뷰포트 안에 있는지 여부를 알아내야 한다. 이를 구현하는 가장 일반적인 방법은 스크롤 이벤트에 bound하여 `Element.getBoundingClientRect()`를 이용하는 것이다.

    ```javascript
    window.addEventListener('scroll', () => {
      const rect = elem.getBoundingClientRect();
      const inViewport = rect.bottom > 0 && rect.right > 0 &&
                         rect.left < window.innerWidth &&
                         rect.top < window.innerHeight;
    });
    ```

    문제는 `getBoundingClientRect`는 불릴 때마다 *reflow*를 일으키기 때문에 성능상 문제가 생긴다는 것이다. 스로틀링을 적용해도 이 때에는 큰 도움은 안 된다.

    - reflow는 문서 안의 요소가 가지는 위치와 형태를 다시 계산하는 과정을 뜻한다.

  - 이 문제는 2016년에 [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)가 소개되면서 해결되었다. 이를 통해 단순히 뷰포트에 남아있는지뿐만 아니라, 한 요소가 그 요소의 어떤 부모라도 겹치는지 여부를 확인할 수 있다. 추가로, 요소 단 1픽셀이라도 겹치는지까지 확인할 수 있다.

    ```javascript
    const observer = new IntersectionObserver(callback, options);
    
    observer.observe(element);
    ```

  - 이 API는 [널리 지원](https://caniuse.com/#search=IntersectionObserver)되고 있지만 몇몇 브라우저는 [폴리필](https://github.com/w3c/IntersectionObserver)을 필요로 한다. 물론 폴리필을 쓰더라도 가장 좋은 솔루션이다.

- 너무 멀리 스크롤하지 않기

  - 스크롤이 가능한 팝업/모달/드롭다운 등을 구현해봤다면 *스크롤 전달* 문제에 대해 알고 있을 것이다. 안쪽 요소의 끝까지 스크롤이 도달하면 전체 페이지가 스크롤되기 시작하는 현상 말이다.

    ![Scrolling chaining](https://cdn.evilmartians.com/front/posts/scroll-to-the-future-modern-javascript-css-scrolling-implementations/chaining-acaea17.gif)

  - 이 "오버스크롤"문제는 페이지의 `overflow` 속성을 조작하거나, 요소의 끝에 도달했을 때부터 스크롤 이벤트를 전달하지 않게 하는 방법으로 제거할 수 있다. 그러나 후자를 Javascript로 구현하는 것은 그다지 안정적이지 않을뿐더러 성능에 나쁜 영향을 미칠 수 있다.

  - 이 문제는 특히 모바일 기기에서 널리 쓰이는 "pull to refresh" 동작때문에 위험하게 된다. 모바일 크롬 브라우저에서 아래로 당겨서 새로운 글들을 로드하려다가 전체 페이지가 새로고침되어버릴 수도 있는 것이다.

  - CSS의 새로운 `overscroll-behavior` 속성이 이 상황을 구제하기 위해 등장했다. 이 속성을 통해 스크롤 끝 부분에 도달했을 때의 동작을 제어할 수 있다. 위 GIF에서의 문제가 크롬, 오페라, 파이어폭스에서 한 줄로 해결된다.

    ```css
    .element {
      overscroll-behavior: contain;
    }
    ```

    IE와 Edge에서는 `-ms-scroll-chaining` 속성을 지원하긴 하나 이걸로 모든 케이스가 해결되지는 않는다. 다행히도 MS 브라우저에서 `overscroll-behavior` 속성의 구현이 현재 진행중이라고 한다.

- 터치에 반응하기

  - "터치 기반 인터페이스에서의 스크롤링"은 따로 다룰 만한 거대한 주제이지만, 이 글에서 굳이 언급하는 이유는 많은 개발자들이 간과하고 있기 때문이다.

  - 애플에서 처음 제시되어 빠르게 스탠다드가 된 "모멘텀" 스크롤링은 기본적으로는 전체 페이지의 스크롤로는 적용되지만 요소를 스크롤할 때는 적용되지 않는다. 이걸 무의식적으로 불편해하는 모바일 사용자는 아주 많다.

  - 이를 CSS로 해결할 수는 있지만 아직 vendor prefix 단계이고 모든 브라우저가 지원하지는 않는다.

    ```css
    .element {
      -webkit-overflow-scrolling: touch;
    }
    ```

  - 
