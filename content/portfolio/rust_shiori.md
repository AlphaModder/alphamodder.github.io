+++
title = "rust-shiori"
date = 2018-12-30
in_search_index = false

[taxonomies]
project-tags = ["interactive software", "programming languages"]

[extra]
thumbnail = "./shiori.png"
clickthrough = "https://github.com/AlphaModder/rust-shiori"
+++

{{ project_header(adjust=-3, badges=["https://img.shields.io/badge/status-development paused-yellowgreen"]) }}

`rust-shiori` is a scripting framework for creating faux-AI characters that a user can interact, talk, and play with on their desktop, called "ghosts." It is built to work with [SakuraScript Player](http://ssp.shillest.net/), which implements a lower-level interface for the same purpose. The plugin interface is written in Rust, but currently most of the code is in the crate `rust-shiori-lua`, which provides a Lua runtime for ghost development on top of `rust-shiori`. I am in the process of developing my own ghost (shown in the picture) using `rust-shiori-lua`, but it is not yet polished enough for release.