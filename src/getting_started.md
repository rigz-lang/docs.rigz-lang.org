# Getting Started

Rigz is a mix of expressions and statements, programs outside of the REPL must end with an expression. Currently only one file is supported but this will change in future versions as imports are improved.

## Hello World

There is no main method in Rigz, the default scope is the main method.

```ruby
puts "Hello, World" # prints "Hello, World", returns none
```

## Expressions

Expressions include everything that isn't a statement; values, do/end blocks, if/else, unless, variables usages, function calls, casting `as Type`, binary expressions, and unary expressions.

The most important difference in Rigz compared to most modern programming languages is that there is no operator precedence, expressions are evaluated from left to right so `1 + 2 * 3` is not equal to `3 * 2 + 1`. **Parenthesis should be used if that is not the desired behavior.** Future versions may allow you to select an option to change how the parser works (Operator precedence or right to left expression evaluation), but that is not currently planned.

### Variables vs Function calls

Variables are looked up through the current call frame, or scope, if they are not present here the parent is checked. The exception to this is if a function exists with the same name, a match will be attempted. If a match is not found this will result in a parse error, future versions will fall back correctly.

### Binary Operators

- `+` - Add
- `-` - Subtract
- `*` - Multiply
- `/` - Divide
- `%` - Modulo, remainder of two values
- `^` - Xor, same behavior as Or, unless both sides are truthy or falsy then it returns none
  - This may change to a bitwise xor in future versions
- `|` - bitwise or
- `||` - Or, returns the first truthy value (errors are false)
- `&` - bitwise and
- `&&` - And, returns the first falsy value
- `>>` - Bit Shift right
- `<<` - Bit shift left
- `<=` - Less than or equal
- `<` - Less than
- `>` - Greater than
- `>=` - Greater than or equal
- `?:` - Elvis operator, if value is none or an error use the right hand side

To see how values of types interact with different types check the definitions [here](https://gitlab.com/rigz_lang/rigz/-/tree/main/crates/vm/src/value?ref_type=heads), documentation will be updated once this is finalized.

### Unary Operators

- `-` - Negative, for ranges and numbers this makes the value negative, booleans are inverted, and all other types remain the same.
- `!` - Not, converts the value to a boolean and inverts it (the only exception are errors which continue to be errors and evaluate to false, `Any.is_err` should be used here)

## Statements

Statements include assignments, function definitions, type definitions, trait definitions, imports and exports.

### Assignments

There are three ways to assign a variable in rigz:

1. In-place assign, this is an immutable variable definition or a mutable re-assignment: `a = 2`
2. `let` assign, this is also an immutable variable: `let a = 2`. In future versions this will allow shadowing.
3. `mut` assign, this is meant for mutable variables. `mut a = "abc"`

If you attempt to overwrite an immutable variable the program will exit with an error, this is one of the few terminal errors and in future versions will be caught at parse time. 

### Function Definitions

Function definitions use the `fn` keyword to define a function, argument types and return types are optional, here are some examples:

By default the return type of standard functions is Any?!, it may be none or an error.

```ruby
fn hello
    "hi there"
end

fn hello = 'hi there'

hello # "hi there"
```

Rigz also supports extension functions, they can be mutable or immutable.

```ruby
fn mut Number.foo -> mut Self
    self *= 3
    self
end
mut a = 2
a.foo.foo.foo # a = 54

fn foo(number: Number) -> Number
    number * 2
end
a = 3
1.to_s + foo a # "1" + 6 = 7
```

Immutable extension functions have the same default return type as standard functions, however if not included the default return type of mutable extensions is mut Self. In future versions the return type will match the type of the last expression.