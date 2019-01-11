- Feature Name: Remove Traits from Pony
- Start Date: 2019-01-11
- RFC PR: 
- Pony Issue: 

# Summary

Remove traits from Pony, leaving only interfaces.

# Motivation

As it currently stands with Pony. Traits and Interfaces are almost identical.  There's nothing you can do with one that you can't do with the other.

New users coming to Pony often end up in IRC asking what the difference between the two are. We generally explain that traits are nominal subtyping and interfaces are structural subtyping and this is mostly true except, that you use the `is` keyword when implementing an interface to get compile time checks to make sure you are implementing said interface.

All in all, its rather confusing. 

Where possible, we should be aiming to provide the minimum number of concepts in Pony to allow a user to solve the problem they have at hand. There is no problem that traits solves that can not be solved with interfaces. There are however things you can do with structual subtyping and interfaces that you can't do with traits.

As Pony currently stands, traits are an anemic form of interfaces and it is my belief that they should be removed from the language.

# Detailed design

This is really a removal checklist:

- Update the standard library to use `interface` instead of `trait`. Current usages are in:

* builtin/_partial_arithmetic.pony
* builtin/real.pony
* builtin_test/_test.pony
* cli/command_spec.pony
* files/_test.pony
* format/format_spec.pony
* format/prefix_spec.pony
* logger/_test.pony
* ponybench/_runner.pony
* ponybench/benchmark.pony
* ponytest/_group.pony
* ponytest/test_list.pony
* ponytest/unit_test.pony
* random/random.pony

Additionally, we need to update tutorial, website, and patterns sites to use interface instead of tutorial.

We should also review all open issue

# How We Teach This

For users familiar with Pony, we are "teaching" the removal:

Note the change in release notes.

For users who come to Pony after this change, we don't have anything to teach. There is one less concept for them to learn. They will only have to learn about interfaces.

However, the [existing tutorial documentation](https://tutorial.ponylang.io/types/traits-and-interfaces.html) should be expanded as interfaces are mostly an afterthought to traits. For example, the usage of `is` is only discussed in relation to traits despite the same functionality being available for interfaces as well.

# How We Test This

Verify that all existing pony and standard library tests continue to pass after the change.

# Drawbacks

This will break existing user code.

# Alternatives

Leave traits in the language.

# Unresolved questions

None that I am aware of.