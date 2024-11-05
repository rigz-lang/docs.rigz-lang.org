# Built In Functionality

There are two built-in functions, `puts` and `log`.

## Puts

`puts` works the same as the ruby counterpart and accepts a list of arguments to print out, each separated by a comma and followed by a new line.

## Log

`log` is a top level function used by the Log module that takes in an argument for the level to log at (either a symbol or string), a string template, followed by the arguments to log.

For example: `log :info, "Hello {}", :world`

## Modules

Modules are written in Rust to provide extra functionality through a `trait` (interface).

There are five built in modules:

- [Std](https://gitlab.com/rigz_lang/rigz/-/blob/main/crates/runtime/src/modules/std_lib.rs?ref_type=heads) - the standard library module which is automatically imported
- [File](https://gitlab.com/rigz_lang/rigz/-/blob/main/crates/runtime/src/modules/file.rs?ref_type=heads) - Functions to interact with files
- [JSON](https://gitlab.com/rigz_lang/rigz/-/blob/main/crates/runtime/src/modules/json.rs?ref_type=heads) - Read and write to json
- [Log](https://gitlab.com/rigz_lang/rigz/-/blob/main/crates/runtime/src/modules/log.rs?ref_type=heads) - Write log messages
- [VM](https://gitlab.com/rigz_lang/rigz/-/blob/main/crates/runtime/src/modules/vm.rs?ref_type=heads) - Interact with the VM directly, these methods may change the VM so use with caution.

## Upcoming Changes

In future versions you will be able to overwrite the `puts` and `log` methods, then the most appropriate function will be used when called.

It's extremely likely that some functionality in the Std module will be moved to an object type in future versions but the design has not been decided yet. 

The following modules are planned:

- Http - an http client with a function similar to Javascript's fetch as well as dedicated methods for each of the HTTP methods.
- Query - A superset module for interacting with data (these are the most likely to become objects)
  - Html - a module to interact with html, mainly for web scraping
  - JSON - jq like functionality to query object data
- Migrations - Initially this will be part of the [migrations](https://crates.io/crates/migrations) CLI tool built on top of [db_dsl](https://crates.io/crates/db_dsl), over time this is expected to become part of the core library.
