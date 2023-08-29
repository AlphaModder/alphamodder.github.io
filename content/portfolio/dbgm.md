+++
title = "dbgm"
date = 2019-09-26
in_search_index = false

[taxonomies]
project-tags = ["tools", "application development"]

[extra]
thumbnail = "./dbgm.png"
clickthrough = "https://github.com/CCS-1L-F19/dbgm"
+++

{{ project_header(adjust=-6, badges=["https://img.shields.io/badge/status-development paused-yellowgreen"]) }}

`dbgm` is a tool for managing a library of Windows desktop backgrounds, written in Rust and using bindings to the C/C++ UI toolkit `dear imgui`. Currently just the core functionality has been implemented. It can import backgrounds from folders on-disk and non-destructively crop them to best fit a particular screen resolution, and keeps track of various other metadata. The edited versions are then saved to a folder from which Windows can generate a slideshow.