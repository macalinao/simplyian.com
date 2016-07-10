title: How Go solves date and time formatting
date: 2016-07-10 14:25:41
tags: go
---

Recently, I've had the [pleasure](http://www.dadhacker.com/blog/?p=1585) of working with date and time in a side project written in Go.

I had to parse some dates in YYYY-mm-dd (ISO 8601) format. I read the [Go documentation](https://golang.org/pkg/time/) on the `time` package and found the `time.Parse` method. The examples were really weird:

```go
// See the example for time.Format for a thorough description of how
// to define the layout string to parse a time.Time value; Parse and
// Format use the same model to describe their input and output.

// longForm shows by example how the reference time would be represented in
// the desired layout.
const longForm = "Jan 2, 2006 at 3:04pm (MST)"
t, _ := time.Parse(longForm, "Feb 3, 2013 at 7:54pm (PST)")
fmt.Println(t)

// shortForm is another way the reference time would be represented
// in the desired layout; it has no time zone present.
// Note: without explicit zone, returns time in UTC.
const shortForm = "2006-Jan-02"
t, _ = time.Parse(shortForm, "2013-Feb-03")
fmt.Println(t)
```

Apparently, you need to pass in an example date or time? From the `time.Format` documentation:

> The layout string used by the Parse function and Format method
> shows by example how the reference time should be represented.
> We stress that one must show how the reference time is formatted,
> not a time of the user's choosing. Thus each layout string is a
> representation of the time stamp,
>   Jan 2 15:04:05 2006 MST
> An easy way to remember this value is that it holds, when presented
> in this order, the values (lined up with the elements above):
>   1 2  3  4  5    6  -7

Of course, me being a hasty programmer when it comes to side projects, I spent about 20 minutes figuring out why `time.Parse("2016-01-01", someTime)` didn't work.

This means that `01` will always represent a month and `02` will always represent a day. See the examples below:

```go
t, _ := time.Parse("2006-01-02", "2016-07-04")
fmt.Println(t.Format(time.RFC822))  // prints out 04 Jul 16 00:00 UTC
t, _ = time.Parse("2006-02-01", "2016-07-04")
fmt.Println(t.Format(time.RFC822))  // prints out 07 Apr 16 00:00 UTC
```

At first, I thought: *Ambiguous magic values? HELL NO.* Furthermore, `01` and `02` aren't even constants defined in the package. There is no `time.Month` or `time.Day`. It's just something you have to know. But after looking at other solutions again, I think this is a better way of doing things.

# Strftime sucks

The most popular date formatting function is probably `strftime`. What if you wanted to format a date in the format of `07/10/2016 18:43PM`? What format string would you use? Stop reading for a few seconds and try to think about it.

.

.

.

.

The answer is, you'd use the string `%m/%d/%Y %H:%M:%p`.

Did you get it right, casing and everything? If so, great! You have an amazing memory. However, you probably don't remember every single flag from `strftime` unless you're some sort of masochist.

Now, how would you write this in Go? Remember the 1, 2, 3, 4, 5, 6 mnemonic. The answer is `01/02/2006 15:04PM`. (15 since we're using 24 hour time, and that is 3PM). You just need to memorize 7 numbers and what they mean and you'll be able to format any date.

Let's try a different one: `Sun, 10 Jul 2016 18:43:00`. Try to do both this time.

In strftime: `%a, %e %b %Y %H:%M:%S`.

In Go: `Mon, 02 Jan 2006 15:04:05`. You probably didn't know you were supposed to use `Mon` -- just remember Go does the most obvious thing, which should have been the first day of the week internationally. You can just remember the RFC3339 string `Mon, 02 Jan 2006 15:04:05 -0700` to remember what the placeholders are.

Which one was easier to come up with? Chances are you had to read through a long man page of some sort to figure out the first one. No wonder websites like [For a Good Strftime](http://www.foragoodstrftime.com/) exist!

You may be a Java programmer. Honestly, I think [SimpleDateFormat](http://docs.oracle.com/javase/6/docs/api/java/text/SimpleDateFormat.html) is just as bad. Try this exercise with this instead of strftime and see the results.

While unconventional, Go does time and date formatting really well. Yet another reason why Go is an amazing language.
