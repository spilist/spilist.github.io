---
title: "자바스크립트 실행 컨텍스트와 스코프"
tags: ["JavaScript", "Context", "Scope", "Performance Optimization"]
---

함수 bind 하는 것을 잊어서 에러가 나는 경우도 많고, React에서 bind를 어떻게 하느냐가 성능에 영향을 준다는 말도 많이 봐서 이것저것 읽어보며 정리했다.

---

[ZeroCho 블로그](https://www.zerocho.com/category/Javascript/post/573b321aa54b5e8427432946)의 [자바스크립트 강좌](https://www.zerocho.com/category/Javascript/)들 중 일부: 내가 자바스크립트를 기초부터 강좌를 듣거나 한게 아니라서 의외로 정확히 모르던 부분이 꽤 있었다.

- [Window 객체와 BOM](https://www.zerocho.com/category/Javascript/post/573b321aa54b5e8427432946)

  - window: 브라우저 전체의 모든 오브젝트, 자바스크립트 엔진 등을 모두 포함한 최상위 전역 객체. 대표적으로 `screen`, `location`, `history`, `document` 같은 객체와 `parseInt()`, `isNaN()` 같은 메소드, `String`, `Boolean`, `Object`, `Number` 등의 자료형을 가지고 있다. window는 전역 객체라서 window 밑의 객체나 메소드 등을 부를 때 생략할 수 있다. 예를 들어 `document.getElementById()` 같은 걸 자연스럽게 사용하는데, 이건 사실 `window.document.getElementById()` 에서 `window.`  가 생략된 것이다. 
  - DOM(Document Object Model): window.document 를 지칭.
  - BOM(Browser Object Model): document 를 제외한 나머지 중 브라우저에 대한 정보를 가지고 있는 객체들. navigator, screen, location, history 등등.

- [this는 무엇인가?](https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb)

  - 글로벌에서 this = window. 객체의 메서드를 호출할 때는 this = 객체.

  - `function.bind(object)` 와 같이,  `bind`, `call`, `apply` 를 함수 function에 대해 호출하면 this가 object 객체를 가리키게 된다.

  - `new` 키워드 없이 일반 함수에서 constructor를 쓰면 this가 window에 붙는다.

    ```javascript
    function Person(name, age) {
      this.name = name;
      this.age = age;
    }
    
    Person('Name', 25);
    console.log(window.name, window.age); // Name 25
    ```

  - ES6에서는 class로 선언하면, new 없이 constructor를 부를 수 없게 에러가 난다.

    ```javascript
    class Person2 {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }
    }
    
    Person2('Name', 25); // Uncaught TypeError: Class constructor Person2 cannot be invoked without 'new'
    ```

  - 이벤트 리스너는 기본적으로는 전역에서 작동한 함수이기 때문에 this = window여야 한다. 하지만 내부적으로 다음과 같은 이벤트 리스너는 this가 객체에 붙는다.

    ```javascript
    document.body.onclick = function() {
      console.log(this); // <body>
    }
    
    $('div').on('click', function() {
      console.log(this); // <div>
    });
    ```

  - 그런데 이 안에서 다시 함수를 정의해서 쓰면 this가 window가 된다. 이를 막으려면 ES6의 => 로 함수를 정의하면 된다. 화살표 함수는 상위 함수의 this에 bind된다.

    ```
    $('div').on('click', function() {
      console.log(this); // <div>
      function inner() {
        console.log('inner', this); // inner Window
      }
      const inner2 = () => {
        console.log('inner2', this); // inner2 <div>
      }
    });
    ```

- [함수의 범위(scope)](https://www.zerocho.com/category/Javascript/post/5740531574288ebc5f2ba97e)

  - lexical scoping: 스코프는 함수를 호출할 때가 아니라 선언할 때 생긴다. 함수를 처음 선언하는 순간, 함수 내부의 변수는 자기 스코프로부터 가장 가까운 곳에 있는 변수를 계속 참조하게 된다.

  - 네임스페이스: 라이브러리에서 사용하는 함수들을 고유 오브젝트에 넣어 네임스페이스를 만든다.

    ```javascript
    var obj = {
      x: 'local',
      y: function() {
        alert(this.x);
      }
    }
    ```

  - 그런데 이렇게만 하면 이 코드 밑에 `obj.x = 'hacked'` 같은 구문을 넣으면 다른 사람이 값을 바꿔버릴 수 있다. 이를 방지하려면 다음과 같이 한다.

    ```javascript
    var another = function () {
      var x = 'local';
      function y() {
        alert(x);
      }
      return { y: y };
    }
    var newScope = another();
    ```

    함수로 감싼 후 return을 통해 공개할 변수(y)만 공개한다.

  - 위를 간략하게 바꾸면 다음과 같다.

    ```javascript
    var newScope = (function () {
      var x = 'local';
      return {
        y: function() {
          alert(x);
        }
      };
    })();
    ```

    `(function() {})()` 을 [즉시 실행 함수 표현](https://developer.mozilla.org/ko/docs/Glossary/IIFE)(IIFE, Immediately Invoked Fuction Expression)이라고 부르고 모듈 패턴이라고도 한다. 자바스크립트에 비공개 변수 기능을 추가해주기 때문에, 많은 라이브러리가 이를 활용하고 있다.

- [실행 컨텍스트와 클로저](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)

  - 컨텍스트의 원칙 네 가지
    - 먼저 전역 컨텍스트가 하나 생성되고, 함수 호출 시마다 컨텍스트가 생김
    - 컨텍스트 생성 시 컨텍스트 안에 **변수객체**(**arguments, variable), scope chain, this**가 생성된다.
    - 컨텍스트 생성 후 함수가 실행되는데, 사용되는 변수들은 변수 객체 안에서 값을 찾고, 없다면 스코프 체인을 따라 올라가며 찾는다.
    - 클로저를 제외하면, 함수 실행이 마무리되면 해당 컨텍스트는 사라진다. 마찬가지로, 페이지가 종료되면 전역 컨텍스트가 사라진다.
  - 