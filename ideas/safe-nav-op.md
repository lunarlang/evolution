# Safe-navigation Operator
Once the type system comes along, this operator (`?.`, `?:`, `?(`, and `?[`) can be used to eliminate nilability from the union type of the member to the left of this operator.

## Rewriting strategy
If the safe-navigation operator was used in an expression, we can simply use the existing expression to our advantage. If it was used as a statement, we will need to rewrite that single statement so that there's an expression to use.

In expressions: rewrite to a PrefixExpression with `x ~= nil and x or nil`

In statements: rewrite to a IfStatement with `x ~= nil or nil`

```lua
-- FunctionCallExpression whose first ArgumentExpression is MemberExpression
print(a?.b)
-- emits the following:
print((a ~= nil and a.b or nil))

-- FunctionCallExpression whose callee is PrefixExpression of BinaryOpExpression whose operator is 'or'
(a?.b or c?.d)()
-- emits the following:
((a ~= nil and a.b) or (c ~= nil and c.d) or nil)()

-- ExpressionStatement whose callee is FunctionCallExpression
a?.b()
-- emits the following:
if a ~= nil then
  a.b()
end

-- AssignmentStatement whose left-hand side is MemberExpression
a?["b"] = "foo"
-- emits the following:
if a ~= nil then
  a["b"] = "foo"
end

-- FunctionCallExpression whose callee is MemberExpression that can be nil
a?("bar")
-- emits the following:
if a ~= nil then
  a("bar")
end
```

This of course can be more complex than just those examples, e.g.
```lua
if a?.b.c?(d?("but why?")) then
  print("you should rewrite this if you happen to come across this")
end
-- emits the following:
if (a ~= nil and a.b.c ~= nil and a.b.c)(d ~= nil and d("but why?")) then
  print("you should rewrite this if you happen to come across this")
end
```
