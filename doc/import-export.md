# Importing
There are two kinds of import statements: one where you import to introduce a side effect, and the other where you import to introduce something that module has exported.

## Side-effect imports
There's not much to say here. You can import a module to cause side effects of a module.

```lua
-- module my_project/a.lua
print("foo") -- this is the side effect!
             -- but nothing happens if this module doesn't get required
```

```lua
-- module b.lua
import "my_project.a" -- entirely analogous with 'require("my_project.a")'

print("bar")
```

## Import members from another module
You can import a member from another module, and optionally alias it with another name if there is a name conflict. You can also import an entire module, except that you must alias it as well.
```lua
from "foo" import Foo, bar as baz, * as M
-- generates the following Lua code:
--    local M = require("foo") -- from "foo" import * as M
--    local Foo = M.Foo -- import Foo
--    local baz = M.bar -- import bar as baz

local foo = Foo.new() -- or one might write M.Foo.new()
local bar = baz() -- or one might write M.bar(), but not bar()!
```
# Exporting
As for exporting, there are also two kinds of export statements: one where you can export multiple members, and one where the module exports as that member.

## Exporting a single member
**NOTE**: This was never implemented, but this is what it would have looked like.

We can have this module export as a single member, however it would clash with other `export`/`export as` statements. Thus, a module can only have one `export as` statement, or one or more `export` statements. Both are exclusive to each other.
```lua
export as class Foo
  function foo()
    print("foo!")
  end
end

-- equivalent to the following Lunar code:
class Foo
  function foo()
    print("foo!")
  end
end

return Foo
```

## Exporting multiple members
Instead of writing a table to return with redundant names, one can now simply write `export` in front of the member.

```lua
export class Foo end
export function bar() end
export baz = "quux"

-- equivalent to the following Lunar code:
class Foo end
local function bar() end
local baz = "quux"

return {
  Foo = Foo,
  bar = bar,
  baz = baz,
}
```
