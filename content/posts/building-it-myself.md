+++
title = "Building it myself"
date = 2025-01-27

[taxonomies]
tags = ["rust"]
+++

I am two or three years into my [Rust](https://www.rust-lang.org/) learning journey. I've published a few small [crates](https://crates.io/users/blackerby) without any expectation that they might be useful to other people, but Rust isn't something I directly use at work. That means I am left to my own devices when it comes to learning proper practices, not just for Rust but for software design, versioning, releasing, CI/CD, and all the other stuff that isn't necessarily writing code that does a useful thing. In other words, I'm never entirely sure I'm doing things the "right" way.

The project getting most of my attention right now is a library I call Capitol. It parses strings like "118hr23", which you might find in various contexts on [Congress.gov](https://congress.gov) or [GovInfo](https://www.govinfo.gov/), into a structure like this:

```rust
Citation {
    congress: Congress(118),
    chamber: Chamber::House,
    object_type: CongObjectType::HouseBill,
    number: 23,
    ver: None,
}
```

that can then be converted into a [URL on Congress.gov](https://www.congress.gov/bill/118th-congress/house-bill/23).

(An explanation of the purpose of the library will need to wait for another post, though the README on [its GitHub page](https://github.com/blackerby/capitol) may give a sense of what I'm thinking.)

When I started the project, I was parsing legislative citations using the [Winnow parser combinator library](https://docs.rs/winnow/latest/winnow/). I pulled in [chrono](https://docs.rs/chrono/latest/chrono/) to get the current year. I added [anyhow](https://docs.rs/anyhow/latest/anyhow/) because that's what you do in a Rust project, right?

Not long after I put version 0.1.0 of Capitol up on crates.io I came across Armin Ronacher's blog post titled [Build It Yourself](https://lucumr.pocoo.org/2025/1/24/build-it-yourself/). If you've written any Python in the last 10 years, you have probably encountered Armin's work. He is the creator of [Flask](https://flask.palletsprojects.com/en/stable/), among many other well-known and frequently used open source Python projects. In other words, he's a really good programmer.

Then [BurntSushi](https://burntsushi.net/) shared the post on [Reddit](https://www.reddit.com/r/rust/comments/1i8wwy0/build_it_yourself/). If you write Rust, you know BurntSushi, the programmer behind [ripgrep](https://github.com/BurntSushi/ripgrep) and Rust's [CSV](https://github.com/BurntSushi/rust-csv) and [regular expressions](https://github.com/rust-lang-nursery/regex) crates. Another programmer who has forgotten more than I'll ever know.

Reading the post and the discussion on Reddit, I was thinking there's no way this applies to me. I am the kind of programmer who absolutely depends on dependencies. How would I get anything done otherwise?

But then I decided to take another look at Capitol. It's a small project. What it does is fairly simple. Do I really need parsing, date, and error dependencies?

So I started a new branch of the project and worked my way towards implementing the desired functionality using only the standard library. Sure, it knocked 1.5 KiB off of the compressed binary size on crates.io, which is pretty good but probably be better, it sped up compile times, and it saved having to learn three libraries to achieve the results I wanted. 

That's all well and good, but realistically speaking, this is a personal project and I am likely the only person who will ever use it. Does that make the extra effort I put into removing dependencies useless?

No. This was an excellent learning opportunity. When I was a high school Latin teacher and would assign a piece of Latin prose to students to read and translate, they would often come to my desk a few minutes after starting their work to ask for help at the first sign of trouble (e.g., some unknown vocabulary, an unrecognized grammatical form). By the end of my teaching career, my go to question for my students in this situation was "Did you look at it and think about it?" In other words, did you try to understand what you are presented with? Did you make use of the knowledge you currently have? Did you use the resources available to you (your textbook and your glossary) to acquire knowledge you need? It occurs to me now I was essentially asking them to RTFM, hopefully with a kinder tone.

Removing dependencies from my little project forced me to look at and think about what I was trying to do: e.g., how much text processing I could do with a [Peekable iterator](https://doc.rust-lang.org/std/iter/struct.Peekable.html) and not with a parser combinator library, how to calculate the current year using the [UNIX_EPOCH](https://doc.rust-lang.org/std/time/struct.SystemTime.html#associatedconstant.UNIX_EPOCH) and not with a massive date and time library, and how to represent errors in my crate, yes with some boilerplate code, but for someone at my skill level, writing that boilerplate is a good exercise.

Version 0.2.0 is now up on crates.io and I am happy with its current state. It's definitely not perfect, but I think it will be a great playground for getting better at Rust and learning to build it myself.

