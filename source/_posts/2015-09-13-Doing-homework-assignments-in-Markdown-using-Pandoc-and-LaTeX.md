title: "Doing homework assignments in Markdown using Pandoc and LaTeX"
date: 2015-09-13 09:57:43
tags:
- markdown
- pandoc
- latex
---

[Markdown][markdown] is a really awesome format for text and prose. It's really easy to manage in any text editor, and it's quick to write. It has a lot of features, including **bolding**, *italicizing*, lists, quotes, embedded code, and more. It's so easy to write that it's the "language" of choice for many major websites such as StackOverflow and Reddit, it being much easier to implement and looking nicer than a WYSIWYG text editor. I'm even writing this blog post using Markdown. However, you can't really send someone a Markdown document. It's meant to be processed into a more readable format, most usually HTML.

[LaTeX][latex] is a great tool for typesetting text. It has a lot of flexibility and standardizes how documents look. It's so powerful that it has become the defacto tool to create research papers. However, there is definitely a learning curve in using the software, and the source doesn't look very nice.

[Pandoc][pandoc] brings the best of both worlds. It allows conversion of Markdown to a predefined LaTeX template, allowing you to use Markdown to write LaTeX documents in a format that works out 99% of the time if you're just writing notes or submitting a linear homework assignment. Usage is simple:

```bash
pandoc input.md -o output.(pdf|tex)
```

This generates either a `.tex` or `.pdf` (compiled LaTeX) file that looks pretty good using the default settings.

## Generating PDFs quickly

Since I use Markdown so much to generate PDFs, I've created the following shell function:

```bash
md2pdf() {
  pandoc $1 -o `basename $1 .md`.pdf
}
```

You can add this to your `.bashrc` or `.zshrc` to add a command like follows:

```bash
md2pdf filename.md
```

This will generate a file named `filename.pdf` in your present working directory.

You can use file watching tools to automatically generate a PDF and leave it open/refreshing in your PDF reader. I personally use a tool called [entr(1)][entr], which can be installed via Homebrew.

## Writing equations

You may want to insert some math into your document. You can do this by surrounding your math in dollar signs (`$`) and writing in LaTeX form, for example:

```latex
## Euler's identity
Below is Euler's identity.

$e^{i\pi} + 1 = 0$

Lorem ipsum dolor sit amet...
```

This produces the equation inline. Documentation for this feature of Pandoc is pretty spotty -- if you know of more ways to embed LaTeX equations in Pandoc-generated documents, please let me know!

## Setting everything up

All of the tools mentioned can be installed via Homebrew.

```
brew install entr pandoc
brew cask install mactex
```

Writing Markdown instead of LaTeX allows me to iterate faster on my homework/notes and lets me worry more about my content than the formatting of my sections and subsections. It's really easy to set everything up, and as a Vim user, it has increased my productivity quite a bit. I hope you find my workflow as useful as I have!

[entr]: http://entrproject.org/
[latex]: http://www.latex-project.org/
[markdown]: http://daringfireball.net/projects/markdown/
[pandoc]: http://pandoc.org/
