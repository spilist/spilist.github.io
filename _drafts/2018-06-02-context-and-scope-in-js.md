---
title: "자바스크립트 실행 컨텍스트와 스코프"
tags: ["JavaScript", "Context", "Scope", "Performance Optimization"]
---

React에서 이벤트 핸들러를 bind 하는 것을 잊어서 에러가 나는 경우도 종종 있고, React에서 bind를 어떻게 하느냐가 성능에 영향을 준다는 말도 많이 봐서 이것저것 읽어보며 정리했다.

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

  - 그런데 이 안에서 다시 함수를 정의해서 쓰면 this가 window가 된다. 이를 막으려면 ES6의 => 로 함수를 정의하면 된다. 화살표 함수는 상위 함수의 this에 bind된다. 이를 lexical scoping이라고 한다.

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
  - 호이스팅(hoisting): 변수를 선언하고 초기화했을 때, 선언 부분이 최상단으로 끌어올려지는 것.
    - 변수와 함수는 선언만 하면 호이스팅된다. 
    - 따라서 코드에서 변수 선언 이전에 변수에 접근하면 에러(null reference)가 아니라, 단순히 값이 아직 초기화되지 않은 변수에 접근했기 때문에 undefined reference가 된다.
    - 함수는 `function FUNC() { ... }` 식으로 선언하면 코드에서 선언한 곳 이전에서도 쓸 수 있다.
    - 하지만 `let FUNC_VAR = function FUNC() { ... }` 와 같이 함수를 선언해서 바로 변수에 대입하는 형식으로 하면, 호이스팅은 FUNC_VAR에 대해서만 되고, 대입은 나중에 일어나기 때문에 선언한 곳 이전에서 쓰면 함수로서 실행할 수 없다.
  - 클로저(closure): 비공개 변수, 즉 '클로저 함수 내부에 생성한 변수도 아니고 매개변수도 아닌 변수'를 가진 함수.
    - 장점: 비공개 변수. 모듈로 배포했을 때 사용자의 잘못된 행동을 막을 수 있다.
    - 단점: 성능과 메모리. 비공개 변수는 자바스크립트에서 언제 메모리 관리를 해야할 지 모른다. 또한 스코프 체인을 거슬러 올라가기 때문에 좀 느리다.



[MDN doc - Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures): 클로저에 대해 조금 더 자세히 알고싶어서 읽어봤다.

- 정의는 "A *closure* is the combination of a function and the lexical environment within which that function was declared." 위 강의에서와는 느낌이 조금 다르다.

- 다시 한번 내용을 읽으면서 뜯어보니 이해가 간다. lexical scoping으로 인해, 함수가 선언시에 접근할 수 있었던 컨텍스트를 그대로 들고 오는 형태다.

- 함수를 리턴하는 함수(function factory)인 `makeAdder` 의 예시를 보자.

  ```javascript
  function makeAdder(x) {
    return function(y) {
      return x + y;
    };
  }
  
  var add5 = makeAdder(5);
  var add10 = makeAdder(10);
  
  console.log(add5(2));  // 7
  console.log(add10(2)); // 12
  ```

  `add5` 와 `add10` 은 둘 다 클로저다. 같은 함수 정의, 그리고 다른 lexical 환경을 가졌다. 

- 위와 비슷하게, 이벤트 핸들러를 리턴하는 함수를 이용하여 argument에 맞는 핸들링을 하게 하는 게 클로저의 실용적 사용 예 중 하나다.

- 또 다른 실용적 예는 제로초 블로그에서 나왔던 것처럼 private method를 emulate할 수 있게 하는 것이다(모듈 패턴). private method도 컨텍스트 안에 들어있으니까 가능하다.

- for 루프를 `var i` 와 함께 쓸 때 클로저를 쓰지 않으면 컨텍스트가 의도치 않게 바깥쪽에 바인딩될 수 있다.

  - ES2015에서는 var 대신 `let` 을 쓰면 block 안에서 컨텍스트가 잡힌다.
  - 또는 `for` 대신 `forEach` 를 쓰면 된다.



React에서 이벤트 핸들러를 binding하는 문제

- [This is why we need to bind event handlers in Class Components in React](https://medium.freecodecamp.org/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb)

  - 기본 원리는 위 강좌에서 나온, 자바스크립트에서 context에 대한 이야기와 같다.

  - React에서 이벤트 핸들러를 bind하지 않은 채 render()에서 호출하면 `this` context가 undefined가 된다.

    - component instance에 bind 되지 않는 이유는 원래 자바스크립트에서 context binding 원리가 그런 것이고..
    - undefined, [자바스크립트 클래스 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)에 따르면 class delaration과 class expression은 [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) 에서 실행되기 때문이다. 이는 constructor, static methods, prototype methods, getter, setter를 포함한다. 여기서 strict mode에서 실행된다 함은 context에서  `this`를 찾을 수 없을 때 global object로 가는 대신 undefined를 반환한다는 뜻.
    - this와 binding에 대해서 더 자세한 것은 [여기](https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md#lexical-this)를 참고.

  - React에서 이벤트 핸들러를 bind하는 세 가지 방법: constructor, [(experimental) public class field](https://babeljs.io/docs/plugins/transform-class-properties/), [arrow function in the callback](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

    ```react
    class Foo extends React.Component {
      // bind in constructor
      constructor(props){
        this.handleClick = this.handleClick.bind(this);
      }
        
      // public class field (not standard yet, babel transpiles it)
      handleClick2 = () => {}
        
      // arrow function in callback
      render() {
        return (
           <button type="button" onClick={e => this.handleClick3(e)}>
            Click Me
          </button>
        )          
      }
    }
    ```

  - 아래의 두 케이스는 모두 ES6의 arrow function을 사용하는데, arrow function에서 `this` 는 lexically bound된다. 즉 자신을 감싸는 함수의 스코프를 가져온다.

    - public class field는 babel로 transpile되면  `Foo` class의 constructor 안에 들어가면서 Foo의 component instance에 bind된다.
    - 그리고 `render()` 는 React가 component instance의 context에서 호출하므로, render() 안쪽에 있는 arrow function은 마찬가지로 Foo의 component instance에 bind된다.

그러면 이 세 가지 방법 중에서는 무엇이 좋을까?

- [The best way to bind event handlers in React](https://medium.freecodecamp.org/the-best-way-to-bind-event-handlers-in-react-282db2cf1530)
- [React, 인라인 함수, 그리고 성능](https://medium.com/steady-study/번역-react-인라인-함수-그리고-성능-9aef85552f2b)