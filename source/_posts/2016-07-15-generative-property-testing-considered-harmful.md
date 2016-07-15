title: Generative property testing considered harmful
date: 2016-07-15 13:27:11
tags: testing
---

There has been a small movement to employ generative property testing in test suites, which is very dangerous.

## What is property testing?

Property testing serves to [check your work][check-your-work] thousands of times in many ways by generating many random values and ensuring that they all meet certain invariants. Property does not refer to an attribute on an object, but it refers to an invariant, like a mathematical property.

For example, let's test a string reversal function:

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
    assertTrue(reverse(reverse(str)) === str)
})
```

The idea is that this function will be run thousands of times to catch weird, random edge cases.

## Who is using this?

QuickCheck is popular in Haskell. https://wiki.haskell.org/Introduction_to_QuickCheck1

Naturally, the Functional Reactive Programming movement has started to notice. https://github.com/jsverify/jsverify

## Why do people use this?

Proponents of property testing believe it allows you to find edge cases easier.

However, I think generative property testing is **bullshit** and causes more problems than it solves.

## Problems

### Test results are non-deterministic

This is the main thing wrong with it. Martin Fowler has [a great article][non-determinism] on why non-deterministic tests are terrible.

### It's harder to cover edge cases

Let's look at a function and its associated generative test.

```js
function 
```

Let's say your search space is all strings. If one string is bad it will never get caught.

If you have a lot of edge cases, that's a different story.

Exhaustive testing is not a proof of correctness. http://blog.regehr.org/archives/917

> "But you can write test cases?"

Sure, but you need to find the edge cases in the first place to do this.

### Slower

Your tests will inevitably run slower if you're running each function 10,000 times instead of once. Test speed is very important for a great feedback loop when practicing TDD or fixing a bug.

### You have to think harder

Writing tests shouldn't force you to think hard about all the different invariants your Fibonnacci function must hold for it to be correct. We are software engineers before we are mathematicians.

An algorithm can be defined by expected inputs and expected outputs. Thinking of generative tests that prove correctness is hard. With unit testing, you test specific classes of inputs and outputs rather than trying to come up with everything.

Furthermore, tests should be documentation. It's easy to think "this function returns this when this happens" rather than "when I use this function, the result should satisfy x y z."

## Solution: Table-driven testing
Fast to write, still adds a ton of test cases with little code, deterministic.

You can write separate "generative" fuzz tests, but don't make them part of your main test suite.

Go makes this easy with `testing.B` -- they are meant to serve as benchmarks but actually run you code thousands of times. Perfect for fuzz testing and doesn't interfere with your tests.

## Conclusion

Generative testing looks cool and new, but it doesn't mean it's good. It may be a great supplement, but you should not consider it part of your main test suite.

## Additional reading

* https://www.schoolofhaskell.com/user/pbv/an-introduction-to-quickcheck-testing
* http://ferd.ca/property-based-testing-basics.html

[check-your-work]: https://blog.8thlight.com/connor-mendenhall/2013/10/31/check-your-work.html
[non-determinism]: http://martinfowler.com/articles/nonDeterminism.html
