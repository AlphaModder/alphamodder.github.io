+++
title = "Ouroboros"
date = 2018-12-25
in_search_index = false

[taxonomies]
project-tags = ["libraries", "black magic"]
+++

{{ project_header(adjust=-3, badges=["https://img.shields.io/badge/status-experimental-orange"]) }}

Ouroboros is an experimental python library that allows one to import python modules into a namespace completely separate from the rest of an application, while still being able to call into their code with no IPC or other intermediary. An arbitrary number of such namespaces can be created, and further code imported by namespaced modules will remain in the namespace. Building it taught me a lot about the internals of cpython, and there is [a detailed technical breakdown in its README.](https://github.com/AlphaModder/Ouroboros/blob/master/README.md)