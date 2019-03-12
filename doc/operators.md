# Operators

## Self-assignment operators
Lunar adds 6 new operators for self-assignment operators: `..=`, `+=`, `-=`, `*=`, `/=`, and `^=`.

These type of self-assignment operators are applicable to the same syntax you use to assign to local (not declaring!) or global variables.

These are all legal.
```lua
local a, b = 1, 2
a, b += 1, 2 --> a = 2, b = 4
```

We do not discard extra expressions so if you intended to have side effects while self-assigning to a variable, it's as easy as...
```lua
local c = 3
c += 4, 5 --> c = 7, and 5 is assigned to nothing

local function some_number(n)
  print(n)
  return n
end

local d = 4
d += 5, some_number(6) --> d = 9, some_number is called and prints 6
```

We have a special case where if you have too many **members** and too few **expressions**, it will emit invalid Lua. This is intentional!

These will throw an error at run time. Eventually this will be caught at compile time, but currently this is a good way of dealing with too many members.
```lua
local a, b = 1, 2
a, b += 1

-- That would emit the following...
a, b = a + 1, b + nil -- ack! using + operator on a nil value is an error!
```
