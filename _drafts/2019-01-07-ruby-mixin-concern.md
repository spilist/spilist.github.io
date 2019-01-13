---
title: "ruby mixin: include, prepend, extend 그리고 ActiveSupport::Concern"
tags: ["ruby", "rails", "object-oriented-programming", "mixin"]
---

루비는 다른 객체지향 언어와 달리 클래스가 여러 부모로부터 상속받을 수 없다. 하지만 `module` mixin을 활용하면 다중 상속과 비슷한, 또는 더 풍부한 효과를 낼 수 있다. 어떤 언어에서든 mixin이 지나치면 코드를 이해하기 어려워지지만, 잘 사용하면 중복이 줄어들고 깔끔해진다. *(지금부터 참조하는 모든 루비 문서는 `2.5.0` 버전을 기준으로 한다.)*

### [Module](https://ruby-doc.org/core-2.5.0/Module.html) ###

루비의 모듈은 "메서드와 상수의 집합"이다. 모듈은 클래스와 달리 instantiate될 수 없으며, 모듈의 주 목적은 그 안에 정의한 메서드를 다양한 클래스에 `include`, `prepend`, `extend`를 통해 mixin해서 재사용하는 것이다. 이렇게 mixin해서 사용하는 메서드를 `instance methods`라고 부르고, 객체 생성 없이 모듈 자체에서 호출하는 메서드를 `module methods`라고 부른다. `module methods`는 mixin해도 사용할 수 없다.

```ruby
module MyModule
  CONST = "My Const"

  def self.module_method
    "moule_method is called"
  end
  
  def instance_method
    "instance_method is called"
  end
end

MyModule::CONST # => "My Const" 
MyModule.module_method # => "module_method is called"
MyModule.new.instance_method # NoMethodError (undefined method `new' for MyModule:Module)
```

### [Ancestor Chains](https://ruby-doc.org/core-2.5.1/Module.html#method-i-ancestors) ###

루비 모듈의 mixin이 어떻게 이루어지는지 이해하려면 우선 `ancestors` 에 대해 이해해야 한다. 루비에서는 클래스가 생성될 때 ancestors 배열에 클래스 조상의 목록을 저장해둔다. 이 배열은 해당 클래스가 상속받는 모든 클래스, 자기 자신, 그리고 `include`와 `prepend` 를 통해 mixin된 모듈들이 포함된다. 클래스의 인스턴스 메서드를 호출하면 ancestors 배열의 앞에서부터 메서드 정의를 찾아서 실행한다. 

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

`upcase` 는 `String` 클래스에, `<` 는 `Comparable` 모듈에, `object_id` 는 `Kernel` 모듈에 정의되어 있다. 상속 개념과 유사하게, 자신이 정의하고 있지 않은 메서드는 ancestors 목록의 다음 조상에게서 찾는다. 즉 둘 이상의 선조들이 같은 이름의 메서드를 정의하고 있다면 더 가까운 선조에 정의된 메서드를 사용한다. (그리고 BasicObject까지 거슬러 올라갔는데도 찾지 못하면 [BasicObject#method_missing](https://ruby-doc.org/core-2.5.0/BasicObject.html#method-i-method_missing)이 실행된다.)

### [Include](https://ruby-doc.org/core-2.5.0/Module.html#method-i-include)  ###

`include`는 모듈에 정의된 메서드를 클래스에서 활용하는 가장 쉽고 널리 알려진 방법이다. 클래스를 정의할 때 모듈을 include하면, 그 모듈은 ancestors 배열상에서 부모 클래스(`superclass`) 앞에 위치하게 된다. 따라서 include된 모듈에 정의된 메서드가 부모 클래스에서 상속받은 메서드와 이름이 같다면 모듈의 메서드가 호출된다.

```ruby
module MyModule
  def log
    "log by MyModule"
  end
end

class BaseClass
  def log
    "log by BaseClass"
  end
end

class MyClass < BaseClass
  include MyModule
end

MyClass.ancestors # => [MyClass, MyModule, BaseClass, Object, Kernel, BasicObject]
MyClass.instance_method(:log) => #<UnboundMethod: MyClass(MyModule)#log>
MyClass.new.log # => log by MyModule
```

### [Prepend](https://ruby-doc.org/core-2.5.0/Module.html#method-i-prepend) ###

`prepend`는 루비 2.0부터 도입된 mixin으로, include와 아주 유사하게 동작한다. prepend된 모듈은 ancestors 배열상에서 원 클래스의 앞에 위치하게 된다. 메서드 호출은 ancesotrs의 앞에서부터 정의를 찾아나가기 때문에, prepend된 모듈의 메서드는 원 클래스의 메서드보다 우선순위를 가진다. 그리고 여기에 다음 ancestor에서 메서드를 찾는 `super` 키워드를 조합하면, 해당 메서드의 앞이나 뒤에 우리가 원하는 동작을 추가할 수 있다.

```ruby
module MyModule
  def run(args)
    result = super
    "run(#{args.inspect}) finished: #{result.inspect}"
  end
end

class MyClass
  prepend MyModule
  
  def run(args)
    args.sum
  end
end

MyClass.ancestors # => [MyModule, MyClass, Object, Kernel, BasicObject]
MyClass.new.run([1, 2, 3]) # => run([1, 2, 3]) finished: 6
```

### Extend ###



### 참고문헌 ###

- Super
  - https://medium.com/rubycademy/the-super-keyword-a75b67f46f05
  - 
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