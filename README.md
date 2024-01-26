Compliance tests for the [RESO RCP-19][RCP-19]'s validation expressions.

## What is this?

This repository contains tests to help encourage compliance and interoperability for parsers and interpreters that target [RCP-19] validation expressions.

Every test takes a known set of inputs and a validation expression and indicates the expected output.

The tests are provided in JSON for maximium interoperability. It is assumed that most languages being used to build validation expression interpreters have an easy way to parse JSON.


## Who is it for?

This repository is most valuable to people implementing a parser and interpreter for [RCP-19] validation expressions. In conjunction with the [RCP-19] spec, these tests can help validate that a parser and interpreter are interoperable with the spec and other implementations.


## How do I run it?

These tests are not runnable on their own. They are intended to be used as inputs into a particular implementation of a validation expression interpreter.

Individual implementations may have ways to pull in these tests and run the test suite.


## Can I add more tests? What if I think the interpretation of the spec is wrong?

YES! Open a pull request. This is intended to be a community-owned resource that helps encourage interoperability between implementations.


## Who is using these tests?

* [rets_expression](https://github.com/zenlist/rets_expression) – [Zenlist](https://zenlist.com)'s parser written in Rust, used to power [rules.zenlist.dev](https://rules.zenlist.dev).

If you are using these tests for your own interpeter – whether that interpeter is open source and has a link or closed source and does not have a link – please feel free to open a PR to add to this list.


## Structure of the tests

The tests in the `tests` folder are broken down into files that are named according to their purpose.

### Files

Each **file** contains:
* a file name, and
* one or more **test set**s.

### Test Sets

Each **test set** contains:
* **name** (required, string) – the name of the particular test set.
* **context** (required, JSON object) – describes the inputs to the interpreter, which typically includes things like the data payload being validated and the previous data payload for use with `LAST FieldName` expressions.
* **checks** (required, JSON array) – an array of checks that describe both the expression to be run (within the provided **context**) and the expected output.

### Context

Each **context** contains:
* **value** (required, JSON object) – the data payload that is being evaluated. This is used for `FieldName`/`[FieldName]` expressions.
* **previousValue** (optional, JSON object) – the previous data payload that is being evaluated. This is used for `LAST FieldName`/`[LAST FieldName]` expressions.
* **now** (optional, [RFC3339] timestamp) – the exact timestamp to use for `.NOW.` expressions. This is sometimes required to test date/time assumptions.
* **timezone** (optional, [IANA tzdb] identifier) – used with the **now** context, describes the timezone that the evaluator is operating in.

### Check

Each **check** contains:
* **expr** (required, string) – the RCP-19 Validation Expression being evaluated.
* One of (required):
  * **expected** (JSON) – the expected output of the expression.
  * **error** (the exact value `true`) – the expression is expected to return an error (either because of a parse error or an evaluation error)



[RCP-19]: https://github.com/RESOStandards/transport/blob/main/proposals/web-api-validation-expression.md
[RFC3339]: https://www.rfc-editor.org/rfc/rfc3339
[IANA tzdb]: https://www.iana.org/time-zones
