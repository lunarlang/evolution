# Lambda Expressions
*also nicknamed do expressions*

Lambda expressions in Lunar is really just an anonymous function. Rather than typing the verbose variant `function(params) return ... end`, you can greatly simplify this with `|params| ...`.

There are two forms of the lambda expressions. First one is a concise body, and the other one is a block body.

## Concise body
The syntax of a concise body lambda expressions is...
```lua
local a = |param1, param2, ...| param1 + param2

-- Which is the equivalent of...
local a = function(param1, param2, ...)
  return param1 + param2
end
```
It is also legal to have parameterless lambda expressions.
```lua
local b = || 1

-- Which is the equivalent of...
local b = function()
  return 1
end
```

A concise body *implicitly* returns the expression, so you do not need to type `|...| return ...`, never mind the fact that it's illegal syntax.

If you can assign your expression to `local something`, then it is legal to use that same expression. The above example would only be legal if you could do `local something = return ...`, which you cant so it's therefore illegal.

## Block body
**NOTE**: This is currently a candidate for a different syntax: `do |...| code end`.

Block-body lambda expressions are similar to the concise-body variant, with a few key differences.

One difference is: for zero parameters, omit it altogether, and for one or more parameters, add `|param1|` just before the `do` keyword.

Another difference is that they allow multiple statements...
```lua
local a = do
  local a = 1
  local b = 2

  return a + b -- and the return statement is not implicit!
end

-- Which is the same as...
local a = function()
  local a = 1
  local b = 2

  return a + b
end
```
And for block-body lambda expressions with parameters...
```lua
local b = |param1, param2, ...| do
  return param1 + param2
end

-- Which is the same as...
local b = function(param1, param2, ...)
  return param1 + param2
end
```
