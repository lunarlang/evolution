# Lunar Language Specification
Lunar is a **superset** programming language of Lua 5.1, which means it inherits all of Lua 5.1's syntax and semantics. Nothing in Lunar should work any differently if it compiled existing Lua 5.1 code.

Check out the [code examples](#examples) on the bottom of this readme.

**ATTENTION**: Lunar is still early in development! All syntax listed below is subject to changes until `v1` release, in which case it will never be changed.

**Disclaimer**: Existing syntaxes are **always** a candidate for changes, even if it's a breaking change. We will try our best to document them.

---

  - [Classes](/doc/classes.md)
    - [Declaration](/doc/classes.md#declaration)
    - [Inheritance](/doc/classes.md#inheritance)
    - [Constructors](/doc/classes.md#constructors)
    - [Fields](/doc/classes.md#fields)
    - [Methods](/doc/classes.md/#methods)
  - [Lambda Expressions](/doc/lambda.md)
    - [Concise body](/doc/lambda.md#concise-body)
    - [Block body](/doc/lambda.md#block-body)
  - [Import/Export Statements](/doc/import-export.md)
    - [Importing](/doc/import-export.md#importing)
    - [Exporting](/doc/import-export.md#exporting)
  - [Operators](/doc/operators.md)
    - [Self-assignment operators](/doc/operators.md#self-assignment-operators)

---

## Examples
Classes, the staple of object-oriented programming, is implemented in Lunar.
```lua
-- unfortunately no syntax highlighting for lunar yet, so we'll stick with lua
class Account
  constructor(name, balance)
    self.name = name
    self.balance = balance or 0
  end

  function deposit(credit)
    self.balance += credit
  end

  function withdraw(debit)
    self.balance -= debit
  end
end

local account = Account.new("Jeff Bezos", 500)
print(account.balance) --> 500
account:deposit(250)
print(account.balance) --> 750
account:withdraw(300)
print(account.balance) --> 450
```

Lunar adds 7 new operators: `..=`, `+=`, `-=`, `*=`, `/=`, `^=`, and `%=`.
```lua
local message = "hello"
message ..= " world!"
print(message) --> "hello world!"

local a, b = 1, 2
a, b += 1, 2
print(a, b) --> 2, 4
```

Lunar also adds lambda expressions making it more convenient to create short and quick functions as well as big functions.
```lua
local divisible = |dividend, divisor| dividend % divisor == 0
local fizz = |n| do
  local message = ""

  if divisible(n, 3) then message ..= "Fizz" end
  if divisible(n, 5) then message ..= "Buzz" end
  if message == "" then message = n end

  return message
end

for i = 1, 100 do
  print(fizz(i))
end
```

Additionally, Lunar also wraps around the module system with a new import and export statement. (**NOTE**: `export as` syntax were never implemented)
```lua
from "my_project.string_utils" import split

-- this module returns a function, not a table with default export
-- the same as 'return count_chars' at the end of the module
export as function count_chars(str, char)
  local n = 0

  for _, c in pairs(split(str)) do
    if c == char then
      n += 1
    end
  end

  return n
end

-- no need to write 'return count_chars' at the end of the module
```
