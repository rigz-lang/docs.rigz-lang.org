# @test

The `@test` lifecycle is built-in to supply an easy way to write unit tests for your code and can be run with `rigz test foo.rg` or the online REPL using the test button.

Consider the following snippet:

```ruby
fn foo = 42

@test
fn test_foo
  assert_eq foo, 43
end
```

## Upcoming features

To support parameterized testing for a function you'll be able to use @test.assert* lifecycle methods like so:

```ruby
@test.assert_eq([], 42)
fn foo = 42
```

Currently only one lifecycle is supported at a time, this will be changing in future versions to support functionality so that they can be combined where appropriate.