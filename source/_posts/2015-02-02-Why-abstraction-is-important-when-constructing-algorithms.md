title: Why abstraction is important when constructing algorithms
date: 2015-02-02 09:09:16
tags: programming
---

In order to get better at algorithms (my greatest weakness), I'm currently going through the [Stanford algorithm design course][course]. To learn the concepts better, I decided to implement [Karatsuba multiplication][karatsuba] in JavaScript. [(The fruits of my labor can be found on my miscellaneous algorithm GitHub repository.)][node-misc-problems].

**This algorithm, only 43 lines, took me about an hour to code.** I already knew the details of the algorithm from the video. Why? Because I was prepending the wrong number of zeroes to the number when figuring out where to split the number.

Why was this happening? Originally, my `prependZeroes` method was being done inline, and I wasn't testing it properly.

Abstraction is important because you can test individual parts of an algorithm to make sure they are correct so you can figure out where your algorithm is failing. It also allows your code to be more symmetrical, making it a lot easier to follow.

If I had abstracted the prependZeroes method and had written unit tests for that method specifically, this algorithm would have been much faster to write. Instead, I wasted a ton of time writing `console.log` statements in order to figure out where my bug was.

Break algorithms up into as many functions/parts as possible, so you can test your algorithms much more easily.

[course]: https://www.coursera.org/course/algo
[karatsuba]: http://en.wikipedia.org/wiki/Karatsuba_algorithm
[node-misc-problems]: https://github.com/simplyianm/node-misc-problems/blob/master/src/karatsuba.js
