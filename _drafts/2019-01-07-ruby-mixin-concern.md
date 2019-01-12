---
title: "ruby mixin: include, prepend, extend 그리고 ActiveSupport::Concern"
tags: ["ruby", "rails", "object-oriented-programming", "mixin"]
---

루비는 다른 객체지향 언어와 달리 클래스의 다중 상속을 지원하지 않는다. 하지만 `module` mixin을 활용하면 다중 상속과 비슷한, 또는 더 풍부한 효과를 낼 수 있다. 어떤 언어에서든 mixin이 지나치면 코드를 이해하기 어려워지지만, 잘 사용하면 중복이 줄어들고 깔끔해진다. *(지금부터 참조하는 모든 루비 문서는 `2.5.0` 버전을 기준으로 한다.)*

### [Module](https://ruby-doc.org/core-2.5.0/Module.html) ###

먼저 모듈에 대해 알아보자. 모듈은 "한 네임스페이스 안에 묶인 메서드와 상수의 집합"이다. 모듈을 만들 때는 `instance methods` 와 `module methods` 를 정의할 수 있다. 모듈은 클래스와 달리 instanitate될 수 없기 때문에,  `instance methods`는 모듈이 다른 클래스 안에 (후술할 `include`, `prepend`, `extend`를 통해) mixin되어야만 사용할 수 있다. 거꾸로, `module methods`는 mixin되어도 사용할 수 없으며, 객체 생성 없이 호출할 수 있다.

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

MyModule::CONST # => "My Const" 
MyModule.module_method # => "module_method is called"
MyModule.new.instance_method # NoMethodError (undefined method `new' for MyModule:Module)
```

### [Ancestor Chains](https://ruby-doc.org/core-2.5.1/Module.html#method-i-ancestors) ###

루비의 mixin을 이해하려면 루비에서 메서드를 호출했을 때 무슨 일이 벌어지는지 이해해야 한다. 루비에서 클래스의 인스턴스에 대한 메서드를 호출하면, `ancestors`라는 목록의 앞쪽에서부터 메서드 정의를 찾아서 실행한다. 이 ancestors는 루비 클래스가 생성될 때 클래스 조상의 목록을 저장해둔 것인데, 목록에는 해당 클래스가 상속받는 모든 클래스, 자기 자신, 그리고 `include`와 `prepend` 를 통해 mixin된 모듈들이 포함된다. 다음 예시를 보자.

```ruby
String.acenstors # => [String, Comparable, Object, Kernel, BasicObject]
String.included_modules # => [Comparable, Kernel]

"foo".instance_of?(String) # => true
"foo".upcase # => "FOO"
"foo" < "bar" # => false
"foo".object_id # => 70264361086420

String.instance_method(:upcase) # => #<UnboundMethod: String#upcase>
String.instance_method(:<) # => #<UnboundMethod: String(Comparable)#<>
String.instance_method(:object_id) # => #<UnboundMethod: String(Kernel)#object_id>
```

`upcase` 는 `String` 클래스에, `<` 는 `Comparable` 모듈에, `object_id` 는 `Kernel` 모듈에 정의되어 있다. 클래스인 `String`이 모듈인 `Comparable` 을 상속받는 것처럼 된다는 개념이 생소하긴 하지만 일단 넘어가자. 어쨌든 루비에서는, 자신이 정의하고 있지 않은 메서드는 ancestors 목록의 다음 후보에서 찾는다는 것이 중요하다. 즉, 복수개의 ancestors들이 같은 이름의 메서드를 정의하고 있다면 순서상 앞의 ancestor 클래스에 정의된 메서드를 사용한다.

```ruby
String.instance_method(:==) # => #<UnboundMethod: String#==>
BasicObject.instance_method(:==) # => #<UnboundMethod: BasicObject#==>

str1 = "foo"
str1.object_id # => 70264361077420
str2 = "foo"
str2.object_id # => 70264369184800
str1 == str2 # => true
```

`String`의 조상 중에 `BasicObject`가 있고, `==`는 양쪽에 정의되어 있으며, `str1`과 `str2`는 오브젝트 입장에서는 다르지만 스트링 입장에서는 같다고 볼 수 있다.


##### [Class](https://ruby-doc.org/core-2.5.0/Class.html) #####

ruby 공식 문서에 나와있는 클래스의 정의는 다음과 같다.

> Classes in Ruby are first-class objects—each is an instance of class `Class`.

`class`가 한 문장에 네 번이나 나온다. "ruby에서 클래스는 [일급 오브젝트](https://ko.wikipedia.org/wiki/일급_객체)이며, 각 클래스는  `Class` 라는 클래스의 인스턴스이다." 상당히 재귀적인 정의인데, 여기서 `Class`는 우리가 일반적으로 말하는 클래스와 다르다. `Class`, `Module`, `Object`는 모두 ruby에서 `metaclass`라고 불리는데, ruby의 메타 프로그래밍에 대해서는 따로 글을 써볼 계획이다. 







### 참고문헌 ###

- Ruby Object Model
  - [Seeing Metaclassess Cleary](http://ruby-metaprogramming.rubylearning.com/html/seeingMetaclassesClearly.html) by [why the lucky stiff](https://whytheluckystiff.net/about/)
  - [Understanding Ruby Object Model](https://medium.com/@shubham7/understanding-the-ruby-object-model-685136dd64d9) by [Shubham Saxena](https://medium.com/@shubham7)
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