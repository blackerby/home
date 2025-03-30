+++
title = "Some ideas"
date = 2025-03-30
+++

I typically learn best when motivated to work on something practical, and am currently a bit adrift with respect to where and how to devote my learning energy in a productive way.

So this post should serve as a place for me to capture some ideas and that I can return to when feeling stuck.

## Tooling for RELAX NG Compact

At $work I've been developing a schema using RELAX NG Compact syntax for an XML data format my team works with. Below are a couple of ideas for related projects.

### rnc2rng-rs

[rnc2rng](https://github.com/djc/rnc2rng) is a Python tool for converting RELAX NG Compact to RELAX NG's XML representation. It might be fun to port this to Rust. As an aside, it appears the maintainer is a skilled Rust developer.

A good first step, valuable on its own, might be to port the [lexer](https://github.com/djc/rnc2rng/blob/main/rnc2rng/parser.py#L15) to Rust using [Logos](https://docs.rs/logos/latest/logos/)

### Study tree-sitter-rnc

I thought I had an original idea (does such a thing exist?): to create a [Tree-sitter](https://tree-sitter.github.io/tree-sitter/) parser for RELAX NG Compact. A web quick search quickly informed me that a brilliant person has [already done so](https://github.com/LdBeth/tree-sitter-rnc). So, my new idea: learn from this work, and perhaps figure out how to incorporate it into Neovim.

### Useful resources

- [RELAX NG Compact Tutorial](https://relaxng.org/compact-tutorial-20030326.html)
- [RELAX NG Compact Spec](https://relaxng.org/compact.html)

## XML and Rust

I saw [this blog post](https://blog.startifact.com/posts/xee/) on [https://lobste.rs/](https://lobste.rs/) this past week. It seems like a great way to learn more about XML, Rust, and programming language implementation. I hope this project succeeds.

A good place to start reading the code is the [lexer](https://github.com/Paligo/xee/tree/main/xee-xpath-lexer), which uses Logos (mentioned above). I'll need to have the [XPath spec](https://www.w3.org/TR/xpath-31/) open next to it.

## Miscellaneous

My mind and interests are always flitting around. Capturing some stray ideas here:
- Work through [Tumble Forth]()
- Study up to get past Sequence Counter in TIS-100

