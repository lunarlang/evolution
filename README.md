# Lunar Language Specification
Lunar is a **superset** programming language of Lua 5.1, which means it inherits all of Lua 5.1's syntax and semantics. Nothing in Lunar should work any differently if it compiled existing Lua 5.1 code.

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
  - [Operators](/doc/operators.md)
    - [Self-assignment operators](/doc/operators.md#self-assignment-operators)
