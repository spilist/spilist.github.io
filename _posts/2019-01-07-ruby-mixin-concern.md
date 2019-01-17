---
title: "루비 mixin: include, prepend, extend 그리고 ActiveSupport::Concern"
tags: ["ruby", "rails", "object-oriented-programming", "mixin"]
---

루비는 다른 객체지향 언어와 달리 클래스가 여러 부모로부터 상속받을 수 없습니다. 하지만 `module`을 mixin하면 다중 상속과 비슷한, 또는 더 풍부한 효과를 낼 수 있죠. 어떤 언어에서든 mixin이 지나치면 코드를 이해하기 어려워지지만, 잘 사용하면 중복이 줄어들고 깔끔해집니다. 루비에서 mixin을 어떻게 사용하는지 파헤쳐봅시다.

*(글의 주제에 집중하기 위해 일부러 디테일을 많이 생략했는데, 이 글에서 다루지 않은 부분이 궁금하시다면 **참고문헌** 섹션의 링크들을 읽어보시길 바랍니다.)*

## 배경지식 ##

기본적으로 다음 두 개념을 알아야 루비의 mixin에 대해 이해할 수 있습니다.

#### [Module](https://ruby-doc.org/core-2.5.0/Module.html) ####

루비에서 **모듈**이란 한마디로 "메서드와 상수의 집합"입니다. 모듈은 클래스와 달리 instantiate될 수 없으며, 모듈의 주 목적은 그 안에 정의한 메서드를 다양한 클래스에 `include`, `prepend`, `extend`를 통해 mixin해서 재사용하는 것입니다. 이렇게 mixin해서 사용하는 메서드를 `instance methods`라고 부르고, 객체 생성 없이 모듈 자체에서 호출하는 메서드를 `module methods`라고 부릅니다. `module methods`는 mixin해도 사용할 수 없습니다.

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

irb > MyModule::CONST # => "My Const" 
irb > MyModule.module_method # => "module_method is called"
irb > MyModule.new.instance_method # NoMethodError (undefined method `new' for MyModule:Module)
```

#### [Ancestors](https://ruby-doc.org/core-2.5.1/Module.html#method-i-ancestors) ####

루비에서는 클래스가 생성될 때 **ancestors** 배열에 클래스 조상의 목록을 저장해둡니다. 이 클래스가 상속받는 모든 클래스, 자기 자신, 그리고 `include`와 `prepend` 를 통해 mixin된 모듈들이 ancestors에 포함되죠. 

클래스의 인스턴스 메서드를 호출하면 ancestors 배열의 앞에서부터 메서드 정의를 찾습니다. 상속 개념과 유사하게, 메서드 정의를 찾지 못하면 다음 조상에게서 찾는 식입니다. 즉 둘 이상의 선조들이 같은 이름의 메서드를 정의하고 있다면 더 가까운 선조에 정의된 메서드를 실행합니다. 참고로 `BasicObject`까지 거슬러 올라갔는데도 메서드를 찾지 못하면 [BasicObject#method_missing](https://ruby-doc.org/core-2.5.0/BasicObject.html#method-i-method_missing)이 실행되는데, 몇몇 루비 gem들은 이를 이용해 이해하기 쉽지 않은 흑마술을 부리기도 하더군요.

```ruby
irb > String.acenstors # => [String, Comparable, Object, Kernel, BasicObject]
irb > String.included_modules # => [Comparable, Kernel]

irb > "foo".instance_of?(String) # => true
irb > "foo".upcase # => "FOO"
irb > "foo" < "bar" # => false
irb > "foo".object_id # => 70264361086420

irb > String.instance_method(:upcase) # => #<UnboundMethod: String#upcase>
irb > String.instance_method(:<) # => #<UnboundMethod: String(Comparable)#<>
irb > String.instance_method(:object_id) # => #<UnboundMethod: String(Kernel)#object_id>
```

## 루비에서의 mixin ##

#### [Include](https://ruby-doc.org/core-2.5.0/Module.html#method-i-include)  ####

`include`는 모듈에 정의된 메서드를 클래스에서 재사용하는 가장 쉽고 널리 알려진 방법입니다. 클래스를 정의할 때 어떤 모듈을 include하면, 그 모듈은 ancestors 배열상에서 부모 클래스(`superclass`) 앞에 위치하게 되죠. 따라서 메서드 이름이 같다면 include된 모듈이 우선순위를 가집니다.

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

irb > MyClass.ancestors # => [MyClass, MyModule, BaseClass, Object, Kernel, BasicObject]
irb > MyClass.instance_method(:log) => #<UnboundMethod: MyClass(MyModule)#log>
irb > MyClass.new.log # => log by MyModule
```

#### [Prepend](https://ruby-doc.org/core-2.5.0/Module.html#method-i-prepend) ####

`prepend`는 루비 `2.0`부터 도입된 mixin으로, include와 동작은 유사하나 용도는 다릅니다. include가 모듈의 메서드를 그대로 사용하기 위함이라면, prepend는 클래스의 기존 메서드를 꾸며주는 역할을 합니다. 이게 가능한 이유는, prepend된 모듈이 ancestors 배열상에서 원 클래스의 앞에 위치하기 때문입니다. 앞서 말씀드렸듯 메서드 호출은 ancesotrs의 앞에서부터 정의를 찾아나가기 때문에, prepend된 모듈의 메서드는 원 클래스의 메서드보다 우선순위가 높습니다. 그리고 여기에 다음 ancestor에서 메서드를 찾는 `super` 키워드를 조합하면, 해당 메서드의 앞이나 뒤에 우리가 원하는 동작을 추가할 수 있죠.

```ruby
module MyModule
  def sum_of(numbers)
    result = super # calls MyClass#sum
    "sum_of(#{numbers.inspect}) finished: #{result.inspect}"
  end
end

class MyClass
  prepend MyModule
  
  def sum_of(numbers)
    numbers.sum
  end
end

irb > MyClass.ancestors # => [MyModule, MyClass, Object, Kernel, BasicObject]
irb > MyClass.new.sum_of([1, 2, 3]) # => sum_of([1, 2, 3]) finished: 6
```

#### [Extend](https://ruby-doc.org/core-2.5.0/Module.html#method-i-extend_object) ####

`extend`는 다른 두 mixin과 동작방식이 다릅니다. include와 prepend가 클래스의 ancestors 배열에 관여하여 **인스턴스 메서드를 확장**하는 개념이었다면, extend는 클래스의 **클래스 메서드를 확장**합니다. 

```ruby
module MyModule
  def log
    "log by MyModule"
  end
end

class MyClass
  extend MyModule
end

irb > MyClass.log # => log by MyModule
irb > MyClass.ancestors # => [MyClass, Object, Kernel, BasicObject]
```

그런데 위 스니펫에서 보듯이 extend해도 MyClass의 ancestors에 변화가 없습니다. 그러면 extend는 어떻게 클래스가 모듈의 메서드에 접근할 수 있게 해주는 것일까요? 아니, 애초에 클래스 메서드는 어떻게 실행되는 것일까요?

사실 루비에서 클래스 메서드라는 것은 존재하지 않습니다. 루비에서는 모든 것이 오브젝트이고, '클래스'도 다른 무언가의 인스턴스이며, 클래스 메서드도 결국은 인스턴스 메서드이기 때문입니다. 이에 대해 확실하게 이해하려면 싱글톤 클래스와 오브젝트 모델에 대해 알아야 하지만, 이 글은 거기까지는 다루지 않으려고 합니다. 다만 "클래스 메서드는 싱글톤 클래스 안에 정의되고, 모듈을 extend하면 싱글톤 클래스가 확장된다"는 것만 기억해 두죠.

```ruby
irb > MyClass.singleton_class # => #<Class:MyClass>
irb > MyClass.singleton_class.ancestors => [#<Class:MyClass>, MyModule, #<Class:Object>, #<Class:BasicObject>, Class, Module, Object, Kernel, BasicObject]
```

MyClass가 extend한 MyModule은 `MyClass.singleton_class` 의 ancestors로 존재합니다. 위치는 include와 유사하게 클래스의 싱글톤 클래스 다음이며, 싱글톤 클래스도 클래스이기 때문에 ancestors의 동작 방식도 같습니다. `MyClass.log`는 먼저 `#<Class:MyClass>`에서 메서드 정의를 찾아보고, 찾을 수 없으면 다음 ancestor인 `MyModule`에서 찾습니다.

## 레일즈에서의 mixin ##

#### include + extend? ####

모듈을 사용하다 보면, 어떤 모듈은 하나의 클래스에 extend하면서 동시에 include하고 싶을 때가 생깁니다. 

```ruby
module MyModule
  def included_method
    "included"
  end
  
  def extended_method
    "extended"
  end
end

class MyClass
  include MyModule
  extend MyModule
end

irb > MyClass.included_method # => "included"
irb > MyClass.extended_method # => "extended"
irb > MyClass.new.included_method # => "included"
irb > MyClass.new.extended_method # => "extended"
```

보다시피 한 모듈을 두 번 mixin하는 것은 문법적으로는 가능하지만, 모든 모듈 메서드가 클래스 메서드가 되면서 동시에 인스턴스 메서드도 되기 때문에 우리가 원했던 상황과는 다릅니다. 

이 문제는 모듈을 mixin할 때 호출되는 hook([included](https://ruby-doc.org/core-2.5.0/Module.html#method-i-included), [prepended](https://ruby-doc.org/core-2.5.0/Module.html#method-i-prepended), [extended](https://ruby-doc.org/core-2.5.0/Module.html#method-i-extended))을 이용하여 해결할 수 있습니다. hook의 파라미터로 모듈을 mixin한 클래스가 넘어오기 때문이데요, 다음은 이를 활용한 레일즈 코드 스니펫입니다.

```ruby
module DisabledModule
  def self.included(base) # base == Record
    base.extend ClassMethods
    base.class_eval do
      scope :disabled, -> { where(enabled: false) }
    end
  end

  module ClassMethods
    def available_list
      where(enabled: true)
    end
  end
  
  def disabled?
    enabled == false
  end
end

class Record < ApplicationRecord
  include DisabledModule
end
```

 `Record` 클래스가 `DisabledModule`을 include함으로써 다음 세 가지가 가능해집니다.

- `Record.new.disabled?`: 모듈이 include되어 인스턴스 메서드가 확장됩니다.
- `Record.available_list`: Record 클래스가 `DisabledModule::ClassMethods`를 extend하여 클래스 메서드가 확장됩니다.
- `Record.disabled`: [class_eval](https://ruby-doc.org/core-2.5.0/Module.html#method-i-class_eval)을 통해 Record 클래스의 컨텍스트에서 블록이 실행되고, Record 모델에 `disabled` scope가 정의됩니다.

#### ActiveSupport::Concern ####

루비 1.9.3에서 included hook이 도입되고부터 위와 같은 패턴을 사용하는 케이스가 많아졌는데, 레일즈 4.0부터 생긴  `ActiveSupport::Concern` 은 이 패턴을 간편하게 줄여줍니다.

 `ActiveSupport::Concern`을 extend한 모듈에서는 다음 두 블록을 사용할 수 있습니다.

- `included` 블록: `self.included(base)`를 대체합니다. Concern에서 이 블록을 class_eval 해주기 때문에, `before_action`이나 `has_many` 등 rails의 여러 유용한 hook이나 association을 재사용하기 쉬워집니다.
- `class_methods` 블록: `base.extend ClassMethods`를 대체합니다. 이 블록 안에서 정의된 메서드는 모듈을 include한 클래스의 클래스 메서드로 확장됩니다.

```ruby
module DisabledModule
  extend ActiveSupport::Concern
  
  included do
    scope :disabled, -> { where(enabled: false) }
  end
  
  class_methods do
    def available_list
      where(enabled: true)
    end
  end

  def disabled?
    enabled == false
  end
end

class Record < ApplicationRecord
  include DisabledModule
end
```

#### 모듈간 의존성 문제 ####

여기까지만 해도 훌륭하지만, `ActiveSupport::Concern`은 모듈간 의존성 문제도 잘 해결해줍니다. 다음 코드 스니펫은 기존에 있던 `UsefulModule`을 `MyModule`로 확장하려는 의도를 가지고 있는데요.

```ruby
module UsefulModule
  def self.included(base)
    base.class_eval { has_many :something }
  end
end

module MyModule
  include UsefulModule
  
  def another_useful_method
  end
end


class MyClass
  def self.has_many(*args)
  	puts "MyClass has many #{args.inspect}"  
  end
  
  include MyModule
end

irb > # NoMethodError (undefined method `has_many' for MyModuleB:Module)
```

 `UsefulModule`의 included hook에 들어온 `base`가 `MyClass`가 아닌 `MyModule`이기 때문에, 스니펫을 실행하면 에러가 뜹니다. 이제 `ActiveSupport::Concern`을 쓴 스니펫을 보시죠.

```ruby
module UsefulModule
  extend ActiveSupport::Concern
  
  included do
    has_many :something
  end
end

module MyModule
  extend ActiveSupport::Concern
  include UsefulModule
  
  def another_useful_method
  end
end

class MyClass
  def self.has_many(*args)
  	puts "MyClass has many #{args.inspect}"  
  end
  
  include MyModule
end

irb > # MyClass has many [:something]
irb > MyClass.ancestors # => [MyClass, MyModuleB, MyModuleA, Object, Kernel, BasicObject]
```

이 스니펫은 문제없이 실행되고, 의도대로 `MyClass`의 `has_many` 메서드가 호출됩니다(레일즈에서는 association 정의를 실행하게 되겠죠). 이게 가능한 이유는 `ActiveSupport::Concern`을 extend한 모듈의 모든 included 블록이, extend하지 않은 최초의 모듈에서 include된 것처럼 (즉 `UsefulModule`이 `MyClass`에 직접 include된 것처럼) 지연 실행되기 때문입니다. 좀 어려운데, 아무튼 개발자 입장에서는 `ActiveSupport::Concern`을 extend한 모듈을 다른 모듈에서도 안심하고 include할 수 있다는 걸 기억하시면 될 것 같습니다. 더 자세하게 알고 싶으신 분은 [소스코드](https://github.com/rails/rails/blob/94b5cd3a20edadd6f6b8cf0bdf1a4d4919df86cb/activesupport/lib/active_support/concern.rb)를 보셔도 좋겠네요. 

## 끝내며: object model 맛보기  ##

루비와 레일즈의 mixin에 대해 알아봤습니다. 되도록 간결하게 적고 싶었는데 그래도 상당히 길어졌네요.사실 너무 길어질까봐 별다른 설명 없이 적어놓은 문장이 꽤 있는데요. 그중 가장 이게 가장 중요한 것 같습니다.

>  루비에서는 모든 것이 오브젝트이고, '클래스'도 다른 무언가의 인스턴스이며

루비에서는 모든 클래스는 `Class` 클래스의 인스턴스이고, `Class`와 `Module`도 `Class` 클래스의 인스턴스입니다.

```ruby
irb > class MyClass; end
irb > MyClass.instance_of?(Class) # => true
irb > Class.instance_of?(Class) # => true
irb > Module.instance_of?(Class) # => true
irb > Class.ancestors # => [Class, Module, Object, Kernel, BasicObject]
```

 `MyClass`는 `Class` 클래스의 인스턴스이므로, `Class`에 정의된 인스턴스 메서드를 `MyClass.xxx`형태로 쓸 수 있습니다.

```ruby
irb > Class.instance_methods(false) # [:new, :allocate, :superclass]
irb > MyClass.ancestors # => [MyClass, Object, Kernel, BasicObject]
irb > MyClass.superclass # => Object
irb > Class.new.superclass # => Object
irb > Class.superclass # => Module
```

사실 `include`와 `prepend`도 Module 클래스의 인스턴스 메서드인데, Class 클래스가 Module 클래스를 상속받기 때문에 우리가 클래스 정의 내에서 사용할 수 있는 것이죠. 오브젝트 모델에 대해 파고들어보면 꽤 복잡하면서도 흥미로운데요. 이에 대해서는 다음 기회에 글을 써보려고 합니다.

## 참고문헌 ##

- Mixin
  - [Ruby Constructs: Class, Module and Mixin](https://matt.aimonetti.net/posts/2012/07/30/ruby-class-module-mixins/) by [Matt Aimonetti](https://twitter.com/mattetti)
  - [Include vs Prepend vs Extend](http://leohetsch.com/include-vs-prepend-vs-extend/) by [Leo Hetsch](https://twitter.com/leo_hetsch)
  - [Ruby Mixins & ActiveSupport::Concern](http://engineering.appfolio.com/2013/06/17/ruby-mixins-activesupportconcern/) by [appfolio](https://twitter.com/appfolioeng)
  - [Stop Worrying and Start Being Concerned: ActiveSupport Concerns](http://vaidehijoshi.github.io/blog/2015/10/13/stop-worrying-and-start-being-concerned-activesupport-concerns/) by [Vaidehi](http://www.twitter.com/vaidehijoshi)
- Singleton Classes
  - [Demystifying Ruby Singleton Classes](http://leohetsch.com/demystifying-ruby-singleton-classes/) by [Leo Hetsch](https://twitter.com/leo_hetsch)
  - [Module#extend: Understanding Ruby Singleton Classes](https://medium.com/@jeremy_96642/module-extend-understanding-ruby-singleton-classes-9dea718c80f2) by [Jem Zornow](https://medium.com/@jeremy_96642)
- Super
  - [The super keyword in Ruby](https://medium.com/rubycademy/the-super-keyword-a75b67f46f05) by [Mehdi Farsi](https://medium.com/@farsi_mehdi)
  - https://ruby-doc.org/core-2.5.0/doc/keywords_rdoc.html 
- Object Model / Metaprogramming
  - [Seeing Metaclassess Cleary](http://ruby-metaprogramming.rubylearning.com/html/seeingMetaclassesClearly.html) by [why the lucky stiff](https://whytheluckystiff.net/about/)
  - [Understanding Ruby Object Model](https://medium.com/@shubham7/understanding-the-ruby-object-model-685136dd64d9) by [Shubham Saxena](https://medium.com/@shubham7)