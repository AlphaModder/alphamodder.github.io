+++
title = "include-lua"
date = 2019-03-28
in_search_index = false

[taxonomies]
project-tags = ["libraries"]
+++

{{project_header(adjust=-3, badges=[
    "https://img.shields.io/badge/status-actively maintained-brightgreen", "https://img.shields.io/crates/v/include-lua.svg"
])}}

`include-lua` is a Rust library that allows a developer to embed a lua source tree into a Rust application binary. This tree can then be loaded into an (https://github.com/kyren/rlua) context, and code imported from it via `require`. It was originally a component of `rust-shiori-lua`, but I spun it off into its own library.