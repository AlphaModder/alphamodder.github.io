+++
title = "glauber-rs"
date = 2019-08-13
in_search_index = false

[taxonomies]
project-tags = ["simulations", "statistical mechanics"]

[extra]
thumbnail = "./glauber.png"
clickthrough = "https://github.com/AlphaModder/glauber-rs"
+++

{{ project_header(adjust=-5, badges=["https://img.shields.io/badge/status-complete-brightscreen"]) }}

`glauber-rs` is my simulation of the [Ising model]("https://en.wikipedia.org/wiki/Ising_model") using Glauber dynamics. The Ising model is a simplified model of a ferromagnet based on a grid of spins, each of which can be up or down, and evolve according to a statistical process. This model replicates the behavior of real ferromagnets in that it exhibits a "Curie temperature." Above this temperature, the spins are mostly independent and display little order, while below it the spins fall into alignment with eachother, "magnetizing" the material. This abrupt change is known as a phase transition, and it is a common object of study in statistical mechanics. `glauber-rs` is designed to be modular, and could implement other simulations of a similar nature.