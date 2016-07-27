title: Property-based testing considered harmful
date: 2016-07-27 13:27:11
tags: testing, functional programming
---

There has been a small movement to employ property-based testing in test suites, which is very dangerous.

For those who haven't heard of this, property-based testing is a testing methodology which employs **generative testing** of a large set of values to test properties[1] that your functions should hold. That is, it runs your function randomly and makes sure the output makes sense.

You can also think of this as [checking your work][check-your-work] (like in high school math class) thousands of times with all sort of inputs.

Take the following test of a string reversal function:

```javascript
it('should reverse', function(t) {
    var expected = "mada m'i madam";
    var result = reverse("madam i'm adam")
    t.assertEqual(expected, result);
})
```

With a property test, you may have something that looks like this:

```javascript
it('reverse should be reverse', function(t) {
    generateStrings(function(str) {
      t.assert(reverse(reverse(str)) === str)
    })
})
```

The idea is that this function will be run thousands of times to catch weird, random edge cases.

One of the earliest instances of property-based testing is [QuickCheck][quickcheck], which is popular in Haskell. Since recently, many variants have spawned for modern languages, including [JSVerify][jsverify] for JavaScript.

## Why do people use this?

From the README of [elm-check][elm-check], a property-based testing framework for the Elm programming language:

> 1) Writing assertions is a very boring and tedious process.
> 2) More often than not, the inputs chosen to test are completely arbitrary and may give little insight to the correctness of your system.
> 3) Even if a unit test did fail, the failed unit may or may not be helpful to diagnose your problem.

These all sound like plausible arguments, but there are a few major problems that make this testing methodology unfeasible.

## Problems

### Test results are non-deterministic

Non-deterministic tests, also known as flaky, flappy, and random tests, should be avoided in a codebase.

According to [Martin Fowler][non-determinism], the primary benefit of automated tests is to "provide bug detection mechanism by acting as regression tests". When a non-deterministic test goes red, you aren't sure if you broke something or if it's just the non-determinism of the test that is causing problems.

Fowler has a lot of great arguments as to why non-deterministic tests are bad -- [you should read his article on this][non-determinism].

### It's harder to cover edge cases

Take the following function.

```js
function doSomething(str) {
    if (str === 'magic') {
        return str;
    }
    return reverse(str);
}
```

Let's say your search space is all strings. If you never pass in the string 'magic', an entire code path will never get triggered.

Obviously this is a very simple example, but one can imagine a case where a very specific input can cause a detrimental bug to be triggered. Property testing forces you to think about solely the larger picture, not the individual code paths.

> "But you can write test cases to cover these things?"

Sure, but you need to find the edge cases in the first place to do this. If you only consider property testing in your initial test suite, you may never trigger the edge case in your generative tests.

### Slower

Your tests will inevitably run slower if you're running each function 10,000 times instead of once. Test speed is very important for a great feedback loop when practicing TDD or fixing a bug.

### You have to think harder

Writing tests shouldn't force you to think hard about all the different invariants your Fibonnacci function must hold for it to be correct. We are software engineers before we are mathematicians.

An algorithm can be defined by expected inputs and expected outputs. Thinking of generative tests that prove correctness is hard, as it forces you to reason about how your algorithm should respond rather than how your algorithm works. With unit testing, you test specific classes of inputs and outputs to cover known code paths rather than trying to come up with everything.

Furthermore, tests should be documentation. It's easy to think "this function should always satisfy this property" rather than "when I use this function, the result should satisfy x y z."

## A possible solution: Table-driven testing

This is in response to the first bullet point made by the author of [elm-check][elm-check]

> 1) Writing assertions is a very boring and tedious process.

[Table-driven tests][tdt] are fast to write, add a ton of test cases with litle code, and are most importantly deterministic.

Below is an example taken directly from the above link:

```go
`var flagtests = []struct {
    in  string
    out string
}{
    {"%a", "[%a]"},
    {"%-a", "[%-a]"},
    {"%+a", "[%+a]"},
    {"%#a", "[%#a]"},
    {"% a", "[% a]"},
    {"%0a", "[%0a]"},
    {"%1.2a", "[%1.2a]"},
    {"%-1.2a", "[%-1.2a]"},
    {"%+1.2a", "[%+1.2a]"},
    {"%-+1.2a", "[%+-1.2a]"},
    {"%-+1.2abc", "[%+-1.2a]bc"},
    {"%-1.2abc", "[%-1.2a]bc"},
}

func TestFlagParser(t *testing.T) {
    var flagprinter flagPrinter
    for _, tt := range flagtests {
        s := Sprintf(tt.in, &flagprinter)
        if s != tt.out {
            t.Errorf("Sprintf(%q, &flagprinter) => %q, want %q", tt.in, s, tt.out)
        }
    }
}
```

The test is rather terse for the amount of code it is testing. I am convinced that this is one of the better testing strategies, as it minimizes copy and paste and is easy to extend.

## Using property-based tests without compromising determinism

You can write separate "generative" fuzz tests, but don't make them part of your main test suite.

Go makes this easy with `testing.B` -- they are meant to serve as benchmarks but actually run you code thousands of times. Perfect for fuzz testing and doesn't interfere with your tests.

## Conclusion

Generative testing looks cool and new, but it doesn't mean it's good. It may be a great supplement, but you should not consider it part of your main test suite.

## Additional reading

* https://www.schoolofhaskell.com/user/pbv/an-introduction-to-quickcheck-testing
* http://ferd.ca/property-based-testing-basics.html

[check-your-work]: https://blog.8thlight.com/connor-mendenhall/2013/10/31/check-your-work.html
[non-determinism]: http://martinfowler.com/articles/nonDeterminism.html
[quickcheck]: https://wiki.haskell.org/Introduction_to_QuickCheck1
[jsverify]: https://github.com/jsverify/jsverify
[elm-check]: https://github.com/TheSeamau5/elm-check
[tdt]: https://github.com/golang/go/wiki/TableDrivenTests

1: To the non-functional programmers: "property" does not refer to an attribute on an object, but it refers to an invariant, like a mathematical property. For example, sqrt(x) > 0 is a property that must always hold if we are dealing with real numbers.
