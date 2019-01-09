---
title: "ruby mixin: include, prepend, extend 그리고 ActiveSupport::Concern"
tags: ["ruby", "rails", "object-oriented-programming", "mixin"]
---

ruby는 다른 객체지향 언어와 달리 클래스의 다중 상속을 지원하지 않는다. 하지만 `module`의 mixin을 활용하면 다중 상속과 비슷한, 또는 더 풍부한 효과를 낼 수 있다. 어떤 언어에서든 mixin을 지나치게 사용하면 코드를 이해하기 어려워지지만, 잘 사용하면 중복이 줄어들고 깔끔해진다. 

### Class와 Module ###

먼저 클래스와 모듈이 어떻게 다른지 간단히 알아보자. 클래스는 객체 지향 프로그래밍에서 많이 들어본 것인데, 모듈은 언제 어떻게 쓰는 걸까? 클래스와 모듈의 차이는 뭘까? (지금부터 참조하는 모든 ruby 문서는 `2.5.0` 버전을 기준으로 한다.)

##### [Class](https://ruby-doc.org/core-2.5.0/Class.html) #####

ruby 공식 문서에 나와있는 클래스의 정의는 다음과 같다.

> Classes in Ruby are first-class objects—each is an instance of class `Class`.

`class`가 한 문장에 네 번이나 나온다. "ruby에서 클래스는 [일급 객체](https://ko.wikipedia.org/wiki/일급_객체)이며, 각 클래스는  `Class` 라는 클래스의 인스턴스이다." 상당히 재귀적인 정의인데, 여기서 `Class`는 우리가 일반적으로 말하는 클래스와 다르다. `Class`, `Module`, `Object`는 모두 ruby에서 `metaclass`라고 불리는데, 자세한 내용은 [ruby metaprogramming](http://ruby-metaprogramming.rubylearning.com/html/seeingMetaclassesClearly.html)과 [ruby object model](https://medium.com/@shubham7/understanding-the-ruby-object-model-685136dd64d9)을 참조하길 바란다.

중요한 사실은 ruby에서 `Class`는 `Module` 을 상속받고, 또 `Module`은 `Object`를 상속받는다는 것이다.

```ruby
class BaseClass
end

class MyClass < BaseClass
end

MyClass.ancestors # [MyClass, BaseClass, Object, Kernel, BasicObject]
```

ancestor chain

##### [Module](https://ruby-doc.org/core-2.5.0/Module.html) #####

모듈은 "한 네임스페이스 안에 묶인 메서드와 상수의 집합"이다. 모듈을 만들 때 `instance methods` 와 `module methods` 를 정의할 수 있다. 모듈은 클래스와 달리 instanitate될 수 없기 때문에,  `instance methods`는 모듈이 다른 클래스 안에 (후술할 `include`, `prepend`, `extend`를 통해) mixin되어야만 사용할 수 있다. 거꾸로, `module methods`는 mixin되어도 사용할 수 없으며, 객체 생성 없이 호출할 수 있다.

```ruby
module MyModule
  CONST = "My Const"

  def self.module_method
    puts "moule_method is called"
  end
  
  def instance_method
    puts "instance_method is called"
  end
end

MyModule::CONST # "My Const" 
MyModule.module_method # "module_method is called"
```



### 참고문헌 ###

- Ruby Mixin
  - [Ruby Constructs: Class, Module and Mixin](https://matt.aimonetti.net/posts/2012/07/30/ruby-class-module-mixins/) by [Matt Aimonetti](https://twitter.com/mattetti)
  - [Include vs Prepend vs Extend](http://leohetsch.com/include-vs-prepend-vs-extend/) by [Leo Hetsch](https://twitter.com/leo_hetsch)
  - [Ruby Mixins & ActiveSupport::Concern](http://engineering.appfolio.com/2013/06/17/ruby-mixins-activesupportconcern/) by [appfolio](https://twitter.com/appfolioeng)
  - [Stop Worrying and Start Being Concerned: ActiveSupport Concerns](http://vaidehijoshi.github.io/blog/2015/10/13/stop-worrying-and-start-being-concerned-activesupport-concerns/) by [Vaidehi](http://www.twitter.com/vaidehijoshi)
- Ruby Singleton Classes
  - [Demystifying Ruby Singleton Classes](http://leohetsch.com/demystifying-ruby-singleton-classes/) by [Leo Hetsch](https://twitter.com/leo_hetsch)
  - [Module#extend: Understanding Ruby Singleton Classes](https://medium.com/@jeremy_96642/module-extend-understanding-ruby-singleton-classes-9dea718c80f2) by [Jem Zornow](https://medium.com/@jeremy_96642)
- Official Documents (ruby 2.5.0 기준)
  - [Module](https://ruby-doc.org/core-2.5.0/Module.html), [Module#module_function](https://ruby-doc.org/core-2.5.0/Module.html#method-i-module_function)
  - [Module#ancestors](https://ruby-doc.org/core-2.5.0/Module.html#method-i-ancestors)
  - [Module#include](https://ruby-doc.org/core-2.5.0/Module.html#method-i-include), [Module#append_features](https://ruby-doc.org/core-2.5.0/Module.html#method-i-append_features), [Module#included](https://ruby-doc.org/core-2.5.0/Module.html#method-i-included)
  - [Module#prepend](https://ruby-doc.org/core-2.5.0/Module.html#method-i-prepend), [Module#prepend_features](https://ruby-doc.org/core-2.5.0/Module.html#method-i-prepend_features), [Module#prepended](https://ruby-doc.org/core-2.5.0/Module.html#method-i-prepended)
  - [Object#extend](https://ruby-doc.org/core-2.5.0/Object.html#method-i-extend), [Module#extend_object](https://ruby-doc.org/core-2.5.0/Module.html#method-i-extend_object), [Module#extended](https://ruby-doc.org/core-2.5.0/Module.html#method-i-extended)
  - [Rails ActiveSupport::Concern](https://api.rubyonrails.org/classes/ActiveSupport/Concern.html)