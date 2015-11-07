title: Ruby WTF? Escaping single quotes in Ruby using gsub
date: 2015-10-19 10:59:27
tags: Ruby
---

I'm currently working on a project which requires me to escape JavaScript (don't ask why). To get it working, I had to escape single quotes. I was encountering weird behavior in my code, so I ran the following in IRB.

```
2.2.1 :002 > "Doesn't work".gsub("'", "\\'")
 => "Doesnt workt work"
```

[WAT.][wat]

I did a bit of investigation (read: [Stack Overflow][so-answer]) and found that `\'` is a special escape sequence in the gsub replacement -- it's a backreference that represents `$'`, the characters that match after the single quote.

In order to fix this bug, you must escape the backslash within gsub as so:

```
2.2.1 :003 > "Doesn't work".gsub("'", "\\\\'")
 => "Doesn\\'t work"
```

*Nota bene: The double backslash returned by IRB is actually a single escaped backslash -- it hasn't generated another one.*

gsub first escapes everything as a Ruby string, then it parses the result of that string as a regex. It's not documented well at all -- I couldn't find anything on this in the documentation.

Ruby's such a weird language.

[so-answer]: http://stackoverflow.com/questions/2180322/ruby-gsub-doesnt-escape-single-quotes
[wat]: https://www.destroyallsoftware.com/talks/wat
