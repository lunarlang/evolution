# Classes

## Declaration
In Lunar, a class declaration takes the following syntax. This will create a class named `C` with no fields or methods, and a default empty constructor.
```lua
class C
end
```

## Inheritance
Classes can easily inherit from another class, given that it has `<< SuperClassName` just after the name of the class, so `class C << S`. The `super()` statement inside of `constructor` passes the arguments of `super` to its super class.
```lua
class S
  constructor(name)
    self.name = name
  end
end

class C << S
  constructor()
    super("Bob Wellington") -- calls S's constructor with its arguments
  end
end

print(C.new().name) --> "Bob Wellington"
```

## Constructors
When in the context of a class body, declaring a class constructor is easy. The constructor is implicitly given a `self` parameter which is **always** the first parameter of your constructor.
```lua
class C
  constructor(param1, param2)
    -- self is still the first parameter
    self.param1 = param1
    self.param2 = param2
  end
end
```

A default empty constructor is added in if the class does not declare a constructor.

The constructor is called in two ways, either by calling `C.new(...)`, or by calling `super(...)` **only** in the context of a constructor that inherits a super class.

## Fields
Fields directly inside a class has the same effects as the fields set inside of a constructor. They are directly inside of a class just like any other members of a class.

Fields can also be a static member of a class, when prefixed with `static` keyword.
```lua
class C
  -- accessible by typing `C.field` in all contexts
  static field1 = "lol"
  -- accessible by typing 'self.field' in the context of a instance member
  field2 = "hello world!"
end

print(C.field1) --> "lol"
print(C.new().field2) --> "hello world!"
```

## Methods
Methods in a class takes the following syntax, and it can also be prefixed with `static` keyword.
```lua
class C
  function an_instance_method()
    -- there is self here as well
    return self.param1
  end

  static function a_static_method()
    -- there is no self
    return "something"
  end
end

print(C.new():an_instance_method()) -- value of self.param1
print(C.a_static_method()) -- "something"
```

## Static/Instance members
Lunar classes do support separation of static and instance members. This means it's legal to have two members named `foo`, as long one of those `foo` is `static`.
```lua
class C
  foo = "an instance field"
  static foo = "a static field"

  function bar()
    return "an instance method"
  end

  static function bar()
    return "a static method"
  end
end

print(C.new().foo) --> "an instance field"
print(C.foo) --> "a static field"

print(C.new():bar()) --> "an instance method"
print(C.bar()) --> "a static method"
```
