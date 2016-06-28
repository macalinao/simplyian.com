title: Should you test private methods?
date: 2016-06-28 15:22:06
tags:
- software
- testing
---

At the last place I worked, I was told not to test private methods since it was an “implementation detail”. Some of these methods involved complex math or tons of branching.

I believe private methods should be tested. Would you only test a car by driving it in a million different conditions? Or would you also test the individual components to see if they are all functioning well? I say the latter.

# Disadvantages of only testing public methods

## You need to write more tests
By only testing public methods, you have to write an exponential amount of test cases to cover every permutation of branching possible in all of the methods each method calls.

For example, if you write a method that calculates something with 4 possible outcomes, you should write 4 tests to cover those branches. However, if that method is private and is called by a function that calculates something with another 3 possible outcomes, you must write 4 * 3 = 12 tests to test every branch.

This is pretty hard to maintain, even if you use something like table-driven tests. When you add another branch, you need to double the amount of tests in your code.

## Your tests run much slower
In general, you only export functions that will be called by other people. Thus these functions are likely to call all sorts of different injected services to perform whatever action they need to accomplish.

To keep your tests reproducible and deterministic, you should be mocking all of the services your functions call in the testing phase. Doing this can take a lot of precious CPU cycles if you have, say, 100 services to stub out.

Furthermore, as said above, you have many more tests to write to test all branches, so you need to worry about running a lot more tests.

## Tests are less concise
In general, integration tests (tests between many functions) have a lot more going on, so they will be much less concise. A test also serves as documentation, so writing a huge test is much harder to parse than a tiny test that documents only what you’re looking at.

## Tests are harder to debug when they break
Less code is easier to debug. Granularity is great because it isolates the bug better.

# Conclusion
Test your private methods. Write less tests. Spend less time debugging. Be a happy developer.

